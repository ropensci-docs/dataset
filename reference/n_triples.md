# Create N-Triples

Create RDF triple statements to annotate your dataset with standard,
interoperable metadata.

## Usage

``` r
n_triples(triples)
```

## Arguments

- triples:

  A character vector of concatenated N-Triples, created with
  [`n_triple()`](https://docs.ropensci.org/dataset/reference/n_triple.md).

## Value

A character vector of unique N-Triple strings.

## Details

N-Triples is a line-based serialization format for RDF. It is easy to
parse and widely supported. For details, see the [W3C RDF 1.2 N-Triples
specification](https://www.w3.org/TR/rdf12-n-triples/).

## Examples

``` r
triple_1 <- n_triple(
  "http://example.org/show/218",
  "http://www.w3.org/2000/01/rdf-schema#label",
  "That Seventies Show"
)

triple_2 <- n_triple(
  "http://example.org/show/218",
  "http://example.org/show/localName",
  '"Cette S<U+00E9>rie des Ann<U+00E9>es Septante"@fr-be'
)

n_triples(c(triple_1, triple_2, triple_1))
#> [1] "<http://example.org/show/218> <http://www.w3.org/2000/01/rdf-schema#label> \"That Seventies Show\"^^<http://www.w3.org/2001/XMLSchema#string> ."
#> [2] "<http://example.org/show/218> <http://example.org/show/localName> \"\"Cette S<U+00E9>rie des Ann<U+00E9>es Septante\"@fr-be\" ."                
```
