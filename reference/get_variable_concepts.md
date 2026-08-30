# Get concepts for all variables in a dataset_df

Returns a named list of concept URIs (or NULLs) for all variables.

## Usage

``` r
get_variable_concepts(x)
```

## Arguments

- x:

  A `dataset_df` object.

## Value

A named list of concept URIs for each variable.

## Examples

``` r
get_variable_concepts(orange_df)
#> $rowid
#> NULL
#> 
#> $tree
#> NULL
#> 
#> $age
#> NULL
#> 
#> $circumference
#> [1] "https://www.wikidata.org/wiki/Property:P2043"
#> 
```
