# Get or set all variable labels on a dataset

Retrieve or assign labels for all variables (columns) in a dataset.

## Usage

``` r
var_labels(
  x,
  unlist = FALSE,
  null_action = c("keep", "fill", "skip", "na", "empty")
)

var_labels(x) <- value
```

## Arguments

- x:

  A `data.frame` or `dataset_df` object.

- unlist:

  Logical; if `TRUE`, return a named character vector instead of a list.
  Defaults to `FALSE`.

- null_action:

  How to handle columns without labels. One of:

  - `"keep"` (default): keep `NULL` values for unlabeled columns.

  - `"fill"`: use the column name as a fallback label.

  - `"skip"`: exclude unlabeled columns from the result.

  - `"na"`: use `NA_character_` for unlabeled columns.

  - `"empty"`: use an empty string `""` for unlabeled columns.

- value:

  - For setting: a named list or named character vector of labels. Names
    must match column names in `x`. Unnamed elements are ignored.

  - For getting: ignored.

## Value

- Getter: a named list (or vector if `unlist = TRUE`) of variable
  labels.

- Setter: the modified `x` with updated labels, returned invisibly.

## Details

This is the dataset-level equivalent of
[`var_label()`](https://docs.ropensci.org/dataset/reference/var_label.md).
It works with any `data.frame`-like object, including
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md),
and returns/sets the `"label"` attribute of each column.

Labels are useful for storing human-readable descriptions of variables
that may have short or cryptic column names.

For internal purposes, this function uses the `"var_labels"` dataset
attribute and delegates to
[`var_label()`](https://docs.ropensci.org/dataset/reference/var_label.md)
and
[`var_label<-()`](https://docs.ropensci.org/dataset/reference/var_label.md)
on individual columns.

## See also

[`var_label()`](https://docs.ropensci.org/dataset/reference/var_label.md)

Other defined metadata methods and functions:
[`var_label`](https://docs.ropensci.org/dataset/reference/var_label.md),
[`var_namespace()`](https://docs.ropensci.org/dataset/reference/var_namespace.md),
[`var_unit()`](https://docs.ropensci.org/dataset/reference/var_unit.md)

## Examples

``` r
df <- dataset_df(
  id = defined(1:3, label = "Observation ID"),
  temp = defined(c(22.5, 23.0, 21.8), label = "Temperature (<U+00B0>C)"),
  site = defined(c("A", "B", "A"))
)

# Get all variable labels
var_labels(df)
#> $rowid
#> NULL
#> 
#> $id
#> [1] "Observation ID"
#> 
#> $temp
#> [1] "Temperature (<U+00B0>C)"
#> 
#> $site
#> NULL
#> 

# Set multiple labels at once
var_labels(df) <- list(site = "Site code")

# Return as a named vector with empty string for unlabeled vars
var_labels(df, unlist = TRUE, null_action = "empty")
#>                     rowid                        id                      temp 
#>                        ""          "Observation ID" "Temperature (<U+00B0>C)" 
#>                      site 
#>               "Site code" 
```
