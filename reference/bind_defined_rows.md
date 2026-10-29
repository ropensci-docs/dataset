# Bind strictly defined rows

Add rows of dataset `y` to dataset `x`, validating all semantic
metadata. Metadata (labels, units, concept definitions, namespaces) must
match exactly. Additional dataset-level metadata such as title and
creator can be overridden using `...`.

## Usage

``` r
bind_defined_rows(x, y, ..., strict = FALSE)
```

## Arguments

- x:

  A `dataset_df` object.

- y:

  A `dataset_df` object to bind to `x`.

- ...:

  Optional dataset-level attributes such as `title` or
  [`creator()`](https://docs.ropensci.org/dataset/reference/creator.md)
  to override.

- strict:

  Logical. If `TRUE` (default), require full semantic compatibility,
  including rowid.

## Value

A new `dataset_df` object with rows from `x` and `y`, combined
semantically.

## Details

This function combines two semantically enriched datasets created with
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).
All variable-level attributes \<U+2014\> including labels, units,
concept definitions, and namespaces \<U+2014\> must match. If
`strict = TRUE` (the default), the row identifier namespace (used in the
`rowid` column) must also match exactly.

If `strict = FALSE`, row identifiers from `y` may differ and will be
ignored; the output will inherit `x`'s row identifier scheme.

## Examples

``` r
A <- dataset_df(
  length = defined(c(10, 15),
    label = "Length",
    unit = "cm", namespace = "http://example.org"
  ),
  identifier = c(id = "http://example.org/dataset#"),
  dataset_bibentry = dublincore(
    title = "Dataset A",
    creator = person("Alice", "Smith")
  )
)

B <- dataset_df(
  length = defined(c(20, 25),
    label = "Length",
    unit = "cm", namespace = "http://example.org"
  ),
  identifier = c(id = "http://example.org/dataset#")
)

bind_defined_rows(A, B) # succeeds
#> Smith (2026): Dataset A [dataset]
#>   rowid length 
#>   <chr>  <dbl>
#> 1 id1       10
#> 2 id2       15
#> 3 id3       20
#> 4 id4       25 

C <- dataset_df(
  length = defined(c(30, 35),
    label = "Length",
    unit = "cm", namespace = "http://example.org"
  ),
  identifier = c(id = "http://another.org/dataset#")
)

if (FALSE) { # \dontrun{
bind_defined_rows(A, C, strict = TRUE) # fails: mismatched rowid
} # }

bind_defined_rows(A, C, strict = FALSE) # succeeds: rowid inherited
#> Smith (2026): Dataset A [dataset]
#>   rowid length 
#>   <chr>  <dbl>
#> 1 id1       10
#> 2 id2       15
#> 3 id3       30
#> 4 id4       35 
```
