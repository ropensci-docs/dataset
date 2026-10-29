# Create a Modern Metadata Object Compatible with bibentry

Constructs a
[`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html) object
extended with Dublin Core and DataCite-compatible fields. This unified
structure supports use with functions such as
[`dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md)
and
[`datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md),
and is the internal format for storing rich metadata with datasets.

## Usage

``` r
bibrecord(
  title,
  author,
  contributor = NULL,
  publisher = NULL,
  year = NULL,
  date = Sys.Date(),
  identifier = NULL,
  subject = NULL,
  ...
)
```

## Arguments

- title:

  A character string specifying the dataset title.

- author:

  A [`utils::person()`](https://rdrr.io/r/utils/person.html) or
  list/vector of person objects. Mapped to `creator` in DataCite and
  DCMI.

- contributor:

  Optional list or vector of
  [`utils::person()`](https://rdrr.io/r/utils/person.html) objects.
  Contributor roles are merged if duplicated.

- publisher:

  A character string or
  [`utils::person()`](https://rdrr.io/r/utils/person.html) representing
  the publishing entity.

- year:

  Publication year. Automatically derived from `date` if not provided
  explicitly.

- date:

  A [Date](https://rdrr.io/r/base/Dates.html) object or character string
  in ISO format.

- identifier:

  A persistent identifier (e.g., DOI or URL).

- subject:

  Optional keyword, tag, or controlled vocabulary term.

- ...:

  Additional fields such as `language`, `format`, `rights`, or
  `description`.

## Value

An object of class `"bibrecord"` and `"bibentry"`, suitable for citation
and embedding in metadata-aware structures such as
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

## See also

Learn more in the vignette:
[bibrecord](https://dataset.dataobservatory.eu/articles/bibrecord.html)

Other bibrecord functions:
[`as_datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md),
[`as_dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md)

## Examples

``` r
bibrecord(
  title = "Gross domestic product, volumes",
  author = person("Eurosat"),
  publisher = person("Eurostat"),
  identifier = "https://doi.org/10.2908/TEINA011",
  date = as.Date("2025-05-20")
)
#> Eurosat (2025). “Gross domestic product, volumes.”
```
