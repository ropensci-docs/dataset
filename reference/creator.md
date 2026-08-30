# Get/set the Creator of the object.

Add the optional `Creator` property as an attribute to a dataset object.

## Usage

``` r
creator(x)

creator(x, overwrite = TRUE) <- value
```

## Arguments

- x:

  A semantically rich data frame object created by
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or `dataset::\link{as_dataset_df}`.

- overwrite:

  If the attributes should be overwritten. In case it is set to
  `FALSE`,it gives a message with the current `Creator` property instead
  of overwriting it. Defaults to `TRUE` when the attribute is set to
  `value` regardless of previous setting.

- value:

  The `Creator` as a
  [`utils::person()`](https://rdrr.io/r/utils/person.html) object.

## Value

The Creator attribute as a character of length one is added to `x`.

## Details

The `Creator` corresponds to
[dct:creator](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/elements11/creator/)
in Dublin Core and Creator in DataCite. The name of the entity that
holds, archives, publishes prints, distributes, releases, issues, or
produces the dataset. This property will be used to formulate the
citation, so consider the prominence of the role.

## See also

Other bibliographic helper functions:
[`contributor()`](https://docs.ropensci.org/dataset/reference/contributor.md),
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
creator(orange_df)
#> [1] "N.R. Draper [cre] (VIAF: http://viaf.org/viaf/84585260)"
#> [2] "H Smith [cre]"                                          
# To change author:
creator(orange_df) <- person("Jane", "Doe")
# To add author:
creator(orange_df, overwrite = FALSE) <- person("John", "Doe")
```
