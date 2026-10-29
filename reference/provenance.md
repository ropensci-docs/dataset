# Get or update provenance information

Retrieve or append provenance statements (in N\<U+2011\>Triples form)
stored on a
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
object.

## Usage

``` r
provenance(x)

provenance(x) <- value
```

## Arguments

- x:

  A dataset created with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- value:

  Character vector of N\<U+2011\>Triples created by
  [`n_triple()`](https://docs.ropensci.org/dataset/reference/n_triple.md)
  or
  [`n_triples()`](https://docs.ropensci.org/dataset/reference/n_triples.md)
  to append to existing provenance.

## Value

- `provenance(x)` returns the contents of the `"prov"` attribute
  (character vector of N\<U+2011\>Triples), or `NULL` if none is set.

- `provenance(x) <- value` appends `value` to the `"prov"` attribute and
  returns the modified dataset invisibly.

## Details

Provenance is stored in the `"prov"` attribute as N\<U+2011\>Triples
text. Use
[`n_triple()`](https://docs.ropensci.org/dataset/reference/n_triple.md)
or
[`n_triples()`](https://docs.ropensci.org/dataset/reference/n_triples.md)
to construct valid statements that follow PROV\<U+2011\>O (e.g.,
`prov:wasGeneratedBy`, `prov:wasInformedBy`).

## Examples

``` r
provenance(orange_df)
#> [1] "<http://example.com/dataset_prov.nt> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Bundle> ."                      
#> [2] "<http://example.com/dataset#> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Entity> ."                             
#> [3] "<http://example.com/dataset#> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://purl.org/linked-data/cube#DataSet> ."                     
#> [4] "<http://viaf.org/viaf/84585260> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Agent> ."                            
#> [5] "\"_:smithh\" <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Agent> ."                                               
#> [6] "<https://doi.org/10.32614/CRAN.package.dataset> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#SoftwareAgent> ."    
#> [7] "<http://example.com/creation> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Activity> ."                           
#> [8] "<http://example.com/creation> <http://www.w3.org/ns/prov#generatedAtTime> \"2025-05-22T23:19:29Z\"^^<http://www.w3.org/2001/XMLSchema#dateTime> ."

# Add a provenance statement:
provenance(orange_df) <- n_triple(
  "https://doi.org/10.5281/zenodo.10396807",
  "http://www.w3.org/ns/prov#wasInformedBy",
  "http://example.com/source#1"
)
```
