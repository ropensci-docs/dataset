# Create a new `dataset_df` object

The `dataset_df()` constructor creates semantically rich modern data
frames. These inherit from `tbl_df` and carry structured metadata using
attributes.

## Usage

``` r
dataset_df(
  ...,
  identifier = c(obs = "http://example.com/dataset#obs"),
  var_labels = NULL,
  units = NULL,
  concepts = NULL,
  dataset_bibentry = NULL,
  dataset_subject = NULL
)

as_dataset_df(
  df,
  identifier = c(obs = "http://example.com/dataset#obs"),
  var_labels = NULL,
  units = NULL,
  concepts = NULL,
  dataset_bibentry = NULL,
  dataset_subject = NULL,
  ...
)

is.dataset_df(x)

# S3 method for class 'dataset_df'
print(x, ...)

is_dataset_df(x)

# S3 method for class 'dataset_df'
names(x)
```

## Arguments

- ...:

  Vectors (columns) that should be included in the dataset.

- identifier:

  A named vector of one or more URI prefixes for row IDs. Defaults to
  `c(eg = "http://example.com/dataset#")`. For example, if your dataset
  will be published under DOI `https://doi.org/1234`, you may use
  `c(obs = "https://doi.org/1234#")`, which will generate row URIs such
  as `https://doi.org/1234#1`, ..., `#n`.

- var_labels:

  A named list of human-readable labels for each variable.

- units:

  A named list of measurement units for measured variables.

- concepts:

  A named list of linked concepts (URIs) for variables or dimensions.

- dataset_bibentry:

  A bibliographic metadata record for the dataset, created using
  [`datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md)
  or
  [`dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md).

- dataset_subject:

  A subject descriptor created with
  [`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)
  or
  [`subject_create()`](https://docs.ropensci.org/dataset/reference/subject.md).

- df:

  A `data.frame` to convert to a `dataset_df`.

- x:

  A `dataset_df` object (used in method dispatch).

## Value

A `dataset_df` object: a tibble with attached metadata stored in
attributes.

`is.dataset_df` returns a logical value (if the object is of class
`dataset_df`.)

## Details

Use `is.dataset_df()` to check class membership.

S3 methods for `dataset_df` include:

- [`print()`](https://rdrr.io/r/base/print.html) to display the dataset
  with metadata

- [`summary()`](https://rdrr.io/r/base/summary.html) to summarize both
  data and metadata

- [`names()`](https://rdrr.io/r/base/names.html) to retrieve variable
  names using standard data frame semantics

For full details, see
[`vignette("dataset_df", package = "dataset")`](https://docs.ropensci.org/dataset/articles/dataset_df.md).

## Note

A simple, serverless scaffolding for publishing `dataset_df` objects on
the web (with HTML + RDF exports) is available at
<https://github.com/dataobservatory-eu/dataset-template>.

## See also

[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md),
[`dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md),
[`datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md),
[`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)

## Examples

``` r
my_dataset <- dataset_df(
  country_name = defined(
    c("AD", "LI"),
    concept = "http://data.europa.eu/bna/c_6c2bb82d",
    namespace = "https://www.geonames.org/countries/$1/"
  ),
  gdp = defined(
    c(3897, 7365),
    label = "Gross Domestic Product",
    unit = "million dollars",
    concept = "http://data.europa.eu/83i/aa/GDP"
  ),
  identifier = c(
    obs = "https://dataobservatory-eu.github.io/dataset-template#"
  ),
  dataset_bibentry = dublincore(
    title = "GDP of Andorra and Liechtenstein",
    description = "A small but semantically rich dataset example.",
    creator = person("Jane", "Doe", role = "cre"),
    publisher = "Open Data Institute",
    language = "en"
  )
)

# Basic usage
print(my_dataset)
#> Doe (2026): GDP of Andorra and Liechtenstein [dataset]
#>   rowid country_name   gdp 
#>   <chr> <chr>        <dbl>
#> 1 obs1  AD            3897
#> 2 obs2  LI            7365 
head(my_dataset)
#> Doe (2026): GDP of Andorra and Liechtenstein [dataset]
#>   rowid country_name   gdp 
#>   <chr> <chr>        <dbl>
#> 1 obs1  AD            3897
#> 2 obs2  LI            7365 
summary(my_dataset)
#> Doe (2026): Summary of GDP of Andorra and Liechtenstein [dataset]
#> 
#> Gross Domestic Product (million dollars)
#>        rowid      country_name      gdp      
#>  Length   :2   Length   :2     Min.   :3897  
#>  N.unique :2   N.unique :2     1st Qu.:4764  
#>  N.blank  :0   N.blank  :0     Median :5631  
#>  Min.nchar:4   Min.nchar:2     Mean   :5631  
#>  Max.nchar:4   Max.nchar:2     3rd Qu.:6498  
#>                                Max.   :7365  

# Metadata access
as_dublincore(my_dataset)
#> Dublin Core Metadata Record
#> --------------------------
#> Title:       GDP of Andorra and Liechtenstein
#> Creator(s):  Jane Doe [cre]
#> Contributor(s): :unas
#> Publisher:   Open Data Institute
#> Year:        2026
#> Language:    en
#> Description: A small but semantically rich dataset example.
as_datacite(my_dataset)
#> DataCite Metadata Record
#> --------------------------
#> Title:       GDP of Andorra and Liechtenstein
#> Creator(s):  Jane Doe [cre]
#> Contributor(s): :unas
#> Identifier:  :tba
#> Publisher:   Open Data Institute
#> Year:        2026
#> Language:    en
#> Description: A small but semantically rich dataset example.

# Export description as RDF triples
my_description <- describe(my_dataset, con = tempfile())
my_description
#> Doe (2026): GDP of Andorra and Liechtenstein [dataset]
#>   rowid country_name   gdp 
#>   <chr> <chr>        <dbl>
#> 1 obs1  AD            3897
#> 2 obs2  LI            7365 
```
