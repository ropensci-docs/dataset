# Coerce a defined vector to character

`as_character()` is the recommended method to convert a
[defined()](https://docs.ropensci.org/dataset/reference/defined.md)
vector into a character vector. It is metadata-aware and provides
explicit control over whether semantic attributes are preserved.

Base R [`as.character()`](https://rdrr.io/r/base/character.html) always
strips the class and metadata.

Convert objects into semantic character representations.

## Usage

``` r
as_character(x, ...)

# S3 method for class 'haven_labelled_defined'
as_character(x, strip_attributes = TRUE, ...)

# S3 method for class 'haven_labelled_defined'
as.character(x, ...)

as_character(x, ...)
```

## Arguments

- x:

  An object.

- ...:

  Additional arguments.

- strip_attributes:

  Logical; should semantic metadata attributes (such as `label`, `unit`,
  `definition`, and `namespace`) be removed from the returned vector?
  Defaults to `FALSE`.

## Value

A character vector (plain or with attributes).

## Details

If `preserve_attributes = TRUE`, the returned character vector retains
metadata attributes (`unit`, `concept`, `namespace`, `label`). The
`"defined"` class is always removed.

If `preserve_attributes = FALSE` (default), a plain character vector is
returned with *all* metadata stripped.

Use `strip_attributes = TRUE` when flattening or preparing data for
external pipelines, but keep the default when working with defined
vectors directly.

Base R's [`as.character()`](https://rdrr.io/r/base/character.html)
always drops all attributes and returns plain character values. It is
equivalent to: `as_character(x, strip_attributes = TRUE)`.

## Examples

``` r
x <- defined(c("apple", "banana"), label = "Fruit", unit = "kg")

# Recommended:
as_character(x)
#> [1] "apple"  "banana"

# Preserve metadata:
as_character(x, strip_attributes = FALSE)
#> [1] "apple"  "banana"
#> attr(,"label")
#> [1] "Fruit"
#> attr(,"unit")
#> [1] "kg"

# Base R:
as.character(x)
#> [1] "apple"  "banana"
```
