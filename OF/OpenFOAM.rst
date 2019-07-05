========
OpenFOAM
========

OpenFOAM is opensource CFD toolbox written using C++ with object oriented approach.

.. contents::
   :local:

OpenFOAM Basics
===============

Resources to Learn or Revise OpenFOAM 

* OpenFOAM User Guide
* OpenFOAM Programmers Guide
* `"3 weeks" series by OpenFOAM wiki <https://wiki.openfoam.com/%223_weeks%22_series>`_
* `The Visual Room <http://thevisualroom.com/24_25_26_27_openfoam_landing_page/openfoam_landing_page.html>`_

OpenFOAM Programing
===================

This section demonstrate how to built custom solver in simple steps.

.. Note:: 
	It is advisable to read and understand the `12 steps to N-S solver <https://lorenabarba.com/blog/cfd-python-12-steps-to-navier-stokes/>`_
	
	Or refer to `The Visual Room short notes <http://www.thevisualroom.com/02_barba_projects/barba_cfd_projects.html>`_  

Linear Advection Diffusion
***************************

* **Problem statement**: Develope a solver for following Linear Advection Diffusion Equation.

.. math::
    \frac{\partial U}{\partial t}+c \nabla U =  \nu \nabla^2 U 

.. toctree::
   :maxdepth: 1
   
   LinearAdvectionDiffusionFoam
   Validation_LAD

Non Linear Advection Diffusion
******************************

* **Problem statement**: Develope a solver for following Non Linear Advection Diffusion Equation.

.. math::
	 \frac{\partial U}{\partial t}+U \bullet \nabla  U =  \nu \nabla^2 U 

.. toctree::
   :maxdepth: 1
   
   NonLinearAdvectionDiffusionFoam
   Validation_nLAD