# Semantic labelled vector class

The class `haven_labelled_defined` represents a semantically enriched
labelled vector created by
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

Objects of this class inherit from:

- `[haven:labelled]()` for numeric, character, and factor data;

- `Date` for temporal dates;

- `POSIXct` and `POSIXt` for timestamps;

- `logical` for boolean data.

The class tag enables S3 method dispatch for:

- `[as_character()]`

- `[as_numeric()]`

- `[as_logical()]`

- `as.Date`

- `as.POSIXct`

- [`print.haven_labelled_defined`](https://docs.ropensci.org/dataset/reference/print.haven_labelled_defined.md)

- [`summary.haven_labelled_defined`](https://docs.ropensci.org/dataset/reference/defined.md)

Users normally do not construct this class directly; it is returned as
the result of calling
[`defined()`](https://docs.ropensci.org/dataset/reference/defined.md).

## Value

No value is returned. This documentation page exists so that the class
can be referenced in help topics.
