# Create a Bibentry Object with DataCite Metadata Fields

Constructs a bibliographic metadata record conforming to the [DataCite
Metadata Schema](https://schema.datacite.org/). The resulting object is
stored as a modified
[`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html) enriched
with structured Dublin Core and DataCite-compliant metadata.

## Usage

``` r
as_datacite(x, type = "bibentry", ...)

datacite(
  Title,
  Creator,
  Identifier = NULL,
  Publisher = NULL,
  PublicationYear = NULL,
  Subject = subject_create(term = "data sets", subjectScheme =
    "Library of Congress Subject Headings (LCSH)", schemeURI =
    "https://id.loc.gov/authorities/subjects.html", valueURI =
    "http://id.loc.gov/authorities/subjects/sh2018002256"),
  Type = "Dataset",
  Contributor = NULL,
  Date = ":tba",
  DateList = NULL,
  Language = NULL,
  AlternateIdentifier = ":unas",
  RelatedIdentifier = ":unas",
  Format = ":tba",
  Version = "0.1.0",
  Rights = ":tba",
  Description = ":tba",
  Geolocation = ":unas",
  FundingReference = ":unas"
)

is.datacite(x)

# S3 method for class 'datacite'
is.datacite(x)

# S3 method for class 'datacite'
print(x, ...)
```

## Source

- [DataCite 4.3 Mandatory
  Properties](https://support.datacite.org/docs/schema-mandatory-properties-v43)

- [DataCite 4.3 Optional
  Properties](https://support.datacite.org/docs/schema-optional-properties-v43)

## Arguments

- x:

  An object that is tested if it has a class "datacite".

- type:

  A DataCite 4.4 metadata can be returned as: `"list"`, `"dataset_df"`,
  `"bibentry"` (default), or `"ntriples"`.

- ...:

  Optional parameters to add to a `datacite` object. For example,
  `author = person("Jane", "Doe")` adds an author if
  `type = "dataset_df"`.

- Title:

  The name(s) by which the resource is known. Similar to
  [dct:title](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/elements11/title/).

- Creator:

  One or more [`utils::person()`](https://rdrr.io/r/utils/person.html)
  objects describing the main authors or contributors responsible for
  creating the resource.

- Identifier:

  A persistent identifier (e.g., DOI or URI). May refer to a specific
  version or all versions of the resource.

- Publisher:

  The name of the organization that holds, publishes, or distributes the
  resource. Required by DataCite. See
  [`publisher()`](https://docs.ropensci.org/dataset/reference/publisher.md).

- PublicationYear:

  The year of public availability (in `YYYY` format). See
  [`publication_year()`](https://docs.ropensci.org/dataset/reference/publication_year.md).

- Subject:

  A topic, keyword, or classification term. See
  [`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)
  and
  [`subject_create()`](https://docs.ropensci.org/dataset/reference/subject.md)
  for structured vocabularies.

- Type:

  The resource type. Defaults to `"Dataset"` for general use. See
  [dcm:type](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/elements11/type/).

- Contributor:

  An individual or institution that contributed to the development,
  distribution, or curation of the resource.

- Date:

  A date in `"YYYY"`, `"YYYY-MM-DD"` or ISO datetime format. Can also be
  a [Date](https://rdrr.io/r/base/Dates.html) or
  [POSIXct](https://rdrr.io/r/base/DateTimeClasses.html) object.

- DateList:

  A list of multiple dates. Currently not supported.

- Language:

  Language code as per IETF BCP 47 / ISO 639-1. See
  [`language()`](https://docs.ropensci.org/dataset/reference/language.md).

- AlternateIdentifier:

  Optional local or secondary identifier. Defaults to `":unas"`.

- RelatedIdentifier:

  Related resources (e.g., prior versions, papers). Defaults to
  `":unas"`.

- Format:

  A technical format (e.g., `"application/pdf"`, `"text/csv"`).

- Version:

  A free-text version string (e.g., `"1.0.0"`). Defaults to `"0.1.0"`.
  See [`version()`](https://rdrr.io/r/base/Version.html).

- Rights:

  Licensing or usage restrictions for the resource. Defaults to
  `":tba"`. See
  [`rights()`](https://docs.ropensci.org/dataset/reference/rights.md).

- Description:

  Free-text summary or additional information. Defaults to `":tba"`.

- Geolocation:

  Geographic location covered or referenced by the resource. See
  [`geolocation()`](https://docs.ropensci.org/dataset/reference/geolocation.md).

- FundingReference:

  Information about funding or financial support. Defaults to `":unas"`.
  Structured funding metadata not yet implemented.

## Value

`as_datacite(x, type)` returns the DataCite bibliographical metadata of
`x` either as a list, a bibentry object, an N-Triples text serialisation
or a dataset_df object.

A [`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html) object
with DataCite-compliant fields. Use `as_datacite()` to extract the
metadata as a list or bibentry object.

`is.datacite()` returns a logical values (if the object `x` is of class
`datacite`).

## Details

DataCite is a leading non-profit organization that provides persistent
identifiers (DOIs) for research data and other research outputs. Members
of the research community use DataCite to register datasets with
globally resolvable metadata for citation and discovery.

This function sets `"Dataset"` as the default resource type. The `Size`
attribute (e.g., bytes, pages, etc.) is automatically added if
available.

## See also

Learn more in the vignette:
[bibrecord](https://dataset.dataobservatory.eu/articles/bibrecord.html)

Other bibrecord functions:
[`as_dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md),
[`bibrecord()`](https://docs.ropensci.org/dataset/reference/bibrecord.md)

## Examples

``` r
datacite(
  Title = "Growth of Orange Trees",
  Creator = c(
    person(
      given = "N.R.",
      family = "Draper",
      role = "cre",
      comment = c(VIAF = "http://viaf.org/viaf/84585260")
    ),
    person(
      given = "H",
      family = "Smith",
      role = "cre"
    )
  ),
  Publisher = "Wiley",
  Date = 1998,
  Language = "en"
)
#> DataCite Metadata Record
#> --------------------------
#> Title:       Growth of Orange Trees
#> Creator(s):  N.R. Draper [cre] (VIAF: http://viaf.org/viaf/84585260); H Smith [cre]
#> Subject(s):  data sets [https://id.loc.gov/authorities/subjects.html]
#> Publisher:   Wiley
#> Year:        1998
#> Language:    en
#> Description: :tba

# Extract bibliographic metadata
as_datacite(orange_df)
#> DataCite Metadata Record
#> --------------------------
#> Title:       Growth of Orange Trees
#> Creator(s):  N.R. Draper [cre] (VIAF: http://viaf.org/viaf/84585260); H Smith [cre]
#> Contributor(s): {Antal Daniel [dtm]}
#> Identifier:  https://doi.org/10.5281/zenodo.14917851
#> Publisher:   Wiley
#> Year:        1998
#> Language:    en
#> Description: The Orange data frame has 35 rows and 3 columns of records of the growth of orange trees.

# As a list
as_datacite(orange_df, "list")
#> $Title
#> [1] "Growth of Orange Trees"
#> 
#> $Creator
#> [1] "N.R. Draper [cre] (VIAF: http://viaf.org/viaf/84585260)"
#> [2] "H Smith [cre]"                                          
#> 
#> $Identifier
#> [1] "https://doi.org/10.5281/zenodo.14917851"
#> 
#> $Publisher
#> [1] "Wiley"
#> 
#> $PublicationYear
#> [1] "1998"
#> 
#> $Subject
#> NULL
#> 
#> $Type
#> [1] "Dataset"
#> 
#> $Contributor
#> [1] "Antal Daniel [dtm]"
#> 
#> $Date
#> [1] "1998"
#> 
#> $Language
#> [1] "en"
#> 
#> $AlternateIdentifier
#> [1] ":unas"
#> 
#> $RelatedIdentifier
#> [1] ":unas"
#> 
#> $Format
#> [1] ":unas"
#> 
#> $Version
#> [1] ":unas"
#> 
#> $Rights
#> [1] ":tba"
#> 
#> $Description
#> [1] "The Orange data frame has 35 rows and 3 columns of records of the growth of orange trees."
#> 
#> $Geolocation
#> [1] ":unas"
#> 
#> $FundingReference
#> [1] ":unas"
#> 
```
