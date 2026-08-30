# Get / set a concept definition for a vector or a dataset

Assigns a concept URI to a vector created with
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).
This method updates the `concept` attribute and validates that the input
is a single character string or NULL.

## Usage

``` r
var_concept(x, ...)

var_concept(x) <- value

# Default S3 method
var_concept(x) <- value
```

## Arguments

- x:

  A vector to which the concept URI will be assigned.

- ...:

  Further parameters for inheritance, not in use.

- value:

  A character string with a concept URI or NULL to remove the concept.

## Value

The (linked) concept of the meaning of the data contained by a vector
constructed
with[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

The modified vector with updated `concept` metadata.

## Details

[`get_variable_concepts()`](https://docs.ropensci.org/dataset/reference/get_variable_concepts.md)
is identical to `var_concept()`.

## Examples

``` r
small_country_dataset <- dataset_df(
  country_name = defined(c("Andorra", "Lichtenstein"), label = "Country"),
  gdp = defined(c(3897, 7365),
    label = "Gross Domestic Product",
    unit = "million dollars"
  )
)
var_concept(small_country_dataset$country_name) <- "http://data.europa.eu/bna/c_6c2bb82d"
var_concept(small_country_dataset$country_name)
#> [1] "http://data.europa.eu/bna/c_6c2bb82d"
# To remove a concept definition of variable
var_concept(small_country_dataset$country_name) <- NULL
x <- defined(c(1, 2, 3), label = "Example Variable")
var_concept(x) <- "http://example.org/concept/XYZ"
var_concept(x)
#> [1] "http://example.org/concept/XYZ"
```
