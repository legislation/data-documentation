# Legislation document data model

We publish UK legislation from 1267 onwards, as well as selected legislation originating from the EU.

An item of legislation is an individually identifiable legal text passed by a legislature or governmental body. Legislation.gov.uk publishes many different types of new and historical legislation, although [we do not record or publish all UK legislation](../what-we-have.md).

For each item of legislation that we record, we assign that item a URI that uniquely identifies it. For example, the URI of the [Localism Act 2011](https://www.legislation.gov.uk/ukpga/2011/20/contents) (c. 20) is:

`http://www.legislation.gov.uk/id/ukpga/2011/20`

We use the same URI to identify an item of legislation across our whole dataset. We encourage you to use these URIs in your own data to uniquely identify items of UK legislation and retained EU origin legislation.

## Structure of a legislation document

An item of legislation is a structured piece of text, consisting of a set of commonly used features. Some of these features separate the text into identifiable divisions, including (but not limited to):

 * preliminary text, which contains the title and number of the legislation, as well as other introductory information;
 * numbered paragraphs and sub-paragraphs;
 * headings (such as parts, chapters and cross-headings), with or without numbers;
 * schedules, appendices and attachments, which follow the main body of the text;
 * a signature block, bearing the names of the officials who authorised the making of the legislation;
 * explanatory text, which appears at the end of the text and describe the purposes for which it was passed.

We assign each of these features a URI, so that it is possible to identify and link to them separately from the document as a whole.

For example:

 * `http://www.legislation.gov.uk/id/ukpga/2000/8/introduction` is the URI of the [preliminary text of the Financial Services and Markets Act 2000](http://www.legislation.gov.uk/id/ukpga/2000/8/introduction) (c. 8). 
 * `http://www.legislation.gov.uk/id/asc/2021/4/section/2` is the URI of [section 2 of the Curriculum and Assessment (Wales) Act 2021](http://www.legislation.gov.uk/id/asc/2021/4/section/2) (asc 4).
 * `http://www.legislation.gov.uk/id/asp/2019/17/part/2/chapter/2` is the URI of [Chapter 2 of Part 2 of the Transport (Scotland) Act 2019](http://www.legislation.gov.uk/id/asp/2019/17/part/2/chapter/2) (asp 17). 
 * `http://www.legislation.gov.uk/id/nia/2016/15/schedule/2` is the URI of [Schedule 2 of the Employment Act (Northern Ireland) 2016](http://www.legislation.gov.uk/id/nia/2016/15/schedule/2) (c. 15 (N.I.)).
 * `http://www.legislation.gov.uk/id/uksi/2013/376/note` is the URI of the [explanatory note for the Universal Credit Regulations 2013 ](http://www.legislation.gov.uk/id/uksi/2013/376/note).
 * `http://www.legislation.gov.uk/id/eur/2016/679/signature` is the URI of the signature block of the UK [GDPR (General Data Protection Regulation)](http://www.legislation.gov.uk/id/eur/2016/679/signature). 

Each of these features may have one or more versions (see below).

## Versions

Each item of legislation has an original version (although we do not always hold its text), or two original versions for dual-language legislation in English and Welsh.

The original text of an item does not change once it is passed, except that for secondary legislation one of the following may occur:

 * the department or body who submitted the legislation may issue a [correction slip](../glossary.md#correction-slip--corrigendum) to correct errors that do not substantially change the meaning of the text; 
 * a court may partly or wholly [quash](https://en.wikipedia.org/wiki/Judicial_review_in_English_law#Quashing_order) the item of legislation (declare it unlawful) if it determines that the government lacked the legal authority to make all or part of the legislation.

An item of legislation may have one or more revised versions. A revised version is a version of the item’s text that shows the item as it applied at a particular point in time or in a particular legal jurisdiction within the UK. A revised version includes applicable amendments and/or other editorial commentary, such as information on which provisions are in force.

A section of an item of legislation also has one or more versions. Each version of a section is contained within a version of its parent item or section

Each revised version of an item or section of legislation may embody that item or section as it stood:

 * at a specific point in time;
 * in a particular geographical extent (one of the legal jurisdictions of the UK)
 * in one of the languages in which the item was or is published.

Where we hold the text for a version, we make it available in one or more formats (either [CLML](../formats/xml.md) and the formats we generate from it, a static PDF, or both). 

We treat the item of legislation, its versions and the formats of those versions as separate (but related) things in separate categories.

### FRBR (Functional Requirements for Bibliographic Records)

We use a variant of the [FRBR model](https://en.wikipedia.org/wiki/Functional_Requirements_for_Bibliographic_Records) to categorise our items, versions and formats. FRBR defines the concept of a “work” (an intellectual creation) separately from an “expression” (the realisation of a work, such as an edition of a book or an arrangement of a song) and a “manifestation” (the embodiment of an expression, such as a print or e-book version of an edition of a book, or a recording of an arrangement of a song). Under this model:

* a work is an abstract idea that is separate from the information any version of that work expresses;
* a version is an abstract idea that is separate from the representation of what any manifestation of that version expresses.

In our data model, we map the FRBR concepts onto the following legislation concepts:

* an item of legislation, or a division of it, is a **work**;
* an version of an item of legislation, or a division of it, is an **expression**;
* a representation of an interpretation of an item or a division, provided in a specific file format, is a **manifestation**.

### Points in time

**Note that some items of legislation have revised versions available as static PDFs, which do not use the below URIs. For more information on these, see the [legislation PDFs](uris/reference.md#legislation-pdfs) section of the URI scheme reference.**

Each newly published item (and each of its sections) has an enacted, made or created version that shows the text of the item as it was passed into law.

For items we have updated (or are planning to update in the near future), the item and its sections will also have one or more edited or revised versions, each at a dated point in time. They will also have a “current” version (shown on the website as “latest available (revised)”) which contains the same text and annotations as the latest point in time version.

The date of the first revised version for a item or section of legislation is normally the day the item or section first comes fully or partly into force, and contains extent and commencement information about the sections of the item in addition to their text. If any amendments apply to the item at or immediately before the time it comes into force, the first dated version will also contain those amendments. There will then be a subsequent dated version on each day on which an amendment or commencement comes into force.

For items of legislation originally published before our [base date](glossary.md#basedate) of 1<sup>st</sup> February 1991 and whose first revised version was published before the 7<sup>th</sup> March 2019, the first revised version will normally fall on that base date. This “base date” version will contain all amendments and commencements that applied as of the base date, as well as extent information. Legislation that was first revised after the 7<sup>th</sup> March 2019 will have a first revised version for the first date on which the legislation came wholly or partly into force.

For example, the URI for the version dated 4<sup>th</sup> May 2022 of the Universal Credit Regulations is:

`http://www.legislation.gov.uk/uksi/2013/376/2022-05-04`

The URI for the version dated 4<sup>th</sup> May 2022 of Part 1 of those Regulations is:

`http://www.legislation.gov.uk/uksi/2013/376/part/1/2022-05-04`

The URI for the latest version of Part 1 of those Regulations (which at the time of writing was the same as the version dated 4<sup>th</sup> May 2022) is:

`http://www.legislation.gov.uk/uksi/2013/376/part/1`

### Geographical extents

An item or section may have different versions for different geographical extents at different points in time, because amendments to it only apply to some extents and not others. 

For example, an amendment may amend a provision only for England and Wales, even though the provision applies in England and Wales and Scotland, so at each point in time when the amendment is in force only in England and Wales, there are two versions of the provision and its parent item:

 * one version for England and Wales, where the amendment extends and is in force, and 
 * one version for Scotland, where the amendment does not extend.

For example, section 3 of the Dogs Act 1906 began to diverge between the legal jurisdiction of England and Wales and the jurisdiction of Scotland on the 1<sup>st</sup> April 1992. The URI for the version of section 3 of that Act as it was in force on that date in England and Wales is:

`http://www.legislation.gov.uk/ukpga/Edw7/6/32/section/3/england+wales/1992-04-01`

The URI for the version of section 3 of that Act as it was in force on that date in Scotland is:

`http://www.legislation.gov.uk/ukpga/Edw7/6/32/section/3/england+wales/1992-04-01`

Section 3 was repealed in England and Wales on the 6<sup>th</sup> April 2008, but is still in force in Scotland. The URI for the latest version of section 3 as it is in force in Scotland is:

`http://www.legislation.gov.uk/ukpga/Edw7/6/32/section/3/scotland`

The URI for the latest version of the section for both jurisdictions, which returns the text of both versions, is `http://www.legislation.gov.uk/ukpga/Edw7/6/32/section/3`.

### Languages

Many items of UK legislation are enacted or made in English and Welsh. These items and their sections have two enacted or made versions, with one version in each language.

For example, the URI for the enacted English version of Part 2 of the School Standards and Organisation (Wales) Act 2013 is:

`http://www.legislation.gov.uk/anaw/2013/1/part/2/enacted`

The corresponding URI for the enacted Welsh version of that Part 2 is:

`http://www.legislation.gov.uk/anaw/2013/1/part/2/enacted/welsh`

We also publish some revised Welsh legislation in both English and Welsh. For example, the URI for the English version dated 7<sup>th</sup> June 2021 of section 4 of the Renting Homes (Fees etc.) (Wales) Act 2019 is:

`https://www.legislation.gov.uk/anaw/2019/2/section/4/2021-06-07`

The corresponding URI for the Welsh version dated the 7<sup>th</sup> June 2021 of that section 4 is:

`https://www.legislation.gov.uk/anaw/2019/2/section/4/2021-06-07/welsh`

### Quashing

When an item has been quashed (set aside by a court) it may be treated as though it was invalid from when it was made (a retrospective quashing), or alternatively on or after the date on which the court made the quashing order (a prospective quashing).

For example, the URI for the quashed interpretation of the Secure Training Centre (Amendment) Rules 2007 is:

`http://www.legislation.gov.uk/uksi/2007/1709/quashed`

We do not currently hold the text of quashed items of legislation on legislation.gov.uk, and so URIs for quashed versions of legislation do not yet resolve.

## Data formats

Each extant version of an item of legislation has at least one *manifestation*, which is a representation of that version in a digital format.

We represent the text of almost all digitally published and edited legislation as XML, in a bespoke XML dialect called [Crown Legislation Markup Language](../formats/xml.md) (or CLML for short). 

We convert legislation to CLML when we ingest it in machine-readable formats from other sources, including new legislation from legislatures ([Parliament](https://www.parliament.uk/), the [Welsh Sennedd](https://www.senedd.cymru), the [Scottish Parliament](https://www.parliament.scot/) or the [Northern Ireland Assembly](http://www.niassembly.gov.uk/)) and government departments, as well as some legislation from historical sources. We then generate other formats from the CLML on demand, including the HTML views for our website, dynamically generated PDFs and other XML formats such as Akoma Ntoso (AKN).

The XML schema for Crown Legislation Markup Language describes the permitted structure of a valid CLML document. The schema is [available on our website](https://www.legislation.gov.uk/schema/legislation.xsd), along with [schema documentation](https://legislation.github.io/clml-schema/) that contains a guide to its use and a reference for the schema’s features. The [XML](../formats/xml.md) section of this guide gives a basic explanation for how to interpret CLML.

We also store some legislation in its original enacted or made version as PDF, as well as some revised versions of legislation produced by third parties. (For example, the Department for Work and Pensions used to produce revised versions of social security Acts and supplied them to us as PDF.)
