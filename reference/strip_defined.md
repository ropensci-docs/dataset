# Strip the class from a defined vector

Converts a `defined` vector to a base R numeric or character, retaining
metadata as passive attributes.

## Usage

``` r
strip_defined(x)
```

## Arguments

- x:

  A `defined` vector.

## Value

A base R vector with attributes (`label`, `unit`, etc.) intact.

## See also

[`as_numeric()`](https://docs.ropensci.org/dataset/reference/as_numeric.md),
[`as_character()`](https://docs.ropensci.org/dataset/reference/as_character.md)

## Examples

``` r
gdp <- defined(c(3897L, 7365L), label = "GDP", unit = "million dollars")
strip_defined(gdp)
#> [1] 3897 7365
#> attr(,"label")
#> [1] "GDP"
#> attr(,"unit")
#> [1] "million dollars"

fruits <- defined(c("apple", "avocado", "kiwi"),
  label = "Fruit", unit = "kg"
)

strip_defined(fruits)
#> [1] "apple"   "avocado" "kiwi"   
#> attr(,"label")
#> [1] "Fruit"
#> attr(,"unit")
#> [1] "kg"
```
