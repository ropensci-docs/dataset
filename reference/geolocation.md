# Get or Set the Geolocation of a Dataset Object

Access or assign the optional `geolocation` attribute to a semantically
rich dataset object.

## Usage

``` r
geolocation(x)

geolocation(x, overwrite = TRUE) <- value
```

## Arguments

- x:

  A dataset object created by
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`dataset::as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- overwrite:

  Logical. If `TRUE` (default), the existing `geolocation` attribute is
  replaced with `value`. If `FALSE`, the function returns a message and
  does not overwrite the existing value.

- value:

  A character string specifying the `geolocation`.

## Value

A character string of length 1, representing the `geolocation` attribute
attached to `x`.

## Details

The `geolocation` field describes the spatial region or named place
where the data was collected or that the dataset is about. This field is
recommended for data discovery in DataCite Metadata Schema 4.4.

See: [DataCite: Geolocation
Guidance](https://support.datacite.org/docs/datacite-metadata-schema-v44-recommended-and-optional-properties#18-geolocation)

## See also

Other bibliographic helper functions:
[`contributor()`](https://docs.ropensci.org/dataset/reference/contributor.md),
[`creator()`](https://docs.ropensci.org/dataset/reference/creator.md),
[`dataset_format()`](https://docs.ropensci.org/dataset/reference/dataset_format.md),
[`dataset_title()`](https://docs.ropensci.org/dataset/reference/dataset_title.md),
[`description()`](https://docs.ropensci.org/dataset/reference/description.md),
[`get_bibentry()`](https://docs.ropensci.org/dataset/reference/get_bibentry.md),
[`language()`](https://docs.ropensci.org/dataset/reference/language.md),
[`publication_year()`](https://docs.ropensci.org/dataset/reference/publication_year.md),
[`publisher()`](https://docs.ropensci.org/dataset/reference/publisher.md),
[`relation()`](https://docs.ropensci.org/dataset/reference/relation.md),
[`rights()`](https://docs.ropensci.org/dataset/reference/rights.md),
[`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)

## Examples

``` r
orange_dataset <- orange_df
geolocation(orange_df) <- "US"
geolocation(orange_df)
#> [1] "US"

geolocation(orange_df, overwrite = FALSE) <- "GB"
#> The dataset has already an Geolocation: US
```
