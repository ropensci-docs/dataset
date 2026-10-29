# Get or set the technical format of a dataset

Adds or retrieves the optional `"format"` field of a dataset's bibentry.
This field is the dataset's technical/media type (e.g., a MIME type).

## Usage

``` r
dataset_format(x)

dataset_format(x, overwrite = FALSE) <- value
```

## Arguments

- x:

  A semantically rich data frame created with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- overwrite:

  Logical. Replace an existing non\<U+2011\>default value? If `FALSE`
  and a non\<U+2011\>default value already exists, a message is emitted
  and the value is kept. Defaults to `FALSE`.

- value:

  A length\<U+2011\>one character string specifying the format (e.g.,
  `"text/csv"`). Use `NULL` to reset to the default.

## Value

The `"format"` (technical format) as a character string (length 1). When
assigning, the updated object `x` is returned invisibly.

## Details

The format field corresponds to
[dct:format](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/elements11/format/)
in Dublin Core and to `format` in
[DataCite](https://schema.datacite.org/). It is useful for indicating
serialization such as `"text/csv"`, `"application/parquet"`, or
`"application/r-rds"`.

If no format is set, this helper uses the package default
`"application/r-rds"`.

## See also

Other bibliographic helper functions:
[`contributor()`](https://docs.ropensci.org/dataset/reference/contributor.md),
[`creator()`](https://docs.ropensci.org/dataset/reference/creator.md),
[`dataset_title()`](https://docs.ropensci.org/dataset/reference/dataset_title.md),
[`description()`](https://docs.ropensci.org/dataset/reference/description.md),
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
dataset_format(orange_df) <- "text/csv"
#> The dataset already has a format: :unas. Use overwrite = TRUE to replace it.
dataset_format(orange_df)
#> [1] ":unas"

# Reset to the package default
dataset_format(orange_df) <- NULL
```
