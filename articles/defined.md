# defined: Semantically Enriched Vectors

The `dataset` package extends R’s native data structures with
machine-readable metadata. It follows a *semantic early-binding*
approach, which means metadata is embedded as soon as the data is
created, making datasets suitable for long-term reuse, FAIR-compliant
publishing, and integration into semantic web systems.

`defined` works naturally with data structured according to tidy data
principles (Wickham, 2014), where each variable is a column, each
observation is a row, and each type of observational unit forms a table.
It adds an additional semantic layer to individual vectors so their
meaning is explicit, consistent, and machine-readable.

In many workflows, semantic clarity is reached gradually. Values may
first be cleaned, compared, or provisionally harmonised before the
analyst is ready to attach a stable definition. The `prelabelled` class
supports this earlier stage: it records provisional semantic mappings
while preserving the original observed values. Once these assumptions
become stable, they can be formalised with
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

This vignette focuses specifically on the `defined` function, which you
can use to create a semantically enriched vector. For details on
semantically enriched data frames, see
[`vignette("dataset_df", package = "dataset")`](https://docs.ropensci.org/dataset/articles/dataset_df.md).

This vignette focuses on the
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
function, which is used once semantic assumptions are sufficiently
stable to create semantically enriched vectors. For provisional mappings
before this stage, see
[`vignette("prelabelled", package = "dataset")`](https://docs.ropensci.org/dataset/articles/prelabelled.md):
Handling Semantic Ambiguity with `prelabelled` Vectors.

## Purpose

The
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
function helps you create **semantically rich labelled vectors** that
are easier to:

- understand by humans,
- validate and process by machines,
- ensure consistency when combining data from multiple sources,
- share across tools, teams, and domains.

By attaching metadata at creation time, `defined` prevents the loss of
context and meaning that often occurs when data is exchanged or
archived. This approach supports the FAIR data principles (Findable,
Accessible, Interoperable, Reusable) and facilitates integration into
semantic web systems.

## Getting started

``` r

library(dataset)
data("gdp")
```

We’ll start by wrapping a numeric GDP vector using
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

``` r

gdp_1 <- defined(
  gdp$gdp,
  label = "Gross Domestic Product",
  unit = "CP_MEUR",
  concept = "http://data.europa.eu/83i/aa/GDP"
)
```

The
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
class builds on labelled vectors by adding rich metadata:

- **label** — a description of what the variable represents
- **unit** — a short code for the measurement unit (e.g., `CP_MEUR`)
- **definition** — a URI linking to a concept or standard
- **namespace** — optional, for classifying coded values (e.g., SDMX
  codes)

This is particularly useful for reproducible research,
standard-compliant data, or long-term interoperability. The class is
implemented with R’s
[`attributes()`](https://rdrr.io/r/base/attributes.html) function, which
guarantees wide compatibility. A defined vector can be used even in base
R.

``` r

attributes(gdp_1)
#> $label
#> [1] "Gross Domestic Product"
#> 
#> $class
#> [1] "haven_labelled_defined" "haven_labelled"         "vctrs_vctr"            
#> [4] "double"                
#> 
#> $unit
#> [1] "CP_MEUR"
#> 
#> $concept
#> [1] "http://data.europa.eu/83i/aa/GDP"
```

From this output it is clear that the actual S3 class is called
`haven_labelled_defined`, which clearly indicates the inheritance from
`haven_labelled` (See:
[labelled::labelled](https://larmarange.github.io/labelled/articles/labelled.html)).
In the dataset summary headers the `<defined>` abbreviation is used.

Use the
[`var_label()`](https://docs.ropensci.org/dataset/reference/var_label.md),
[`var_unit()`](https://docs.ropensci.org/dataset/reference/var_unit.md)
and
[`var_concept()`](https://docs.ropensci.org/dataset/reference/var_concept.md)
helper functions to set or retrieve metadata individually.

``` r

cat("Get the label only: ", var_label(gdp_1), "\n")
#> Get the label only:  Gross Domestic Product
cat("Get the unit only: ", var_unit(gdp_1), "\n")
#> Get the unit only:  CP_MEUR
cat("Get the concept definition only: ", var_concept(gdp_1), "\n")
#> Get the concept definition only:  http://data.europa.eu/83i/aa/GDP
cat("All attributes:\n")
#> All attributes:
```

## Printing and summary

The most frequently used vector methods, such as print or summary are
implemented as expected:

``` r

print(gdp_1)
#> gdp_1: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#>  [1] 2354.8 2593.9 2883.7 3119.5 5430.5 6423.7 6758.6 1265.1 1461.4 1612.3
```

``` r

summary(gdp_1)
#> Gross Domestic Product (CP_MEUR)
#>    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#>    1265    1798    2739    3390    4853    6759
```

## Handling ambiguity

If you try to concatenate a semantically under-specified new vector to
an existing `defined` vector, you will get an intended error indicating
that some attributes are not compatible. This prevents combining values
that differ in meaning, such as GDP figures expressed in different
currencies.

``` r

gdp_2 <- defined(
  c(2523.6, 2725.8, 3013.2),
  label = "Gross Domestic Product"
)
```

In the following example, `gdp_1` and `gdp_2` are not defined with the
same level of precision.

``` r

c(gdp_1, gdp_2)
```

    Error in vec_c():
    ! Can't combine ..1 <haven_labelled_defined> and ..2 <haven_labelled_defined>.
    ✖ Some attributes are incompatible.

To resolve this, you can add the missing attributes so that the vectors
are semantically compatible.

Let’s define better the GDP of the Faroe Islands:

``` r

var_unit(gdp_2) <- "CP_MEUR"
```

``` r

var_concept(gdp_2) <- "http://data.europa.eu/83i/aa/GDP"
```

Once the metadata matches, you can combine them.

``` r

new_gdp <- c(gdp_1, gdp_2)
summary(new_gdp)
#> Gross Domestic Product (CP_MEUR)
#>    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
#>    1265    2355    2726    3244    3120    6759
```

## Using namespaces for coded values

You can also define variables that store codes (like country codes) with
a namespace that points to a human- and machine-readable definition of
those codes. In statistical datasets, such attribute columns describe
characteristics of the observations or the measured variables.

``` r

country <- defined(
  c("AD", "LI", "SM"),
  label = "Country name",
  concept = "http://purl.org/linked-data/sdmx/2009/dimension#refArea",
  namespace = "https://www.geonames.org/countries/$1/"
)
```

For example, the namespace definition above points to:

- <https://www.geonames.org/countries/AD/> in the case of Andorra
- <https://www.geonames.org/countries/LI/> for Liechtenstein
- <https://www.geonames.org/countries/SM/> for San Marino

You can get or set the namespace of a defined vector with
[`var_namespace()`](https://docs.ropensci.org/dataset/reference/var_namespace.md).

``` r

var_namespace(country)
#> [1] "https://www.geonames.org/countries/$1/"
```

A URI such as
<http://publications.europa.eu/resource/authority/bna/c_6c2bb82d>
resolves to a machine-readable definition of geographical names.

The use of several `defined` vectors in a `dataset_df` object is
explained in a separate vignette.

## Basic Usage

You can create `defined` vectors from character values as well as
numeric values. Methods like
[`as_character()`](https://docs.ropensci.org/dataset/reference/as_character.md)
and
[`as_numeric()`](https://docs.ropensci.org/dataset/reference/as_numeric.md)
let you coerce back to base R types while controlling what happens to
the metadata.

``` r

countries <- defined(
  c("AD", "LI"),
  label = "Country code",
  namespace = "https://www.geonames.org/countries/$1/"
)

countries
#> x: Country code
#> Defined vector 
#> [1] "AD" "LI"
as_character(countries)
#> [1] "AD" "LI"
```

### Subsetting and coercion

Subsetting a `defined` vector works like subsetting any other vector.

``` r

gdp_1[1:2]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 2354.8 2593.9
gdp_1[gdp_1 > 5000]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 5430.5 6423.7 6758.6
```

- [`as.vector()`](https://rdrr.io/r/base/vector.html) removes the
  metadata entirely.  
- [`as.list()`](https://rdrr.io/r/base/list.html) retains the metadata
  for each element (definitions are repeated for each entry).

``` r

as.vector(gdp_1)
#>  [1] 2354.8 2593.9 2883.7 3119.5 5430.5 6423.7 6758.6 1265.1 1461.4 1612.3
as.list(gdp_1)
#> [[1]]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 2354.8
#> 
#> [[2]]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 2593.9
#> 
#> [[3]]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 2883.7
#> 
#> [[4]]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 3119.5
#> 
#> [[5]]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 5430.5
#> 
#> [[6]]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 6423.7
#> 
#> [[7]]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 6758.6
#> 
#> [[8]]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 1265.1
#> 
#> [[9]]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 1461.4
#> 
#> [[10]]
#> x: Gross Domestic Product
#> Defined as http://data.europa.eu/83i/aa/GDP, measured in CP_MEUR 
#> [1] 1612.3
```

### Coerce to base R types

[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
vectors support a family of coercion helpers.  
These methods avoid silent metadata loss and provide predictable
conversions while respecting the underlying data type.

All coercion functions follow the same principles:

- **They operate on the underlying values**, not on labels.

- **Metadata is removed by default** unless explicitly preserved.

- **Errors are thrown when coercion would lose information** (e.g.,
  converting character data to numeric).

Below are the available coercion helpers.

#### Character coercion

[`as_character()`](https://docs.ropensci.org/dataset/reference/as_character.md)
converts the vector to a base R character vector.

If value labels are present, they become the character representation;
otherwise, the underlying values are coerced.

``` r

as_character(country)
#> [1] "AD" "LI" "SM"
as_character(c(gdp_1, gdp_2))
#>  [1] "2354.8" "2593.9" "2883.7" "3119.5" "5430.5" "6423.7" "6758.6" "1265.1"
#>  [9] "1461.4" "1612.3" "2523.6" "2725.8" "3013.2"
```

#### Factor coercion

[`as_factor()`](https://docs.ropensci.org/dataset/reference/as_factor.md)
converts the vector into a factor.

- If value labels exist, they become factor levels.
- If not, the underlying values determine the factor levels.

``` r

as_factor(country)
#> [1] AD LI SM
#> Levels: AD LI SM
```

#### Numeric coercion

[`as_numeric()`](https://docs.ropensci.org/dataset/reference/as_numeric.md)
converts numeric `defined` vectors to base R numeric.

It throws an error if the underlying data is not numeric.

``` r

as_numeric(c(gdp_1, gdp_2))
#>  [1] 2354.8 2593.9 2883.7 3119.5 5430.5 6423.7 6758.6 1265.1 1461.4 1612.3
#> [11] 2523.6 2725.8 3013.2
```

#### Logical coercion

[`as_logical()`](https://docs.ropensci.org/dataset/reference/as_logical.md)
converts `defined` vectors whose underlying data is logical
(`TRUE`/`FALSE`).

Logical `defined` vectors cannot have value labels, ensuring consistent
behaviour.

``` r

flag <- defined(c(TRUE, FALSE, TRUE), label = "Example flag")
as_logical(flag)
#> [1]  TRUE FALSE  TRUE
```

#### Date coercion

`as_Date()` converts a `defined` vector that inherits from `Date` back
into a standard R `Date` vector.

Metadata is removed unless requested.

``` r

dates <- defined(
  as.Date(c("2020-01-01", "2020-01-02")),
  label = "Reference date"
)
as.Date(dates)
#> [1] "2020-01-01" "2020-01-02"
```

#### POSIXct coercion

`as_POSIXct()` converts a POSIXct-based `defined` vector back into a
base R `POSIXct` object.

Time zones and the underlying numeric representation are always
preserved.

``` r

times <- defined(
  as.POSIXct(c("2020-01-01 12:00:00", "2020-01-01 18:00:00")),
  label = "Timestamp"
)

times
#> x: Timestamp
#> Defined vector 
#> [1] 1577880000 1577901600
```

These coercion helpers ensure that `defined` vectors behave predictably
in modelling, exporting, and data cleaning workflows — while still
preserving semantic metadata when necessary.

## Conclusion

The
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
function provides a lightweight yet powerful way to make vectors
self-descriptive by attaching semantic metadata directly to them. By
combining a variable label, unit of measurement, concept definition, and
optional namespace, `defined` ensures that each vector’s meaning is
explicit, consistent, and machine-readable.

Because the metadata is embedded at creation time, it travels with the
vector throughout your workflow — whether you are analysing,
transforming, or exporting data.  
This prevents context loss, supports the FAIR data principles (Findable,
Accessible, Interoperable, Reusable), and facilitates integration with
semantic web technologies.

`defined` vectors work seamlessly with the
[`dataset_df`](https://dataset.dataobservatory.eu/articles/dataset_df.html)
class to create semantically enriched data frames where both datasets
and their constituent variables carry rich, standardised metadata.  
For more on creating semantically enriched datasets, see the
**dataset_df** vignette.

For guidance on recording bibliographic metadata and citations, see the
**bibrecord** vignette.
