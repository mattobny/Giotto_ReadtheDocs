# `spatialGridObj-class`

S4 spatialGridObj Class


## Description

Framework to store spatial grid


## Details

This is an S4 object that defines a spatial grid. The structure of the grid is stored as a
 `data.table` within the `gridDT` slot and is defined by start and stop spatial
 locations along the spatial axes. The `data.table` also includes names for each cell
 of the grid and names for each of the spatial axis locations that make up the cell.
 Grids can be annotated with both spatial and feature information


