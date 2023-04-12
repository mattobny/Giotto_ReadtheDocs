==========================
Giotto Object and Classes
==========================

:Date: 2022-10-12

1. How to create a Giotto Object
================================

In this tutorial, the methodology and syntax to create a
**giottoObject** is shown and osmFISH data is used throughout the
tutorial.

.. container:: cell

   .. code:: r
      
      # Ensure Giotto Suite is installed.
      if(!"Giotto" %in% installed.packages()) {
        devtools::install_github("drieslab/Giotto@suite")
      }

      # Ensure GiottoData, a small, helper module for tutorials, is installed.
      if(!"GiottoData" %in% installed.packages()) {
        devtools::install_github("drieslab/GiottoData")
      }
      library(Giotto)
      # Ensure the Python environment for Giotto has been installed.
      genv_exists = checkGiottoEnvironment()
      if(!genv_exists){
        # The following command need only be run once to install the Giotto environment.
        installGiottoEnvironment()
      }


1.1 Import Giotto and Download the Data
---------------------------------------

To download this data, please ensure that
`wget <https://www.gnu.org/software/wget/?>`__ is installed locally.

.. container:: cell

   .. code:: r

      library(Giotto)
      library(GiottoData)

      # Specify path from which data may be retrieved/stored
      data_directory = paste0(getwd(),'/gobject_data/')
      # alternatively, "/path/to/where/the/data/lives/"

      # Specify path to which results may be saved
      results_directory = paste0(getwd(),'/gobject_results/') 
      # alternatively, "/path/to/store/the/results/"

      # Download osmFISH dataset to data_directory
      getSpatialDataset(dataset = 'osmfish_SS_cortex', directory = data_directory, method = 'wget')

1.2 Minimum requirements for a Giotto Object
--------------------------------------------

-  Expression matrix
-  Spatial locations (*unnecessary for scRNAseq analysis*)

Here, creating a **giottoObject** with the minimum requirements is shown
in two examples. Data formatting guidelines are shown below this code
block.

.. container:: cell

   .. code:: r

      # Example 1.
      # Create a Giotto object using data directly from file paths 
      osm_exprs = paste0(data_directory, "osmFISH_prep_expression.txt")
      osm_locs = paste0(data_directory, "osmFISH_prep_cell_coordinates.txt")

      minimum_gobject1 = createGiottoObject(expression = osm_exprs,
                                            spatial_locs = osm_locs)

      # Example 2.
      # Create a Giotto object using objects already loaded into workspace
      expression_matrix = readExprMatrix(path = osm_exprs) # fast method to read expression matrix
      cell_locations = data.table::fread(file = osm_locs)

      minimum_gobject2 = createGiottoObject(expression = expression_matrix,
                                            spatial_locs = cell_locations)

.. raw:: html

   <details>

.. raw:: html

   <summary>

Expression file formatting

.. raw:: html

   </summary>

|  Expression count matrices accepted by Giotto should have columns
  correlating to individual cells (**cell IDs**) and rows to individual
  features (**feature IDs**).
| **data.table** objects and text-based files ie: (**.csv, .tsv, .txt**)
  to be read in should have column 1 be **feature IDs**.

== ======= ====== ====== ====== =
\  feat_ID Cell_1 Cell_2 Cell_3 …
== ======= ====== ====== ====== =
1  Gene1                        
2  Gene2                        
3  Gene3                        
\  …                            
== ======= ====== ====== ====== =

**matrix** and **DelayedMatrix** objects should have **feature IDs**
already incorporated as the rownames.

===== ====== ====== ====== =
\     Cell_1 Cell_2 Cell_3 …
===== ====== ====== ====== =
Gene1                      
Gene2                      
Gene3                      
…                          
===== ====== ====== ====== =

.. raw:: html

   </details>

.. raw:: html

   <details>

.. raw:: html

   <summary>

Locations file formatting

.. raw:: html

   </summary>

Numerical columns will be interpreted in order of x, y, and (optionally)
z coordinate. The first non-numerical column will be taken as **cell
IDs**

