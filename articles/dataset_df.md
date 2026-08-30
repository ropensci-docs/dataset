# dataset_df: Create Datasets that are Easy to Share Exchange and Extend

The `dataset` package extends R’s native data structures with
machine-readable metadata. It follows a *semantic early-binding*
approach: metadata is embedded as soon as the data is created, making
datasets suitable for long-term reuse, FAIR-compliant publishing, and
integration into semantic web systems.

In R, a `data.frame` is defined as a tightly coupled collection of
variables that share many of the properties of matrices and lists, and
it serves as the fundamental data structure for most of R’s modeling
software. Users of the R ecosystem often use the term *data frame*
interchangeably with *dataset*. However, the standards used in
libraries, repositories, and statistical systems for publishing,
exchanging, and reusing datasets require metadata that even “tidy” data
frames do not provide.

This vignette introduces the `dataset_df` class and the
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
constructor, which extend tidy data frames with a semantic layer. For
details on semantically enriched vectors, see
[`vignette("defined", package = "dataset")`](https://docs.ropensci.org/dataset/articles/defined.md).
Readers interested in the underlying ISO and W3C definitions of
*dataset* will find them discussed in
[`vignette("design", package = "dataset")`](https://docs.ropensci.org/dataset/articles/design.md).

## Purpose

The
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
function helps you create **semantically rich datasets** that meet the
interoperability, exchange, and reuse requirements of libraries,
repositories, and statistical systems. It defines a new S3 class,
inherited from the modernised data frame of
[`tibble::tibble()`](https://tibble.tidyverse.org/reference/tibble.html),
that retains compatibility with existing workflows but is easier to:

- understand by humans,  
- validate and process by machines,  
- deposit, exchange, and publish,  
- share across tools, teams, and domains.

This vignette walks you through creating such a dataset using a subset
of the *GDP and main aggregates – international data cooperation annual
data* dataset from Eurostat  
(DOI:
[https://doi.org/10.2908/NAIDA_10_GDP).](https://doi.org/10.2908/NAIDA_10_GDP).)

## Load example data

``` r

library(dataset)
data("gdp")
```

``` r

print(gdp)
#> # A tibble: 10 × 5
#>    geo    year   gdp unit    freq 
#>    <chr> <int> <dbl> <chr>   <chr>
#>  1 AD     2020 2355. CP_MEUR A    
#>  2 AD     2021 2594. CP_MEUR A    
#>  3 AD     2022 2884. CP_MEUR A    
#>  4 AD     2023 3120. CP_MEUR A    
#>  5 LI     2020 5430. CP_MEUR A    
#>  6 LI     2021 6424. CP_MEUR A    
#>  7 LI     2022 6759. CP_MEUR A    
#>  8 SM     2020 1265. CP_MEUR A    
#>  9 SM     2021 1461. CP_MEUR A    
#> 10 SM     2022 1612. CP_MEUR A
```

This example dataset is already in tidy format: each row represents a
single observation for a country and year, and each column is a
variable. `dataset_df` builds on this structure by adding semantic
information to the variables and the dataset itself, ensuring that both
the shape and the meaning of the data are preserved and unambiguous.

While the raw dataset represented in the `gdp` data.frame is valid and
tidy, it can be hard to interpret without external documentation. For
example:

- Countries are encoded in the `geo` variable.

- Reporting frequency (e.g., `A` for annual) is stored in `freq`.

## Add metadata to your dataset

The
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
constructor enables two levels of semantic annotation for a `tbl_df`
object:

- **Variable-level metadata** — label, unit, definition, namespace.

- **Dataset-level metadata** — title, author, license, description.

- Let’s create a smaller dataset and enrich it with metadata.

Let’s create a semantically enriched subset:

``` r

small_country_dataset <- dataset_df(
  geo = defined(
    gdp$geo,
    label = "Country name",
    concept = "http://purl.org/linked-data/sdmx/2009/dimension#refArea",
    namespace = "https://dd.eionet.europa.eu/vocabulary/eurostat/geo/$1"
  ),
  year = defined(
    gdp$year,
    label = "Reference Period (Year)",
    concept = "http://purl.org/linked-data/sdmx/2009/dimension#refPeriod"
  ),
  gdp = defined(
    gdp$gdp,
    label = "Gross Domestic Product",
    unit = "CP_MEUR",
    concept = "http://data.europa.eu/83i/aa/GDP"
  ),
  unit = defined(
    gdp$unit,
    label = "Unit of Measure",
    concept = "http://purl.org/linked-data/sdmx/2009/attribute#unitMeasure",
    namespace = "https://dd.eionet.europa.eu/vocabulary/eurostat/unit/$1"
  ),
  freq = defined(
    gdp$freq,
    label = "Frequency",
    concept = "http://purl.org/linked-data/sdmx/2009/code"
  ),
  dataset_bibentry = dublincore(
    title = "Small Country Dataset",
    creator = person("Jane", "Doe"),
    publisher = "Example Inc.",
    datasource = "https://doi.org/10.2908/NAIDA_10_GDP",
    rights = "CC-BY",
    coverage = "Andorra, Liechtenstein, San Marino and the Feroe Islands"
  )
)
```

## Inspecting variable-level metadata

Columns created with the `defined` class store semantic information such
as the label, the concept’s definition link, and the unit of measure.

Check the variable label:

``` r

var_label(small_country_dataset$gdp)
#> [1] "Gross Domestic Product"
```

And the measure of unit:

``` r

var_unit(small_country_dataset$gdp)
#> [1] "CP_MEUR"
```

## Adding dataset-level metadata

A
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
object can also store metadata describing the dataset as a whole. This
metadata follows widely adopted standards:

- Dublin Core Terms
  ([`dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md)),
  used in libraries and data repositories.
- DataCite
  ([`datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md)),
  commonly used in research data repositories.

Each metadata field can be accessed or modified using simple assignment
functions. For example, you can set the dataset language.

``` r

language(small_country_dataset) <- "en"
```

## Reviewing dataset-level metadata

To see the complete dataset description, you can print it as a
BibTeX-style entry, which is suitable for citation or export.

``` r

print(get_bibentry(small_country_dataset), "bibtex")
#> Dublin Core Metadata Record
#> --------------------------
#> Title:       Small Country Dataset
#> Creator(s):  Jane Doe [ctb]
#> Publisher:   Example Inc.
#> Year:        2026
#> Language:    eng
```

This prints a complete BibTeX-style entry, suitable for citation or
export.

## Joining datasets

The previous dataset contains observations for three data subjects —
Andorra, Liechtenstein, and San Marino — but does not include the Feroe
Islands.

``` r

feroe_df <- data.frame(
  geo = rep("FO", 3),
  year = 2020:2022,
  gdp = c(2523.6, 2725.8, 3013.2),
  unit = rep("CP_MEUR", 3),
  freq = rep("A", 3)
)
```

The `dataset_df` class does not allow binding two datasets directly
unless their concept definitions, units of measure, and URI namespaces
match.

``` r

rbind(small_country_dataset, feroe_df)
```

    Error in rbind(deparse.level, ...) :
    numbers of columns of arguments do not match

While this constraint can feel restrictive during an analysis workflow,
it ensures semantic consistency when the data is later published or
exchanged.

This is similar in spirit to tidy data principles: when combining
datasets, both structure and meaning must align. In `dataset_df`, the
tidy data rule that “variables are columns” is complemented by the
requirement that variables with the same name also share the same
definition, units, and concept references.

To add the missing Feroe Islands data, first create a compatible dataset
using the same definitions, country coding, and units of measure as the
original.

``` r

feroe_dataset <- dataset_df(
  geo = defined(
    feroe_df$geo,
    label = "Country name",
    concept = "http://purl.org/linked-data/sdmx/2009/dimension#refArea",
    namespace = "https://dd.eionet.europa.eu/vocabulary/eurostat/geo/$1"
  ),
  year = defined(
    feroe_df$year,
    label = "Reference Period (Year)",
    concept = "http://purl.org/linked-data/sdmx/2009/dimension#refPeriod"
  ),
  gdp = defined(
    feroe_df$gdp,
    label = "Gross Domestic Product",
    unit = "CP_MEUR",
    concept = "http://data.europa.eu/83i/aa/GDP"
  ),
  unit = defined(
    feroe_df$unit,
    label = "Unit of Measure",
    concept = "http://purl.org/linked-data/sdmx/2009/attribute#unitMeasure",
    namespace = "https://dd.eionet.europa.eu/vocabulary/eurostat/unit/$1"
  ),
  freq = defined(
    feroe_df$freq,
    label = "Frequency",
    concept = "http://purl.org/linked-data/sdmx/2009/code"
  )
)
```

Once the new dataset is defined in this way, you can combine it with the
existing one using
[`bind_defined_rows()`](https://docs.ropensci.org/dataset/reference/bind_defined_rows.md).

``` r

joined_dataset <- bind_defined_rows(small_country_dataset, feroe_dataset)
joined_dataset
#> Doe (2026): Small Country Dataset [dataset]
#>    rowid geo    year   gdp unit    freq  
#>    <chr> <chr> <int> <dbl> <chr>   <chr>
#>  1 obs1  AD     2020 2355. CP_MEUR A    
#>  2 obs2  AD     2021 2594. CP_MEUR A    
#>  3 obs3  AD     2022 2884. CP_MEUR A    
#>  4 obs4  AD     2023 3120. CP_MEUR A    
#>  5 obs5  LI     2020 5430. CP_MEUR A    
#>  6 obs6  LI     2021 6424. CP_MEUR A    
#>  7 obs7  LI     2022 6759. CP_MEUR A    
#>  8 obs8  SM     2020 1265. CP_MEUR A    
#>  9 obs9  SM     2021 1461. CP_MEUR A    
#> 10 obs10 SM     2022 1612. CP_MEUR A    
#> 11 obs11 FO     2020 2524. CP_MEUR A    
#> 12 obs12 FO     2021 2726. CP_MEUR A    
#> 13 obs13 FO     2022 3013. CP_MEUR A
```

The combined dataset behaves like a regular tibble but retains its
metadata. If you convert it to a base R `data.frame`, you will lose the
helper methods and built-in checks, but the metadata will remain in the
object’s attributes.

``` r

attributes(as.data.frame(joined_dataset))
#> $names
#> [1] "rowid" "geo"   "year"  "gdp"   "unit"  "freq" 
#> 
#> $class
#> [1] "data.frame"
#> 
#> $row.names
#>  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13
#> 
#> $dataset_bibentry
#> Dublin Core Metadata Record
#> --------------------------
#> Title:       Small Country Dataset
#> Creator(s):  Jane Doe [ctb]
#> Publisher:   Example Inc.
#> Year:        2026
#> Language:    eng
#> 
#> $subject
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
#> 
#> $prov
#> [1] "<http://example.com/dataset_prov.nt> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Bundle> ."                  
#> [2] "<http://example.com/dataset#> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Entity> ."                         
#> [3] "<http://example.com/dataset#> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://purl.org/linked-data/cube#DataSet> ."                 
#> [4] "_:unknownauthor <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Agent> ."                                        
#> [5] "<https://doi.org/10.32614/CRAN.package.dataset> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#SoftwareAgent> ."
#> [6] "<http://example.com/creation> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <http://www.w3.org/ns/prov#Activity> ."                       
#> [7] "<http://example.com/creation> <http://www.w3.org/ns/prov#generatedAtTime> \"2026-08-30T07:44:55Z\"^^<xsd:dateTime> ."
```

### Coercion inside `dataset_df` conversion

When converting a `dataset_df` to a base `data.frame`:

``` r

as.data.frame(small_country_dataset)
#>    rowid geo year    gdp    unit freq
#> 1   obs1  AD 2020 2354.8 CP_MEUR    A
#> 2   obs2  AD 2021 2593.9 CP_MEUR    A
#> 3   obs3  AD 2022 2883.7 CP_MEUR    A
#> 4   obs4  AD 2023 3119.5 CP_MEUR    A
#> 5   obs5  LI 2020 5430.5 CP_MEUR    A
#> 6   obs6  LI 2021 6423.7 CP_MEUR    A
#> 7   obs7  LI 2022 6758.6 CP_MEUR    A
#> 8   obs8  SM 2020 1265.1 CP_MEUR    A
#> 9   obs9  SM 2021 1461.4 CP_MEUR    A
#> 10 obs10  SM 2022 1612.3 CP_MEUR    A
```

the following rules apply:

- **By default**, all semantic attributes are stripped (`label`, `unit`,
  `concept`, `namespace`).

- Categorical variables (with labels) become **character vectors**.

- Numeric
  [`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
  vectors become **numeric**.

- Date / POSIXct vectors keep their underlying date/time values.

- The `haven_labelled_defined` class is always removed.

- Dataset-level metadata (`dataset_bibentry`, `prov`, `subject`) is
  preserved.

- You can retain semantic attributes via:

``` r

as.data.frame(small_country_dataset,
  strip_attributes = FALSE
)
#>    rowid geo year    gdp    unit freq
#> 1   obs1  AD 2020 2354.8 CP_MEUR    A
#> 2   obs2  AD 2021 2593.9 CP_MEUR    A
#> 3   obs3  AD 2022 2883.7 CP_MEUR    A
#> 4   obs4  AD 2023 3119.5 CP_MEUR    A
#> 5   obs5  LI 2020 5430.5 CP_MEUR    A
#> 6   obs6  LI 2021 6423.7 CP_MEUR    A
#> 7   obs7  LI 2022 6758.6 CP_MEUR    A
#> 8   obs8  SM 2020 1265.1 CP_MEUR    A
#> 9   obs9  SM 2021 1461.4 CP_MEUR    A
#> 10 obs10  SM 2022 1612.3 CP_MEUR    A
```

[`as_tibble()`](https://docs.ropensci.org/dataset/reference/as_tibble.dataset_df.md)
behaves the same way as
[`as.data.frame()`](https://rdrr.io/r/base/as.data.frame.html) but
returns a tibble:

``` r

as_tibble(orange_df)
#> # A tibble: 35 × 4
#>    rowid     tree    age circumference
#>    <chr>     <chr> <dbl>         <dbl>
#>  1 orange:1  1       118            30
#>  2 orange:2  1       484            58
#>  3 orange:3  1       664            87
#>  4 orange:4  1      1004           115
#>  5 orange:5  1      1231           120
#>  6 orange:6  1      1372           142
#>  7 orange:7  1      1582           145
#>  8 orange:8  2       118            33
#>  9 orange:9  2       484            69
#> 10 orange:10 2       664           111
#> # ℹ 25 more rows
```

## Conclusion

With
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
your datasets are:

- **Self-descriptive** — variables carry labels, units, and definitions.
- **Machine-readable** — linked vocabularies and standard identifiers
  are embedded.
- **Ready to publish and share** — compliant with metadata standards
  like Dublin Core and DataCite.

This approach supports the FAIR data principles (Findable, Accessible,
Interoperable, Reusable) and makes your data easier to reuse, interpret,
and validate. By maintaining metadata from creation through publication,
`dataset_df` helps preserve meaning across the entire data lifecycle.

The package is designed to work seamlessly with the rOpenSci
[rdflib](https://github.com/ropensci/rdflib) package and complements
tidyverse workflows while enabling exports to semantic web formats like
RDF.
