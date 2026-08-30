# Create a semantically enriched vector with variable-level metadata

`defined()` constructs a vector that behaves like a base R vector but
carries semantic metadata used for documentation, validation, and
interoperability. The resulting object inherits from
[`haven::labelled()`](https://haven.tidyverse.org/reference/labelled.html)
(for numeric, character, and factor data) or from base date/time
classes, and adds:

## Usage

``` r
defined(
  x,
  labels = NULL,
  label = NULL,
  unit = NULL,
  concept = NULL,
  namespace = NULL,
  ...
)

is.defined(x)

# S3 method for class 'haven_labelled_defined'
summary(object, ...)
```

## Arguments

- x:

  A vector to annotate.

- labels:

  Optional named vector of value labels. Only supported for numeric or
  character vectors (not for logical).

- label:

  A short human-readable variable label (character of length 1).

- unit:

  Unit of measurement (character length 1) or `NULL`.

- concept:

  A URI or identifier describing the meaning or definition of the
  variable. This replaces the deprecated `definition` argument.

- namespace:

  Optional string or named character vector used to generate value-level
  URIs via substitution (`$1` macro).

- ...:

  For backward compatibility; the deprecated `definition` argument is
  still accepted and mapped to `concept`.

- object:

  An R object to be summarised.

## Value

A vector of class `haven_labelled_defined` or `datetime_defined`,
depending on the input type.

## Details

- a human-readable variable label,

- an optional unit of measurement,

- a **concept URI** identifying the meaning of the variable (formerly
  called *definition*),

- an optional namespace used for value-level URI expansion,

- optional labelled values (where supported).

The `concept` attribute is a general semantic anchor and may refer to: a
measure or dimension concept (SDMX-style), a property IRI (e.g.
Wikibase), or any URI that defines or describes the variable.

`defined()` vectors preserve their metadata during subsetting, printing,
summarizing, comparisons, and many tidyverse operations. They integrate
smoothly with
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
objects and can be safely flattened via
[`as.data.frame()`](https://rdrr.io/r/base/as.data.frame.html),
[`as_tibble()`](https://docs.ropensci.org/dataset/reference/as_tibble.dataset_df.md),
or coercion helpers such as
[`as_numeric()`](https://docs.ropensci.org/dataset/reference/as_numeric.md)
and
[`as_character()`](https://docs.ropensci.org/dataset/reference/as_character.md).

## Supported input types

- numeric (integer or double)

- character

- factor (converted via
  [`labelled::to_labelled()`](https://larmarange.github.io/labelled/reference/to_labelled.html))

- `Date`

- `POSIXct`

- [`haven::labelled()`](https://haven.tidyverse.org/reference/labelled.html)

- logical (with restrictions: logical vectors **cannot** have value
  labels)

## See also

`is.defined()`,
[`as_numeric()`](https://docs.ropensci.org/dataset/reference/as_numeric.md),
[`as_character()`](https://docs.ropensci.org/dataset/reference/as_character.md),
[`as_logical()`](https://docs.ropensci.org/dataset/reference/as_logical.md),
[`strip_defined()`](https://docs.ropensci.org/dataset/reference/strip_defined.md),
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

## Examples

``` r
gdp_vector <- defined(
  c(3897, 7365, 6753),
  label = "Gross Domestic Product",
  unit = "million dollars",
  concept = "http://data.europa.eu/83i/aa/GDP"
)

is.defined(gdp_vector)
#> [1] TRUE
print(gdp_vector)
#> gdp_vector: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in million dollars 
#> [1] 3897 7365 6753
summary(gdp_vector)
#> Gross Domestic Product (million dollars)
#>    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#>    3897    5325    6753    6005    7059    7365 
gdp_vector[1:2]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in million dollars 
#> [1] 3897 7365
```
