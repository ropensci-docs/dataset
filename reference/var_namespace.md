# Get or Set the Namespace of a Variable

Retrieve or assign the namespace part of a permanent, global variable
identifier, independent of the current R session or instance.

## Usage

``` r
var_namespace(x, ...)

var_namespace(x) <- value

get_variable_namespaces(x, ...)

namespace_attribute(x)

get_namespace_attribute(x)

set_namespace_attribute(x, value)

namespace_attribute(x) <- value
```

## Arguments

- x:

  A vector.

- ...:

  Additional arguments for method compatibility with other classes.

- value:

  A character string specifying the namespace, or `NULL` to remove it.

## Value

A character string representing the namespace attribute of a vector
constructed with
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).
Returns the updated object (in setter forms).

## Details

The `namespace` attribute is useful when working with remote, linked, or
open data sources. Variable identifiers in such datasets are often
qualified with a common namespace prefix. When combined, the prefix and
namespace form a persistent URI or IRI for the variable.

Retaining the namespace ensures the identifiers remain valid and
resolvable during validation, merging, or future updates of the vector
(such as when it is used as a column in a dataset).

`get_variable_namespaces()` is an alias for `var_namespace()`.
`namespace_attribute()` and `set_namespace_attribute()` are internal
helpers.

For full usage, see:
[`vignette("defined", package = "dataset")`](https://docs.ropensci.org/dataset/articles/defined.md)
\<U+2014\> demonstrating integration of variable labels, namespaces,
units of measure, and machine-independent identifiers.

## See also

Other defined metadata methods and functions:
[`var_label`](https://docs.ropensci.org/dataset/reference/var_label.md),
[`var_labels()`](https://docs.ropensci.org/dataset/reference/var_labels.md),
[`var_unit()`](https://docs.ropensci.org/dataset/reference/var_unit.md)

## Examples

``` r
# Define a vector with a namespace
x <- defined("Q42", namespace = c(wd = "https://www.wikidata.org/wiki/"))

# Get the namespace
var_namespace(x)
#>                               wd 
#> "https://www.wikidata.org/wiki/" 
get_variable_namespaces(x)
#>                               wd 
#> "https://www.wikidata.org/wiki/" 

# Set the namespace
var_namespace(x) <- "https://example.org/ns/"

# Remove the namespace
var_namespace(x) <- NULL

# Use lower-level helpers (not typically used directly)
namespace_attribute(x)
#> NULL
namespace_attribute(x) <- "https://example.org/custom/"
```
