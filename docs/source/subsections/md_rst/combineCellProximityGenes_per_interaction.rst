=========================================
combineCellProximityGenes_per_interaction
=========================================

:Date: 2022-10-06

--------------

Description
===========

Combine CPG scores per interaction

Usage
=====

.. code:: r

   combineCellProximityGenes_per_interaction(
     cpgObject,
     sel_int,
     selected_genes = NULL,
     specific_genes_1 = NULL,
     specific_genes_2 = NULL,
     min_cells = 5,
     min_int_cells = 3,
     min_fdr = 0.05,
     min_spat_diff = 0,
     min_log2_fc = 0.5
   )
