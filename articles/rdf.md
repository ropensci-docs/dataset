# From R to RDF

## From tidy data to RDF triples

This vignette demonstrates how to convert tidy R datasets into
semantically enriched RDF triple structures, using the `dataset` and
`rdflib` packages. These packages help you annotate variables with
machine-readable concepts, units, and links to controlled vocabularies.

We’ll start with a small example of a tidy dataset representing
countries (`geo`) with unique identifiers (`rowid`) and then show how to
transform the dataset into RDF triples using standard vocabularies.

``` r

library(dataset)
library(rdflib)
#> Warning: package 'rdflib' was built under R version 4.6.1
data("gdp")
```

## Creating a minimal semantically defined dataset

``` r

small_geo <- dataset_df(
  geo = defined(
    gdp$geo[1:3],
    label = "Geopolitical entity",
    concept = "http://purl.org/linked-data/sdmx/2009/dimension#refArea",
    namespace = "https://www.geonames.org/countries/$1/"
  ),
  identifier = c(
    obs = "https://dataset.dataobservatory.eu/examples/dataset.html#"
  )
)
```

The dataset has no creator or author, but the rows have identifiers that
can be resolved with
<https://dataset.dataobservatory.eu/examples/dataset.html#>. In real
publishing scenarios, you would replace these with persistent URIs that
identify actual datasets and their observations. For example, a
DOI-based identifier such as:

`https://doi.org/10.5281/zenodo.14917851#obs:1`

So let’s see how this minimal dataset prints in R:

``` r

print(small_geo)
#> Unknown (2026): Untitled Dataset [dataset]
#>   rowid geo   
#>   <chr> <chr>
#> 1 obs1  AD   
#> 2 obs2  AD   
#> 3 obs3  AD
```

A tidy dataset can always be pivotted to a three-column long (tidy)
format, which can define every cell value in the tabular dataset with a
subject-predicate-object triple.

``` r

triples_df <- dataset_to_triples(small_geo)
knitr::kable(triples_df)
```

| s | p | o |
|:---|:---|:---|
| <https://dataset.dataobservatory.eu/examples/dataset.html#obs1> | <http://purl.org/linked-data/sdmx/2009/dimension#refArea> | <https://www.geonames.org/countries/AD/> |
| <https://dataset.dataobservatory.eu/examples/dataset.html#obs2> | <http://purl.org/linked-data/sdmx/2009/dimension#refArea> | <https://www.geonames.org/countries/AD/> |
| <https://dataset.dataobservatory.eu/examples/dataset.html#obs3> | <http://purl.org/linked-data/sdmx/2009/dimension#refArea> | <https://www.geonames.org/countries/AD/> |

This produces triples like:

``` r

ntriples <- dataset_to_triples(small_geo, format = "nt")
```

``` r

cat(ntriples, sep = "\n")
```

``` r

cat(ntriples, sep = "\n")
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs1> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs2> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs3> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> .
```

