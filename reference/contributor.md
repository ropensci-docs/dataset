# Get or set contributors

`contributor()` is a lightweight wrapper around
[`creator()`](https://docs.ropensci.org/dataset/reference/creator.md)
that works only with contributors. It retrieves or updates only the
contributor entries in the dataset's bibliographic metadata.

## Usage

``` r
contributor(x)

contributor(x, overwrite = FALSE) <- value
```

## Arguments

- x:

  A dataset object created with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- overwrite:

  Logical. If `TRUE`, replace all existing contributors with `value`. If
  `FALSE`, append `value` to the existing contributors. Defaults to
  `FALSE`.

- value:

  A [`utils::person()`](https://rdrr.io/r/utils/person.html) object
  representing a single contributor. If the `role` field is missing, it
  will be set to `"ctb"`. If `NULL`, the dataset is returned unchanged.

## Value

- `contributor()` returns a
  [`utils::person()`](https://rdrr.io/r/utils/person.html) or a list of
  such objects corresponding to contributors.

- `contributor<-()` returns the updated dataset (invisibly).

## Details

All people are stored in the `author` slot of the underlying
[`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html). This
helper preserves primary creators and filters or updates only those
entries that represent contributors.

A *contributor* is defined as:

- a person with `role == "ctb"`, **or**

- a person with a `comment[["contributorType"]]`.

  Primary creators (authors) typically have `role %in% c("aut", "cre")`.

  Contributors can be further annotated with metadata in `comment`, for
  example:

`comment = c(contributorType = "hostingInstitution",`
` ORCID = "0000-0000-0000-0000")`

## See also

Other bibliographic helper functions:
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
[`rights()`](https://docs.ropensci.org/dataset/reference/rights.md),
[`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)

## Examples

``` r
df <- dataset_df(data.frame(x = 1))
creator(df) <- person("Jane", "Doe", role = "aut")

# Add a contributor
contributor(df, overwrite = FALSE) <-
  person("GitHub",
    role = "ctb",
    comment = c(contributorType = "hostingInstitution")
  )

# Replace all contributors
contributor(df) <- person("Support", "Team", role = "ctb")

# Inspect only contributors
contributor(df)
#> [1] "GitHub [ctb] (contributorType: hostingInstitution)"
#> [2] "Support Team [ctb]"                                
```