== ===== ===== ===== =======
\  sdimx sdimy sdimz cell_ID
== ===== ===== ===== =======
1                    
2                    
3                    
\                    
== ===== ===== ===== =======

.. raw:: html

   </details>

**\*Note:** multiple expression files during can be given at once during
Giotto object creation by using a named list.

.. container:: cell

   .. code:: r

      # Arbitrary modifications
      scaled_matrix = expression_matrix * 1.2
      custom_matrix = expression_matrix * 0.5

      # Provide multiple expression matrices at once to the Giotto Object
      # If these matrices are stored in files rather than in the workspace,
      # file paths may be provided instead of variables
      multi_expr_gobject = createGiottoObject(expression = list(raw = expression_matrix,
                                                                scaled = scaled_matrix,
                                                                custom = custom_matrix),
                                              spatial_locs = cell_locations)

1.3 Customizing the Giotto Object
---------------------------------

By providing values to other **createGiottoObject** parameters, it is
possible to add:

-  **Cell** or **feature (gene) metadata**: see
   `addCellMetadata <../md_rst/addCellMetadata.html>`__ and
   `addFeatMetadata <../md_rst/addFeatMetadata.html>`__

-  **Spatial networks** or **grids**: see
   `Visualizations <../tools/visualizations.html>`__

-  **Dimension reduction**: see
   `Clustering <../analyses/dimension_reduction.html>`__

-  **Images**: see `Imaging <../tools/getting_started_images.html>`__

-  **giottoInstructions**: see
   `createGiottoInstructions <../md_rst/createGiottoInstructions.html>`__
   and below

Providing **giottoInstructions** allows the specification of:

-  An alternative python path if using the Giotto Environment (default)
   is not desired
-  A directory to which resulting plots will save
-  Plot formatting

There are four functions to utilize when setting instructions:

-  **createGiottoInstructions**: creates instructions that are provided
   to **createGiottoObject**
-  **showGiottoInstructions**: displays the instructions of a Giotto
   object
-  **changeGiottoInstructions**: replaces 1 or more of the instruction
   parameters (e.g. plotting format)
-  **replaceGiottoInstructions**: replaces all instructions with new
   instructions (e.g after subsetting)

Here is an example of a more customized Giotto object.

.. container:: cell

   .. code:: r

      # Specify data with file paths 
      osm_exprs = paste0(data_directory, "osmFISH_prep_expression.txt")
      osm_locs = paste0(data_directory, "osmFISH_prep_cell_coordinates.txt")
      meta_path = paste0(data_directory, "osmFISH_prep_cell_metadata.txt")

      # Create instructions

      # Optional: Specify a path to a Python executable within a conda or miniconda 
      # environment. If set to NULL (default), the Python executable within the previously
      # installed Giotto environment will be used.
      my_python_path = NULL # alternatively, "/local/python/path/python" if desired.

      instrs = createGiottoInstructions(python_path = my_python_path,
                                        save_dir = results_directory,
                                        plot_format = 'png',
                                        dpi = 200,
                                        height = 9,
                                        width = 9)

      # Create Giotto object
      custom_gobject = createGiottoObject(expression = osm_exprs,
                                          spatial_locs = osm_locs,                                      
                                          instructions = instrs)

      # Add field annotations as cell metadata
      metadata = data.table::fread(file = meta_path)
      custom_gobject = addCellMetadata(custom_gobject, new_metadata = metadata,
                                       by_column = T, column_cell_ID = 'CellID')

      # Check which Giotto instructions are associated with the Giotto object
      showGiottoInstructions(custom_gobject)

Note that although parameters *show_plot*, *return_plot*, and
*save_plot* were not specified within the call to
**createGiottoInstructions**, default values were provided to these
instruction parameters. All instruction parameters have default values,
such that **createGiottoInstructions** may be called with some or no
arguments yet all instruction parameters will have a value after its
execution.

