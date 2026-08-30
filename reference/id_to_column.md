# Add Identifier to First Column of a Dataset

Adds a prefixed identifier (e.g., `eg:`) to the first column of a
dataset, useful for generating semantic row IDs (e.g., for RDF
serialization).

## Usage

``` r
id_to_column(x, prefix = "eg:", ids = NULL)
```

## Arguments

- x:

  A dataset created with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md),
  or a regular data frame.

- prefix:

  A character string used as the prefix for row identifiers. Defaults to
  `"eg:"` (referring to [example.com](https://example.com)).

- ids:

  Optional. A character vector of custom IDs to use instead of row
  names.

## Value

A dataset of the same class as `x`, with the first column updated to
include unique prefixed identifiers.

## Examples

``` r
# Example with a dataset_df object:
id_to_column(orange_df)
#> Draper-Smith (1998): Growth of Orange Trees [dataset], https://doi.org/10.5281/zenodo.14917851
#>    rowid tree    age circumference 
#>    <chr> <chr> <dbl>         <dbl>
#>  1 eg:1  1       118            30
#>  2 eg:2  1       484            58
#>  3 eg:3  1       664            87
#>  4 eg:4  1      1004           115
#>  5 eg:5  1      1231           120
#>  6 eg:6  1      1372           142
#>  7 eg:7  1      1582           145
#>  8 eg:8  2       118            33
#>  9 eg:9  2       484            69
#> 10 eg:10 2       664           111
#> # ℹ 25 more rows 

# Example with a regular data.frame:
id_to_column(Orange, prefix = "orange:")
#>        rowid Tree  age circumference
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
