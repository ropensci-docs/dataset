# Dataset to triples (three columns or N-Triples)

Converts a dataset to RDF-style triples with subject, predicate, and
object columns. Supports semantic expansion via variable metadata.

## Usage

``` r
dataset_to_triples(x, idcol = NULL, expand_uri = TRUE, format = "data.frame")
```

## Arguments

- x:

  A `dataset_df` or `data.frame`.

- idcol:

  Name or index of the subject column. If NULL, defaults to `"rowid"` or
  rownames.

- expand_uri:

  Logical; if TRUE, expands URIs using namespaces and definitions.

- format:

  Output format: `"data.frame"` (default) or `"nt"` for N-Triples.

## Value

Either a `data.frame` with columns `s`, `p`, and `o`, or a character
vector of N-Triple lines.

## Details

For publishing examples, a minimal serverless scaffold is provided at
<https://github.com/dataobservatory-eu/dataset-template>, which shows
how to host CSV + RDF serialisations on GitHub Pages without any server
setup.

## Note

A simple, serverless scaffolding for publishing `dataset_df` objects on
the web (with HTML + RDF exports) is available at
<https://github.com/dataobservatory-eu/dataset-template>.

## Examples

``` r
# A minimal example with just rowid and geo
data("gdp", package = "dataset")
small_geo <- dataset_df(
  geo = defined(
    gdp$geo[1:3],
    label = "Geopolitical entity",
    concept = "http://example.com/prop/geo",
    namespace = "https://dd.eionet.europa.eu/vocabulary/eurostat/geo/$1"
  )
)

# View as triple table
dataset_to_triples(small_geo)
#>                                    s                           p
#> 1 http://example.com/dataset#obsobs1 http://example.com/prop/geo
#> 2 http://example.com/dataset#obsobs2 http://example.com/prop/geo
#> 3 http://example.com/dataset#obsobs3 http://example.com/prop/geo
#>                                                        o
#> 1 https://dd.eionet.europa.eu/vocabulary/eurostat/geo/AD
#> 2 https://dd.eionet.europa.eu/vocabulary/eurostat/geo/AD
#> 3 https://dd.eionet.europa.eu/vocabulary/eurostat/geo/AD

# View as N-Triples
dataset_to_triples(small_geo, format = "nt")
#> [1] "<http://example.com/dataset#obsobs1> <http://example.com/prop/geo> <https://dd.eionet.europa.eu/vocabulary/eurostat/geo/AD> ."
#> [2] "<http://example.com/dataset#obsobs2> <http://example.com/prop/geo> <https://dd.eionet.europa.eu/vocabulary/eurostat/geo/AD> ."
#> [3] "<http://example.com/dataset#obsobs3> <http://example.com/prop/geo> <https://dd.eionet.europa.eu/vocabulary/eurostat/geo/AD> ."
```
