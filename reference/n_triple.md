# Create an N-Triple

Create a single N-Triple triple.

## Usage

``` r
n_triple(s, p, o)
```

## Source

[RDF 1.1 N-Triples](https://www.w3.org/TR/n-triples/)

## Arguments

- s:

  The subject of a triplet.

- p:

  The predicate of a triplet.

- o:

  The object of a triplet.

## Value

A character vector containing one N-Triple string.

## Details

N-Triples is an easy to parse line-based subset of Turtle to serialize
RDF. An N-Triple triple is a sequence of RDF terms representing the
subject, predicate and object of an RDF Triple. Use
[`n_triples()`](https://docs.ropensci.org/dataset/reference/n_triples.md)
to serialize multiple statements.

## Examples

``` r
s <- "http://example.org/show/218"
p <- "http://www.w3.org/2000/01/rdf-schema#label"
o <- "That Seventies Show"
n_triple(s, p, o)
#> [1] "<http://example.org/show/218> <http://www.w3.org/2000/01/rdf-schema#label> \"That Seventies Show\"^^<http://www.w3.org/2001/XMLSchema#string> ."
```
