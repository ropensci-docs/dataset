# Coerce a defined vector to numeric

`as_numeric()` converts a
[defined()](https://docs.ropensci.org/dataset/reference/defined.md)
vector to a numeric vector. It validates that the underlying data are
numeric, and optionally preserves or strips semantic metadata.

## Usage

``` r
as_numeric(x, ...)

# S3 method for class 'haven_labelled_defined'
as_numeric(x, strip_attributes = TRUE, ...)
```

## Arguments

- x:

  A vector created with
  [`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

- ...:

  Reserved for future use.

- strip_attributes:

  Logical; whether to remove semantic metadata (`label`, `unit`,
  `concept`, `namespace`). Defaults to `TRUE`.

## Value

A numeric vector with or without preserved attributes.

## Details

Use `strip_attributes = TRUE` when flattening or preparing data for
external pipelines, but keep the default when working with defined
vectors directly.

[`as.numeric()`](https://rdrr.io/r/base/numeric.html) drops all metadata
and returns only the numeric values in a vector.

## Examples

``` r
x <- defined(
  1:3,
  label = "Count",
  unit = "n",
  concept = "http://example.org/count",
  namespace = "http://example.org/ns"
)

as_numeric(x)
#> [1] 1 2 3
```
