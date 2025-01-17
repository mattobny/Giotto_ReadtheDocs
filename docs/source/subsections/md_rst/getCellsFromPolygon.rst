Get cells located within the polygons area
------------------------------------------

.. link-button:: https://github.com/drieslab/Giotto/tree/suite/R/interactivity.R#L164
		:type: url
		:text: View Source Code
		:classes: btn-outline-primary btn-block

Last Updated: |today|

Description
~~~~~~~~~~~

Get cells located within the polygons area

Usage
~~~~~

::

   getCellsFromPolygon(
     gobject,
     polygon_name = "selections",
     spat_unit = "cell",
     spat_loc_name = "raw",
     polygons = NULL
   )

Arguments
~~~~~~~~~

+-----------------------------------+-----------------------------------+
| ``gobject``                       | A Giotto object                   |
+-----------------------------------+-----------------------------------+
| ``polygon_name``                  | name of polygon selections        |
+-----------------------------------+-----------------------------------+
| ``spat_unit``                     | spatial unit, default = 'cell'    |
+-----------------------------------+-----------------------------------+
| ``spat_loc_name``                 | name of spatial locations to use, |
|                                   | default = 'raw'                   |
+-----------------------------------+-----------------------------------+
| ``polygons``                      | character. A vector with polygon  |
|                                   | names to extract cells from. If   |
|                                   | NULL, cells from all polygons are |
|                                   | retrieved                         |
+-----------------------------------+-----------------------------------+

Value
~~~~~

A terra 'SpatVector' with cell ID, x y coordinates, and polygon ID where
each cell is located in.

Examples
~~~~~~~~

::

   ## Not run: 
   ## Plot interactive polygons
   my_spatPlot <- spatPlot2D(gobject = my_giotto_object,
                             show_image = TRUE,
                             point_alpha = 0.75,
                             save_plot = FALSE)
   my_polygon_coords <- plotInteractivePolygons(my_spatPlot)

   ## Add polygon coordinates to Giotto object
   my_giotto_polygons <- createGiottoPolygonsFromDfr(my_polygon_coords)
   my_giotto_object <- addGiottoPolygons(gobject = my_giotto_object,
                                         gpolygons = list(my_giotto_polygons))

   ## Get cells located within polygons area
   getCellsFromPolygon(my_giotto_object)

   ## Get only cells from polygon 1
   getCellsFromPolygon(my_giotto_object, polygons = "polygon 1")

   ## End(Not run)
