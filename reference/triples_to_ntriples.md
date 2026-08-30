# Internal: Convert triple data.frame to N-Triples format

Turns a data.frame with `s`, `p`, `o` columns into N-Triples strings.

## Usage

``` r
triples_to_ntriples(df)
```

## Arguments

- df:

  A data.frame with columns `s`, `p`, and `o`.

## Value

A character vector of N-Triple lines.
