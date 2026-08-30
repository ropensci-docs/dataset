# A Small GDP Dataset

A compact sample of GDP and main aggregates from Eurostat's annual
international cooperation dataset. This data subset contains
illustrative records for select countries and time periods.

## Usage

``` r
gdp
```

## Format

A data frame with 10 rows and 5 variables:

- `geo`: Country name (character)

- `year`: Reference year (integer)

- `gdp`: Gross Domestic Product value (numeric)

- `unit`: Unit of measurement, e.g., "Million EUR" (character)

- `freq`: Observation frequency, e.g., "Annual" (character)

## Source

Eurostat (2021). GDP and main aggregates - international data
cooperation (annual data).
[doi:10.2908/NAIDA_10_GDP](https://doi.org/10.2908/NAIDA_10_GDP)

## Details

This dataset is intended for examples, tests, and demonstration
purposes. It reflects simplified GDP data as published by Eurostat. The
actual Eurostat dataset includes more countries, breakdowns, and
metadata.

## Examples

``` r
head(gdp)
#> # A tibble: 6 × 5
#>   geo    year   gdp unit    freq 
#>   <chr> <int> <dbl> <chr>   <chr>
#> 1 AD     2020 2355. CP_MEUR A    
#> 2 AD     2021 2594. CP_MEUR A    
#> 3 AD     2022 2884. CP_MEUR A    
#> 4 AD     2023 3120. CP_MEUR A    
#> 5 LI     2020 5430. CP_MEUR A    
#> 6 LI     2021 6424. CP_MEUR A    
```
