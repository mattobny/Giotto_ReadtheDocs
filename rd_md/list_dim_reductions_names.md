# `list_dim_reductions_names`

list_dim_reductions_names


## Description

return the available dimension reductions object names


## Usage

```r
list_dim_reductions_names(
  gobject,
  data_type = "cells",
  spat_unit = NULL,
  feat_type = NULL,
  dim_type = NULL
)
```


## Arguments

Argument      |Description
------------- |----------------
`gobject`     |     giotto object
`data_type`     |     cells or feats dim reduction
`spat_unit`     |     spatial unit (e.g. "cell")
`feat_type`     |     feature type (e.g. "rna", "dna", "protein")
`dim_type`     |     dimensional reduction type (method)


## Details

function that can be used to find which names have been used


## Value

names of dimension reduction object


