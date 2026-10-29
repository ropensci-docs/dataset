# Get or Set a Unit of Measure

Adds or retrieves a unit of measure (UoM) attribute to a vector. Units
provide semantic meaning for numeric or character data \<U+2014\> such
as currency, weight, or time \<U+2014\> helping prevent incorrect
operations like merging values measured in incompatible units.

The `var_unit<-` assignment method sets, updates, or removes the
`"unit"` attribute of a vector. This can be used with
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
vectors or base vectors to ensure consistent semantic annotation.

`unit_attribute()` is a low-level helper to directly access the `"unit"`
attribute of a vector, without applying fallback logic. It is mainly
used internally.

`get_unit_attribute()` is an alias for `unit_attribute()`, included for
naming consistency in codebases that distinguish getter/setter patterns.

`set_unit_attribute()` is the low-level assignment function that sets or
removes the `"unit"` attribute of an object. Used internally by
`unit_attribute<-`.

## Usage

``` r
var_unit(x, ...)

var_unit(x) <- value

# Default S3 method
var_unit(x) <- value

get_variable_units(x, ...)

unit_attribute(x)

get_unit_attribute(x)

set_unit_attribute(x, value)

unit_attribute(x) <- value
```

## Arguments

- x:

  A vector.

- ...:

  Further arguments for method extensions.

- value:

  A single character string or `NULL`. If not of length one, an error is
  thrown.

## Value

- `var_unit(x)` returns the `"unit"` attribute as a character string.

- `var_unit(x) <- value` sets, updates, or removes the unit and returns
  the modified vector invisibly.

The modified object `x`, returned invisibly with the updated `"unit"`
attribute.

The `"unit"` attribute of the object `x`, or `NULL` if not set.

The object `x` with updated `"unit"` attribute.

## Details

The `"unit"` attribute stores a machine-readable representation of a
unit of measure (e.g., `"kg"`, `"USD"`, `"days"`). This is useful when
working with linked open data or when combining data from multiple
sources where silent mismatches in units could cause errors.

For full integration with semantic metadata (e.g., labels, concepts,
namespaces), use
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
vectors or
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
objects.

`get_variable_units()` is an alias for `var_unit()`.

See
[`vignette("defined", package = "dataset")`](https://docs.ropensci.org/dataset/articles/defined.md)
for end-to-end examples involving semantic enrichment.

## See also

Other defined metadata methods and functions:
[`var_label`](https://docs.ropensci.org/dataset/reference/var_label.md),
[`var_labels()`](https://docs.ropensci.org/dataset/reference/var_labels.md),
[`var_namespace()`](https://docs.ropensci.org/dataset/reference/var_namespace.md)

## Examples

``` r
# Retrieve the unit of measure (if defined)
var_unit(orange_df$circumference)
#> [1] "milimeter"

# Regular data.frame columns have no unit by default
var_unit(mtcars$wt)
#> NULL

# Add a unit to a column
var_unit(mtcars$wt) <- "1000 lbs"

# Remove the unit
var_unit(mtcars$wt) <- NULL
```
