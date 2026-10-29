# Internal: Expand multi-valued DC fields to RDF triples

Converts scalar or vector fields into RDF triples.

## Usage

``` r
expand_triples(dataset_id, predicate_uri, values)
```

## Arguments

- dataset_id:

  The subject URI

- predicate_uri:

  The RDF predicate URI

- values:

  A scalar, character vector, or list (e.g., person objects)

## Value

A character vector of RDF triples