Alternatively, a named list may also be provided to the *instructions*
argument of **createGiottoObject**. However, ensure that all arguments
to
`createGiottoInstructions <../md_rst/createGiottoInstructions.html>`__
are defined when providing instructions as a named list, since default
values are only applied to instructions when made with
**createGiottoInstructions**. *Note that python_path must be specified
when providing instructions as a named list, and may not be provided as
NULL.*

The **giottoInstructions** may be changed, or completely replaced:

.. container:: cell

   .. code:: r

      # Change a previously set parameter, e.g. change dpi = 200 to dpi = 300
      custom_gobject = changeGiottoInstructions(custom_gobject, 
                                                param = 'dpi', 
                                                new_value = 300)

      # Observe that the instructions have changed
      showGiottoInstructions(custom_gobject)

      # Create new instructions using a named list
      sub_results_directory = paste0(results_directory, 'specific_results/')
      my_python_path = custom_gobject@instructions$python_path
      new_instrs = list(python_path = my_python_path,
                        show_plot = TRUE,
                        return_plot = FALSE,
                        save_plot = TRUE,
                        save_dir = sub_results_directory,
                        plot_format = 'jpg',
                        dpi = 250,
                        units = 'in',
                        height = 12,
                        width = 12,
                        is_docker = FALSE)

      # Change all instructions
      custom_gobject = replaceGiottoInstructions(custom_gobject,
                                                 instructions = new_instrs)

      # Observe that the instructions have changed
      showGiottoInstructions(custom_gobject)

1.4 Plotting Data from a Giotto Object
--------------------------------------

Each plotting function in Giotto has three important binary parameters:

-  **show_plot**: print the plot to the console, default is TRUE
-  **return_plot**: return the plot as an object, default is TRUE
-  **save_plot**: automatically save the plot, default is FALSE

These parameters are stored within a **giottoObject** that was provided
instructions from **createGiottoInstructions** and are provided to
plotting functions accordingly. To change these parameters from the
default values, the instructions may be changed or replaced, or these
parameters may be *manually overwritten* within plotting functions.

See `showSaveParameters <../md_rst/showSaveParameters.html>`__
and the `Saving Options <./getting_started_saving.html>`__ tutorial for
alternative methods to save plots.

.. container:: cell

   .. code:: r

      # Plot according to Giotto Instructions (default)
      spatPlot(custom_gobject)

      # Plot clusters, create, and save to a new subdirectory, all while overwriting formatting
      spatPlot(custom_gobject, 
               cell_color = 'ClusterName', 
               save_plot = TRUE,
               return_plot = TRUE,
               show_plot = TRUE,
               save_param = list(save_folder = 'plots/', # Create subdirectory
                                 save_name = 'cell_clusters', 
                                 save_format = 'png', 
                                 units = 'in',
                                 base_height = 9,
                                 base_width = 9))

.. image:: /images/images_pkgdown/getting_started_figs/getting_started_gobject/cell_clusters.png

2. Giotto Object Structure
==========================

Usage of the Giotto package revolves around the **giottoObject**. This
is an S4 object class that holds spatial expression data and facilitates
its manipulation and visualization with the Giotto package’s functions.
Additional metadata and other outputs generated from certain Giotto
functions, which may used in downstream analyses, are also be stored
within the **giottoObject**. Its self-contained nature renders a
convenient representation of the entire spatial experiment and is why
most Giotto functions take a given **giottoObject** as input and return
a **giottoObject** as output.

| Data is organized within the **giottoObject** in defined **slots** as
  described in the diagram below.
|  |image1|
| |image2|
| |image3|

3. Nested Organization of the Giotto Object
===========================================

| Spatial data has tiered organization and thus so too does Giotto.
  Tissue regions can be divided down into individual cells and then
  further into organelles. The data structure of Giotto mirrors
  biological structure by nesting data within slots related to spatial
  data by **spat_unit** (spatial unit). Additonally, to facilitate the
  integration of multiple -omic data, slots related to feature data will
  be nested with **feat_type** (feature type).
