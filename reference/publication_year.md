# Get or Set the Publication Year of a Dataset Object

Access or assign the optional `publication_year` attribute to a
semantically rich dataset object.

## Usage

``` r
publication_year(x)

publication_year(x, overwrite = TRUE) <- value
```

## Arguments

- x:

  A dataset object created by
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`dataset::as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- overwrite:

  Logical. If `TRUE` (default), the existing `publication_year`
  attribute is replaced with `value`. If `FALSE`, the function returns a
  message and does not overwrite the existing value.

- value:

  A character string specifying the publication year.

## Value

The `publication_year` attribute as a character string.

## Details

The `publication_year` represents the year when the dataset was or will
be made publicly available, in `YYYY` format. For additional context,
see [DataCite: Publication Year-Additional
Guidance](https://support.datacite.org/docs/datacite-metadata-schema-v44-mandatory-properties#publicationyearadditional-guidance).

## See also

Other bibliographic helper functions:
[`contributor()`](https://docs.ropensci.org/dataset/reference/contributor.md),
[`creator()`](https://docs.ropensci.org/dataset/reference/creator.md),
[`dataset_format()`](https://docs.ropensci.org/dataset/reference/dataset_format.md),
[`dataset_title()`](https://docs.ropensci.org/dataset/reference/dataset_title.md),
[`description()`](https://docs.ropensci.org/dataset/reference/description.md),
[`geolocation()`](https://docs.ropensci.org/dataset/reference/geolocation.md),
[`get_bibentry()`](https://docs.ropensci.org/dataset/reference/get_bibentry.md),
[`language()`](https://docs.ropensci.org/dataset/reference/language.md),
[`publisher()`](https://docs.ropensci.org/dataset/reference/publisher.md),
[`relation()`](https://docs.ropensci.org/dataset/reference/relation.md),
[`rights()`](https://docs.ropensci.org/dataset/reference/rights.md),
[`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)

## Examples

``` r
publication_year(orange_df)
#> [1] "1998"
publication_year(orange_df) <- "1998"
```
