# Get or Set a Variable Label

Adds or retrieves a human-readable label as a metadata attribute for a
variable or vector. This label is useful for making variables easier to
understand than their programmatic names (e.g., column names).

`label_attribute()` is a low-level helper that retrieves the `"label"`
attribute of an object without any fallback or printing logic. It is
primarily used internally.

The `var_label<-` assignment method sets or removes the `"label"`
attribute of a vector or data frame column. This allows attaching
human-readable descriptions to variables for interpretability and
downstream metadata use.

## Usage

``` r
# S3 method for class 'defined'
var_label(x, ...)

label_attribute(x)

var_label(x) <- value

# S3 method for class 'haven_labelled_defined'
var_label(x) <- value

# S3 method for class 'dataset_df'
var_label(
  x,
  unlist = FALSE,
  null_action = c("keep", "fill", "skip", "na", "empty"),
  recurse = FALSE,
  ...
)
```

## Arguments

- x:

  A vector or data frame.

- ...:

  Further arguments passed to or used by methods.

- value:

  A character string to assign as the label, or `NULL` to remove it.

- unlist:

  For data frames, return a named vector instead of a list.

- null_action:

  For data frames, controls how to handle columns without a variable
  label. Options are:

  - `"keep"` (default): keep `NULL` for unlabeled columns

  - `"fill"`: use the column name as a fallback

  - `"skip"`: exclude columns with no label from the result

  - `"na"`: use `NA_character_`

  - `"empty"`: use an empty string `""`

- recurse:

  If `TRUE`, applies `var_label()` recursively on packed columns (as
  created by
  [`tidyr::pack()`](https://tidyr.tidyverse.org/reference/pack.html)) to
  retrieve sub-column labels. If `FALSE`, only the outer (grouped)
  column label is returned.

## Value

- `var_label(x)` returns the `"label"` attribute of `x` as a character
  string.

- `var_label(x) <- value` sets, removes, or replaces the label attribute
  of `x`, returning the updated object invisibly.

A character string if the `"label"` attribute exists, or `NULL` if not
present.

The modified object `x`, returned invisibly with the updated `"label"`
attribute.

## Details

This interface builds on
[`labelled::var_label()`](https://larmarange.github.io/labelled/reference/var_label.html)
and is compatible with the
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
infrastructure for semantic metadata (labels, namespaces, units, and
variable identifiers).

See
[`labelled::var_label()`](https://larmarange.github.io/labelled/reference/var_label.html)
for low-level usage. For a comprehensive guide to working with variable
labels and semantic metadata, see:
[`vignette("defined", package = "dataset")`](https://docs.ropensci.org/dataset/articles/defined.md).

## See also

[`labelled::var_label()`](https://larmarange.github.io/labelled/reference/var_label.html),
[`var_labels()`](https://docs.ropensci.org/dataset/reference/var_labels.md),
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)

Other defined metadata methods and functions:
[`var_labels()`](https://docs.ropensci.org/dataset/reference/var_labels.md),
[`var_namespace()`](https://docs.ropensci.org/dataset/reference/var_namespace.md),
[`var_unit()`](https://docs.ropensci.org/dataset/reference/var_unit.md)

## Examples

``` r
# Retrieve the label attribute
var_label(orange_df$circumference)
#> [1] "circumference at breast height"

# Set or update the label attribute
var_label(orange_df$circumference) <- "circumference (breast height)"

# Example: Retrieve variable labels from a dataset_df
df <- dataset_df(
  id = defined(1:3, label = "Observation ID"),
  temp = defined(c(22.5, 23.0, 21.8), label = "Temperature (<U+00B0>C)"),
  site = defined(c("A", "B", "A"))
)

# List form (default)
var_label(df)
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

# Character vector form
var_label(df, unlist = TRUE, null_action = "empty")
#>                     rowid                        id                      temp 
#>                        ""          "Observation ID" "Temperature (<U+00B0>C)" 
#>                      site 
#>                        "" 

# Exclude variables without labels
var_label(df, null_action = "skip")
#> $id
#> [1] "Observation ID"
#> 
#> $temp
#> [1] "Temperature (<U+00B0>C)"
#> 

# Replace missing labels with column names
var_label(df, null_action = "fill")
#> $rowid
#> [1] "rowid"
#> 
#> $id
#> [1] "Observation ID"
#> 
#> $temp
#> [1] "Temperature (<U+00B0>C)"
#> 
#> $site
#> [1] "site"
#> 
```
