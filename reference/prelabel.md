# Add lightweight semantic mappings to a vector

`prelabel()` applies lightweight semantic mappings to a vector before
formal definition with
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

## Usage

``` r
prelabel(x, labels, unmatched = "keep", missing_label = "<NA>")

is.prelabelled(x)
```

## Arguments

- x:

  A vector.

- labels:

  Candidate semantic mappings describing provisional semantic
  assertions.

  `labels` is internally normalised with
  [`as_value_key()`](https://docs.ropensci.org/dataset/reference/as_value_key.md)
  and may therefore be supplied as:

  - a named vector;

  - a named list;

  - a two-column data frame or tibble.

- unmatched:

  Behaviour for unmatched observational values.

  One of:

  - `"keep"` (default): preserve unmatched values as self-describing
    semantic assertions;

  - `"na"`: operationalise unmatched values as `NA` during semantic
    coercion.

- missing_label:

  Semantic assertion used internally for missing observational values.

## Value

A vector with:

- class `"prelabelled"`;

- attached provisional semantic vocabulary stored in the `"prelabel"`
  attribute.

## Details

The `prelabelled` class is intended for:

- provisional harmonisation;

- contextual grouping;

- lightweight classification;

- semantic preprocessing workflows.

Unlike
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md),
`prelabel()` does not enforce formal semantic definitions, namespaces,
or units.

Semantic mappings may be supplied as:

- named vectors;

- named lists;

- two-column data frames.

These mappings are normalised internally with
[`as_value_key()`](https://docs.ropensci.org/dataset/reference/as_value_key.md).

`is.prelabelled()` tests if a vector inherits the `prelabelled` class.

`prelabelled` vectors intentionally separate:

- observational evidence;

- semantic operationalisation;

- contextual semantic refinement.

The original observational values remain unchanged while semantic
assertions may evolve through iterative refinement workflows.

Semantic operationalisation is provided with:

- [`as.character()`](https://rdrr.io/r/base/character.html) for
  lightweight semantic coercion;

- [`as_character()`](https://docs.ropensci.org/dataset/reference/as_character.md)
  for provenance-preserving semantic workspaces.

## Examples

``` r

x <- c("R","png", "csv", "unknown")

extension_map <- c(
  R = "functional_programming",
  png = "visualisation",
  csv = "tabular_data"
)

x <- prelabel(x, labels = extension_map)

x
#> [1] "R"       "png"     "csv"     "unknown"
#> attr(,"prelabel")
#>                        R                      png                      csv 
#> "functional_programming"          "visualisation"           "tabular_data" 
#>                  unknown 
#>                "unknown" 
#> attr(,"class")
#> [1] "prelabelled" "character"  

is.prelabelled(x)
#> [1] TRUE

as.character(x)
#> [1] "functional_programming" "visualisation"          "tabular_data"          
#> [4] "unknown"               

semantic_workspace <- as_character(x)

attributes(semantic_workspace)
#> $prelabel
#>                        R                      png                      csv 
#> "functional_programming"          "visualisation"           "tabular_data" 
#>                  unknown 
#>                "unknown" 
#> 
#> $original_values
#> [1] "R"       "png"     "csv"     "unknown"
#> attr(,"prelabel")
#>                        R                      png                      csv 
#> "functional_programming"          "visualisation"           "tabular_data" 
#>                  unknown 
#>                "unknown" 
#> 
```
