================
Giotto Ecosystem
================

:Date: 2023-02-15

We plan to curate an ecosystem of different, related packages to modularize Giotto Suite as we extend its functionalities.
Here, we detail some different helper module(s) within the Giotto Ecosystem. 

1. GiottoData
=============

This package depends on Gioto Suite and leverages various functions within it for saving 
and loading Giotto objects. It contains dataset helper functions ``loadGiottoMini()`` and
``getSpatialDataset()``. **Note that** ``getSpatialDataset()`` **was moved from Giotto Suite to GiottoData!**

In addition to dataset helpers, we have created mini Giotto Objects for testing
Giotto Suite's capabilities rapidly and streamlining the tutorial experience. 
GiottoData currently includes two mini Giotto Objects which are derived from
Vizgen and Visium data; more mini Giotto Objects will be published in the future.
Further, we include mini objects, S4 subobjects of a Giotto Object (i.e. exprObj), 
in an effort to make the Giotto Object structure as transparent as possible. 

GiottoData may be downloaded in a similar fashion to Giotto Suite:

.. container:: 

    .. code:: R

        devtools::install_github("drieslab/GiottoData")

The scripts used to create both the mini giotto objects and mini objects are available in
the repository so that we may extend and/or improve them and that you may utilize them for your own purposes!