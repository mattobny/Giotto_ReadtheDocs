addSpatialCentroidLocations
---------------------------

.. link-button:: https://github.com/drieslab/Giotto/tree/suite/R/giotto_structures.R#L1821
		:type: url
		:text: View Source Code
		:classes: btn-outline-primary btn-block

Last Updated: |today|

Description
~~~~~~~~~~~

Calculates the centroid locations for the polygons within one or more
selected layers

Usage
~~~~~

::

   addSpatialCentroidLocations(
     gobject,
     poly_info = "cell",
     feat_type = NULL,
     spat_loc_name = "raw",
     provenance = poly_info,
     init_metadata = TRUE,
     return_gobject = TRUE,
     verbose = TRUE
   )

Arguments
~~~~~~~~~

+-----------------------------------+-----------------------------------+
| ``gobject``                       | giotto object                     |
+-----------------------------------+-----------------------------------+
| ``poly_info``                     | polygon information               |
+-----------------------------------+-----------------------------------+
| ``feat_type``                     | feature type                      |
+-----------------------------------+-----------------------------------+
| ``spat_loc_name``                 | name to give to the created       |
|                                   | spatial locations                 |
+-----------------------------------+-----------------------------------+
| ``provenance``                    | (optional) provenance to assign   |
|                                   | to generated spatLocsObj. If not  |
|                                   | provided, provenance will default |
|                                   | to ``poly_info``                  |
+-----------------------------------+-----------------------------------+
| ``init_metadata``                 | initialize cell and feature       |
|                                   | metadata for this spatial unit    |
|                                   | (default = TRUE, but should be    |
|                                   | turned off if generated earlier   |
|                                   | in the workflow)                  |
+-----------------------------------+-----------------------------------+
| ``return_gobject``                | return giotto object (default:    |
|                                   | TRUE)                             |
+-----------------------------------+-----------------------------------+
| ``verbose``                       | be verbose                        |
+-----------------------------------+-----------------------------------+

Value
~~~~~

If ``return_gobject = TRUE`` the giotto object containing the calculated
polygon centroids will be returned. If ``return_gobject = FALSE`` only
the generated polygon centroids will be returned as ``spatLocObj``.
