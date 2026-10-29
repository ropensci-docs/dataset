# Coerce a `dataset_df` to a tibble

`as_tibble()` method for `dataset_df` objects.

Converts a `dataset_df` into a tibble. By default, additional metadata
attached to the object is removed unless `strip_attributes = FALSE` is
specified.

## Usage

``` r
as_tibble(x, ...)

# S3 method for class 'dataset_df'
as_tibble(x, ..., strip_attributes = TRUE, .name_repair = "check_unique")

as.tibble.dataset_df(
  x,
  ...,
  strip_attributes = TRUE,
  .name_repair = "check_unique"
)
```

## Arguments

- x:

  A `dataset_df` object.

- ...:

  Additional arguments passed to
  [`as.data.frame.dataset_df()`](https://docs.ropensci.org/dataset/reference/as.data.frame.dataset_df.md).

- strip_attributes:

  Logical: should column-level semantic metadata be stripped? Default:
  `TRUE`.

- .name_repair:

  Treatment of problematic column names:

  - `"minimal"`: No name checks.

  - `"unique"`: Enforce uniqueness.

  - `"check_unique"`: (default) require unique names.

  - `"universal"`: Make unique and syntactic.

  - A function or purrr-style anonymous function, see
    [`rlang::as_function()`](https://rlang.r-lib.org/reference/as_function.html).

## Value

A
\[tibble`][tibble::tibble()] containing the data (and optionally some attributes) of the `dataset_df\`.

## Metadata handling

The `strip_attributes` argument controls which attributes of the
`dataset_df` object are preserved. When `strip_attributes = TRUE` (the
default), only column-level information is kept.

## About column names

The `dataset_df` class may internally use reserved names for indexing,
identifiers, or metadata. These are never exposed in the resulting
tibble. Column names in the output tibble may be repaired according to
`.name_repair`.

## See also

- [`tibble::as_tibble()`](https://tibble.tidyverse.org/reference/as_tibble.html)

- [`as.data.frame.dataset_df()`](https://docs.ropensci.org/dataset/reference/as.data.frame.dataset_df.md)

## Examples

``` r
# Convert a dataset_df to a tibble
x <- dataset_df(orange_df)
as_tibble(x)
#> # A tibble: 35 × 4
#>    rowid     tree    age circumference
#>    <chr>     <chr> <dbl>         <dbl>
#>  1 orange:1  1       118            30
#>  2 orange:2  1       484            58
#>  3 orange:3  1       664            87
#>  4 orange:4  1      1004           115
#>  5 orange:5  1      1231           120
#>  6 orange:6  1      1372           142
#>  7 orange:7  1      1582           145
#>  8 orange:8  2       118            33
#>  9 orange:9  2       484            69
#> 10 orange:10 2       664           111
#> # ℹ 25 more rows

# Keep attributes
as_tibble(x, strip_attributes = FALSE)
#> # A tibble: 35 × 4
#>    rowid     tree    age circumference
#>    <chr>     <chr> <dbl>         <dbl>
#>  1 orange:1  1       118            30
#>  2 orange:2  1       484            58
#>  3 orange:3  1       664            87
#>  4 orange:4  1      1004           115
#>  5 orange:5  1      1231           120
#>  6 orange:6  1      1372           142
#>  7 orange:7  1      1582           145
#>  8 orange:8  2       118            33
#>  9 orange:9  2       484            69
#> 10 orange:10 2       664           111
#> # ℹ 25 more rows
```
