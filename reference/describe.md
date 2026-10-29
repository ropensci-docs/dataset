# Describe a dataset in N-Triples format

Writes provenance and Dublin Core metadata of a dataset to a file or
connection in N-Triples format.

## Usage

``` r
describe(x, con)
```

## Arguments

- x:

  A `dataset_df` object.

- con:

  A connection or a character string path (e.g. from
  [`tempfile()`](https://rdrr.io/r/base/tempfile.html)).

## Value

Writes N-Triples to `con` and invisibly returns `x`.

## Examples

``` r
test_ds <- dataset_df(
  rowid = defined(c("eg:1", "eg:2"),
    namespace = "http://example.com/dataset#"
  ),
  geo = defined(
    gdp$geo[1:2],
    label = "Country",
    concept = "http://example.com/prop/geo",
    namespace = "https://eionet.europa.eu/geo/$1"
  ),
  dataset_bibentry = dublincore(
    title = "Example Dataset",
    creator = person("John", "Doe")
  )
)

# returns invisibly the contents of the text file serialisation:
testdescription <- describe(test_ds, con = tempfile())
testdescription
#> Doe (2026): Example Dataset [dataset]
#>   rowid geo   
#>   <chr> <chr>
#> 1 eg:1  AD   
#> 2 eg:2  AD    
```
