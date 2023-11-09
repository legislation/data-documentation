# Formats

The Legislation API currently offers legislation in the following formats:

|Format|MIME Type|Filename|
|---|---|---|
|Crown Legislation Markup Language (CLML)|`application/xml`|`data.xml`|
|Akoma Ntoso (AKN)|`application/xml`|`data.akn`|
|HTML|`application/xhtml+xml`|`data.htm` or `data.xht`|
|HTML5|`text/html`|`data.html`|
|PDF|`application/pdf`|`data.pdf`|
|Atom (for feeds only)|`application/atom+xml`|`data.feed`|

## XML

We provide the content of legislation in two XML formats: 

* Crown Legislation Markup Language (or CLML), a format that uses our [Legislation Schema](https://www.legislation.gov.uk/schema/legislation.xsd) to represent UK legislation and legislation originating from the EU.
* [Akoma Ntoso](http://www.akomantoso.org/) (or AKN), a general-purpose format for representing parliamentary, legislative and judiciary documents, with some extensions to support the representation of UK and EU origin legislation.

[Read more about XML formats](xml.md).

## HTML

Where an item of legislation is available as XML, we provide its content in two HTML formats designed for reuse in other applications:

 * XHTML, which is an embeddable “snippet” form of the same HTML we use on the website for legislation content;
 * HTML5, which comes as complete HTML files with linked styles suitable for standalone display.

[Read more about HTML formats](html.md).

## PDF

We provide the following types of document as PDF:

 * dynamically generated PDFs of legislation available as XML;
 * static PDFs of legislation as enacted, made, created or adopted;
 * static PDFs of certain revised legislation, such as DWP legislation and legislation originating from the EU;
 * static PDFs of associated documents such as Impact Assessments and Correction slips.

[Read more about PDF formats](pdf.md).

## Atom

We provide lists of, and search results for, both [legislation](/api/search.md#listings) and [effects](/api/search.md#changes) in [Atom](http://tools.ietf.org/html/rfc4287).

[Read more about Atom feeds](atom.md).
