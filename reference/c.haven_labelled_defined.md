# Combine defined vectors with metadata checks

The [`c()`](https://rdrr.io/r/base/c.html) method for `defined` vectors
ensures that all semantic metadata (label, unit, concept, namespace, and
value labels) match exactly. This prevents accidental loss or mixing of
incompatible definitions during concatenation.

## Usage

``` r
# S3 method for class 'haven_labelled_defined'
c(...)
```

## Arguments

- ...:

  One or more vectors created with
  [`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

## Value

A single `defined` vector with concatenated values and retained
metadata.

## Details

All input vectors must:

- Have identical `label` attributes

- Have identical `unit`, `concept`, and `namespace`

- Have identical value labels (or none)

## See also

[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)

## Examples

``` r
a <- defined(1:3, label = "Length", unit = "meter")
b <- defined(4:6, label = "Length", unit = "meter")
c(a, b)
#> x: Length
#> Measured in meter 
#> [1] 1 2 3 4 5 6
```
