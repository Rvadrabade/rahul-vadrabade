===============================
NonLinearAdvectionDiffusionFoam
===============================
* **Problem statement**: To develop a solver for following Non Linear Advection Diffusion Equation.

.. math::
    \frac{\partial U}{\partial t}+ U \bullet \nabla U =  \nu \nabla^2 U
		  
Where  **U**  is Vector velocity field in 3D i.e. *(u v w)* .

.. contents::
   :local:
   
Source code
===========

`Source Code <https://github.com/Rvadrabade/OpenFOAM-Programing/tree/master/nonLinearAdvectionDiffusionFoam>`_

Family of equations.
====================

.. list-table::
   :header-rows: 1

   * - Name
     - Equation
     - Name
     - Equation   
   * - 1D First-order Non Linear Advection 
     - .. math:: 
   	    \frac{\partial u}{\partial t} + u \frac{\partial u}{\partial x} =  0
     - 1D Second-order Non Linear Advection Diffusion 
     - .. math:: 
           \frac{\partial u}{\partial t} + u \frac{\partial u}{\partial x} = \nu \frac{\partial^2 u}{\partial x^2} 
   
   * - 2D First-order Non Linear Advection 
     - .. math:: 
           \frac{\partial u}{\partial t}+ u \frac{\partial u}{\partial x} + v \frac{\partial u}{\partial y} =  0
                                          
           \frac{\partial v}{\partial t}+ u \frac{\partial v}{\partial x} + v \frac{\partial v}{\partial y} =  0
     - 2D Second-order Non Linear Advection Diffusion 
     - .. math:: 
           \frac{\partial u}{\partial t} + u \frac{\partial u}{\partial x} + v \frac{\partial u}{\partial y} = \nu ( \frac{\partial^2 u}{\partial x^2} +  \frac{\partial^2 u}{\partial y^2} )
                                                                                                        
           \frac{\partial v}{\partial t} + u \frac{\partial v}{\partial x} + v \frac{\partial v}{\partial y} = \nu ( \frac{\partial^2 v}{\partial x^2} +  \frac{\partial^2 v}{\partial y^2} )

Step 1: Understanding modified advection term.
==============================================

.. math::
    \frac{\partial U}{\partial t}+ 0.5 * \nabla \bullet (U U) =  \nabla \bullet (\nu \nabla U) = \nu \nabla^2 U
    
In OpenFOAM advection is represented as ``div(phi,U)`` where  ``phi = U * face area of cell = flux`` 

Step 2: Create a base directory for solver.
===========================================

``foamNewApp`` is script to create template for a new application in easiest way which Creates a directory 
containing source .C file and Make directory rather than copying/modifying exiting solver code.

`For more details <https://cfd.direct/openfoam/user-guide/v6-compiling-applications/#x10-710003.2>`_

.. code-block:: bash
    
    mkdir -p $FOAM_RUN                             // Creates directory "/home/user/OpenFOAM/user-foamVerion/run"
    cd $FOAM_RUN                                   // Enter into directory                                
    foamNewApp nonLinearAdvectionDiffusionFoam     // Creates base directory for solver 
    cd nonLinearAdvectionDiffusionFoam             // Enter into directory
    ls */*                                         // List the contents
    
In **nonLinearAdvectionDiffusionFoam** directory there are files i.e. **Make/files, Make/options, nonLinearAdvectionDiffusionFoam.C**

Step 3: Contents of nonLinearAdvectionDiffusionFoam.C .
=======================================================

Open file with any text editor or use ``nano`` in terminal. Basic header declarations are already 
present. Add following lines and create a ``createFields.H`` file ``(mind the extension .H)``.

.. code-block:: C++
  :linenos:

   #include "fvCFD.H"
   // * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //
   int main(int argc, char *argv[])
   {
       #include "setRootCase.H"
       #include "createTime.H"
       #include "createMesh.H"    //<----
       
       #include "createFields.H"  //<----

       // * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //

       Info<< nl << "ExecutionTime = " << runTime.elapsedCpuTime() << " s"
           << "  ClockTime = " << runTime.elapsedClockTime() << " s"
           << nl << endl;

       Info<< "End\n" << endl;

       return 0;
   }

Step 4: Create field and variables *(U,nu)* in createFields.H
===============================================================

Insert the following code in ``createFields.H`` file. *'c'* is defined vector to generalized code.

**Note** the last line ``createPhi.H`` is include which is currently not in base directory.

.. code-block:: C++
  :linenos:
  
   Info<< "Reading transportProperties\n" << endl;
        // * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //
   IOdictionary transportProperties
   (
       IOobject
       (
           "transportProperties",
           runTime.constant(),
           mesh,
           IOobject::MUST_READ_IF_MODIFIED,
           IOobject::NO_WRITE
       )
   );
   
   dimensionedScalar nu
   (
       
       transportProperties.lookup("nu")        //---------- Contents is same
   );                                          //---------- icoFoam solver
   
   Info<< "Reading field U\n" << endl;
   
   volVectorField U
   (
       IOobject
       (
           "U",
           runTime.timeName(),
           mesh,
           IOobject::MUST_READ,
           IOobject::AUTO_WRITE
       ),
       mesh
   );
   
   
   #include "createPhi.H"               //<------ Note here 

Step 5: About ``createPhi.H``
=============================

Although this step is not mandatory but for this tutorial ``createPhi.H`` file is copied to current 
directory without any changes.

.. code:: bash

    cp /opt/openfoam5/src/finiteVolume/cfdTools/incompressible/createPhi.H .

.. code-block:: C++
  :linenos:
  
   Info<< "Reading/calculating face flux field phi\n" << endl;

   surfaceScalarField phi
   (
       IOobject
       (
           "phi",
           runTime.timeName(),
           mesh,
           IOobject::READ_IF_PRESENT,
           IOobject::AUTO_WRITE
       ),
       fvc::flux(U)              //<--- set to default and preferred in recent 
       //U & mesh.Sf()           //<--- versions, although this works too 
   );  

Step 6: Adding main code.
=========================

Again open nonLinearAdvectionDiffusionFoam.C file and add/edit following code snippet.

.. code-block:: C++
  :linenos:
  
   Info<< "\nStarting time loop\n" << endl;
   
   while (runTime.loop())
   {
       Info<< "Time = " << runTime.timeName() << nl << endl;
       
       #include "CourantNo.H"
       
       // * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //
   
       fvVectorMatrix UEqn
       (
           fvm::ddt(U)
         + 0.5*fvm::div(phi, U)
         - fvm::laplacian(nu, U)
       );
       
       UEqn.solve();
   
   	runTime.write();
   
   	Info<< nl << "ExecutionTime = " << runTime.elapsedCpuTime() << " s"
   	    << "  ClockTime = " << runTime.elapsedClockTime() << " s"
   	    << nl << endl;
   
   }
    
Step 7: Compiling code.
=======================

OpenFOAM provides ``wmake`` system to build a project or application to avoid complex compilation process. Run following command in terminal.

.. code:: bash 
    
    wmake 

Step 8: Testing 
===============

Finally solver is ready and time to build a cases for validation. See :doc:`Validation_nLAD`