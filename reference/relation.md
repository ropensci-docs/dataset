# Add or retrieve related items (DataCite/Dublin Core)

Manage related resources for a dataset using a unified accessor.

- For **DataCite 4.x**, this maps to `relatedIdentifier` (+ type &
  relation).

- For **Dublin Core**, this maps to `dct:relation` (string).

## Usage

``` r
relation(x)

relation(x) <- value

related_create(
  relatedIdentifier,
  relationType,
  relatedIdentifierType,
  resourceTypeGeneral = NULL
)

is.related(x)

related_item(x)

related_item(x) <- value
```

## Arguments

- x:

  A dataset object created with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- value:

  A `related` object from `related_create()` or a character. Vectors of
  characters are also supported and will be converted to a list of
  `"related"` objects.

- relatedIdentifier:

  A string with the identifier of the related resource.

- relationType:

  A string naming the relation type (per DataCite vocabulary).

- relatedIdentifierType:

  A string naming the identifier type (`"DOI"`, `"URL"`, etc.).

- resourceTypeGeneral:

  Optional: a string naming the general type of the related resource.

## Value

- `relation(x)` returns:

  - a single structured `"related"` object (from `related_create()`) if
    only one relation is present,

  - a list of `"related"` objects if multiple relations are present,

  - otherwise it falls back to the bibentry field (`relatedidentifier`
    for DataCite or `relation` for Dublin Core).

- `relation(x) <- value` sets the `"relation"` attribute (structured
  object or list of objects) and the bibentry string fields
  (`relatedidentifier` and `relation`), and returns the dataset
  invisibly.

- `related_create()` constructs a structured `"related"` object.

- `is.related(x)` returns `TRUE` if `x` inherits from class `"related"`.

## Details

To remain compatible with
[`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html), the
bibentry stores only the **string identifier** (e.g., DOI/URL). The full
structured object created by `related_create()` is preserved in the
`"relation"` attribute.

A `"related"` object is a small S3 list with the following elements:

- `relatedIdentifier`: the related resource identifier (DOI, URL, etc.)

- `relationType`: the DataCite relation type (e.g., `"IsPartOf"`,
  `"References"`)

- `relatedIdentifierType`: the type of identifier (`"DOI"`, `"URL"`,
  etc.)

- `resourceTypeGeneral`: optional, the general type of the related
  resource (e.g., `"Text"`, `"Dataset"`)

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
[`rights()`](https://docs.ropensci.org/dataset/reference/rights.md),
[`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)

## Examples

``` r
df <- dataset_df(data.frame(x = 1))
relation(df) <- related_create(
  relatedIdentifier = "10.1234/example",
  relationType = "IsPartOf",
  relatedIdentifierType = "DOI"
)
relation(df) # structured object
#> $relatedIdentifier
#> [1] "10.1234/example"
#> 
#> $relationType
#> [1] "IsPartOf"
#> 
#> $relatedIdentifierType
#> [1] "DOI"
#> 
#> $resourceTypeGeneral
#> NULL
#> 
#> attr(,"class")
#> [1] "related" "list"   
get_bibentry(df)$relation # "10.1234/example"
#> [1] "10.1234/example"
get_bibentry(df)$relatedidentifier # "10.1234/example"
#> [1] "10.1234/example"

# Character input is normalized to a DOI/URL with default types
relation(df) <- "https://doi.org/10.5678/xyz"
relation(df) # structured object (relationType/Type filled with defaults)
#> $relatedIdentifier
#> [1] "https://doi.org/10.5678/xyz"
#> 
#> $relationType
#> [1] "IsPartOf"
#> 
#> $relatedIdentifierType
#> [1] "URL"
#> 
#> $resourceTypeGeneral
#> NULL
#> 
#> attr(,"class")
#> [1] "related" "list"   

# Create related object directly
rel <- related_create("https://doi.org/10.5678/xyz", "References", "DOI")
is.related(rel) # TRUE
#> [1] TRUE
```
