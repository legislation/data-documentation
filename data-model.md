# Our data model

<!--
What is a data model?
What do we represent in our data model?
How do I understand each of these things?
-->

## Introduction

Legislation.gov.uk provides many different kinds of data about different things. Our data model describes how the things relate to one another and how we represent information about them in our data.

The key concepts we represent in our data are:

 * **Items of legislation** and their **divisions**, which represent in abstract a particular law or part independently of its text or any version of it;
 * **Versions** of items of legislation and their divisions, which embody the text of an item or a given division as it stood at a particular point in time (and, for dual-language legislation, in a particular language);
 * **Effects** and **commencements**, where an item of legislation either changes or brings into force one or more provisions of legislation.

## URIs (Uniform Resource Identifiers)

We identify things in our data using URIs (short for "uniform resource identifier"). A URI is an identifier that looks like an address of a page or resource on a website. In many cases these URIs *are* functioning web addresses: we say that it is possible to **resolve** these URIs, which means that if you open the URI in a web browser or other suitable application, you can get a page or resource that represents the thing that the URI identifies.

The following are examples of legislation.gov.uk URIs:

 * `http://www.legislation.gov.uk/id/ukpga/1985/67` identifies the Transport Act 1985
 * `http://www.legislation.gov.uk/uksi/2013/376/regulation/12/2015-03-27` identifies regulation 12 of the Universal Credit Regulations 2013, as they stood on 27/3/2015
 * `http://www.legislation.gov.uk/anaw/2016/3/part/3/enacted/welsh/data.pdf` identifies the PDF manifestation of the Welsh enacted version of Part 3 of the Environment (Wales) Act 2016
 * `http://www.legislation.gov.uk/id/effect/key-f8ca0da7874670764680c0bcf1a72bbe` identifies an effect from article 59(9) of the Criminal Justice (Northern Ireland) Order 2008, substituting words in article 21(2) of the Road Traffic (Northern Ireland) Order 1995
 * `http://www.legislation.gov.uk/def/legislation/NorthernIrelandAct` identifies the legislation type “Act of the Northern Ireland Assembly”

A URI identifies the same item or resource across legislation.gov.uk. Whatever part of our data set you use, a given URI will always refer to the same thing.

All our URIs start with `http://www.legislation.gov.uk/` and follow a consistent **URI scheme**. You can find out more about the URIs for each type of data in the section for that type, and about the scheme in the [URI scheme reference]() section of the guide.

## Legislation documents

We publish UK legislation from 1267 onwards, as well as selected  legislation originating from the EU.

An item of legislation is an individually identifiable legal text passed by a legislature or governmental body. Legislation.gov.uk publishes many different types of new and historical legislation, although [we do not record or publish all UK legislation](). For each item of legislation that we record, we assign that item a URI that uniquely identifies it wherever it appears in our data.

### Structure of a legislation document

An item of legislation is a structured piece of text, consisting of a set of commonly used features. Some of these features separate the text into identifiable divisions, including (but not limited to):

 * preliminary text, which contains the title and number of the legislation, as well as other introductory information;
 * numbered paragraphs and sub-paragraphs;
 * headings (such as parts, chapters and cross-headings), with or without numbers;
 * schedules, appendices and attachments, which follow the main body of the text;
 * a signature, bearing the names of the officials who authorised the making of the legislation;
 * explanatory text, which appears at the end of the text and describe the purposes for which it was passed.

We assign each of these features a URI, so that it is possible to identify and link to them separately from the document as a whole.

