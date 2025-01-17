Plot interaction changed features
---------------------------------

.. link-button:: https://github.com/drieslab/Giotto/tree/suite/R/spatial_interaction_visuals.R#L1510
		:type: url
		:text: View Source Code
		:classes: btn-outline-primary btn-block

Last Updated: |today|

Description
~~~~~~~~~~~

Create barplot to visualize interaction changed features

Usage
~~~~~

::

   plotInteractionChangedFeats(
     gobject,
     icfObject,
     source_type,
     source_markers,
     ICF_feats,
     cell_color_code = NULL,
     show_plot = NA,
     return_plot = NA,
     save_plot = NA,
     save_param = list(),
     default_save_name = "plotInteractionChangedFeats"
   )

Arguments
~~~~~~~~~

+-----------------------------------+-----------------------------------+
| ``gobject``                       | giotto object                     |
+-----------------------------------+-----------------------------------+
| ``icfObject``                     | ICF (interaction changed feature) |
|                                   | score object                      |
+-----------------------------------+-----------------------------------+
| ``source_type``                   | cell type of the source cell      |
+-----------------------------------+-----------------------------------+
| ``source_markers``                | markers for the source cell type  |
+-----------------------------------+-----------------------------------+
| ``ICF_feats``                     | named character vector of ICF     |
|                                   | features                          |
+-----------------------------------+-----------------------------------+
| ``cell_color_code``               | cell color code for the           |
|                                   | interacting cell types            |
+-----------------------------------+-----------------------------------+
| ``show_plot``                     | show plots                        |
+-----------------------------------+-----------------------------------+
| ``return_plot``                   | return plotting object            |
+-----------------------------------+-----------------------------------+
| ``save_plot``                     | directly save the plot [boolean]  |
+-----------------------------------+-----------------------------------+
| ``save_param``                    | list of saving parameters from    |
|                                   | ``all_plots_save_function``       |
+-----------------------------------+-----------------------------------+
| ``default_save_name``             | default save name for saving,     |
|                                   | don't change, change save_name in |
|                                   | save_param                        |
+-----------------------------------+-----------------------------------+

Value
~~~~~

plot
