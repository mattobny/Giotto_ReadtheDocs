plot_spat_image_layer_ggplot
----------------------------

Description
~~~~~~~~~~~

create background image in ggplot

Usage
~~~~~

::

   plot_spat_image_layer_ggplot(
     gg_obj,
     gobject,
     gimage,
     feat_type = NULL,
     spat_unit = NULL,
     spat_loc_name = NULL,
     polygon_feat_type = NULL,
     sdimx = NULL,
     sdimy = NULL
   )

Arguments
~~~~~~~~~

+-----------------------------------+-----------------------------------+
| ``gg_obj``                        | ggplot2 object                    |
+-----------------------------------+-----------------------------------+
| ``gobject``                       | giotto object                     |
+-----------------------------------+-----------------------------------+
| ``gimage``                        | a giotto image or a list/vector   |
|                                   | of giotto images                  |
+-----------------------------------+-----------------------------------+
| ``feat_type``                     | feature type                      |
+-----------------------------------+-----------------------------------+
| ``spat_unit``                     | spatial unit                      |
+-----------------------------------+-----------------------------------+
| ``spat_loc_name``                 | name for spatial locations        |
+-----------------------------------+-----------------------------------+
| ``polygon_feat_type``             | name for feature type associated  |
|                                   | with polygon information          |
+-----------------------------------+-----------------------------------+
| ``sdimx``                         | x-axis dimension name (default =  |
|                                   | 'sdimx')                          |
+-----------------------------------+-----------------------------------+
| ``sdimy``                         | y-axis dimension name (default =  |
|                                   | 'sdimy')                          |
+-----------------------------------+-----------------------------------+

Value
~~~~~

ggplot
