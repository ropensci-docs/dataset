# An Introduction to the dataset Package

## Overview

The `dataset` package extends tidy data with semantic metadata,
provenance, and machine-readable definitions.

It supports a gradual workflow from provisional semantic harmonisation
with
[`prelabel()`](https://docs.ropensci.org/dataset/reference/prelabel.md)
to formally defined variables with
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
and fully described datasets with
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

This makes datasets easier to exchange, reuse, publish, and serialize to
RDF and other FAIR-compliant formats.

This vignette provides a high-level introduction. For details on key
components, see:

- [`vignette("prelabelled", package = "dataset")`](https://docs.ropensci.org/dataset/articles/prelabelled.md):
  Handling Semantic Ambiguity with `prelabelled` Vectors.
- [`vignette("defined", package = "dataset")`](https://docs.ropensci.org/dataset/articles/defined.md):
  Semantic vectors with
  [`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
- [`vignette("dataset_df", package = "dataset")`](https://docs.ropensci.org/dataset/articles/dataset_df.md):
  Structuring and metadata with
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
- [`vignette("rdf", package = "dataset")`](https://docs.ropensci.org/dataset/articles/rdf.md):
  Exporting to RDF and Linked Data
- [`vignette("bibrecord", package = "dataset")`](https://docs.ropensci.org/dataset/articles/bibrecord.md):
  Creating rich citation metadata using
  [`bibrecord()`](https://docs.ropensci.org/dataset/reference/bibrecord.md)

## Why extend tidy data?

Hadley Wickham (2014) defines [tidy
data](https://vita.had.co.nz/papers/tidy-data.pdf) with three
principles:

- Each variable forms a column
- Each observation forms a row
- Each observational unit forms a table

This structure is ideal for analysis because it links the structure of a
dataset with its meaning. A variable represents an underlying attribute,
and an observation represents measurements collected on the same unit.

In practice, however, analysts rarely begin with perfectly harmonized
data. During data cleaning, transformation, and integration, they make
many semantic decisions: resolving inconsistent coding schemes,
standardizing categories, selecting units of measurement, or deciding
how concepts from different sources correspond to one another. By the
time a dataset is ready for analysis, these assumptions are usually
clear to the analyst who created it.

The problem arises when the dataset leaves its original context. Other
analysts may use different terminology, apply different coding
conventions, or simply lack knowledge of the decisions that were made
during data preparation. Even the original analyst may find these
assumptions difficult to reconstruct months or years later.

The `dataset` package extends tidy data by making such semantic
assumptions explicit and preserving them alongside the data. Rather than
treating semantic harmonisation and data provenance as undocumented
steps in a workflow, it allows them to be recorded incrementally as the
dataset evolves.

The goal is not to burden analysts with complex semantic technologies.
Instead, the package provides lightweight tools for gradually recording
the information needed to review, reuse, audit, publish, and correctly
combine datasets across projects, organisations, and time.

## Example: gradual semantic stabilisation

Many data integration problems begin with values that refer to the same
concept but use different coding conventions.

``` r

library(dataset)

country <- prelabel(
  c("AD", "Andorra", "AND", "LI", "Liechtenstein"),
  labels = c(
    Andorra = "AD",
    AND = "AD",
    Liechtenstein = "LI"
  )
)

country
#> [1] "AD"            "Andorra"       "AND"           "LI"           
#> [5] "Liechtenstein"
#> attr(,"prelabel")
#>       Andorra           AND Liechtenstein            AD            LI 
#>          "AD"          "AD"          "LI"          "AD"          "LI" 
#> attr(,"class")
#> [1] "prelabelled" "character"
```

The `prelabelled` class records provisional semantic assumptions without
requiring a formal semantic definition. In this example, “AD”,
“Andorra”, and “AND” are treated as equivalent representations of the
same geopolitical entity.

The current mappings can be inspected directly:

``` r

attr(country, "prelabel")
#>       Andorra           AND Liechtenstein            AD            LI 
#>          "AD"          "AD"          "LI"          "AD"          "LI"
```

This approach is useful during data cleaning and integration, where
semantic assumptions may still evolve. Once these assumptions become
sufficiently stable, they can be formalized with
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

For further information, see
[`vignette("prelabelled", package = "dataset")`](https://docs.ropensci.org/dataset/articles/prelabelled.md):
Handling Semantic Ambiguity with `prelabelled` Vectors.

## Example: defining semantically rich vectors

After values have been harmonized, variables can be formally defined
with machine-readable semantic metadata.

Semantically rich vectors are vectors in a data.frame that contain
richer semantics than a simple column name; a long-form human-readable
title; a machine- and human-readable variable definition; and if needed,
an external resource that contains the codebook.

``` r

library(dataset)

gdp <- defined(
  c(2355, 2592, 2884),
  label = "Gross Domestic Product",
  unit = "CP_MEUR",
  concept = "http://data.europa.eu/83i/aa/GDP"
)

geo <- defined(
  rep("AD", 3),
  label = "Geopolitical Entity",
  concept = "http://purl.org/linked-data/sdmx/2009/dimension#refArea",
  namespace = "https://www.geonames.org/countries/$1/"
)

gdp
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 2355 2592 2884
geo
#> x: Geopolitical Entity
#> Defined as http://purl.org/linked-data/sdmx/2009/dimension#refArea 
#> [1] "AD" "AD" "AD"
```

In this case, we define `geo` as the geopolitical entity
<http://purl.org/linked-data/sdmx/2009/dimension#refArea>, and we know
that the `AD` value can resolve to Andorra:
<https://www.geonames.org/countries/AD/>. These vectors now carry
metadata you can inspect directly — including their label, unit, and
concept URI — which will be preserved even after transformation or
storage.

For further information, see vignette(“defined”, package =
“dataset”)`: Semantic vectors with`defined()\`.

## Example: creating a dataset from a metadata-enriched data frame

``` r

small_dataset <- dataset_df(
  geo = geo,
  gdp = gdp,
  identifier = c(gdp = "http://example.com/dataset#gdp"),
  dataset_bibentry = dublincore(
    title = "Small GDP Dataset",
    creator = person("Jane", "Doe", role = "aut"),
    publisher = "Small Repository",
    subject = "Gross Domestic Product"
  )
)

small_dataset
#> Doe (2026): Small GDP Dataset [dataset]
#>   rowid geo     gdp 
#>   <chr> <chr> <dbl>
#> 1 gdp1  AD     2355
#> 2 gdp2  AD     2592
#> 3 gdp3  AD     2884
```

For further information see
[`vignette("dataset_df", package = "dataset")`](https://docs.ropensci.org/dataset/articles/dataset_df.md):
Structuring and metadata with
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

This dataset not only stores the variables and values, but also includes
embedded metadata that supports precise interpretation and
repository-level publication.

``` r

as_dublincore(small_dataset)
#> Dublin Core Metadata Record
#> --------------------------
#> Title:       Small GDP Dataset
#> Creator(s):  Jane Doe [aut]
#> Contributor(s): :unas
#> Subject(s):  Gross Domestic Product
#> Publisher:   Small Repository
#> Year:        2026
#> Language:    :unas
#> Description: :unas
```

For further information
see[`vignette("bibrecord", package = "dataset")`](https://docs.ropensci.org/dataset/articles/bibrecord.md):
Creating rich citation metadata using
[`bibrecord()`](https://docs.ropensci.org/dataset/reference/bibrecord.md)

## Exporting to RDF

As Carl Boettinger has shown in the vignettes accompanying the R-binding
to the popular Python library
[rdflib](https://CRAN.R-project.org/package=rdflib), (see: [A tidyverse
lover’s intro to
RDF](https://docs.ropensci.org/rdflib/articles/rdf_intro.html)), tidy
datasets can be retrofitted with rich metadata if they are pivoted to a
strictly three-column long format.

Our packages tries to lower the burden of such retrofitting with early
binding and sensible defaults to serialise the dataset’s contents and
the dataset’s bibliographic data to this format for those who are not
familiar with RDF.

You can convert any `dataset_df` object into a tidy 3-column
representation (subject–predicate–object) using
[`dataset_to_triples()`](https://docs.ropensci.org/dataset/reference/dataset_to_triples.md):

``` r

triples <- dataset_to_triples(small_dataset,
  format = "nt"
)
triples
#> [1] "<http://example.com/dataset#gdpgdp1> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> ."
#> [2] "<http://example.com/dataset#gdpgdp2> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> ."
#> [3] "<http://example.com/dataset#gdpgdp3> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> ."
#> [4] "<http://example.com/dataset#gdpgdp1> <http://data.europa.eu/83i/aa/GDP> \"2355\"^^<xsd:decimal> ."                                        
#> [5] "<http://example.com/dataset#gdpgdp2> <http://data.europa.eu/83i/aa/GDP> \"2592\"^^<xsd:decimal> ."                                        
#> [6] "<http://example.com/dataset#gdpgdp3> <http://data.europa.eu/83i/aa/GDP> \"2884\"^^<xsd:decimal> ."
```

This 3-column format (subject–predicate–object) is compatible with
semantic web tools such as SPARQL, `rdflib`, and triple stores.

``` r

mycon <- tempfile("my_dataset",
  fileext = "nt"
)
my_description <- describe(
  x = small_dataset,
  con = mycon
)

# Only three statements are shown:
readLines(mycon)[c(4, 8, 12)]
#> [1] "_:doejane <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Agent> ."                                      
#> [2] "<http://example.com/dataset_tba/> <http://purl.org/dc/terms/title> \"Small GDP Dataset\"^^<http://www.w3.org/2001/XMLSchema#string> ."
#> [3] "<http://example.com/dataset_tba/> <http://purl.org/dc/terms/type> <http://purl.org/dc/dcmitype/Dataset> ."
```

``` r

## Show two lines of provenance:
provenance(small_dataset)[c(6, 7)]
#> [1] "<http://example.com/creation> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Activity> ."
#> [2] "<http://example.com/creation> <http://www.w3.org/ns/prov#generatedAtTime> \"2026-08-30T07:45:06Z\"^^<xsd:dateTime> ."
```

For further information, see
[`vignette("rdf", package = "dataset")`](https://docs.ropensci.org/dataset/articles/rdf.md):
Exporting to RDF and Linked Data.

## Coercing back

There may be use cases when your richer dataset needs to be simplified
to as base R `data.frame` or a `tbf_df`.

We offer two coercion forms:

``` r

small_df <- as.data.frame(small_dataset,
  strip_attributes = FALSE
)

attr(small_dataset, "subject")
#> $term
#> [1] "Data sets"
#> 
#> $subjectScheme
#> [1] "LCSH"
#> 
#> $schemeURI
#> [1] "http://id.loc.gov/authorities/subjects"
#> 
#> $valueURI
#> [1] "http://id.loc.gov/authorities/subjects/sh2018002256"
#> 
#> $classificationCode
#> NULL
#> 
#> $prefix
#> [1] "lcsh:"
#> 
#> attr(,"class")
#> [1] "subject" "list"
```

Using the `strip_attributes = FALSE` the rich attributes remain in the
base R data.frame. In most pipelines the attributes play no role, and
you can retain it, and perhaps later load it back to a richer form.

You can also strip all these attributes, and choose `tbl_df` (if you
have `tibble`) installed”:

``` r

small_tbl <- as_tibble(
  small_dataset,
  strip_attributes = TRUE
)

small_tbl
#> # A tibble: 3 × 3
#>   rowid geo     gdp
#>   <chr> <chr> <dbl>
#> 1 gdp1  AD     2355
#> 2 gdp2  AD     2592
#> 3 gdp3  AD     2884
```

## Summary

The *dataset* package enriches tidy data by attaching metadata from the
start of the workflow. It helps avoid semantic mismatches, supports RDF
publication, and meets interoperability standards like SDMX, DataCite,
and Dublin Core. Use it when you need:

- Meaningful variable descriptions and URIs

- Dataset-level metadata embedded directly in .rds or .rda files

- Easy export to RDF and semantic web formats.
