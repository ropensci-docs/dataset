# Coerce a defined Date vector to a base R Date

Coerces a `haven_labelled_defined` vector whose underlying type is
`Date` into a base R `Date` vector.

This method preserves the underlying date values and, by default, also
retains any semantic metadata attached to the variable.

## Usage

``` r
# S3 method for class 'haven_labelled_defined'
as.Date(x, strip_attributes = FALSE, ...)
```

## Arguments

- x:

  A vector created with
  [`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
  with underlying type `Date`.

- strip_attributes:

  Logical; should the semantic metadata attributes (label, unit,
  definition, namespace) be removed from the returned vector? Defaults
  to `FALSE`.

- ...:

  Additional arguments passed to
  [`base::as.Date()`](https://rdrr.io/r/base/as.Date.html).

## Value

A `Date` vector, optionally carrying semantic metadata.

## Details

Use `strip_attributes = TRUE` when flattening or preparing data for
external pipelines, but keep the default when working with defined
vectors directly.

Base R's [`as.Date()`](https://rdrr.io/r/base/as.Date.html) also works,
as it dispatches to this method via S3. However, using
[`as.Date()`](https://rdrr.io/r/base/as.Date.html) on defined vectors is
considered safe because this method ensures metadata is handled
predictably.

## See also

[`as.POSIXct()`](https://rdrr.io/r/base/as.POSIXlt.html),
[`as_numeric()`](https://docs.ropensci.org/dataset/reference/as_numeric.md),
[`as_character()`](https://docs.ropensci.org/dataset/reference/as_character.md),
[`as_logical()`](https://docs.ropensci.org/dataset/reference/as_logical.md),
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)

## Examples

``` r
d <- defined(Sys.Date() + 0:2, label = "Observation date")

# Recommended usage
as.Date(d)
#> [1] "2026-08-30" "2026-08-31" "2026-09-01"

# Stripping metadata
as.Date(d, strip_attributes = TRUE)
#> [1] "2026-08-30" "2026-08-31" "2026-09-01"
```
