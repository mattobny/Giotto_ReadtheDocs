silhouetteRankTest
------------------

.. link-button:: https://github.com/drieslab/Giotto/tree/suite/R/spatial_genes.R#L1678
		:type: url
		:text: View Source Code
		:classes: btn-outline-primary btn-block

Last Updated: |today|

Description
~~~~~~~~~~~

Multi parameter aggregator version of ``silhouetteRank``

Usage
~~~~~

::

   silhouetteRankTest(
     gobject,
     expression_values = c("normalized", "scaled", "custom"),
     subset_genes = NULL,
     overwrite_input_bin = TRUE,
     rbp_ps = c(0.95, 0.99),
     examine_tops = c(0.005, 0.01, 0.05, 0.1, 0.3),
     matrix_type = "dissim",
     num_core = 4,
     parallel_path = "/usr/bin",
     output = NULL,
     query_sizes = 10L,
     verbose = FALSE
   )

Arguments
~~~~~~~~~

+-----------------------------------+-----------------------------------+
| ``gobject``                       | giotto object                     |
+-----------------------------------+-----------------------------------+
| ``expression_values``             | expression values to use          |
+-----------------------------------+-----------------------------------+
| ``subset_genes``                  | only run on this subset of genes  |
+-----------------------------------+-----------------------------------+
| ``overwrite_input_bin``           | overwrite input bin               |
+-----------------------------------+-----------------------------------+
| ``rbp_ps``                        | fractional binarization           |
|                                   | thresholds                        |
+-----------------------------------+-----------------------------------+
| ``examine_tops``                  | top fractions to evaluate with    |
|                                   | silhouette                        |
+-----------------------------------+-----------------------------------+
| ``matrix_type``                   | type of matrix                    |
+-----------------------------------+-----------------------------------+
| ``num_core``                      | number of cores to use            |
+-----------------------------------+-----------------------------------+
| ``parallel_path``                 | path to GNU parallel function     |
+-----------------------------------+-----------------------------------+
| ``output``                        | output directory                  |
+-----------------------------------+-----------------------------------+
| ``query_sizes``                   | size of query                     |
+-----------------------------------+-----------------------------------+
| ``verbose``                       | be verbose                        |
+-----------------------------------+-----------------------------------+

Value
~~~~~

data.table with spatial scores