Each row of your dataset becomes a **subject**, each variable a
**predicate**, and each value either a **URI** or a typed literal (like
a date or number) — depending on how it’s defined. The first statement
in the example defines the intersection of the first row (observation,
identified by the `rowid`) `dataset#eg:1` and the column [reference
area](http://purl.org/linked-data/sdmx/2009/dimension#refArea) defined
by the URI as [Andorra](https://www.geonames.org/countries/AD/).The
advantage of this approach is that the row and column definitions as
well as coded cell values have a permanent metadata definition.

### RDF triples enable interoperability

The Resource Description Framework (RDF) represents data as
subject–predicate–object triples. This allows your dataset to be
machine-readable, linkable to external vocabularies, and to be ready for
queries via SPARQL.

### RDF triples enable interoperability

The Resource Description Framework (RDF) represents data as
subject–predicate–object triples. This allows your dataset to be
machine-readable, linkable to external vocabularies, and queryable via
SPARQL.

``` r

n_triple(
  s = "https://dataset.dataobservatory.eu/examples/dataset.html#obs1",
  p = "http://purl.org/dc/terms/title",
  o = "Small Country Dataset"
)
#> [1] "<https://dataset.dataobservatory.eu/examples/dataset.html#obs1> <http://purl.org/dc/terms/title> \"Small Country Dataset\"^^<http://www.w3.org/2001/XMLSchema#string> ."
```

``` r

# We write to a temporary file our Ntriples created earlier
temp_file <- tempfile(fileext = ".nt")
writeLines(ntriples, con = temp_file)

rdf_graph <- rdf()
rdf_parse(rdf_graph, doc = temp_file, format = "ntriples")
#> Total of 3 triples, stored in hashes
#> -------------------------------
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs1> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs2> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs3> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> .
rdf_graph
#> Total of 3 triples, stored in hashes
#> -------------------------------
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs1> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs2> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs3> <http://purl.org/linked-data/sdmx/2009/dimension#refArea> <https://www.geonames.org/countries/AD/> .
```

A simple, serverless scaffolding for publishing `dataset_df` objects on
the web (with HTML + RDF exports) is available at
<https://github.com/dataobservatory-eu/dataset-template> with the
example of this vignette tutorial.

## Clean up

It is a good practice to close connections, or clean up larger objects
living in the memory:

``` r

# Clean up: delete file and clear RDF graph
unlink(temp_file)
rm(rdf_graph)
gc()
#>           used (Mb) gc trigger  (Mb) max used (Mb)
#> Ncells 1105594 59.1    2203125 117.7  1548354 82.7
#> Vcells 1908658 14.6    8388608  64.0  3129591 23.9
```

## Scale up

We build a slightly bigger graph, save it, and reload it.

``` r

small_country_dataset <- dataset_df(
  geo = defined(
    gdp$geo,
    label = "Country name",
    concept = "http://dd.eionet.europa.eu/vocabulary/eurostat/geo/",
    namespace = "https://www.geonames.org/countries/$1/"
  ),
  year = defined(
    gdp$year,
    label = "Reference Period (Year)",
    concept = "http://purl.org/linked-data/sdmx/2009/dimension#refPeriod"
  ),
  gdp = defined(
    gdp$gdp,
    label = "Gross Domestic Product",
    unit = "https://dd.eionet.europa.eu/vocabularyconcept/eurostat/unit/CP_MEUR",
    concept = "http://data.europa.eu/83i/aa/GDP"
  ),
  unit = gdp$unit,
  freq = defined(
    gdp$freq,
    label = "Frequency",
    concept = "http://purl.org/linked-data/sdmx/2009/code"
  ),
  identifier = c(
    obs = "https://dataset.dataobservatory.eu/examples/dataset.html#"
  ),
  dataset_bibentry = dublincore(
    title = "Small Country Dataset",
    creator = person("Jane", "Doe"),
    publisher = "Example Inc.",
    datasource = "https://doi.org/10.2908/NAIDA_10_GDP",
    rights = "CC-BY",
    coverage = "Andorra, Lichtenstein and San Marino"
  )
)
```

``` r

small_country_df_nt <- dataset_to_triples(
  small_country_dataset,
  format = "nt"
)
```

The following lines read as:

- \[1\] `Observation #1` is a geopolitical entity, `Andorra`.
- \[11\] `Observation #1` has a reference time period of `2020`.
- \[21\] `Observation #1` has a decimal GDP value of `2354.8`
- \[31\] `Observation #1` has a unit of `million euros, current prices`.
- \[41\] `Observation #1` has a measurement frequency that is `annual`.

``` r

## See rows 1,11,21
small_country_df_nt[c(1, 11, 21, 31, 41)]
#> [1] "<https://dataset.dataobservatory.eu/examples/dataset.html#obs1> <http://dd.eionet.europa.eu/vocabulary/eurostat/geo/> <https://www.geonames.org/countries/AD/> ."
#> [2] "<https://dataset.dataobservatory.eu/examples/dataset.html#obs1> <http://purl.org/linked-data/sdmx/2009/dimension#refPeriod> \"2020\"^^<xsd:integer> ."           
#> [3] "<https://dataset.dataobservatory.eu/examples/dataset.html#obs1> <http://data.europa.eu/83i/aa/GDP> \"2354.8\"^^<xsd:decimal> ."                                  
#> [4] "<https://dataset.dataobservatory.eu/examples/dataset.html#obs1> <http://example.com/prop/unit> \"CP_MEUR\"^^<xsd:string> ."                                      
#> [5] "<https://dataset.dataobservatory.eu/examples/dataset.html#obs1> <http://purl.org/linked-data/sdmx/2009/code> \"A\"^^<xsd:string> ."
```

he statements about `Observation 1`, i.e. Andorra’s national economy in
2020, is not serialised consecutively in the text file. This is not
necessary, because each cell is precisely connected to the *row* (first
part of the triple) and *column* (second part of the triple). We could
say that the entire map to the original dataset is embedded into the
flat text file, therefore it can be easily imported into a database.

*Note: The `.html#` in these example IRIs does not mean the resource is
an HTML file.  
Any absolute IRI is valid in RDF. This form is used here only for
illustration;  
in practice, a bare namespace such as `/dataset#` is more conventional.*

``` r

# We write to a temporary file our Ntriples created earlier
temp_file <- tempfile(fileext = ".nt")
writeLines(small_country_df_nt,
  con = temp_file
)

rdf_graph <- rdf()
rdf_parse(rdf_graph, doc = temp_file, format = "ntriples")
#> Total of 50 triples, stored in hashes
#> -------------------------------
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs8> <http://example.com/prop/unit> "CP_MEUR"^^<xsd:string> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs8> <http://dd.eionet.europa.eu/vocabulary/eurostat/geo/> <https://www.geonames.org/countries/SM/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs6> <http://dd.eionet.europa.eu/vocabulary/eurostat/geo/> <https://www.geonames.org/countries/LI/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs7> <http://dd.eionet.europa.eu/vocabulary/eurostat/geo/> <https://www.geonames.org/countries/LI/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs6> <http://purl.org/linked-data/sdmx/2009/code> "A"^^<xsd:string> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs10> <http://purl.org/linked-data/sdmx/2009/code> "A"^^<xsd:string> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs7> <http://purl.org/linked-data/sdmx/2009/code> "A"^^<xsd:string> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs4> <http://data.europa.eu/83i/aa/GDP> "3119.5"^^<xsd:decimal> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs3> <http://example.com/prop/unit> "CP_MEUR"^^<xsd:string> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs2> <http://example.com/prop/unit> "CP_MEUR"^^<xsd:string> .
#> 
#> ... with 40 more triples
```

``` r

rdf_graph
```

``` r

rdf_graph
#> Total of 50 triples, stored in hashes
#> -------------------------------
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs8> <http://example.com/prop/unit> "CP_MEUR"^^<xsd:string> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs8> <http://dd.eionet.europa.eu/vocabulary/eurostat/geo/> <https://www.geonames.org/countries/SM/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs6> <http://dd.eionet.europa.eu/vocabulary/eurostat/geo/> <https://www.geonames.org/countries/LI/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs7> <http://dd.eionet.europa.eu/vocabulary/eurostat/geo/> <https://www.geonames.org/countries/LI/> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs6> <http://purl.org/linked-data/sdmx/2009/code> "A"^^<xsd:string> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs10> <http://purl.org/linked-data/sdmx/2009/code> "A"^^<xsd:string> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs7> <http://purl.org/linked-data/sdmx/2009/code> "A"^^<xsd:string> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs4> <http://data.europa.eu/83i/aa/GDP> "3119.5"^^<xsd:decimal> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs3> <http://example.com/prop/unit> "CP_MEUR"^^<xsd:string> .
#> <https://dataset.dataobservatory.eu/examples/dataset.html#obs2> <http://example.com/prop/unit> "CP_MEUR"^^<xsd:string> .
#> 
#> ... with 40 more triples
```

Your dataset is now ready to be exported to meet the true FAIR
standards, because they are:

- **self-descriptive**: variables carry labels, units, and definitions.
- **machine-readable**: linked vocabularies and standard identifiers.
- **ready to publish and share**: they carry the metadata of each
  variable, potentially each observation unit, and through metadata
  standards like Dublin Core and DataCite the information about the
  whole dataset, too.

``` r

# Create temporary JSON-LD output file
jsonld_file <- tempfile(fileext = ".jsonld")

# Serialize (export) the entire graph to JSON-LD format
rdf_serialize(rdf_graph, doc = jsonld_file, format = "jsonld")
```

Read it back to R for display (only first 30 lines are shown):

``` r

cat(readLines(jsonld_file)[1:30], sep = "\n")
#> {
#>   "@graph": [
#>     {
#>       "@id": "https://dataset.dataobservatory.eu/examples/dataset.html#obs1",
#>       "http://data.europa.eu/83i/aa/GDP": {
#>         "@type": "xsd:decimal",
#>         "@value": "2354.8"
#>       },
#>       "http://dd.eionet.europa.eu/vocabulary/eurostat/geo/": {
#>         "@id": "https://www.geonames.org/countries/AD/"
#>       },
#>       "http://example.com/prop/unit": {
#>         "@type": "xsd:string",
#>         "@value": "CP_MEUR"
#>       },
#>       "http://purl.org/linked-data/sdmx/2009/code": {
#>         "@type": "xsd:string",
#>         "@value": "A"
#>       },
#>       "http://purl.org/linked-data/sdmx/2009/dimension#refPeriod": {
#>         "@type": "xsd:integer",
#>         "@value": "2020"
#>       }
#>     },
#>     {
#>       "@id": "https://dataset.dataobservatory.eu/examples/dataset.html#obs10",
#>       "http://data.europa.eu/83i/aa/GDP": {
#>         "@type": "xsd:decimal",
#>         "@value": "1612.3"
#>       },
```

    #>           used (Mb) gc trigger  (Mb) max used  (Mb)
    #> Ncells 1175712 62.8    2203125 117.7  2126497 113.6
    #> Vcells 2027337 15.5    8388608  64.0  3304364  25.3
