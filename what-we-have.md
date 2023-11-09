# What data we hold on legislation.gov.uk

## Overview

**We only hold a partial dataset of UK legislation texts and metadata**, although we are acquiring more data. This page explains what data we do and do not hold.<!-- TODO add in when origins text is ready For an explanation as to why we only hold some data, read our description of the [origins of our data](origins.md).-->

### Legislation texts

We hold the text of almost all UK primary and secondary legislation published since 1988, plus the text of some UK legislation published before that date.

Of the legislation we hold published since 1988, we hold most of it in a machine-readable format called [XML](formats/xml.md). All legislation held in XML format is available as HTML web pages and [dynamically generated PDF files](formats/pdf.md#dynamically-generated-pdfs), and is also available for full-text search. We also hold revised XML versions of most UK Public General Acts enacted before 1988, as these were rekeyed from the [Statutes in Force](glossary.md#statutes-in-force) volumes.

Most UK legislation we hold that was enacted or made before 1988 is currently only available as PDF.

We do not hold text of any of the following types of legislation, although we do hold [metadata](api/sparql.md) for them:

 * Letters Patent
 * Royal Charters
 * Royal Instructions
 * Royal Proclamations

We do hold some legislation originating from the EU, to fulfil our obligations under [Schedule 5 of the European Union (Withdrawal) Act 2018](http://www.legislation.gov.uk/id/ukpga/2018/16/schedule/5). The EU origin legislation we hold is:

 * All EU legislation classified as “legal acts” in the EUR-Lex database (sector 3), plus their consolidated versions (sector 0) and any [corrigenda](glossary.md#correction-slip--corrigendum)
 * the following EU treaties, both the “Official Journal” version and any consolidated versions:
    + the Treaty on European Union,
    + the Treaty on the Functioning of the European Union,
    + the Euratom Treaty, and
    + the EEA agreement

The [EU Exit Web Archive](https://webarchive.nationalarchives.gov.uk/eu-exit) holds many other EU documents not published on legislation.gov.uk.

### Changes to legislation

We normally only record amendments _from_ amending documents enacted or made in 1994 onwards. There are some notable exceptions:

 * We have recorded some amendments from “EU implementing” secondary legislation made from 1972 onwards.
 * We have uploaded all amendments by EU documents on other EU documents, which date from 1953, the first year from which legislation was enacted by the European Communities.

There are some types of legislation for which we do not record either changes made by them, changes made to them, or either.

## Details of data held (by legislation category and type)

### Primary legislation (current types)

|Legislation type|Which documents do we have?|Are we updating these items?|Do we record amendments made _by_ these items?|Do we record amendments made _to_ these items?|
|---|---|---|---|---|
|UK Public General Acts (1801–)|{::nomarkdown}<p>All UK Public General Acts from 1988 onwards</p><p>Some UK Public General Acts from before 1988—mostly those still in force as of 1 February 1991 (the [base date](glossary.md#base-date))</p>{:/}|Yes, although not older UK Public General Acts only available as King’s Printer PDF|Yes, but normally only for UK Public General Acts enacted in 1994 onwards|Yes|
|UK Local Acts (1801–)|{::nomarkdown}<p>All UK Local Acts from 1991 onwards</p><p>Some UK Public General Acts from before 1991—mostly only available as King’s Printer PDF</p>{:/}|Yes, although not older UK Local Acts only available as King’s Printer PDF|Yes, but  only for UK Local Acts enacted in 1994 onwards|Yes|
|Measures and Acts of the National Assembly for Wales (2008–2020), Acts of Senedd Cymru (2020–)|All Welsh primary legislation|Yes, but only in English|Yes|Yes|
|Acts of the Scottish Parliament (1999–)|All Acts of the Scottish Parliament|Yes|Yes|Yes|
|Acts of the Northern Ireland Assembly (2000–)|All Acts of the Northern Ireland Assembly|Yes|Yes|Yes|
|Northern Ireland Orders in Council (1972–)|{::nomarkdown}<p>All Northern Ireland Orders in Council from 1987 onwards</p><p>Some Northern Ireland Orders in Council from before 1987—mostly those still in force as of 1 January 2006 (the [NI base date](glossary.md#base-date))</p>{:/}|Yes, although not older Northern Ireland Orders in Council only available as King’s Printer PDF|Yes, but normally only for Northern Ireland Orders in Council made in 1994 onwards|Yes|
|UK Church Measures (1920–)|{::nomarkdown}<p>All UK Church Measures from 1988 onwards, as XML and King’s Printer PDFs</p><p>Some UK Church Measures from before 1988</p>{:/}|Yes|Yes, but only for UK Church Measures enacted in 1994 onwards|Yes|

### Secondary legislation (current types)

<!--TODO: find out what associated documents are / are not present-->

|Legislation type|Which documents do we have?|Are we updating these items?|Do we record amendments made _by_ these items?|Do we record amendments made _to_ these items?|
|---|---|---|---|---|
|UK Statutory Instruments (1948–)|{::nomarkdown}<p>All UK Statutory Instruments since 1987, except for Local Statutory Instruments and non-prints (all except Local and non-prints available as XML, most available as King’s Printer PDF)</p><p>All Local and non-print UK Statutory Instruments since 2011 (only available as King’s Printer PDFs)</p>{:/}|Yes, but only where available as XML|Yes, but normally only for UK Statutory Instruments made in 1994 onwards, plus selected UK Statutory Instruments made between 1972 and 1993|Yes|
|Welsh Statutory Instruments (1999–)|{::nomarkdown}<p>All Welsh Statutory Instruments, except for Local Statutory Instruments and non-prints (all except Local and non-prints available as XML, most available as King’s Printer PDF)</p><p>All Local and non-print Welsh Statutory Instruments since 2011 (only available as King’s Printer PDFs)</p>{:/}|Yes, but only in English and where available as XML|Yes|Yes|
|Scottish Statutory Instruments (1999–)|{::nomarkdown}<p>All Scottish Statutory Instruments, except for Local Statutory Instruments and non-prints (all except Local and non-prints available as XML, most available as King’s Printer PDF)</p><p>All Local and non-print Scottish Statutory Instruments since 2007 (only available as King’s Printer PDFs)</p>{:/}|Yes, but only where available as XML|Yes|Yes|
|Northern Ireland Statutory Rules (1974–)|{::nomarkdown}<p>All Northern Ireland Statutory Rules since 1996, except for Local Statutory Instruments and non-prints (all except Local and non-prints available as XML, most available as King’s Printer PDF)</p><p>All Local and non-print Northern Ireland Statutory Rules since 2011 (only available as King’s Printer PDFs)</p>{:/}|Yes, but only where available as XML|Yes, but only for Northern Ireland Statutory Rules made from 1994 onwards|Yes|
|UK Ministerial Directions (2023–)|All UK Ministerial Directions from 2023 onwards (only available as King’s Printer PDFs)|No|Yes|Yes|
|UK Ministerial Orders (1953–)|All UK Ministerial Orders from 2013 onwards (only available as King’s Printer PDFs)|No|No|No|

### Historical legislation types

#### Primary

|Legislation type|Which documents do we have?|Are we updating these items?|Do we record amendments made _by_ these items?|Do we record amendments made _to_ these items?|
|---|---|---|---|---|
|Acts of the Parliament of Northern Ireland (1921–1972)|Some Acts of the Parliament of Northern Ireland from 1921 onwards|Yes|No|Yes|
|Measures of the Northern Ireland Assembly (1974)|Some Measures of the Northern Ireland Assembly (available as revised XML only)|Yes|No|No|
|UK Private and Personal Acts (1801–1987)|{::nomarkdown}<p>All UK Private and Personal Acts from 1946 onwards</p><p>Some UK Private and Personal Acts from before 1946</p><p>(All only available as King’s Printer PDF)</p>{:/}|No|No|No|
|Acts of the Parliament of Great Britain (1707–1800)|Some Acts of the Parliament of Great Britain from 1707 onwards—available either as XML or as scanned PDF, depending on whether the Act was present in [Statutes in Force](glossary.md#statutes-in-force)|Yes, but only where available as XML|No|Yes|
|Local Acts of the Parliament of Great Britain (1797–1800)|{::nomarkdown}<p>All Local Acts of the Parliament of Great Britain enacted from 1797 to 1799 (only available as King’s Printer PDF)</p><p>Some Local Acts of the Parliament of Great Britain enacted in 1800 (only available as King’s Printer PDF)</p>{:/}|No|No|No|
|Acts of the English Parliament (1235–1706)|Some Acts of the English Parliament from 1267 onwards—available either as XML or as scanned PDF, depending on whether the Act was present in [Statutes in Force](glossary.md#statutes-in-force)|Yes, but only where available as XML|No|Yes|
|Acts of the Old Scottish Parliament (1424–1707)|Some Acts of the Old Scottish Parliament from 1424, only available as revised XML (rekeyed from [Statutes in Force](glossary.md#statutes-in-force))|Yes|No|Yes|
|Acts of the Old Irish Parliament (1495–1800)|Some Acts of the Old Irish Parliament from 1495, only available as revised XML (rekeyed from [Statutes in Force](glossary.md#statutes-in-force))|Yes|No|Yes|

#### Secondary

|Legislation type|Which documents do we have?|Are we updating these items?|Do we record amendments made _by_ these items?|Do we record amendments made _to_ these items?|
|---|---|---|---|---|
|UK Statutory Rules and Orders (1894–1947)|{::nomarkdown}<p>Some UK Statutory Orders from 1894 onwards, as King’s Printer PDFs only</p><p>(The UK SR&O series only officially began in 1894, but currently we publish some older instruments in that category as well)</p>{:/}|No|No|Yes|
|Northern Ireland Statutory Rules and Orders (1922–1973)|Some Northern Ireland Statutory Rules and Orders from 1922 onwards, as King’s Printer PDFs only|No|No|Yes|
|UK Church Instruments (1991–2016)|All UK Church Instruments, as XML only (no King’s Printer PDF versions)|No|Yes, but only for UK Church Instruments created in 1994 onwards|No|

#### Legislation originating from the EU

|Legislation type|Which documents do we have?|Are we updating these items?|Do we record amendments made _by_ these items?|Do we record amendments made _to_ these items?|
|---|---|---|---|---|
|All Regulations, Decisions and Directives in [sector 3](https://eur-lex.europa.eu/content/tools/TableOfSectors/types_of_documents_in_eurlex.html), plus their consolidated versions and any [corrigenda](glossary.md#correction-slip--corrigendum)|Almost all EU documents adopted from 2004 onwards are available as XML and original PDFs. Most EU documents adopted before 2004 are only available as original PDF, except for a small number that have consolidated versions in XML|We are applying domestic “EU Exit” amendments to these documents only—as of the end of the implementation period no further EU amendments apply|Yes, all known amendments from the EU origin documents we hold have been recorded|Yes, but only for domestic “EU Exit” amendments and any EU amendments made before the end of the implementation period|

## Limitations

<!-- TODO: Re-add when history is ready As shown in the History of our Data Collection and Data Completeness sections, the --> Our database is both large and complex, with more than 300,000 items of legislation from data collections deriving from different sources. As a result, the content held within the database has some limitations.

### Missing legislation

#### Primary legislation

The text of the Statute Law Database, from which much of our revised primary legislation originates, was derived from two earlier official hardcopy editions of revised primary legislation, Statutes in Force (SIF) and The Northern Ireland Statutes Revised (NISR). The final text of SIF was revised to 1<sup>st</sup> February 1991, and that of NISR to 1<sup>st</sup> January 2006. These dates form the basedates for SLD legislation, which means the dates from which revision work has been taken forward.

As a result, we do not have XML for all UK primary legislation that was not at least partially in force on or after the basedate of 1<sup>st</sup> February 1991. For Northern Ireland, we do not have XML for all primary legislation that was not at least partially in force on or after the basedate of 1<sup>st</sup> January 2006.

#### Secondary legislation

We have acquired secondary legislation from various sources, many of which are not complete. Consequently, we do not have complete sets of the following secondary legislation:

 * Statutory instruments of a local character made before 1987 (or Northern Ireland statutory rules of a local character made before 1996);
 * Statutory instruments made before 2012 that were not printed (usually temporary legislation).

### Revised legislation

Not all legislation on the website is up to date. Typically, over 95% of all primary legislation on the website is up to date, and over 85% of the top 5,000 documents (including secondary legislation) are up to date. These figures fluctuate as Parliament and ministers regularly enact new amendments to legislation.

Until 7<sup>th</sup> March 2019, the initial revised version of all legislation either came from the original Statutes In Force/Northern Ireland Statutes Revised datasets or was produced using the legacy Statute Law Database editorial system. As a result, no version history is available prior to the base date of 1<sup>st</sup> February 1991 (or 1<sup>st</sup> January 2006 for Northern Ireland legislation) for legislation initially revised before 7<sup>th</sup> March 2019.

If you view a revised version that is not up to date, you will see a red “Changes to Legislation” banner that will explain which amendments are yet to be applied. You can also find unapplied amendments on the [changes to legislation](https://www.legislation.gov.uk/changes) search page and in the `<ukm:UnappliedEffects>` element in the [XML](formats/xml.md) representation of a revised item or section of legislation. 

### Formats

Not all documents are available in all formats. For instance, some documents are only available in PDF format, or do not have a printed PDF format available. For more information on the formats available on the website and how to access them, see the [formats](formats/overview.md) section.

### No ALT text

Images within documents (including diagrams, forms and mathematical formulae) do not currently have descriptive ALT text.

### Errors in historical data

Completeness and accuracy of the data of documents from before the base date cannot be guaranteed, as documents may have been rekeyed or OCRed and may therefore contain errors.

## Data updates

New legislation is published on legislation.gov.uk at the same time as it is printed, which happens as quickly as possible once we are authorised to publish it. This generally occurs within 48 hours of the legislation being enacted, made or laid. Newly published legislation appears on the New Legislation page and feeds on legislation.gov.uk. 

Any document which is especially complex in terms of its size or its typography may take longer to prepare. Sometimes, we publish PDFs for some items of new legislation before XML is available, and then upload the XML later. 

We sometimes alter legislation data after we first publish it. This can occur in a few scenarios: a formal correction of the legislation (e.g. a correction slip); the correction of data versions to better represent the official PDF version; or a reprint/reissue of the relevant legislation item.

It is possible to subscribe to the legislation feeds to get details of the latest legislation as soon as it is published without having to check the new legislation page each day. You can find more details about this service by reading the New Legislation page. <!--TI 15/9/22: Do we need to explain here how to subscribe to the feed, considering that many users do not seem to understand how it works? Or should we just improve the guide on the New Legislation page? -->

For revised legislation, information about effects are extracted and added to the Changes to Legislation page as quickly as we can, although it can take up to six weeks if the document is large or if there is a high volume of new legislation (for more information see Our editorial practice and timescales). 

If you are interested in knowing when a document has last changed, it is possible to check this information by opening the XML format of the document and looking at the dc:modified value. To know how to access the XML format of a document, as well as other formats, see the [Formats](formats/overview.md) section of this documentation.

Usually, documents (either enacted or revised) are not removed from legislation.gov.uk except in rare cases with agreement of the originating department where the item was not valid law, e.g. if it was published because of administrative error or if a court judgment has ruled that it was invalid. If data are missing from legislation.gov.uk then this is usually because we do not yet hold it.
