==========
Test cases 
==========
.. Note ::
    This section is under **review** and needs improvement. In next update those issues will be addressed.
    
`Test cases <https://github.com/Rvadrabade/OpenFOAM-Programing/tree/master/nonLinearAdvectionDiffusionFoam_cases>`_

Various cases
=============

.. list-table::
   :header-rows: 1
   
   * - Case
     - Dimensions & tmax=0.5 s
     - Domain (in m)
     - Constant value
     - IC (t=0)
     - BC 
   * - :ref:`Casen_1`
     - 1D
     - :math:`0 \leq x \leq 2`
     - Advection 
     - :math:`u =\begin{cases}2 & 0.5 \leq x \leq 1\\1 & else \end{cases}`
     - Periodic
   * - :ref:`Casen_2`
     - 1D
     - :math:`0 \leq x \leq 2`
     - Advection-Diffusion **nu = 0.1** in :math:`m^2/s`
     - :math:`u =\begin{cases}2 & 0.5 \leq x \leq 1\\1 & else \end{cases}`
     - Periodic
   * - :ref:`Casen_3` 
     - 2D
     - :math:`0 \leq x \leq 2`
     
       :math:`0 \leq y \leq 2`
     - Advection 
     - :math:`u,v =\begin{cases}2 & 0.5 \leq x,y \leq 1\\1 & else \end{cases}`
     - Periodic
   * - :ref:`Casen_4`
     - 2D
     - :math:`0 \leq x \leq 2`
     
       :math:`0 \leq y \leq 2`
     - Advection-Diffusion **nu = 0.1** in :math:`m^2/s`
     - :math:`u,v =\begin{cases}2 & 0.5 \leq x,y \leq 1\\1 & else \end{cases}`
     - Periodic
     
.. _Casen_1:
     
Case 1
------
Scheme: Gauss upwind

.. list-table::
   :header-rows: 1
   :align: center
   
   * - 1.0
     - 1.1
   * - .. figure:: images/Tn1.0.png
          :width: 320
     - .. figure:: images/Tn1.1.png
          :width: 320
          
.. _Casen_2:
     
Case 2
------
 Scheme: Gauss upwind & Gauss linear orthogonal

.. list-table::
   :header-rows: 1
   :align: center
   
   * - 2.0
     - 2.1
   * - .. figure:: images/Tn2.0.png
          :width: 320
     - .. figure:: images/Tn2.1.png
          :width: 320    
.. _Casen_3:
     
Case 3
------
Scheme: Gauss upwind

.. list-table::
   :header-rows: 1
   :align: center
   
   * - 3.0 
     - 3.1
   * - .. figure:: images/Tnx3.0.png
          :width: 320
     - .. figure:: images/Tnx3.1.png
          :width: 320
   * - .. figure:: images/Tny3.0.png
          :width: 320
     - .. figure:: images/Tny3.1.png
          :width: 320       
          
.. _Casen_4:
     
Case 4
------
Scheme: Gauss upwind & Gauss linear orthogonal

.. list-table::
   :header-rows: 1
   :align: center
   
   * - 4.0 
     - 4.1
   * - .. figure:: images/Tnx4.0.png
          :width: 320        
     - .. figure:: images/Tnx4.1.png
          :width: 320       
   * - .. figure:: images/Tny4.0.png
          :width: 320        
     - .. figure:: images/Tny4.1.png
          :width: 320  