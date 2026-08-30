# Coerce a defined POSIXct vector to a base R POSIXct

Coerces a `haven_labelled_defined` vector whose underlying type is
`POSIXct` into a base R `POSIXct` time vector.

This method preserves both the timestamp values and the original time
zone. By default, semantic metadata is also retained.

## Usage

``` r
# S3 method for class 'haven_labelled_defined'
as.POSIXct(x, tz = "", strip_attributes = TRUE, ...)
```

## Arguments

- x:

  A vector created with
  [`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
  with underlying type `POSIXct`.

- tz:

  a character string. The time zone specification to be used for the
  conversion, if one is required. System-specific timezones (see
  [`base::timezones()`](https://rdrr.io/r/base/timezones.html), but ""
  is the current time zone, and "GMT" is UTC (Universal Time,
  Coordinated). Invalid values are most commonly treated as UTC, on some
  platforms with a warning.

- strip_attributes:

  Logical; should semantic metadata attributes (label, unit, definition,
  namespace) be removed? Defaults to `FALSE`.

- ...:

  Additional arguments passed to
  [`base::as.POSIXct()`](https://rdrr.io/r/base/as.POSIXlt.html).

## Value

A `POSIXct` vector with timestamp values preserved.

## Details

Use `strip_attributes = TRUE` when flattening or preparing data for
external pipelines, but keep the default when working with defined
vectors directly.  
Base R's [`as.POSIXct()`](https://rdrr.io/r/base/as.POSIXlt.html) also
works, as it dispatches to this method via S3. Using this method
directly is preferred when metadata preservation matters.

## See also

[`as.Date()`](https://rdrr.io/r/base/as.Date.html),
[`as_numeric()`](https://docs.ropensci.org/dataset/reference/as_numeric.md),
[`as_character()`](https://docs.ropensci.org/dataset/reference/as_character.md),
[`as_logical()`](https://docs.ropensci.org/dataset/reference/as_logical.md),
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)

## Examples

``` r
p <- defined(
  as.POSIXct("2024-01-01 12:00:00", tz = "UTC"),
  label = "Timestamp"
)

# Recommended usage
as.POSIXct(p)
#> [1] "2024-01-01 12:00:00 UTC"

# Explicit attribute stripping
as.POSIXct(p, strip_attributes = TRUE)
#> [1] "2024-01-01 12:00:00 UTC"
```
