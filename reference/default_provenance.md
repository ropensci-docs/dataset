# Build default provenance bundle

Construct a small PROV bundle (as N\<U+2011\>Triples) describing the
dataset, the software agent, and an optional creation time.

## Usage

``` r
default_provenance(
  dataset_id = "http://example.com/dataset#",
  author = NULL,
  dtm = NULL,
  generated_at_time = NULL
)
```

## Arguments

- dataset_id:

  Base IRI for the dataset (used as the `Entity` subject).

- author:

  Optional creator/author agent.

- dtm:

  Optional data team/maintainer agent.

- generated_at_time:

  Optional POSIXct time; defaults to
  [`Sys.time()`](https://rdrr.io/r/base/Sys.time.html).

## Value

A character vector of N\<U+2011\>Triples suitable for the `"prov"`
attribute.

## Details

This helper is used internally to seed provenance metadata. It emits a
set of PROV statements including an `Entity` for the dataset, an
`Activity` for creation, and `SoftwareAgent` entries for the package
citation.
