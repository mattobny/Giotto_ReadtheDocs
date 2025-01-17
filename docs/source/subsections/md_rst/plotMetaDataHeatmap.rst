plotMetaDataHeatmap
-------------------

.. link-button:: https://github.com/drieslab/Giotto/tree/suite/R/auxiliary_visuals.R#L1224
		:type: url
		:text: View Source Code
		:classes: btn-outline-primary btn-block

Last Updated: |today|

Description
~~~~~~~~~~~

Creates heatmap for genes within aggregated clusters.

Usage
~~~~~

::

   plotMetaDataHeatmap(
     gobject,
     spat_unit = NULL,
     feat_type = NULL,
     expression_values = c("normalized", "scaled", "custom"),
     metadata_cols = NULL,
     selected_feats = NULL,
     selected_genes = NULL,
     first_meta_col = NULL,
     second_meta_col = NULL,
     show_values = c("zscores", "original", "zscores_rescaled"),
     custom_cluster_order = NULL,
     clus_cor_method = "pearson",
     clus_cluster_method = "complete",
     custom_feat_order = NULL,
     custom_gene_order = NULL,
     feat_cor_method = "pearson",
     gene_cor_method = NULL,
     feat_cluster_method = "complete",
     gene_cluster_method = NULL,
     gradient_color = c("blue", "white", "red"),
     gradient_midpoint = 0,
     gradient_limits = NULL,
     x_text_size = 10,
     x_text_angle = 45,
     y_text_size = 10,
     strip_text_size = 8,
     show_plot = NA,
     return_plot = NA,
     save_plot = NA,
     save_param = list(),
     default_save_name = "plotMetaDataHeatmap"
   )

Arguments
~~~~~~~~~

+-----------------------------------+-----------------------------------+
| ``gobject``                       | giotto object                     |
+-----------------------------------+-----------------------------------+
| ``spat_unit``                     | spatial unit (e.g. "cell")        |
+-----------------------------------+-----------------------------------+
| ``feat_type``                     | feature type (e.g. "rna", "dna",  |
|                                   | "protein")                        |
+-----------------------------------+-----------------------------------+
| ``expression_values``             | expression values to use (e.g.    |
|                                   | "normalized", "scaled", "custom") |
+-----------------------------------+-----------------------------------+
| ``metadata_cols``                 | annotation columns found in       |
|                                   | pDataDT(gobject)                  |
+-----------------------------------+-----------------------------------+
| ``selected_feats``                | subset of features to use         |
+-----------------------------------+-----------------------------------+
| ``selected_genes``                | deprecated. See                   |
|                                   | ``selected_feats`` param          |
+-----------------------------------+-----------------------------------+
| ``first_meta_col``                | if more than 1 metadata column,   |
|                                   | select the x-axis factor          |
+-----------------------------------+-----------------------------------+
| ``second_meta_col``               | if more than 1 metadata column,   |
|                                   | select the facetting factor       |
+-----------------------------------+-----------------------------------+
| ``show_values``                   | which values to show on heatmap   |
|                                   | (e.g. "zscores", "original",      |
|                                   | "zscores_rescaled")               |
+-----------------------------------+-----------------------------------+
| ``custom_cluster_order``          | custom cluster order (default =   |
|                                   | NULL)                             |
+-----------------------------------+-----------------------------------+
| ``clus_cor_method``               | correlation method for clusters,  |
|                                   | default to "pearson"              |
+-----------------------------------+-----------------------------------+
| ``clus_cluster_method``           | hierarchical cluster method for   |
|                                   | the clusters, default to          |
|                                   | "complete"                        |
+-----------------------------------+-----------------------------------+
| ``custom_feat_order``             | custom feature order (default =   |
|                                   | NULL)                             |
+-----------------------------------+-----------------------------------+
| ``custom_gene_order``             | deprecated. See                   |
|                                   | ``custom_feat_order`` param       |
+-----------------------------------+-----------------------------------+
| ``feat_cor_method``               | correlation method for features,  |
|                                   | default to "pearson"              |
+-----------------------------------+-----------------------------------+
| ``gene_cor_method``               | deprecated. See                   |
|                                   | ``feat_cor_method`` param         |
+-----------------------------------+-----------------------------------+
| ``feat_cluster_method``           | hierarchical cluster method for   |
|                                   | the features, default to          |
|                                   | "complete"                        |
+-----------------------------------+-----------------------------------+
| ``gene_cluster_method``           | deprecated. See                   |
|                                   | ``feat_cluster_method`` param     |
+-----------------------------------+-----------------------------------+
| ``gradient_color``                | vector with 3 colors for numeric  |
|                                   | data                              |
+-----------------------------------+-----------------------------------+
| ``gradient_midpoint``             | midpoint for color gradient       |
+-----------------------------------+-----------------------------------+
| ``gradient_limits``               | vector with lower and upper       |
|                                   | limits                            |
+-----------------------------------+-----------------------------------+
| ``x_text_size``                   | size of x-axis text               |
+-----------------------------------+-----------------------------------+
| ``x_text_angle``                  | angle of x-axis text              |
+-----------------------------------+-----------------------------------+
| ``y_text_size``                   | size of y-axis text               |
+-----------------------------------+-----------------------------------+
| ``strip_text_size``               | size of strip text                |
+-----------------------------------+-----------------------------------+
| ``show_plot``                     | show plot. TRUE or FALSE          |
+-----------------------------------+-----------------------------------+
| ``return_plot``                   | return ggplot object. TRUE or     |
|                                   | FALSE                             |
+-----------------------------------+-----------------------------------+
| ``save_plot``                     | directly save the plot. TRUE or   |
|                                   | FALSE                             |
+-----------------------------------+-----------------------------------+
| ``save_param``                    | list of saving parameters, see    |
|                                   | ``showSaveParameters``            |
+-----------------------------------+-----------------------------------+
| ``default_save_name``             | default save name                 |
+-----------------------------------+-----------------------------------+

Details
~~~~~~~

Creates heatmap for the average expression of selected genes in the
different annotation/cluster groups. Calculation of cluster or gene
order is done on the provided expression values, but visualization is by
default on the z-scores. Other options are the original values or
z-scores rescaled per gene (-1 to 1).

Value
~~~~~

ggplot or data.table

See Also
~~~~~~~~

``plotMetaDataCellsHeatmap`` for numeric cell annotation instead of gene
expression.
