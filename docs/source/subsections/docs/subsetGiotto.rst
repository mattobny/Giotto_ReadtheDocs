subsetGiotto
------------

.. link-button:: https://github.com/drieslab/Giotto/tree/suite/R/auxiliary_giotto.R#L1203
		:type: url
		:text: View Source Code
		:classes: btn-outline-primary btn-block

Last Updated: |today|

Description
~~~~~~~~~~~

Subsets Giotto object including previous analyses.

Usage
~~~~~

::

   subsetGiotto(
     gobject,
     spat_unit = NULL,
     feat_type = NULL,
     cell_ids = NULL,
     feat_ids = NULL,
     gene_ids = NULL,
     poly_info = NULL,
     all_spat_units = TRUE,
     all_feat_types = TRUE,
     x_max = NULL,
     x_min = NULL,
     y_max = NULL,
     y_min = NULL,
     verbose = TRUE,
     toplevel_params = 2
   )

Arguments
~~~~~~~~~

+-----------------------------------+-----------------------------------+
| ``gobject``                       | giotto object                     |
+-----------------------------------+-----------------------------------+
| ``spat_unit``                     | spatial unit                      |
+-----------------------------------+-----------------------------------+
| ``feat_type``                     | feature type to use               |
+-----------------------------------+-----------------------------------+
| ``cell_ids``                      | cell IDs to keep                  |
+-----------------------------------+-----------------------------------+
| ``feat_ids``                      | feature IDs to keep               |
+-----------------------------------+-----------------------------------+
| ``poly_info``                     | polygon information to use        |
+-----------------------------------+-----------------------------------+
| ``all_spat_units``                | subset all spatial units with     |
|                                   | selected feature ids              |
+-----------------------------------+-----------------------------------+
| ``all_feat_types``                | subset all feature type data with |
|                                   | selected cell ids                 |
+-----------------------------------+-----------------------------------+
| ``x_max, x_min, y_max, y_min``    | minimum and maximum x and y       |
|                                   | coordinates to keep for feature   |
|                                   | coordinates                       |
+-----------------------------------+-----------------------------------+
| ``verbose``                       | be verbose                        |
+-----------------------------------+-----------------------------------+
| ``toplevel_params``               | parameters to extract             |
+-----------------------------------+-----------------------------------+

Details
~~~~~~~

Subsets a Giotto object for a specific spatial unit and feature type

Value
~~~~~

giotto object
