# Convert to XML Schema Definition (XSD) Types

Converts R vectors, data frames, and `dataset_df` objects to [XML Schema
Definition (XSD)](https://www.w3.org/TR/xmlschema11-2/) compatible
string representations such as `xsd:decimal`, `xsd:boolean`, `xsd:date`,
and `xsd:dateTime`.

## Usage

``` r
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'haven_labelled_defined'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'data.frame'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'dataset_df'
xsd_convert(x, idcol = "rowid", shortform = TRUE, ...)

# S3 method for class 'tbl_df'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'character'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'numeric'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'integer'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'logical'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'factor'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'POSIXct'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'Date'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)

# S3 method for class 'difftime'
xsd_convert(x, idcol = NULL, shortform = TRUE, ...)
```

## Arguments

- x:

  An object (vector, data frame, tibble, or `dataset_df`).

- idcol:

  Column name or position to use as row (observation) identifier. If
  `NULL`, row names are used.

- shortform:

  Logical. If `TRUE` (default), datatypes are abbreviated with the
  `xsd:` prefix (e.g. `"42"^^<xsd:integer>`). If `FALSE`, datatypes are
  expanded to full URIs (e.g.
  `"42"^^<http://www.w3.org/2001/XMLSchema#integer>`).

- ...:

  Additional arguments passed to methods.

## Value

A character vector or data frame with values serialized as
XSD-compatible RDF literals.

## Details

This is primarily used for generating RDF-compatible typed literals.

- For **vectors**, returns a character vector of typed literals.

- For **data frames** or tibbles, returns a data frame with the same
  structure but with all values converted to XSD strings.

- For `dataset_df` objects, behaves like the data frame method but
  preserves dataset-level attributes.

## Class-specific examples

    xsd_convert(42L)                   # integer -> xsd:integer
    xsd_convert(c(TRUE, FALSE, NA))    # logical -> xsd:boolean
    xsd_convert(Sys.Date())            # Date -> xsd:date
    xsd_convert(Sys.time())            # POSIXct -> xsd:dateTime
    xsd_convert(factor("apple"))       # factor -> xsd:string
    xsd_convert(c("apple", "banana"))  # character -> xsd:string

## Examples

``` r
# Simple data frame with mixed types
df <- data.frame(
  id     = 1:2,
  value  = c(3.14, 2.71),
  active = c(TRUE, FALSE),
  date   = as.Date(c("2020-01-01", "2020-12-31"))
)

# Short vs long-form URI:
xsd_convert(120L, shortform = TRUE)
#> [1] "\"120\"^^<xsd:integer>"
xsd_convert(121L, shortform = FALSE)
#> [1] "\"121\"^^<http://www.w3.org/2001/XMLSchema#integer>"
```
