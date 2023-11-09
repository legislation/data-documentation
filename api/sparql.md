# Linked Data and the SPARQL endpoint

## What is the Linked Data service?

The Legislation Linked Data service provides metadata about UK legislation from 1235 to the present day, including historical legislation enacted before the existence of Great Britain and the United Kingdom. You can query the metadata through a SPARQL query service (see the section on [querying using SPARQL](#sparql) below), and we intend to also offer the data via a REST API in future (see the section on [future developments](#future) below).

The metadata in the Linked Data store come from various sources, including the legislation itself and various reference texts and databases supplied to us by other organisations. We are grateful to our partner organisations for their contributions to the core reference dataset.

The Legislation Linked Data service is **currently in beta** and the service is subject to change (see the section on [limitations and future developments](#limitations) below). We want to gather diverse feedback and very much appreciate all users who are able to find time to experiment with the service and tell us about their experiences. You are welcome to [contact us](index.md#contact-us) with feedback.

## What does the Linked Data service provide?

### Purpose of the service

The purpose of the Linked Data service is to be a single source of truth for UK legislation, combining different kinds of data about legislation from many sources and making it available in one place through a unified interface. We are modelling our data using public ontologies, both pre-existing and bespoke (read about our [ontologies and vocabularies](#ontologies) below), so that our data have a coherent and consistent structure.

We hope that the Linked Data service will enable developers and data users to more easily find information about legislation and build applications that use legislation data.

### The data

#### Sources of data

The Linked Data service will provide legislation data from multiple sources (internal and external systems, reference texts and databases, external organisations) and on various topics (basic data, amendments to legislation, citations and cross-references and so on). We have designed our data model to distinguish which data for each item of legislation relate to which source and topic (see the section on [datasets](#datasets) below), so that it is possible to query for only certain kinds of data for a given item or items.

The sources of data we currently use include:

 * Information from [legislation.gov.uk](https://www.legislation.gov.uk/)’s Publishing and bibliographic systems, provided by the departments and organisations making legislation and by our publishing and content teams;
 * Information from historical reference texts, such as printed volumes of legislation and the Chronological Tables of Statutes;
 * Databases of legislation, such as the [legislation.gov.uk](https://www.legislation.gov.uk/) website database and datasets provided by partners.

We will continue to add new sources and kinds of data to the Linked Data service (see the section on [future developments](#future) below).

#### Categories of available data

The Linked Data service currently provides basic metadata about:

<table class="linked-data">
<tbody>
<tr>
<th>Thing</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="3">Legislation and interpretations</td>
<td>The current and original interpretation of each item of UK legislation and the item of legislation that it represents</td>
</tr>
<tr>
<td>Welsh-language interpretations of legislation</td>
</tr>
<tr>
<td>Quashed items of UK legislation</td>
</tr>
<tr>
<td>Monarchs, reigns and parliamentary sessions</td>
<td>For older legislation, the parliamentary sessions, reigns and regnal years during which legislation was enacted, and the reigning monarchs for those periods</td>
</tr>
<tr>
<td>Datasets</td>
<td>Datasets available through the service</td>
</tr>
<tr>
<td>Ontology</td>
<td>Classes and properties used in the core reference ontology</td>
</tr>
<tr>
<td>The service</td>
<td>The service itself and its SPARQL endpoint</td>
</tr>
<tr>
<td>Provenance</td>
<td>Information about the provenance of data in the store, such as when and how it was created</td>
</tr>
</tbody>
</table>

### Understanding the structure of the data

#### Legislation, versions and FRBR

We use a variant of the [FRBR model](https://en.wikipedia.org/wiki/Functional_Requirements_for_Bibliographic_Records) to structure our legislation and its metadata. FRBR defines the concept of a “work” (an intellectual creation) separately from an “expression” (the realisation of a work, such as an edition of a book or an arrangement of a song) and a “manifestation” (the embodiment of an expression, such as a print or e-book version of an edition of a book, or a recording of an arrangement of a song).

In the legislation ontology, we map the FRBR concepts onto the following legislation concepts:

 * an item of legislation is a work;
 * an interpretation (version) of an item of legislation is an expression;
 * an interpretation of an item in a specific file format is a manifestation.

An item of legislation will always have at least one interpretation, which is the text of the item as it was enacted by a legislature or made by a government minister or body. If the item has been amended, it will also have additional interpretations for each time period (and in some cases geographical extent) where the text or meaning or the document differs. Currently, the core reference dataset only contains information on the original and current interpretation of each item of legislation (plus an additional Welsh original and current interpretation for Welsh dual-language items), or a “quashed” interpretation for any item that the courts have declared unlawful.

Note that we only provide metadata about items and interpretations of legislation, not their manifestations.

#### Triples

The Linked Data store is a triplestore – a database that contains triples. Each triple is a three-part statement consisting of:

 * a _subject_ (a URI representing the entity the triple is about),
 * a _predicate_ (a URI representing a property or relationship of the subject) and
 * an _object_ (a URI representing an entity that the predicate relates to the subject, or a URI or value that is the value of the property represented by the predicate)

For example, a triple stating that the title of 2021 c. 10 is “Trade Act 2021” could be represented as follows:

```
prefix @leg: <http://www.legislation.gov.uk/def/legislation>

<http://www.legislation.gov.uk/id/ukpga/2021/10> leg:title "Trade Act 2021"@en.
```

In this example:

 * the URI ending `/ukpga/2021/10` is the subject,
 * `leg:title` is the predicate (short for `<http://www.legislation.gov.uk/def/legislation/title>`, read more about [ontologies and vocabularies](#Ontologies) below) and
 * `"Trade Act 2021"@en` is the object – in this case, a string with an `@en` (English) language tag.

Here, the URI ending `/ukpga/2021/10` is the subject, `leg:title` (short for `<http://www.legislation.gov.uk/def/legislation/title>`) is the predicate and `"Trade Act 2021"@en` is the object – in this case, a string with an `@en` (English) language tag.

#### Ontologies and vocabularies<a id="ontologies"></a>

The Linked Data service uses a bespoke legislation ontology. The ontology specifies a vocabulary of classes and properties that entities in the data can use, such as `ScottishAct` or `title`. There is [documentation for the ontology](../def/legislation/).

The most commonly used vocabularies in the Linked Data service are:

<table class="linked-data">
<tbody>
<tr>
<th>Ontology</th>
<th>Namespace prefix</th>
<th>Description</th>
</tr>
<tr>
<td>Core legislation ontology</td>
<td>`http://www.legislation.gov.uk/def/legislation/`</td>
<td>Defines core classes and properties for linked data for legislation.gov.uk</td>
</tr>
<tr>
<td>RDF vocabulary</td>
<td>`http://www.w3.org/1999/02/22-rdf-syntax-ns#`</td>
<td>Defines core classes and properties for relational data</td>
</tr>
<tr>
<td>RDF schema vocabulary</td>
<td>`http://www.w3.org/2000/01/rdf-schema#`</td>
<td>Defines core classes and properties for describing ontologies</td>
</tr>
<tr>
<td>Dublin Core</td>
<td>`http://purl.org/dc/terms/`</td>
<td>Defines common classes and properties for metadata</td>
</tr>
<tr>
<td>OWL (Web Ontology Language)</td>
<td>`http://www.w3.org/2002/07/owl#`</td>
<td>Defines further classes and properties for describing ontologies</td>
</tr>
</tbody>
</table>

#### Graphs

Each triple in the Linked Data store exists within a named graph, which is a group of triples named by a URI. The Linked Data service uses graphs to group together triples that relate to one or more entities and also share a specific theme and source. For example, the above triple exists within the graph named `<http://www.legislation.gov.uk/graph/core/publishingsystem/department/ukpga/2021/10>`. The graph URI indicates that this graph is part of the “core” topic dataset, the “publishing” system dataset and the “department” origin dataset (see below).

#### Datasets

The Linked Data service subdivides its data into different datasets according to the following attributes:

 * **Topic:** The topic or theme of the data. Currently, the only topic is “core”, which relates to core data about legislation such as titles and citations, years and numbers and the languages of the text;
 * **System:** The system that provided the data. Currently, the only systems are “alignment” (which contains information derived from reference texts and various databases) and “publishing” (which contains information about modern legislation published through [legislation.gov.uk](https://www.legislation.gov.uk/)’s Publishing system);
 * **Origin:** The process, agent or other source responsible for the data in the relevant system. Currently, the only sources are “coreinputs” (the dataset in the alignment system containing the core data) and “department” (data about an item of legislation input to the Publishing system by the entity publishing it);
 * **Data unit:** An intersection of a topic, system and origin. Currently, there are two data units: one is the intersection of the “core” topic, the “alignment” system and the “coreinputs” origin, and the other is the intersection of the “core” topic, the “publishing” system and the “department” origin. There can be multiple data units for each topic, system and origin. Only certain combinations of topics, systems and origins will contain data – for example, not all systems or origins will provide data for the “core” topic, and the “department” origin is currently only relevant to the “publishing” system.

Each topic, system, origin and data unit has a dataset in the Linked Data store. Each dataset links to all the graphs that contain related data (either data within the dataset’s topic, from the dataset’s related system or origin, or within the related data unit).

#### Provenance information

The Linked Data store contains provenance information, which explains when and how a particular graph or dataset was modified. Each graph and dataset links to one or more provenance events via the predicate `<http://www.w3.org/ns/prov#wasInfluencedBy>`, each of which indicates a type of event (creation or update) and a time of occurrence.

### Limitations and future developments

#### Limitations<a id="limitations"></a>

The Legislation Linked Data service is **currently in beta** and so its functionality may change, including:

 * The items for which metadata are available
 * Metadata about any individual document or set of documents
 * The structure of the data and the ontologies and schemas that specify it
 * The API endpoints the service provides
 * The URI schemes the data and service use

However, we do not expect to make many breaking changes to the ontology, or to remove more than a very small amount of data. We do not normally remove data unless they are erroneous.

The Linked Data service does not not currently support querying legislation document structure or text.

#### Future developments<a id="future"></a>

In future, we intend to release a Linked Data API that will allow users to retrieve metadata from the Linked Data service for individual legislation items and entities. It will augment the existing Legislation API available on legislation.gov.uk by providing metadata from the Linked Data service both as individual metadata resources and embedded within legislation documents.

We also plan for the Linked Data service to provide the following additonal data:

 * Legislation publishing data, e.g. data collected in our publishing and bibliographic systems during the registration and publication of new legislation
 * Publishing audit trail data, e.g. audit of receipt, processing, transformation, publication of new legislation on [legislation.gov.uk](https://www.legislation.gov.uk/)
 * Website data, e.g. documents, versions and formats held in the main [legislation.gov.uk](https://www.legislation.gov.uk/) database
 * Effects data (records of amendments to legislation)
 * Enabling powers (the enabling acts for secondary legislation)
 * Subject classifications, e.g. Statutory Instrument subject headings, EU legislation subject categories
 * Metadata in the European Legislation Identifier (ELI) ontology

Please [contact us](../index.md#contact-us) if you want to request or suggest other legislation data that we could make available through the Linked Data service.

### Querying using SPARQL<a id="sparql"></a>

You can query the data in the Linked Data store directly through a [SPARQL endpoint](https://www.legislation.gov.uk/sparql), either with our in-browser query editor or connecting directly or using your own software. The endpoint is compliant with the SPARQL 1.1 Query Language specification. For more information on using SPARQL to query linked data, read the [specification for the SPARQL query language](https://www.w3.org/TR/sparql11-query/).

The SPARQL endpoint allows you to query all data available from the Linked Data service. For example, the following SPARQL query returns all the data units containing data about the Kew Gardens (Leases) Act 2019 (c. 25) and its interpretations, along with information about each of the provenance events that affected them:

```
PREFIX prov: <http://www.w3.org/ns/prov#>

SELECT DISTINCT ?dataunit ?prov ?provProperty ?provValue WHERE {
  VALUES ?item {
  <http://www.legislation.gov.uk/id/ukpga/2019/25>
  <http://www.legislation.gov.uk/ukpga/2019/25>
  <http://www.legislation.gov.uk/ukpga/2019/25/enacted>
  }

  GRAPH ?dataunit { 
  ?item ?p []
  }

  ?dataunit prov:wasInfluencedBy ?prov .
  ?prov ?provProperty ?provValue
}
ORDER BY ?dataunit ?prov ?provProperty</pre>
```

## Licence

For information on licensing and re-using our data, please see the [Licence](../reuse-licence.md) page.
