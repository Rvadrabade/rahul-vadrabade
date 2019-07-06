==========
Test cases 
==========

`Test cases <https://github.com/Rvadrabade/OpenFOAM-Programing/tree/master/LinearAdvectionDiffusionFoam_cases>`_

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
   * - :ref:`Case_1`
     - 1D
     - :math:`0 \leq x \leq 2`
     - Advection **c = (0.5 0 0)** :math:`m/s`
     - :math:`u =\begin{cases}2 & 0.5 \leq x \leq 1\\1 & else \end{cases}`
     - Periodic
   * - :ref:`Case_2`
     - 1D
     - :math:`0 \leq x \leq 2`
     - Diffusion **nu = 0.1** in :math:`m^2/s`
     - :math:`u =\begin{cases}2 & 0.5 \leq x \leq 1\\1 & else \end{cases}`
     - Periodic
   * - :ref:`Case_3` 
     - 2D
     - :math:`0 \leq x \leq 2`
     
       :math:`0 \leq y \leq 2`
     - Advection **c = (0.5 0 0)** :math:`m/s`
     - :math:`u,v =\begin{cases}2 & 0.5 \leq x,y \leq 1\\1 & else \end{cases}`
     - Periodic
   * - :ref:`Case_4`
     - 2D
     - :math:`0 \leq x \leq 2`
     
       :math:`0 \leq y \leq 2`
     - Diffusion **nu = 0.1** in :math:`m^2/s`
     - :math:`u,v =\begin{cases}2 & 0.5 \leq x,y \leq 1\\1 & else \end{cases}`
     - Periodic
     
.. _Case_1:
     
Case 1
------
Scheme: Gauss upwind

.. list-table::
   :header-rows: 1
   :align: center
   
   * - 1.0
     - 1.1
   * - .. figure:: images/T10.png
          :width: 320
     - .. figure:: images/T11.png
          :width: 320

.. _Case_2:
     
Case 2
------
Scheme: Gauss linear orthogonal

.. list-table::
   :header-rows: 1
   :align: center
   
   * - 2.0
     - 2.1
   * - .. figure:: images/T20.png
          :width: 320
     - .. figure:: images/T21.png
          :width: 320

.. _Case_3:
     
Case 3
------
Scheme: Gauss upwind

.. list-table::
   :header-rows: 1
   :align: center
   
   * - 3.0 (50*50)
     - 3.1 (200*200)
   * - .. figure:: images/T30.png
          :width: 480
     - .. figure:: images/T31.png
          :width: 480

.. _Case_4:
     
Case 4
------
Scheme: Gauss linear orthogonal

.. list-table::
   :header-rows: 1
   :align: center
   
   * - 4.0 (20*20)
     - 4.1 (80*80)
   * - .. figure:: images/T40.png
          :width: 480
     - .. figure:: images/T41.png
          :width: 480