# Set the Primary Language of a Dataset

Assign the primary language of a semantically rich dataset object using
an ISO 639 language code or full language name. This sets the `language`
attribute in the dataset's metadata.

## Usage

``` r
language(x)

language(x, iso_639_code = "639-3") <- value

language(x, iso_639_code = "639-3") <- value
```

## Arguments

- x:

  A dataset object created by
  [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  or
  [`as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md).

- iso_639_code:

  A character string indicating the desired return format: either
  `"639-3"` (default; terminologic) or `"639-1"` (2-letter code).

- value:

  A 2-letter or 3-letter language code (ISO 639-1 or ISO 639-2), or a
  full language name (case-insensitive).

## Value

The dataset with an updated `language` attribute, typically an ISO
639-2/T code (`Alpha_3_T`) such as `"fra"`, `"eng"`, `"spa"`, etc.

## Details

This function supports recognition of:

- 2-letter codes (ISO 639-1, e.g., `"en"`, `"fr"`)

- 3-letter codes from both:

  - `Alpha_3_B` (bibliographic, e.g., `"fre"`)

  - `Alpha_3_T` (terminologic, e.g., `"fra"`)

- Full language names (e.g., `"English"`, `"French"`)

For compatibility with open science repositories and modern metadata
standards, this function **returns the terminologic code** (`Alpha_3_T`)
when available. If `Alpha_3_T` is missing for a language, the legacy
bibliographic code (`Alpha_3_B`) is used as a fallback.

Full language names (e.g., `"English"`, `"Spanish"`) are matched
case-insensitively against the ISO 639-2 Name field. Exact matches are
attempted first; if none are found, a prefix match is used. For example:

- `"English"` returns `"eng"`

- `"English, Old"` returns `"ang"`

This means that:

- Both `"fra"` (terminologic) and `"fre"` (bibliographic) will be
  accepted as valid input for French

- The resulting value stored and returned will be `"fra"`

This behaviour aligns with:

- [DataCite Metadata Schema
  4.4](https://support.datacite.org/docs/datacite-metadata-schema-v44-recommended-and-optional-properties#9-language)

- [schema.org](https://schema.org/inLanguage)

- Common repository practices (Zenodo, OSF, Figshare)

If `value` is `NULL`, the language is marked as `":unas"` (unspecified).

In some cases\<U+2014\>especially for historical or moribund
languages\<U+2014\>multiple similar names may exist. In such cases, it
is safer to use a specific language code (e.g., `"ang"` instead of
`"English, Old"` and `"enm"` for `"English, Middle (1100-1500)"`). You
can also refer directly to the definitions in
[ISOcodes::ISO_639_2](https://rdrr.io/pkg/ISOcodes/man/ISO_639.html) for
clarity.

## See also

Other bibliographic helper functions:
[`contributor()`](https://docs.ropensci.org/dataset/reference/contributor.md),
[`creator()`](https://docs.ropensci.org/dataset/reference/creator.md),
[`dataset_format()`](https://docs.ropensci.org/dataset/reference/dataset_format.md),
[`dataset_title()`](https://docs.ropensci.org/dataset/reference/dataset_title.md),
[`description()`](https://docs.ropensci.org/dataset/reference/description.md),
[`geolocation()`](https://docs.ropensci.org/dataset/reference/geolocation.md),
[`get_bibentry()`](https://docs.ropensci.org/dataset/reference/get_bibentry.md),
[`publication_year()`](https://docs.ropensci.org/dataset/reference/publication_year.md),
[`publisher()`](https://docs.ropensci.org/dataset/reference/publisher.md),
[`relation()`](https://docs.ropensci.org/dataset/reference/relation.md),
[`rights()`](https://docs.ropensci.org/dataset/reference/rights.md),
[`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)

## Examples

``` r
df <- dataset_df(data.frame(x = 1:3))

language(df) <- "English" # Returns "eng"
language(df) <- "fre" # Legacy code; returns "fra"
language(df) <- "fra" # Returns "fra"
language(df, iso_639_code = "639-1") <- "fra" # Returns "fr"

language(df) <- NULL # Sets ":unas"
```
