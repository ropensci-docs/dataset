# Internal: Generate RDF triples for a single column

Create subject-predicate-object triples from one column of a dataset

## Usage

``` r
triples_column_generate(s_vec, col, colname)
```

## Arguments

- s_vec:

  A character vector of subject URIs (length = number of rows)

- col:

  The column vector (e.g., `x[[i]]`)

- colname:

  The name of the column (used as fallback for predicate)

## Value

A data.frame with columns s, p, o