For example:

 * `http://www.legislation.gov.uk/id/ukpga/2000/8/introduction` is the URI of the [preliminary text of the Financial Services and Markets Act 2000](http://www.legislation.gov.uk/id/ukpga/2000/8/introduction) (c. 8). 
 * `http://www.legislation.gov.uk/id/asc/2021/4/section/2` is the URI of [section 2 of the Curriculum and Assessment (Wales) Act 2021](http://www.legislation.gov.uk/id/asc/2021/4/section/2) (asc 4).
 * `http://www.legislation.gov.uk/id/asp/2019/17/part/2/chapter/2` is the URI of [Chapter 2 of Part 2 of the Transport (Scotland) Act 2019](http://www.legislation.gov.uk/id/asp/2019/17/part/2/chapter/2) (asp 17). 
 * `http://www.legislation.gov.uk/id/nia/2016/15/schedule/2` is the URI of [Schedule 2 of the Employment Act (Northern Ireland) 2016](http://www.legislation.gov.uk/id/nia/2016/15/schedule/2) (c. 15 (N.I.)).
 * `http://www.legislation.gov.uk/id/uksi/2013/376/note` is the URI of the [explanatory note for the Universal Credit Regulations 2013 ](http://www.legislation.gov.uk/id/uksi/2013/376/note).
 * `http://www.legislation.gov.uk/id/eur/2016/679/signature` is the signature of the [GDPR (General Data Protection Regulation)](http://www.legislation.gov.uk/id/eur/2016/679/signature). 

Each of these features may have one or more versions (see below).

### Versions

Each item of legislation has an original version (although we do not always hold its text), or two original versions for dual-language legislation in English and Welsh.

The original text of an item does not change once it is passed, except that for secondary legislation one of the following may occur:

 * the department or body who submitted the legislation may issue a [correction slip]() to correct errors that do not substantially change the meaning of the text; 
 * a court may partly or wholly [quash]() the item of legislation (declare it unlawful) if it determines that the government lacked the legal authority to make all or part of the legislation.

An item of legislation may have one or more revised versions. A revised version is a version of the item's text that shows the item as it applied at a particular point in time or in a particular legal jurisdiction within the UK. A revised version includes applicable amendments and/or other editorial commentary, such as information on which provisions are in force.

A section of an item of legislation also has one or more versions. Each version of a section is contained within a version of its parent item or section

Each revised version of an item or section of legislation may embody that item or section as it stood:

 * at a specific point in time;
 * in a particular geographical extent (one of the legal jurisdictions of the UK)
 * in one of the languages in which the item was or is published.

Where we hold the text for a version, we make it available in one or more formats (XML and the formats we generate from it, or a static PDF). 

We treat the item of legislation, its versions and the formats of those versions as separate (but related) things in separate categories.

#### FRBR (Functional Requirements for Bibliographic Records)

We use a variant of the [FRBR model](https://en.wikipedia.org/wiki/Functional_Requirements_for_Bibliographic_Records) to categorise our items, versions and formats. FRBR defines the concept of a “work” (an intellectual creation) separately from an “expression” (the realisation of a work, such as an edition of a book or an arrangement of a song) and a “manifestation” (the embodiment of an expression, such as a print or e-book version of an edition of a book, or a recording of an arrangement of a song). Under this model:

* a work is an abstract idea that is separate from the information any version of that work expresses;
* a version is an abstract idea that is separate from the representation of what any manifestation of that version expresses.

In our data model, we map the FRBR concepts onto the following legislation concepts:

* an item of legislation, or a division of it, is a **work**;
* an version of an item of legislation, or a division of it, is an **expression**;
* a representation of an interpretation of an item or a division in a specific file format is a **manifestation**.

#### Points in time

<!-- TODO Add URIs -->

Each newly published item (and each of its sections) has an enacted, made or created version that shows the text of the item as it was passed into law.

For items we have updated or intend to update, the item and its sections will also have one or more edited or revised versions, each at a dated point in time. 

The date of the first revised version for a item or section of legislation is normally the day the item or section first comes fully or partly into force, and contains extent and commencement information about the sections of the item in addition to their text. If any amendments apply to the item at or immediately before the time it comes into force, the first dated version will also contain those amendments. There will then be a subsequent dated version on each day on which an amendment or commencement comes into force.

For items of legislation published before our [base date]() of 1<sup>st</sup> February 1991, the first dated version will fall on that base date. This &ldquo;base date&rdquo; version will contain all amendments and commencements that applied as of the base date, as well as extent information.

#### Geographical extents

<!-- TODO Add URIs -->

An item or section may have different versions for different geographical extents at different points in time, because amendments to it only apply to some extents and not others. 

For example, an amendment may amend a provision only for England and Wales, even though the provision applies in England and Wales and Scotland, so at each point in time when the amendment is in force only in England and Wales, there are two versions of the provision and its parent item:

 * one version for England and Wales, where the amendment is in force, and 
 * one version for Scotland, where the amendment is not in force.

#### Languages

Many items of UK legislation are enacted or made in English and Welsh. These items and their sections have two enacted or made versions, with one version in each language.

For example, the URI for the enacted English version of Part 2 of the School Standards and Organisation (Wales) Act 2013 is:

`http://www.legislation.gov.uk/anaw/2013/1/part/2/enacted`

The corresponding URI for the enacted Welsh version of that Part 2 is:

`http://www.legislation.gov.uk/anaw/2013/1/part/2/enacted/welsh`

Currently, we do not hold revised versions of Welsh legislation. <!--TODO change when Welsh update is released-->

#### Quashing

When an item has been quashed (set aside by a court) it may be treated as though it was invalid from when it was made (a retrospective quashing), or alternatively on or after the date on which the court made the quashing order (a prospective quashing).

For example, the URI for the quashed interpretation of the Secure Training Centre (Amendment) Rules 2007 is:

`http://www.legislation.gov.uk/uksi/2007/1709/quashed`

We do not currently hold the text of quashed items of legislation on legislation.gov.uk, and so URIs for quashed versions of legislation do not yet resolve.

### Data formats

Each extant version of an item of legislation has at least one *manifestation*, which is a representation of that version in a digital format.

We represent the text of almost all digitally published and edited legislation as XML, in a bespoke XML dialect called Crown Legislation Markup Language (or CLML for short). 

We convert legislation to CLML when we ingest it in machine-readable formats from other sources, including new legislation from legislatures ([Parliament](https://www.parliament.uk/), the [Welsh Sennedd](https://www.senedd.cymru), the [Scottish Parliament]() or the [Northern Ireland Assembly]()) and government departments, as well as some legislation from historical sources. We then generate other formats from the CLML on demand, including the HTML views for our website, dynamically generated PDFs and other XML formats such as Akoma Ntoso (AKN).

The XML schema for Crown Legislation Markup Language describes the permitted structure of a valid CLML document. The schema is [available on our website](), along with [schema documentation]() that contains a guide to its use and a reference for the schema’s features. The [legislation document data]() section of this guide gives a basic explanation for how to interpret CLML.

We also store some legislation in its original enacted or made version as PDF, as well as some revised versions of legislation produced by third parties (for example, the Department for Work and Pensions used to produce revised versions of social security Acts and supplied them to legislation.gov.uk as PDF).

## Effects (amendments and commencements)

When an item of legislation makes a change to one or more provisions of legislation, our editors record the change in our Editorial system as an *effect*. An effect is a record of the change that helps our editors track where (and when) to apply amendments and commencements, and helps our readers and data re-users find changes to legislation both before and after we have applied them.

### Effect data

An effect contains information on:

* the type of amendment (such as “inserted”, “words substituted”, “repealed” or “modified”);
* the provision(s) or item of legislation to be amended;
* the amending provision(s);
* other information on when and how the amendment applies;
* the editorial activity relating to the amendment, including whether it has been applied;
* additional internal data the Editorial team uses to help guide editors in applying the amendment.

The effect does not contain the amending text, and nor does it contain machine-readable instructions on how to apply the amendment to the amended provision. (However, for some effects, we are able to partly or fully automate applying them. For example, our Editorial system supports one-click application of revocations of whole items, parts or provisions, and automatically applies "non-textual" amendments where only an annotation is applied to the text). 

The effect does link to the amending provision, which allows our editors to research how to apply any amendments, and our readers to consult it themselves.

### Effect URIs

An effect normally has a URI generated using a hash of the key fields in the effect (although some older effects use a different format). For example, the URI for the revocation of S.I. 2000/1408 by Schedule 1 of S.I. 2004/1315 is:

`http://www.legislation.gov.uk/id/effect/key-322c74ea5935adababe5cb5d4de686f6`

You can [view the data for this effect](http://www.legislation.gov.uk/changes/affected/uksi/2000/1408/affecting/uksi/2004/1315) on the legislation.gov.uk website, or as XML via the following API URI:

`http://www.legislation.gov.uk/changes/affected/uksi/2000/1408/affecting/uksi/2004/1315/data.feed`

### Application of effects

When one of our editors update an item of legislation, they use our Editorial system to create a new version of the item. The Editorial system instructs the editor which amendments to apply to the version, and the editor then amends the text of the version using these instructions and those contained in the amending provision of legislation from which the effect originates.

The Editorial system automatically adds [revision tags]() and [commentaries]() for the amendments that they apply. For recently applied amendments, both the revision tags and commentaries have identifiers that link them to the effect.

(Although most amendments are applied this way, some amendments either pre-date the current Editorial system or are applied manually. These have identifiers that do not correspond to an effect.)