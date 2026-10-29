# Get or set the bibentry

Retrieve or replace the bibliographic entry stored in a dataset's
attributes. The entry is a
[`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html) used to
hold citation metadata for
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
objects.

## Usage

``` r
get_bibentry(dataset)

set_bibentry(dataset) <- value
```

## Arguments

- dataset:

  A dataset created with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- value:

  A [`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html) to
  store on the dataset. If `NULL`, a minimal default entry is created.

## Value

- `get_bibentry(dataset)` returns the
  [`utils::bibentry()`](https://rdrr.io/r/utils/bibentry.html) stored in
  `dataset`'s attributes.

- `set_bibentry(dataset) <- value` sets the attribute and returns the
  modified dataset invisibly.

## Details

New datasets are initialized with reasonable defaults. To build a new
bibentry with sensible defaults and field names, use
[`datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md)
(DataCite) or
[`dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md)
(Dublin Core), then assign it with `set_bibentry(dataset) <- value`.

See the vignette for more background:
`vignette("bibentry", package = "dataset")`.

## See also

Other bibliographic helper functions:
[`contributor()`](https://docs.ropensci.org/dataset/reference/contributor.md),
[`creator()`](https://docs.ropensci.org/dataset/reference/creator.md),
[`dataset_format()`](https://docs.ropensci.org/dataset/reference/dataset_format.md),
[`dataset_title()`](https://docs.ropensci.org/dataset/reference/dataset_title.md),
[`description()`](https://docs.ropensci.org/dataset/reference/description.md),
[`geolocation()`](https://docs.ropensci.org/dataset/reference/geolocation.md),
[`language()`](https://docs.ropensci.org/dataset/reference/language.md),
[`publication_year()`](https://docs.ropensci.org/dataset/reference/publication_year.md),
[`publisher()`](https://docs.ropensci.org/dataset/reference/publisher.md),
[`relation()`](https://docs.ropensci.org/dataset/reference/relation.md),
[`rights()`](https://docs.ropensci.org/dataset/reference/rights.md),
[`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)

## Examples

``` r
# Get the bibentry of a dataset_df object:
be <- get_bibentry(orange_df)

# Create a well-formed bibentry (DataCite-style):
be2 <- datacite(
  Creator = person("Jane", "Doe"),
  Title = "The Orange Trees Dataset",
  Publisher = "MyOrg"
)

# Assign the new bibentry:
set_bibentry(orange_df) <- be2

# Inspect in different notations:
as_datacite(orange_df, type = "list")
#> $Title
#> [1] "The Orange Trees Dataset"
#> 
#> $Creator
#> [1] "Jane Doe"
#> 
#> $Identifier
#> [1] ":tba"
#> 
#> $Publisher
#> [1] "MyOrg"
#> 
#> $PublicationYear
#> [1] ":tba"
#> 
#> $Subject
#> $term
#> [1] "data sets"
#> 
#> $subjectScheme
#> [1] ""
#> 
#> $schemeURI
#> [1] ""
#> 
#> $valueURI
#> [1] ""
#> 
#> $classificationCode
#> NULL
#> 
#> $prefix
#> [1] ""
#> 
#> attr(,"class")
#> [1] "subject" "list"   
#> 
#> $Type
#> [1] "Dataset"
#> 
#> $Contributor
#> NULL
#> 
#> $Date
#> [1] ":tba"
#> 
#> $Language
#> [1] ":unas"
#> 
#> $AlternateIdentifier
#> [1] ":unas"
#> 
#> $RelatedIdentifier
#> [1] ":unas"
#> 
#> $Format
#> [1] ":tba"
#> 
#> $Version
#> [1] "0.1.0"
#> 
#> $Rights
#> [1] ":tba"
#> 
#> $Description
#> [1] ":tba"
#> 
#> $Geolocation
#> [1] ":unas"
#> 
#> $FundingReference
#> [1] ":unas"
#> 
as_dublincore(orange_df, type = "list")
#> $title
#> [1] "The Orange Trees Dataset"
#> 
#> $creator
#> [1] "Jane Doe"
#> 
#> $identifier
#> [1] ":tba"
#> 
#> $publisher
#> [1] "MyOrg"
#> 
#> $subject
#> [1] "data sets"
#> 
#> $type
#> [1] "DCMITYPE:Dataset"
#> 
#> $contributor
#> [1] ""
#> 
#> $date
#> [1] ":tba"
#> 
#> $language
#> [1] ":unas"
#> 
#> $relation
#> [1] ":unas"
#> 
#> $dataset_format
#> [1] ":tba"
#> 
#> $rights
#> [1] ":tba"
#> 
#> $datasource
#> [1] ":unas"
#> 
#> $description
#> [1] ":tba"
#> 
#> $coverage
#> [1] ":unas"
#> 
```
