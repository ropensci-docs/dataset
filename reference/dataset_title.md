# Get or Set the Title of a Dataset

Retrieve or assign the main title of a dataset, typically used as the
primary label in metadata exports (e.g., DataCite or Dublin Core).

## Usage

``` r
dataset_title(x)

dataset_title(x, overwrite = FALSE) <- value
```

## Arguments

- x:

  A dataset object created by
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- overwrite:

  Logical. If `TRUE`, the existing title is replaced. If `FALSE`
  (default) and a title is already present, a warning is issued and the
  title is not changed.

- value:

  A character string representing the new title. If `NULL`, a
  placeholder value `":tba"` is assigned. If `value` is a character
  vector of length \> 1, an error is raised.

## Value

`dataset_title()` returns the current dataset title as a character
string. `dataset_title<-()` returns the updated dataset object
(invisible).

## Details

According to the \[Dublin Core specification for
[title](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/elements11/title/),
the title represents the name by which the resource is formally known.

The DataCite metadata schema supports multiple titles (e.g., translated,
alternative), but this function currently supports only a single main
title.

## See also

Other bibliographic helper functions:
[`contributor()`](https://docs.ropensci.org/dataset/reference/contributor.md),
[`creator()`](https://docs.ropensci.org/dataset/reference/creator.md),
[`dataset_format()`](https://docs.ropensci.org/dataset/reference/dataset_format.md),
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
dataset_title(orange_df)
#> [1] "Growth of Orange Trees"

# Set a new title with overwrite = TRUE
dataset_title(orange_df, overwrite = TRUE) <- "The Growth of Orange Trees"
dataset_title(orange_df)
#> [1] "The Growth of Orange Trees"
```
