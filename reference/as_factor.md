# Coerce a defined vector to a factor

`as_factor()` converts a
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
vector into a standard R factor. If value labels are present, they are
turned into factor levels via
[`haven::as_factor()`](https://forcats.tidyverse.org/reference/as_factor.html).
Otherwise, the underlying values are converted with
[`base::factor()`](https://rdrr.io/r/base/factor.html).

## Usage

``` r
as_factor(x, ...)

# S3 method for class 'haven_labelled_defined'
as_factor(x, strip_attributes = TRUE, ...)
```

## Arguments

- x:

  A vector created with
  [`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

- ...:

  Reserved for future extensions.

- strip_attributes:

  Logical; should semantic metadata attributes (such as `label`, `unit`,
  `definition`, and `namespace`) be removed from the returned vector?
  Defaults to 'TRUE'.

## Value

A factor vector.

## Details

Use `strip_attributes = TRUE` when flattening or preparing data for
external pipelines, but keep the default when working with defined
vectors directly.

## Examples

``` r
sex <- defined(
  c(0, 1, 1, 0),
  label  = "Sex",
  labels = c("Female" = 0, "Male" = 1)
)

as_factor(sex)
#> [1] Female Male   Male   Female
#> Levels: Female Male
as_factor(sex, strip_attributes = FALSE)
#> [1] Female Male   Male   Female
#> Levels: Female Male
```
