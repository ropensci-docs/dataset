# Add or Retrieve Dublin Core Metadata

Adds or retrieves metadata conforming to the [Dublin Core Metadata
Terms](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/)
standard, enabling consistent and structured citation and retrieval of R
dataset objects.

`is.dublincore()` checks whether an object inherits from the
`"dublincore"` class.

## Usage

``` r
as_dublincore(x, type = "bibentry", ...)

dublincore(
  title,
  creator,
  contributor = NULL,
  year = NULL,
  publisher = NULL,
  identifier = NULL,
  subject = NULL,
  type = "DCMITYPE:Dataset",
  dataset_date = NULL,
  language = NULL,
  relation = NULL,
  dataset_format = "application/r-rds",
  rights = NULL,
  datasource = NULL,
  description = NULL,
  coverage = NULL
)

is.dublincore(x)

# S3 method for class 'dublincore'
print(x, ...)
```

## Source

- [DCMI Metadata
  Terms](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/)

## Arguments

- x:

  An object to test.

- type:

  The resource type. For datasets, use `"Dataset"`. See [DCMI Type
  Vocabulary](https://www.dublincore.org/specifications/dublin-core/dcmi-type-vocabulary/).

- ...:

  Additional metadata fields.

- title:

  A name given to the resource. See
  [`dataset_title()`](https://docs.ropensci.org/dataset/reference/dataset_title.md).

- creator:

  One or more [`utils::person()`](https://rdrr.io/r/utils/person.html)
  objects representing the creator(s). See
  [`creator()`](https://docs.ropensci.org/dataset/reference/creator.md).

- contributor:

  Additional contributors
  ([`utils::person()`](https://rdrr.io/r/utils/person.html)) with
  optional roles. See
  [`contributor()`](https://docs.ropensci.org/dataset/reference/contributor.md).

- year:

  An explicit publication year. If omitted, inferred from
  `dataset_date`.

- publisher:

  A character or
  [`utils::person()`](https://rdrr.io/r/utils/person.html) indicating
  the publishing entity. See
  [`publisher()`](https://docs.ropensci.org/dataset/reference/publisher.md).

- identifier:

  A unique persistent identifier (e.g., DOI). See
  [`identifier()`](https://docs.ropensci.org/dataset/reference/identifier.md).

- subject:

  A keyword or controlled vocabulary term. See
  [`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)
  and
  [`subject_create()`](https://docs.ropensci.org/dataset/reference/subject.md).

- dataset_date:

  A publication or release date (`Date`, `POSIXct`, or character in
  `YYYY`, `YYYY-MM-DD`, or ISO format).

- language:

  ISO 639-1 language code. See
  [`language()`](https://docs.ropensci.org/dataset/reference/language.md).

- relation:

  A related resource (e.g., version, paper, or parent dataset).
  Currently only supports an URI, for example,
  `"https:://doi.org/10.32614/CRAN.package.dataset"`.

- dataset_format:

  The technical format of the dataset (e.g., MIME type). See
  [`dataset_format()`](https://docs.ropensci.org/dataset/reference/dataset_format.md).

- rights:

  A string describing intellectual property or usage rights. Use a URI
  like `"https://creativecommons.org/public-domain/cc0/"`.

- datasource:

  A URL or label for the original source of the dataset.

- description:

  A free-text summary of the dataset. See
  [`description()`](https://docs.ropensci.org/dataset/reference/description.md).

- coverage:

  Geographic or temporal extent (spatial/temporal coverage).

## Value

A `bibentry` object extended with class `"bibrecord"`, storing
structured Dublin Core metadata. Use `as_dublincore()` to extract the
metadata in list, tabular, or RDF form.

A logical value: `TRUE` if `x` is a Dublin Core metadata record (i.e.,
inherits from `"dublincore"`), otherwise `FALSE`.

## Details

The Dublin Core Metadata Element Set (DCMES) is a standardized
vocabulary for describing digital and physical resources. It includes 15
core fields and is formally standardized as ISO 15836, IETF RFC 5013,
and ANSI/NISO Z39.85.

This function constructs a
[`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html) object
extended with DCMI terms and is compatible with
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
objects. The resulting metadata can be used for semantic documentation
and machine-readable citation.

For compatibility with
[`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html), the
`dataset_date` parameter is automatically used to derive both
`publication_date` and `year` fields.

## See also

Learn more in the vignette:
[bibrecord](https://dataset.dataobservatory.eu/articles/bibrecord.html)

Other bibrecord functions:
[`as_datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md),
[`bibrecord()`](https://docs.ropensci.org/dataset/reference/bibrecord.md)

## Examples

``` r
orange_bibentry <- dublincore(
  title = "Growth of Orange Trees",
  creator = c(
    person(
      given = "N.R.",
      family = "Draper",
      role = "cre",
      comment = c(VIAF = "http://viaf.org/viaf/84585260")
    ),
    person(given = "H", family = "Smith", role = "cre")
  ),
  contributor = person(given = "Antal", family = "Daniel", role = "dtm"),
  publisher = "Wiley",
  datasource = "https://isbnsearch.org/isbn/9780471170822",
  dataset_date = 1998,
  identifier = "https://doi.org/10.5281/zenodo.14917851",
  language = "en",
  description = "The Orange data frame has 35 rows and 3 columns of records
                 of the growth of orange trees."
)

# To inspect structured metadata from a dataset_df object:
as_dublincore(orange_df, type = "list")
#> $title
#> [1] "Growth of Orange Trees"
#> 
#> $creator
#> [1] "N.R. Draper [cre] (VIAF: http://viaf.org/viaf/84585260)"
#> [2] "H Smith [cre]"                                          
#> 
#> $identifier
#> [1] "https://doi.org/10.5281/zenodo.14917851"
#> 
#> $publisher
#> [1] "Wiley"
#> 
#> $subject
#> NULL
#> 
#> $type
#> [1] "DCMITYPE:Dataset"
#> 
#> $contributor
#> [1] "Antal Daniel [dtm]"
#> 
#> $date
#> [1] "1998"
#> 
#> $language
#> [1] "en"
#> 
#> $relation
#> [1] ":unas"
#> 
#> $dataset_format
#> [1] ":unas"
#> 
#> $rights
#> [1] ":tba"
#> 
#> $datasource
#> [1] "https://isbnsearch.org/isbn/9780471170822"
#> 
#> $description
#> [1] "The Orange data frame has 35 rows and 3 columns of records of the growth of orange trees."
#> 
#> $coverage
#> [1] ":unas"
#> 
```
