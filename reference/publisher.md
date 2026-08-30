# Get or Set the Publisher of a Dataset Object

The publisher is the entity responsible for holding, archiving,
releasing, or distributing the resource. It is typically included in
dataset citation metadata.

For software, this might refer to a code repository (e.g., GitHub). If
both a hosting platform and a producing institution are involved, use
the publisher for the institution and
[`creator()`](https://docs.ropensci.org/dataset/reference/creator.md)
with `contributorType = "hostingInstitution"` for the platform.

## Usage

``` r
publisher(x)

publisher(x, overwrite = TRUE) <- value
```

## Arguments

- x:

  A dataset object created with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- overwrite:

  Logical. Should existing publisher metadata be overwritten? Defaults
  to `FALSE`. If `FALSE` and the field exists, a warning is issued.

- value:

  A character string specifying the publisher.

## Value

A character string of length one containing the `"publisher"` attribute.
When assigning, the updated object `x` is returned invisibly.

## Details

Adds or retrieves the optional `"publisher"` attribute for a dataset
object. This property aligns with `dct:publisher` (Dublin Core) and
`publisher` (DataCite).

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
[`relation()`](https://docs.ropensci.org/dataset/reference/relation.md),
[`rights()`](https://docs.ropensci.org/dataset/reference/rights.md),
[`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)

## Examples

``` r
publisher(orange_df) <- "Wiley"
publisher(orange_df)
#> [1] "Wiley"
```
