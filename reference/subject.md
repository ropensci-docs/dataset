# Create, add, or retrieve a subject

Manage the subject metadata of a dataset. The subject can be stored as a
simple character term or as a structured object with subproperties
created by `subject_create()`.

## Usage

``` r
subject(x)

subject_create(
  term,
  schemeURI = NULL,
  valueURI = NULL,
  prefix = NULL,
  subjectScheme = NULL,
  classificationCode = NULL
)

subject(x) <- value

is.subject(x)
```

## Arguments

- x:

  A dataset object created with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- term:

  A subject term, for example `"Data sets"`.

- schemeURI:

  URI of the subject identifier scheme, for example
  `"http://id.loc.gov/authorities/subjects"`.

- valueURI:

  URI of the subject term, for example
  `"https://id.loc.gov/authorities/subjects/sh2018002256"`.

- prefix:

  Abbreviated prefix for a scheme URI, for example `"lcch:"`. Widely
  used namespaces (schemes) have conventional abbreviations.

- subjectScheme:

  Name of the subject scheme, classification code, or authority if one
  is used. This acts as a namespace.

- classificationCode:

  Classification code for schemes that do not have `valueURI` entries
  for each subject term (e.g., ANZSRC).

- value:

  A subject object created by `subject_create()` or a character string.
  Used by `subject<-` to replace the subject.

## Value

- `subject(x)` returns:

  - a single `"subject"` object if only one is present,

  - a list of `"subject"` objects if multiple are present,

  - otherwise falls back to the plain string from the bibentry.

- `subject(x) <- value` accepts a character vector, a `"subject"`
  object, or a list of `"subject"` objects, and updates both the
  bibentry slot and the `"subject"` attribute. Returns the dataset
  invisibly.

- `subject_create()` returns a structured `"subject"` object \<U+2014\>
  or a list of them if multiple terms are provided.

- `is.subject(x)` returns `TRUE` if `x` inherits from class `"subject"`.

## Details

The subject property records what the dataset is about. The [DataCite
subject property](https://schema.datacite.org/meta/kernel-4/) allows
multiple subproperties, but these cannot be stored directly in a
standard [`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html)
object. Therefore:

- If you set a character string as the subject, it is stored in both the
  bibentry and the `"subject"` attribute.

- If you set a structured subject (via `subject_create()`), the `$term`
  value is stored in the bibentry, and the full object is stored in the
  `"subject"` attribute of the `dataset_df` object.

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
[`rights()`](https://docs.ropensci.org/dataset/reference/rights.md)

## Examples

``` r
# Set a structured subject
subject(orange_df) <- subject_create(
  term = "Oranges",
  schemeURI = "http://id.loc.gov/authorities/subjects",
  valueURI = "http://id.loc.gov/authorities/subjects/sh85095257",
  subjectScheme = "LCCH",
  prefix = "lcch:"
)

# Retrieve subject with subproperties
subject(orange_df)
#> $term
#> [1] "Oranges"
#> 
#> $subjectScheme
#> [1] "LCCH"
#> 
#> $schemeURI
#> [1] "http://id.loc.gov/authorities/subjects"
#> 
#> $valueURI
#> [1] "http://id.loc.gov/authorities/subjects/sh85095257"
#> 
#> $classificationCode
#> NULL
#> 
#> $prefix
#> [1] "lcch:"
#> 
#> attr(,"class")
#> [1] "subject" "list"   
```
