# Growth of Orange Trees

A dataset recording the growth of orange trees, replicated from the
classic
[datasets::Orange](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/Orange.html)
dataset and implemented as a `dataset_df` S3 class with enhanced
semantic metadata.

## Usage

``` r
orange_df
```

## Format

A data frame with 35 rows and 4 variables:

- `rowid`: A unique identifier for each row (character)

- `tree`: Tree identifier (ordered factor)

- `age`: Age of the tree in days (numeric)

- `circumference`: Trunk circumference in mm (numeric)

## Details

This is a semantically enriched version of the classic Orange dataset,
constructed using the
[`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
and
[`dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md)
constructors. Each column includes semantic metadata such as units,
labels, concepts, or namespace identifiers. The dataset also embeds a
machine-readable citation for reproducibility and provenance tracking.

### Constructor Example

    orange_bibentry <- dublincore(
      title = "Growth of Orange Trees",
      creator = c(
        person(
          given = "N.R.",
          family = "Draper",
          role = "cre",
          comment = c(VIAF = "http://viaf.org/viaf/84585260")
        ),
        person(
          given = "H",
          family = "Smith",
          role = "cre"
        )
      ),
      contributor = person(
        given = "Antal",
        family = "Daniel",
        role = "dtm"
      ),
      publisher = "Wiley",
      datasource = "https://isbnsearch.org/isbn/9780471170822",
      dataset_date = 1998,
      identifier = "https://doi.org/10.5281/zenodo.14917851",
      language = "en",
      description = "The Orange data frame has 35 rows and 3 columns of records of the growth of orange trees."
    )

    orange_df <- dataset_df(
      rowid = defined(paste0("orange:", row.names(Orange)),
        label = "ID in the Orange dataset",
        namespace = c("orange" = "datasets::Orange")
      ),
      tree = defined(Orange$Tree,
        label = "The number of the tree"
      ),
      age = defined(Orange$age,
        label = "The age of the tree",
        unit = "days since 1968/12/31"
      ),
      circumference = defined(Orange$circumference,
        label = "circumference at breast height",
        unit = "milimeter",
        concept = "https://www.wikidata.org/wiki/Property:P2043"
      ),
      dataset_bibentry = orange_bibentry
    )

    orange_df$rowid <- defined(orange_df$rowid,
      namespace = "https://doi.org/10.5281/zenodo.14917851"
    )

## References

- Draper, N. R. & Smith, H. (1998). *Applied Regression Analysis* (3rd
  ed.). Wiley.

- Pinheiro, J. C. & Bates, D. M. (2000). *Mixed-effects Models in S and
  S-PLUS*. Springer.

- Becker, R. A., Chambers, J. M. & Wilks, A. R. (1988). *The New S
  Language*. Wadsworth & Brooks/Cole.

## Examples

``` r
# Print with semantic citation and data preview
print(orange_df)
#> Draper-Smith (1998): Growth of Orange Trees [dataset], https://doi.org/10.5281/zenodo.14917851
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

# Access semantic metadata associated with variables
print(orange_df$age)
#> orange_df$age: The age of the tree
#> Measured in days since 1968/12/31 
#>  [1]  118  484  664 1004 1231 1372 1582  118  484  664 1004 1231 1372 1582  118
#> [16]  484  664 1004 1231 1372 1582  118  484  664 1004 1231 1372 1582  118  484
#> [31]  664 1004 1231 1372 1582

# Retrieve the embedded bibliographic record
as_dublincore(orange_df)
#> Dublin Core Metadata Record
#> --------------------------
#> Title:       Growth of Orange Trees
#> Creator(s):  N.R. Draper [cre] (VIAF: http://viaf.org/viaf/84585260); H Smith [cre]
#> Contributor(s): :unas
#> Publisher:   Wiley
#> Year:        1998
#> Language:    en
#> Description: The Orange data frame has 35 rows and 3 columns of records of the growth of orange trees.
```
