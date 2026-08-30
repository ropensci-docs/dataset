# Coerce a defined vector to logical

Coerces a `haven_labelled_defined` vector created with
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
into a base R logical vector.

This function is the recommended, semantic-aware interface for
converting defined logical vectors. It preserves the underlying logical
values and, unless otherwise requested, retains the semantic metadata
attached to the variable.

## Usage

``` r
as_logical(x, ...)

# S3 method for class 'haven_labelled_defined'
as_logical(x, strip_attributes = TRUE, ...)
```

## Arguments

- x:

  A vector created with
  [`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

- ...:

  Additional arguments (currently unused).

- strip_attributes:

  Logical; should semantic metadata attributes (such as `label`, `unit`,
  `definition`, and `namespace`) be removed from the returned vector?
  Defaults to `FALSE`.

## Value

A logical vector. If `strip_attributes = FALSE`, any semantic metadata
attached to `x` will be carried over to the returned vector.

## Details

Use `strip_attributes = TRUE` when flattening or preparing data for
external pipelines, but keep the default when working with defined
vectors directly.

Users may also call base R's
[`as.logical()`](https://rdrr.io/r/base/logical.html), which will
dispatch to this method automatically via S3. However, `as_logical()` is
preferred because it makes the semantics explicit and supports the
`strip_attributes` argument.

## See also

[`as_numeric()`](https://docs.ropensci.org/dataset/reference/as_numeric.md),
[`as_character()`](https://docs.ropensci.org/dataset/reference/as_character.md),
[`as.Date()`](https://rdrr.io/r/base/as.Date.html),
[`as.POSIXct()`](https://rdrr.io/r/base/as.POSIXlt.html),
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)

## Examples

``` r
# Basic usage
flg <- defined(c(TRUE, FALSE, TRUE), label = "Flag")
as_logical(flg)
#> [1]  TRUE FALSE  TRUE

# Metadata preserved by default
attr(as_logical(flg), "label")
#> NULL

# Stripping metadata
as_logical(flg, strip_attributes = TRUE)
#> [1]  TRUE FALSE  TRUE

# Base R coercion also works (via S3 method dispatch)
as.logical(flg)
#> [1]  TRUE FALSE  TRUE
```
