# Coerce prelabelled vectors to semantic character workspace

Convert a `prelabelled` vector into a semantic character workspace
suitable for iterative refinement and inference workflows.

## Usage

``` r
# S3 method for class 'prelabelled'
as_character(x, ...)
```

## Arguments

- x:

  A `prelabelled` vector.

- ...:

  Unused.

## Value

A character vector where:

- values are derived from the semantic labels;

- original observations are preserved as attributes;

- refinement metadata is retained;

- the `"prelabelled"` class is removed.

## Details

Unlike base [`as.character()`](https://rdrr.io/r/base/character.html),
this method preserves:

- original observational values;

- semantic label mappings;

- refinement metadata;

- additional custom attributes.

The method operationalises provisional semantic labels into working
character values while retaining the original observed vector for
reversibility and provenance-aware workflows.

This allows workflows such as:

- `prelabel() %>% as.character() %>% refine()`

- `prelabel() %>% as.character() %>% infer()`

- iterative semantic harmonisation;

- contextual semantic derivation.

The original observational values are preserved in the
`"original_values"` attribute.

The method intentionally separates:

- observational evidence;

- semantic operationalisation.

This distinction is important for provenance-aware semantic refinement
workflows where semantic interpretations may evolve while original
observations remain stable.

The coercion is therefore semantically reversible.

## Examples

``` r

x <- prelabel(
  c(
    "r",
    "pdf",
    "qmd"
  ),
  labels = c(
    r = "software development",
    pdf = "publication",
    qmd = "documentation"
  )
)

x
#> [1] "r"   "pdf" "qmd"
#> attr(,"prelabel")
#>                      r                    pdf                    qmd 
#> "software development"          "publication"        "documentation" 
#> attr(,"class")
#> [1] "prelabelled" "character"  

y <- as_character(x)

y
#> [1] "software development" "publication"          "documentation"       
#> attr(,"prelabel")
#>                      r                    pdf                    qmd 
#> "software development"          "publication"        "documentation" 
#> attr(,"original_values")
#> [1] "r"   "pdf" "qmd"
#> attr(,"original_values")attr(,"prelabel")
#>                      r                    pdf                    qmd 
#> "software development"          "publication"        "documentation" 

attributes(y)
#> $prelabel
#>                      r                    pdf                    qmd 
#> "software development"          "publication"        "documentation" 
#> 
#> $original_values
#> [1] "r"   "pdf" "qmd"
#> attr(,"prelabel")
#>                      r                    pdf                    qmd 
#> "software development"          "publication"        "documentation" 
#> 

attr(
  y,
  "original_values"
)
#> [1] "r"   "pdf" "qmd"
#> attr(,"prelabel")
#>                      r                    pdf                    qmd 
#> "software development"          "publication"        "documentation" 
```
