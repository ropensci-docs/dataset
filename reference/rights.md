# Get or Set the Rights of a Dataset Object

Adds or retrieves the optional `"rights"` attribute of a dataset object.
This field contains information about intellectual property or usage
rights.

## Usage

``` r
rights(x)

rights(x, overwrite = FALSE) <- value
```

## Arguments

- x:

  A semantically rich data frame created with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- overwrite:

  Logical. Should the existing value be replaced? If `FALSE` and a value
  already exists, the function emits a message instead of overwriting.
  Defaults to `FALSE`.

- value:

  A character string specifying the rights (e.g., `"CC-BY-4.0"`).

## Value

The `"rights"` attribute of the dataset as a character string (length
1). When assigning, the updated object `x` is returned invisibly.

## Details

The `"rights"` field corresponds to
[dct:rights](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/elements11/rights/)
from Dublin Core, and to `rights` in
[DataCite](https://schema.datacite.org/).

Rights information typically includes statements about legal ownership,
licensing, or usage conditions. It helps ensure that users understand
how a dataset may be reused, cited, or shared.

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
[`publication_year()`](https://docs.ropensci.org/dataset/reference/publication_year.md),
[`publisher()`](https://docs.ropensci.org/dataset/reference/publisher.md),
[`relation()`](https://docs.ropensci.org/dataset/reference/relation.md),
[`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)

## Examples

``` r
rights(orange_df) <- "CC-BY-SA"
#> The dataset has already a rights field: :tba
rights(orange_df)
#> [1] ":tba"
```
