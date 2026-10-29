# Coerce semantic mappings to canonical key-value form

Convert semantic mapping carriers into a canonical named character
vector representation.

Convert semantic mappings into a two-column relational form suitable for
joins, inspection, and roundtrip conversion with `as_value_key()`.

## Usage

``` r
as_value_key(x)

invert_value_key(x)
```

## Arguments

- x:

  A semantic mapping carrier:

  - named character vector;

  - named list;

  - two-column data frame or tibble.

## Value

A named character vector representing canonical semantic key-value
mappings.

## Details

`as_value_key()` standardises lightweight semantic mappings supplied as:

- named vectors;

- named lists;

- two-column data frames or tibbles.

The resulting object is suitable for:

- [`prelabel()`](https://docs.ropensci.org/dataset/reference/prelabel.md);

- semantic grouping;

- contextual reconstruction;

- relational projection workflows.

Named lists may contain one-to-many mappings:


    list(
      conceptualisation = c(
        "D:/_package/alpha",
        "D:/_markdown/alpha-methodology"
      ),
      betaR = c(
        "D:/_packages/beta",
        "D:/_packages/prebeta"
      )
    )

where multiple values share the same semantic key.

The function is intentionally lightweight. It does not:

- validate ontologies;

- enforce uniqueness;

- resolve semantic conflicts;

- construct graph objects;

- perform recursive inheritance logic.

## Examples

``` r

# named vector
as_value_key(
  c(
    R = "functional_programming",
    png = "visualisation"
  )
)
#>                        R                      png 
#> "functional_programming"          "visualisation" 

# named list
as_value_key(
  list(
    R = "functional_programming",
    png = "visualisation"
  )
)
#>                        R                      png 
#> "functional_programming"          "visualisation" 

# tibble
mapping_tbl <- tibble::tibble(
  extension = c("R", "png"),
  activity = c(
    "functional_programming",
    "visualisation"
  )
)

as_value_key(mapping_tbl)
#>                        R                      png 
#> "functional_programming"          "visualisation" 
```
