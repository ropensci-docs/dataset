# Format contributors into a citation string

Format a list of [`utils::person`](https://rdrr.io/r/utils/person.html)
objects into a compact string, merging roles per person and normalizing
names. Contributors without explicit roles are assigned `"ctb"`. If
`NULL` or `":unas"` is supplied, returns `":unas"`.

## Usage

``` r
fix_contributor(contributors = NULL)
```

## Arguments

- contributors:

  A vector or list of `person` objects, or `NULL`, or the character
  string `":unas"`.

## Value

A single character string, e.g.
`"{Jane Doe [dtm, ctb]} and {John Smith [ctb]}"`.
