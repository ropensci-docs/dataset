# Package index

## Dataset

Work with DataSet objects that resemble the W3C and SDMX datacube model.

- [`dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  [`as_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  [`is.dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  [`print(`*`<dataset_df>`*`)`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  [`is_dataset_df()`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  [`names(`*`<dataset_df>`*`)`](https://docs.ropensci.org/dataset/reference/dataset_df.md)
  :

  Create a new `dataset_df` object

- [`bind_defined_rows()`](https://docs.ropensci.org/dataset/reference/bind_defined_rows.md)
  : Bind strictly defined rows

- [`as.data.frame(`*`<dataset_df>`*`)`](https://docs.ropensci.org/dataset/reference/as.data.frame.dataset_df.md)
  :

  Convert a `dataset_df` to a base `data.frame`

- [`as_tibble()`](https://docs.ropensci.org/dataset/reference/as_tibble.dataset_df.md)
  [`as.tibble.dataset_df()`](https://docs.ropensci.org/dataset/reference/as_tibble.dataset_df.md)
  :

  Coerce a `dataset_df` to a tibble

## Semantic harmonisation

Lightweight semantic mappings and semantic preprocessing.

- [`prelabel()`](https://docs.ropensci.org/dataset/reference/prelabel.md)
  [`is.prelabelled()`](https://docs.ropensci.org/dataset/reference/prelabel.md)
  : Add lightweight semantic mappings to a vector
- [`as_character(`*`<prelabelled>`*`)`](https://docs.ropensci.org/dataset/reference/as_character.prelabelled.md)
  : Coerce prelabelled vectors to semantic character workspace
- [`as_value_key()`](https://docs.ropensci.org/dataset/reference/as_value_key.md)
  [`invert_value_key()`](https://docs.ropensci.org/dataset/reference/as_value_key.md)
  : Coerce semantic mappings to canonical key-value form

## Defined

A labelled subclass that retains unit, definition and namespace.

- [`defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
  [`is.defined()`](https://docs.ropensci.org/dataset/reference/defined.md)
  [`summary(`*`<haven_labelled_defined>`*`)`](https://docs.ropensci.org/dataset/reference/defined.md)
  : Create a semantically enriched vector with variable-level metadata
- [`var_label(`*`<defined>`*`)`](https://docs.ropensci.org/dataset/reference/var_label.md)
  [`label_attribute()`](https://docs.ropensci.org/dataset/reference/var_label.md)
  [`` `var_label<-`() ``](https://docs.ropensci.org/dataset/reference/var_label.md)
  [`var_label(`*`<dataset_df>`*`)`](https://docs.ropensci.org/dataset/reference/var_label.md)
  : Get or Set a Variable Label
- [`var_labels()`](https://docs.ropensci.org/dataset/reference/var_labels.md)
  [`` `var_labels<-`() ``](https://docs.ropensci.org/dataset/reference/var_labels.md)
  : Get or set all variable labels on a dataset
- [`var_unit()`](https://docs.ropensci.org/dataset/reference/var_unit.md)
  [`` `var_unit<-`() ``](https://docs.ropensci.org/dataset/reference/var_unit.md)
  [`get_variable_units()`](https://docs.ropensci.org/dataset/reference/var_unit.md)
  [`unit_attribute()`](https://docs.ropensci.org/dataset/reference/var_unit.md)
  [`get_unit_attribute()`](https://docs.ropensci.org/dataset/reference/var_unit.md)
  [`set_unit_attribute()`](https://docs.ropensci.org/dataset/reference/var_unit.md)
  [`` `unit_attribute<-`() ``](https://docs.ropensci.org/dataset/reference/var_unit.md)
  : Get or Set a Unit of Measure
- [`var_concept()`](https://docs.ropensci.org/dataset/reference/var_concept.md)
  [`` `var_concept<-`() ``](https://docs.ropensci.org/dataset/reference/var_concept.md)
  : Get / set a concept definition for a vector or a dataset
- [`var_namespace()`](https://docs.ropensci.org/dataset/reference/var_namespace.md)
  [`` `var_namespace<-`() ``](https://docs.ropensci.org/dataset/reference/var_namespace.md)
  [`get_variable_namespaces()`](https://docs.ropensci.org/dataset/reference/var_namespace.md)
  [`namespace_attribute()`](https://docs.ropensci.org/dataset/reference/var_namespace.md)
  [`get_namespace_attribute()`](https://docs.ropensci.org/dataset/reference/var_namespace.md)
  [`set_namespace_attribute()`](https://docs.ropensci.org/dataset/reference/var_namespace.md)
  [`` `namespace_attribute<-`() ``](https://docs.ropensci.org/dataset/reference/var_namespace.md)
  : Get or Set the Namespace of a Variable
- [`as_numeric()`](https://docs.ropensci.org/dataset/reference/as_numeric.md)
  : Coerce a defined vector to numeric
- [`as_character()`](https://docs.ropensci.org/dataset/reference/as_character.md)
  [`as.character(`*`<haven_labelled_defined>`*`)`](https://docs.ropensci.org/dataset/reference/as_character.md)
  : Coerce a defined vector to character
- [`as_factor()`](https://docs.ropensci.org/dataset/reference/as_factor.md)
  : Coerce a defined vector to a factor
- [`as_logical()`](https://docs.ropensci.org/dataset/reference/as_logical.md)
  : Coerce a defined vector to logical
- [`as.Date(`*`<haven_labelled_defined>`*`)`](https://docs.ropensci.org/dataset/reference/as.Date.haven_labelled_defined.md)
  : Coerce a defined Date vector to a base R Date
- [`as.POSIXct(`*`<haven_labelled_defined>`*`)`](https://docs.ropensci.org/dataset/reference/as.POSIXct.haven_labelled_defined.md)
  : Coerce a defined POSIXct vector to a base R POSIXct
- [`print(`*`<haven_labelled_defined>`*`)`](https://docs.ropensci.org/dataset/reference/print.haven_labelled_defined.md)
  : Print a defined (haven_labelled_defined) vector
- [`strip_defined()`](https://docs.ropensci.org/dataset/reference/strip_defined.md)
  : Strip the class from a defined vector
- [`get_variable_concepts()`](https://docs.ropensci.org/dataset/reference/get_variable_concepts.md)
  : Get concepts for all variables in a dataset_df
- [`c(`*`<haven_labelled_defined>`*`)`](https://docs.ropensci.org/dataset/reference/c.haven_labelled_defined.md)
  : Combine defined vectors with metadata checks

## Bibliography functions

Constructors for extended bibentry classes (DataCite / DCTERMS).

- [`bibrecord()`](https://docs.ropensci.org/dataset/reference/bibrecord.md)
  : Create a Modern Metadata Object Compatible with bibentry
- [`as_datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md)
  [`datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md)
  [`is.datacite()`](https://docs.ropensci.org/dataset/reference/datacite.md)
  [`print(`*`<datacite>`*`)`](https://docs.ropensci.org/dataset/reference/datacite.md)
  : Create a Bibentry Object with DataCite Metadata Fields
- [`as_dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md)
  [`dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md)
  [`is.dublincore()`](https://docs.ropensci.org/dataset/reference/dublincore.md)
  [`print(`*`<dublincore>`*`)`](https://docs.ropensci.org/dataset/reference/dublincore.md)
  : Add or Retrieve Dublin Core Metadata

## Bibliography helpers

Helpers to read/update bibliography attributes of dataset_df.

- [`get_bibentry()`](https://docs.ropensci.org/dataset/reference/get_bibentry.md)
  [`` `set_bibentry<-`() ``](https://docs.ropensci.org/dataset/reference/get_bibentry.md)
  : Get or set the bibentry
- [`dataset_title()`](https://docs.ropensci.org/dataset/reference/dataset_title.md)
  [`` `dataset_title<-`() ``](https://docs.ropensci.org/dataset/reference/dataset_title.md)
  : Get or Set the Title of a Dataset
- [`creator()`](https://docs.ropensci.org/dataset/reference/creator.md)
  [`` `creator<-`() ``](https://docs.ropensci.org/dataset/reference/creator.md)
  : Get/set the Creator of the object.
- [`contributor()`](https://docs.ropensci.org/dataset/reference/contributor.md)
  [`` `contributor<-`() ``](https://docs.ropensci.org/dataset/reference/contributor.md)
  : Get or set contributors
- [`language()`](https://docs.ropensci.org/dataset/reference/language.md)
  [`` `language<-`() ``](https://docs.ropensci.org/dataset/reference/language.md)
  : Set the Primary Language of a Dataset
- [`subject()`](https://docs.ropensci.org/dataset/reference/subject.md)
  [`subject_create()`](https://docs.ropensci.org/dataset/reference/subject.md)
  [`` `subject<-`() ``](https://docs.ropensci.org/dataset/reference/subject.md)
  [`is.subject()`](https://docs.ropensci.org/dataset/reference/subject.md)
  : Create, add, or retrieve a subject
- [`relation()`](https://docs.ropensci.org/dataset/reference/relation.md)
  [`` `relation<-`() ``](https://docs.ropensci.org/dataset/reference/relation.md)
  [`related_create()`](https://docs.ropensci.org/dataset/reference/relation.md)
  [`is.related()`](https://docs.ropensci.org/dataset/reference/relation.md)
  [`related_item()`](https://docs.ropensci.org/dataset/reference/relation.md)
  [`` `related_item<-`() ``](https://docs.ropensci.org/dataset/reference/relation.md)
  : Add or retrieve related items (DataCite/Dublin Core)
- [`publication_year()`](https://docs.ropensci.org/dataset/reference/publication_year.md)
  [`` `publication_year<-`() ``](https://docs.ropensci.org/dataset/reference/publication_year.md)
  : Get or Set the Publication Year of a Dataset Object
- [`publisher()`](https://docs.ropensci.org/dataset/reference/publisher.md)
  [`` `publisher<-`() ``](https://docs.ropensci.org/dataset/reference/publisher.md)
  : Get or Set the Publisher of a Dataset Object
- [`dataset_format()`](https://docs.ropensci.org/dataset/reference/dataset_format.md)
  [`` `dataset_format<-`() ``](https://docs.ropensci.org/dataset/reference/dataset_format.md)
  : Get or set the technical format of a dataset
- [`rights()`](https://docs.ropensci.org/dataset/reference/rights.md)
  [`` `rights<-`() ``](https://docs.ropensci.org/dataset/reference/rights.md)
  : Get or Set the Rights of a Dataset Object
- [`identifier()`](https://docs.ropensci.org/dataset/reference/identifier.md)
  [`` `identifier<-`() ``](https://docs.ropensci.org/dataset/reference/identifier.md)
  : Get or Set the Identifier of a Dataset or Metadata Record
- [`description()`](https://docs.ropensci.org/dataset/reference/description.md)
  [`` `description<-`() ``](https://docs.ropensci.org/dataset/reference/description.md)
  : Get or set the dataset Description
- [`geolocation()`](https://docs.ropensci.org/dataset/reference/geolocation.md)
  [`` `geolocation<-`() ``](https://docs.ropensci.org/dataset/reference/geolocation.md)
  : Get or Set the Geolocation of a Dataset Object

## RDF Serialisation

Describe data/metadata in RDF.

- [`describe()`](https://docs.ropensci.org/dataset/reference/describe.md)
  : Describe a dataset in N-Triples format
- [`provenance()`](https://docs.ropensci.org/dataset/reference/provenance.md)
  [`` `provenance<-`() ``](https://docs.ropensci.org/dataset/reference/provenance.md)
  : Get or update provenance information
- [`xsd_convert()`](https://docs.ropensci.org/dataset/reference/xsd_convert.md)
  : Convert to XML Schema Definition (XSD) Types
- [`n_triples()`](https://docs.ropensci.org/dataset/reference/n_triples.md)
  : Create N-Triples
- [`n_triple()`](https://docs.ropensci.org/dataset/reference/n_triple.md)
  : Create an N-Triple
- [`dataset_to_triples()`](https://docs.ropensci.org/dataset/reference/dataset_to_triples.md)
  : Dataset to triples (three columns or N-Triples)
- [`id_to_column()`](https://docs.ropensci.org/dataset/reference/id_to_column.md)
  : Add Identifier to First Column of a Dataset

## Replication Datasets

Enriched Orange and simple GDP demo datasets.

- [`orange_df`](https://docs.ropensci.org/dataset/reference/orange_df.md)
  : Growth of Orange Trees
- [`gdp`](https://docs.ropensci.org/dataset/reference/gdp.md) : A Small
  GDP Dataset
