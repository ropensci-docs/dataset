# Get or set the dataset Description

Get or set the optional `Description` property as an attribute on a
dataset object.

## Usage

``` r
description(x)

description(x, overwrite = FALSE) <- value
```

## Arguments

- x:

  A dataset object created with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- overwrite:

  Logical. If `TRUE`, will overwrite any existing description. If
  `FALSE` (default), will warn and keep the existing description.

- value:

  The new description, as a character string.

## Value

The `Description` attribute as a character vector of length 1.

## Details

The `Description` is recommended for discovery in DataCite. It captures
additional information that does not fit other metadata categories
\<U+2014\> such as technical notes or dataset usage. It is a free-text
field. See
[dct:description](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/elements11/description/).

## See also

Other bibliographic helper functions:
[`contributor()`](https://docs.ropensci.org/dataset/reference/contributor.md),
[`creator()`](https://docs.ropensci.org/dataset/reference/creator.md),
[`dataset_format()`](https://docs.ropensci.org/dataset/reference/dataset_format.md),
[`dataset_title()`](https://docs.ropensci.org/dataset/reference/dataset_title.md),
[`geolocation()`](https://docs.ropensci.org/dataset/reference/geolocation.md),
[`get_bibentry()`](https://docs.ropensci.org/dataset/reference/get_bibentry.md),
[`language()`](https://docs.ropensci.org/dataset/reference/language.md),
[`publication_year()`](https://docs.ropensci.org/dataset/reference/publication_year.md),
[`publisher()`](https://docs.ropensci.org/dataset/reference/publisher.md),
[`relation()`](https://docs.ropensci.org/dataset/reference/relation.md),
[`rights()`](https://docs.ropensci.org/dataset/reference/rights.md),
[`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)

## Examples

``` r
description(orange_df)
#> [1] "The Orange data frame has 35 rows and 3 columns of records of the growth of orange trees."
description(orange_df, overwrite = TRUE) <- "This dataset records orange tree growth."
description(orange_df)
#> [1] "This dataset records orange tree growth."
```