| Included below is a description of this nesting and also, for advanced
  users and contributors/developers, accessor functions for the slots
  are also provided.

3.0.1 Slots and Subnesting
--------------------------

.. role:: pink
.. role:: blue
.. role:: purple
.. role:: magenta
.. role:: orange


.. list-table:: Slots and Subnesting
   :widths: 35 15 15 35
   :header-rows: 1
   :class: tight-table

   * - Slot
     - Nested
     - Example
     - Accessors
   * - **@expression**
     - :blue:`spat_unit` - :pink:`feat_type` -  :magenta:`name`
     - :blue:`cell` - :pink:`rna` - :magenta:`raw`
     - get_expression_values()
       set_expression_values()
       showGiottoExpression()
   * - **@cell_metadata**
     - :blue:`spat_unit` - :pink:`feat_type`
     - :blue:`cell` - :pink:`rna`
     - pDataDT()
       addCellMetadata()
   * - **@feat_metadata**
     - :blue:`spat_unit` - :pink:`feat_type`
     - :blue:`cell` - :pink:`rna`
     - fDataDT()        
       addFeatMetadata()
   * - **@spatial_grid**
     - :blue:`spat_unit` - :magenta:`name`
     - :blue:`grid`- :magenta:`grid`
     - get_spatialGrid()
       set_spatialGrid()
       showGiottoSpatGrids()
   * - **@nn_network**
     - :blue:`spat_unit`- :orange:`method` -:magenta:`name`
     - :blue:`cell`- :orange:`sNN` - :magenta:`sNN_results1`
     - get_NearestNetwork()
       set_NearestNetwork()
   * - **@dimension_reduction**
     - :purple:`approach` - :blue:`spat_unit` - :pink:`feat_type` - :orange:`method` - :magenta:`name`
     - :purple:`cells` - :blue:`cell` - :pink:`rna` - :orange:`pca` - :magenta:`pca`
     - get_dimReduction()
       set_dimReduction()
       showGiottoDimRed()
   * - **@spatial_enrichment**
     - :blue:`spat_unit` - :pink:`feat_type` - :magenta:`name`
     - :blue:`cell` - :pink:`rna` - :magenta:`results1`
     - get_spatial_enrichment()
       set_spatial_enrichment()
       showGiottoSpatEnrichments()
   * - **@spatial_info**
     - :blue:`spat_unit`
     - :blue:`cell`
     - get_polygon_info()
       set_polygon_info()
       showGiottoSpatialInfo()
   * - **@spatial_locs**
     - :blue:`spat_unit` - :magenta:`name`
     - :blue:`cell`- :magenta:`raw`
     - get_spatial_locations()
       set_spatial_locations()
       showGiottoSpatLocs()
   * - **@spatial_network**
     - :blue:`spat_unit` - :magenta:`name`
     - :blue:`cell`- :magenta:`Delaunay_network1`
     - get_spatialNetwork()
       set_spatialNetwork()
       showGiottoSpatNetworks()
   * - **@feat_info**
     - :pink:`feat_type`
     - :pink:`rna`
     - get_feature_info()
       set_feature_info()
       showGiottoFeatInfo()
   * - **@images**
     - :magenta:`name`
     - :magenta:`image`
     - getGiottoImage()
       addGiottoImage()
       showGiottoImageNames()
   * - **@largeImages**
     - :magenta:`name`
     - :magenta:`image`
     - getGiottoImage()
       addGiottoImage()
       showGiottoImageNames()
   * - **@instructions**
     - 
     - 
     - replaceGiottoInstructions()
       showGiottoInstructions()


.. |image1| image:: /images/images_pkgdown/getting_started_figs/getting_started_gobject/Giotto_suite_object-01.svg
   :width: 100.0%
.. |image2| image:: /images/images_pkgdown/getting_started_figs/getting_started_gobject/Giotto_suite_object-02.svg
   :width: 100.0%
.. |image3| image:: /images/images_pkgdown/getting_started_figs/getting_started_gobject/Giotto_suite_object-03.svg
   :width: 100.0%
