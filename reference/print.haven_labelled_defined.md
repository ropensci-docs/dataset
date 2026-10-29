# Print a defined (haven_labelled_defined) vector

Custom print method for
[haven_labelled_defined](https://docs.ropensci.org/dataset/reference/haven_labelled_defined.md)
vectors created with
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).
It prints the variable name, label, and a short semantic summary before
the underlying values.

## Usage

``` r
# S3 method for class 'haven_labelled_defined'
print(x, ...)
```

## Arguments

- x:

  A `haven_labelled_defined` vector.

- ...:

  Passed on to [`base::print()`](https://rdrr.io/r/base/print.html).

## Value

`x`, invisibly.

## See also

[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md),
[`summary.haven_labelled_defined()`](https://docs.ropensci.org/dataset/reference/defined.md)

## Examples

``` r
sex <- defined(
  c(0, 1, 1, 0),
  label  = "Sex",
  labels = c("Female" = 0, "Male" = 1)
)

print(sex)
#> sex: Sex
#> Defined vector 
#> [1] 0 1 1 0
```
