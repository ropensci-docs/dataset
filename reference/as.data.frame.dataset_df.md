# Convert a `dataset_df` to a base `data.frame`

Converts a `dataset_df` into a plain `data.frame`. By default this
strips semantic metadata (label, unit, concept/definition, namespace)
from each column, but this can be controlled via the `strip_attributes`
argument.

Dataset-level metadata remains attached as inert attributes.

## Usage

``` r
# S3 method for class 'dataset_df'
as.data.frame(
  x,
  ...,
  strip_attributes = TRUE,
  optional = FALSE,
  stringsAsFactors = FALSE
)
```

## Arguments

- x:

  A `dataset_df`.

- ...:

  Passed to
  [`base::as.data.frame()`](https://rdrr.io/r/base/as.data.frame.html).

- strip_attributes:

  Logical: should column-level semantic metadata be stripped? Default:
  `TRUE`.

- optional:

  logical. If `TRUE`, setting row names and converting column names (to
  syntactic names: see
  [`make.names`](https://rdrr.io/r/base/make.names.html)) is optional.
  Note that all of R's base package
  [`as.data.frame()`](https://rdrr.io/r/base/as.data.frame.html) methods
  use `optional` only for column names treatment, basically with the
  meaning of
  [`data.frame`](https://rdrr.io/r/base/data.frame.html)`(*, check.names = !optional)`.
  See also the `make.names` argument of the `matrix` method.

- stringsAsFactors:

  logical: should the character vector be converted to a factor?

## Value

A base R `data.frame` without the `dataset_df` class.

## Examples

``` r
data(orange_df)
as.data.frame(orange_df)
#>        rowid tree  age circumference
#> 1   orange:1    1  118            30
#> 2   orange:2    1  484            58
#> 3   orange:3    1  664            87
#> 4   orange:4    1 1004           115
#> 5   orange:5    1 1231           120
#> 6   orange:6    1 1372           142
#> 7   orange:7    1 1582           145
#> 8   orange:8    2  118            33
#> 9   orange:9    2  484            69
#> 10 orange:10    2  664           111
#> 11 orange:11    2 1004           156
#> 12 orange:12    2 1231           172
#> 13 orange:13    2 1372           203
#> 14 orange:14    2 1582           203
#> 15 orange:15    3  118            30
#> 16 orange:16    3  484            51
#> 17 orange:17    3  664            75
#> 18 orange:18    3 1004           108
#> 19 orange:19    3 1231           115
#> 20 orange:20    3 1372           139
#> 21 orange:21    3 1582           140
#> 22 orange:22    4  118            32
#> 23 orange:23    4  484            62
#> 24 orange:24    4  664           112
#> 25 orange:25    4 1004           167
#> 26 orange:26    4 1231           179
#> 27 orange:27    4 1372           209
#> 28 orange:28    4 1582           214
#> 29 orange:29    5  118            30
#> 30 orange:30    5  484            49
#> 31 orange:31    5  664            81
#> 32 orange:32    5 1004           125
#> 33 orange:33    5 1231           142
#> 34 orange:34    5 1372           174
#> 35 orange:35    5 1582           177
```
