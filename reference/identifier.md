# Get or Set the Identifier of a Dataset or Metadata Record

Retrieve or assign the `identifier` attribute of a dataset or
bibliographic metadata object.

## Usage

``` r
identifier(x)

identifier(x, overwrite = TRUE) <- value
```

## Arguments

- x:

  A
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  object or a
  [`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html) object
  (including
  [`dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md)
  or
  [`datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md)
  records).

- overwrite:

  Logical. If `TRUE` (default), any existing identifier is replaced. If
  `FALSE`, an existing identifier is preserved unless it is `":unas"` or
  `":tba"`.

- value:

  A character string giving the identifier. Can be named (e.g.,
  `c(doi = "...")`) or unnamed. Numeric values are coerced to character.

## Value

For `identifier()`, the current identifier as a character string. For
`identifier<-()`, the updated object (invisible).

## Details

An *identifier* provides an unambiguous reference to a resource.
Recommended practice is to supply a persistent identifier string, such
as a DOI, ISBN, or URN, that conforms to a recognized identification
system.

Both [Dublin
Core](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/#identifier)
and [DataCite
4.4](https://support.datacite.org/docs/datacite-metadata-schema-v44-mandatory-properties#1-identifier)
define `identifier` as a core property. If the identifier is a DOI, it
will also be stored in the `doi` field of the metadata record.

Although `identifier` is not part of the minimal Dublin Core term set,
it is always included in `dataset` metadata for compatibility with
publishing and indexing systems. You may omit it if working under a
strict DC profile.

For best practice in choosing identifier schemes, see the
[IANA-registered URI
schemes](https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml).

## Examples

``` r
orange_copy <- orange_df

# Get the current identifier
identifier(orange_copy)
#> [1] "https://doi.org/10.5281/zenodo.14917851"

# Set a new identifier (e.g., a DOI)
identifier(orange_copy) <- "https://doi.org/10.9999/example.doi"

# Prevent accidental overwrite
identifier(orange_copy, overwrite = FALSE) <- "https://example.org/id"
#> Warning: The dataset has already an identifier: https://doi.org/10.9999/example.doi.
#> You can overwrite this message with identifier(x, overwrite = TRUE) <- value

# Use numeric and NULL values
identifier(orange_copy) <- 12345
identifier(orange_copy) <- NULL # Sets ":unas"
```
