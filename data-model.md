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

We identify things in our data using URIs (short for "uniform resource identifier"). A URI is an identifier that looks like an address of a page or resource on a website. In some cases these URIs *are* working web addresses: we say that it is possible to **resolve** these URIs, which means that if you open the URI in a web browser or other suitable application, you can get a page or resource that represents the thing that the URI identifies.

The following are examples of legislation.gov.uk URIs:

 * `http://www.legislation.gov.uk/id/ukpga/1985/67` identifies the Transport Act 1985
 * `http://www.legislation.gov.uk/uksi/2013/376/regulation/12/2015-03-27` identifies regulation 12 of the Universal Credit Regulations 2013, as they stood on 27/3/2015
 * `http://www.legislation.gov.uk/anaw/2016/3/part/3/enacted/welsh/data.pdf` identifies the PDF manifestation of the Welsh enacted version of Part 3 of the Environment (Wales) Act 2016
 * `http://www.legislation.gov.uk/id/effect/key-f8ca0da7874670764680c0bcf1a72bbe` identifies an effect from article 59(9) of the Criminal Justice (Northern Ireland) Order 2008, substituting words in article 21(2) of the Road Traffic (Northern Ireland) Order 1995
 * `http://www.legislation.gov.uk/def/legislation/NorthernIrelandAct` identifies the legislation type “Act of the Northern Ireland Assembly”

A URI identifies the same item or resource across legislation.gov.uk. Whatever part of our data set you use, a given URI will always refer to the same thing.

All our URIs start with `http://www.legislation.gov.uk/` and follow a consistent **URI scheme**. You can find out more about the URIs for each type of data in the section for that type, and about the scheme in the [URI scheme reference]() section of the guide.

## Legislation documents

We publish UK legislation from 1267 onwards, as well as selected EU legislation.

An item of legislation is an individually identifiable legal text passed by a legislature or governmental body. Legislation.gov.uk publishes many different types of new and historical legislation, although [we do not record or publish all UK legislation](). For each item of legislation that we record, we assign that item a URI that uniquely identifies it wherever it appears in our data.

Each item of legislation has an original version (although we do not always hold its text), or two original versions for dual-language legislation in English and Welsh. The original text of an item does not change,

An item of legislation has at least two versions:

 * An original version, or two original versions for dual-language legislation (one in English and one in Welsh). The text of the original version(s) does not change once it is passed, except that for secondary legislation the department or body who submitted the legislation may issue a correction slip to correct errors that do not substantially change the meaning of the text.
 * One or more revised versions. <!-- todo explain what a revised version is. should probably split these explanations out into separate paras but keep the bullet list to help structure -->

Where we hold the text for a version, we make it available in one or more formats (XML and the formats we generate from it, or a static PDF). 

We treat the item of legislation, its versions and the formats of those versions as separate (but related) things in separate categories.

### FRBR (Functional Requirements for Bibliographic Records)

We use a variant of the [FRBR model](https://en.wikipedia.org/wiki/Functional_Requirements_for_Bibliographic_Records) to categorise our items, versions and formats. FRBR defines the concept of a “work” (an intellectual creation) separately from an “expression” (the realisation of a work, such as an edition of a book or an arrangement of a song) and a “manifestation” (the embodiment of an expression, such as a print or e-book version of an edition of a book, or a recording of an arrangement of a song). Under this model:

* a work is an abstract idea that is separate from the information any version of that work expresses;
* a version is an abstract idea that is separate from the representation of what the version expresses by any manifestation of that version.

In our data model, we map the FRBR concepts onto the following legislation concepts:

* an item of legislation, or a division of it, is a **work**;
* an version of an item of legislation, or a division of it, is an **expression**;
* a representation of an interpretation of an item or a division in a specific file format is a **manifestation**.

We describe items, versions and representations in more detail below.

### Document data formats

We represent the text of digitally published and edited legislation as XML, in a bespoke XML dialect called Crown Legislation Markup Language (or CLML for short). We convert legislation to CLML when we ingest it in machine-readable formats from other sources, including new legislation from Parliament, government departments and the devolved legislatures, as well as legislation from historical sources. We then generate other formats from the CLML on demand, including the HTML views for our website, dynamically generated PDFs and other XML formats such as Akoma Ntoso (AKN).

The XML schema for Crown Legislation Markup Language describes the permitted structure of a valid CLML document. The schema is [available on our website](), along with [schema documentation]() that contains a guide to its use and a reference for the schema’s features. The [legislation document data]() section of this guide gives a basic explanation for how to interpret CLML.

We also store some legislation in its original enacted or made version as PDF, as well as some revised versions of legislation produced by third parties (for example, the Department for Work and Pensions used to produce revised versions of social security Acts and supplied them to legislation.gov.uk as PDF).