# Formats

This page describes the formats that are currently available within Legislation API. Although only a few formats are available at the moment, we intend to make legislation content including metadata and the results of searches, available in a variety of different formats so that you can pick one that suits your needs. The available formats, their mime type and the filename used within the [representation URI](uris.md#representations) for the document are listed in the following table.

|Format|Mime Type|Filename|
|---|---|---|
|[XML](/developer/formats#xml)|`application/xml` or `text/xml`|`data.xml`|
|[HTML](/developer/formats#html)|`application/xhtml+xml`|`data.rdf`|
|[RDF/XML](/developer/formats#rdf)|`application/rdf+xml`|`data.rdf`|
|[Atom](/developer/formats#atom)|`application/atom+xml`|`data.feed`|

## XML

We provide the content of legislation in XML format using a [Legislation Schema](/schema/legislation.xsd) that includes both metadata and the content of legislation. The Legislation Schema uses [Dublin Core](http://dublincore.org/documents/dces/) for metadata, [XHTML](http://www.w3.org/TR/xhtml1/) for tables and [MathML](http://www.w3.org/Math/) for formulae.

Both the table of contents and the full content of the legislation includes links to other parts of the legislation. The `IdURI` attribute provides the [identifier URI](/developer/uris#identifiers) for the section. This URI identifies the section, but not the particular version that should be linked to from the view of the legislation that you are looking at. The `DocumentURI` attribute provides the [document URI](/developer/uris#documents) for the section, which includes any selected extent and the currently viewed version.

[Read more...](/developer/formats/xml)

## HTML

We provide the content of sections and tables of contents in a ready-transformed HTML format that is suitable for embedding within a web page. **These HTML snippets are only available through their [representation URI](/developer/uris#representations) and not through content negotiation.**

[Read more...](/developer/formats/html)

## RDF/XML

We are publishing RDF about the legislation that is provided here using the vocabularies:

|Vocabulary|Prefix|Namespace|
|---|---|---|
|[RDF Schema](http://www.w3.org/TR/rdf-schema/)|`rdfs`|`http://www.w3.org/2000/01/rdf-schema#`|
|[OWL](http://www.w3.org/TR/owl-features/)|`owl`|`http://www.w3.org/2002/07/owl#`|
|[Dublin Core Terms](http://dublincore.org/documents/dcmi-terms/)|`dct`|`http://purl.org/dc/terms/`|
|[FOAF](http://xmlns.com/foaf/spec/)|`foaf`|`http://xmlns.com/foaf/0.1/`|
|[XHTML Vocabulary](http://www.w3.org/1999/xhtml/vocab/)|`xhv`|`http://www.w3.org/1999/xhtml/vocab#`|
|[FRBR](http://vocab.org/frbr/core.html)|`frbr`|`http://purl.org/vocab/frbr/core#`|
|[Metalex](http://www.metalex.eu/)|`metalex`|`http://purl.org/vocab/frbr/core#`|

We are using these vocabularies because they will provide high recognition and ability for reuse without developers having to understand a specific legislation ontology. We do intend to use a specific legislation ontology in addition.

[Read more...](/developer/formats/rdf)

## Atom Feeds

We provide [lists](/developer/searching#listing) of legislation in [Atom](http://tools.ietf.org/html/rfc4287).

[Read more...](/developer/formats/atom)