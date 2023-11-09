# URI schema reference

This page describes the URI scheme that is used on the Legislation API. The Legislation API attempts to follow the guidance given in [Linked Data: Evolving the Web into a Global Data Space](http://linkeddatabook.com/editions/1.0/#htoc10).

## Legislation

**The best way of finding out the URI for a particular piece of legislation is to [search](../api/search.md) for it. A search on the title of a piece of legislation will redirect you to the proper URI for that item of legislation without you having to construct the URI yourself.**

We define three levels of URIs for legislation:

*   [identifier URIs](#identifier-uris); for example, “The Transport Act 1985”, `http://www.legislation.gov.uk/id/ukpga/1985/67`
*   [document URIs](#document-uris); for example, “The current version of The Transport Act 1985” (as opposed to a previous version), `http://www.legislation.gov.uk/ukpga/1985/67`
*   [representation URIs](#representation-uris); for example, “The current version of The Transport Act 1985 in XML” (as opposed to an HTML document), `http://www.legislation.gov.uk/ukpga/1985/67/data.xml`

When you request an identifier URI, the response will usually be a `303 See Other` redirection to a document URI. When you request a document URI, you will usually get a `200 OK` response and a `Content-Location` header that will point to an appropriate representation URI based on the `Accept` headers that you use in the request.

### Identifier URIs

**We recommend that you link to identifier URIs.**

Identifier URIs generally follow the template:

<code>http://www.legislation.gov.uk/id/{<a href="#legislation-types">type</a>}/{<a href="#legislation-years">year</a>}/{<a href="#legislation-numbers">number</a>}[/{<a href="#legislation-sections">section</a>}]</code>

However, legislation is often quoted without a chapter number, which can make it hard to automatically construct these URIs. If you don’t know the chapter number for a piece of legislation, you can use a search URI of the form:

`http://www.legislation.gov.uk/id?title={title}`

If the title is recognised, this will result in a `301 Moved Permanently` redirection to the canonical URI for the legislation. For example, requesting:

`http://www.legislation.gov.uk/id?title=The%20Transport%20Act%201985`

will result in a `301 Moved Permanently` redirection to

`http://www.legislation.gov.uk/id/ukpga/1985/67`

On occasion, items of legislation have very similar titles, and the title search will result in multiple possibilities. In this case, the response will be a `303 Multiple Choices` containing a simple XHTML document. For example, requesting

`http://www.legislation.gov.uk/id?title=Disability%20Rights%20Commission%20Act`

will result in a document containing

```
<ul>
  <li><a href="/id/uksi/2006/3189">The Disability Rights Commission Act 1999 (Commencement No.3) Order 2006</a></li>
  <li><a href="/id/uksi/2000/880">The Disability Rights Commission Act 1999 (Commencement No. 2 and Transitional Provision) Order 2000</a></li>
  <li><a href="/id/uksi/1999/2210">The Disability Rights Commission Act 1999 (Commencement No. 1 and Transitional Provision) Order 1999</a></li>
  <li><a href="/id/uksi/1999/17">Disability Rights Commission Act 1999</a></li>
</ul>
```

#### Legislation types

The legislation type codes used in the API are as follows:

|Description|Document Main Type|URI abbreviation|
|---|---|---|
| **Primary Legislation** |||
|UK Public General Acts|`UnitedKingdomPublicGeneralAct`|`ukpga`|
|UK Local Acts|`UnitedKingdomLocalAct`|`ukla`|
|UK Private and Personal Acts|`UnitedKingdomPrivateOrPersonalAct`|`ukppa`|
|Local Acts of the Parliament of Great Britain (1797-1800)|`GreatBritainLocalAct`|`gbla`|
|Acts of the Parliament of Great Britain (1707-1800)|`GreatBritainAct`|`apgb`|
|Private and Personal Acts of the Parliament of Great Britain (1707-1800)|`GreatBritainPrivateOrPersonalAct`|`gbppa`|
|Acts of the English Parliament (1267-1706)|`EnglandAct`|`aep`|
|Acts of the Old Scottish Parliament (1424-1707)|`ScottishOldAct`|`aosp`|
|Acts of the Scottish Parliament|`ScottishAct`|`asp`|
|Acts of the Old Irish Parliament (1495-1800)|`IrelandAct`|`aip`|
|Acts of the Northern Ireland Parliament (1921-1972)|`NorthernIrelandParliamentAct`|`apni`|
|Measures of the Northern Ireland Assembly (1974)|`NorthernIrelandAssemblyMeasure`|`mnia`|
|Acts of the Northern Ireland Assembly|`NorthernIrelandAct`|`nia`|
|UK Church Measures|`UnitedKingdomChurchMeasure`|`ukcm`|
|Measures of the Welsh Assembly|`WelshAssemblyMeasure`|`mwa`|
|Acts of the Welsh Assembly|`WelshNationalAssemblyAct`|`anaw`|
|Acts of Senedd Cymru|`WelshParliamentAct`|`asc`|
| **Secondary Legislation** |||
|UK Statutory Instruments|`UnitedKingdomStatutoryInstrument`|`uksi`|
|Scottish Statutory Instruments|`ScottishStatutoryInstrument`|`ssi`|
|Wales Statutory Instruments|`WelshStatutoryInstrument`|`wsi`|
|Northern Ireland Statutory Rules|`NorthernIrelandStatutoryRule`|`nisr`|
|UK Church Instruments|`UnitedKingdomChurchInstrument`|`ukci`|
|Northern Ireland Orders in Council|`NorthernIrelandOrderInCouncil`|`nisi`|
|UK Ministerial Orders|`UnitedKingdomMinisterialOrder`|`ukmo`|
|Northern Ireland Statutory Rules and Orders|`NorthernIrelandStatutoryRuleOrOrder`|`nisro`|
| **Draft Legislation** |||
|UK Draft Statutory Instruments|`UnitedKingdomDraftStatutoryInstrument`|`ukdsi`|
|Scottish Draft Statutory Instruments|`ScottishDraftStatutoryInstrument`|`sdsi`|
|Northern Ireland Statutory Rules|`NorthernIrelandDraftStatutoryRule`|`nidsr`|
|Northern Ireland Draft Orders in Council|`NorthernIrelandDraftOrderInCouncil`|`nidsi`|
|Welsh Draft Statutory Instruments|`WelshDraftStatutoryInstrument`|`wdsi`|

Wales Statutory Instruments and Northern Ireland Orders in Council follow the same numbering sequence as UK Statutory Instruments, and can therefore be legitimately referred to through a URI using either `wsi`/`nisi` or `uksi`. In these cases, the `wsi` or `nisi` URI is the canonical one. For example, a request to

`http://www.legislation.gov.uk/id/uksi/2002/808`

will result in a `301 Moved Permanently` response with a `Location` header pointing to

`http://www.legislation.gov.uk/id/wsi/2002/808`

#### Legislation years

The legislation year can be a calendar year or a [regnal year](http://en.wikipedia.org/wiki/Regnal_year). For primary legislation, calendar years can be used for legislation enacted after 1963, but before that time legislation is unambiguously identified based on the year of reign of the monarch. (The only exception to this is Acts of the Old Scottish Parliament, which are all identified by calendar year.)

For example:

`http://www.legislation.gov.uk/id/ukpga/1985/67`

identifies The Transport Act 1986 (c. 67), and:

`http://www.legislation.gov.uk/id/ukpga/Edw7/7/51`

identifies the Sheriff Courts (Scotland) Act 1907 (c. 51). If you use a calendar year prior to 1963 within a URI, you will be redirected to the canonical identifier, which uses the regnal year. For example, requesting:

`http://www.legislation.gov.uk/id/ukpga/1907/51`

will result in a `301 Moved Permanently` response with a `Location` header pointing to

`http://www.legislation.gov.uk/id/ukpga/Edw7/7/51`

On a few occasions, a pre-1963 calendar year in a URI does not uniquely identify a particular piece of legislation. For example:

`http://www.legislation.gov.uk/id/ukpga/1955/19`

Could refer to the Friendly Societies Act 1955 (c.19) or the Air Force Act 1955 (c.19). These items of legislation have different regnal years, but the same calendar years. The above request will result in a `300 Multiple Choices` response, and the result will be XHTML that includes:

```
<ul>
  <li><a href="/id/ukpga/Eliz2/3-4/19">Air Force Act 1955</a></li>
  <li><a href="/id/ukpga/Eliz2/4-5/19">Friendly Societies Act 1955</a></li>
</ul>
```

#### Legislation numbers

The legislation number is an integer that reflects the legislation’s chapter or other series number according to the primary numbering sequence for the type. For example:

 * the Financial Services and Markets Act 2000 has the chapter number 8, and so its URI is [http://www.legislation.gov.uk/id/ukpga/2000/8]](http://www.legislation.gov.uk/id/ukpga/2000/8);
 * the Universal Credit Regulations 2013 has the number 376 in the UK Statutory Instrument series, and so its URI is [http://www.legislation.gov.uk/id/uksi/2013/376](http://www.legislation.gov.uk/id/uksi/2013/376).

Secondary legislation is sometimes assigned one or more additional numbers in different numbering series. Secondary numbering schemes are:

|Numbering Scheme|Description|URI Number Prefix|
|---|---|---|
|Commencement and/or Appointed Day orders (C)|Bring into force an Act or part of an Act.|`c`|
|Legal series (L)|Relate to fees or procedures in Courts in England and Wales.|`l`|
|Scottish series (S)|Instruments covering reserved matters applying to Scotland only, not to be confused with Scottish Statutory Instruments made under powers devolved under the [Scotland Act 1998](http://www.legislation.gov.uk/id/ukpga/1998/46).|`s`|
|Northern Ireland series (NI)|Orders in Council made under [section 1(3) of the Northern Ireland (Temporary Provisions) Act 1972](http://www.legislation.gov.uk/id/ukpga/1972/22/section/1/3) or [paragraph 1 of Schedule 1 to the Northern Ireland Act 1974](http://www.legislation.gov.uk/id/ukpga/1974/28/schedule/1/paragraph/1).|`ni`|
|Welsh series (W/Cy)|Statutory Instruments made by Senedd Cymru (formerly the National Assembly for Wales) and applying to Wales only. Such instruments will generally be made in both the English and Welsh languages.|`w`|

It is possible to use a secondary number within a URI by prefixing the number with the appropriate prefix as shown in the above table. This will result in a `301 Moved Permanently` redirection to the URI using the main numbering scheme. For example, requesting

`http://www.legislation.gov.uk/id/wsi/2002/w89`

will result in a `301 Moved Permanently` redirection to

`http://www.legislation.gov.uk/id/wsi/2002/808`

#### Legislation sections

You can refer to particular sections, articles, regulations and so on within a piece of legislation by appending `/{divisionName}/{number}` to the URI. For example, to refer to section 6 of the Road Traffic Regulation Act 1984, you can use

`http://www.legislation.gov.uk/id/ukpga/1984/27/section/6`

The name of the division that is used depends on the type of the legislation as follows:

|Legislation Type|Division Name|
|---|---|
|Act, Scheme|`section`|
|Order, Order in Council or Order of Council, EU origin legislation|`article`|
|Regulations|`regulation`|
|Rules|`rule`|

For example, regulation 6 of the Overseas Life Insurance Companies Regulations 2004 can be referenced with:

`http://www.legislation.gov.uk/id/uksi/2004/2200/regulation/6`

Further subsections can be listed after the section number, using forward slashes as separators. For example:

`http://www.legislation.gov.uk/id/ukpga/1975/63/section/1/1/ba`

The numbering scheme used for the sections, subsections and so on is that used within the legislation itself.

Whole schedules can be referred to with `/schedule/{numberOrLetter}`, and paragraphs within schedules using `/schedule/{numberOrLetter}/paragraph/{paraNumber}`. For example:

`http://www.legislation.gov.uk/id/ukpga/2005/6/schedule/1/paragraph/2`

Sub-paragraphs can be referred as with sub-sections described above.

In cases where a piece of legislation only has one schedule, the keyword schedule can be used on its own. For example:

`http://www.legislation.gov.uk/id/ukpga/1996/6/schedule`

To refer to other structures within a piece of legislation, such as parts, chapter and so on, the appropriate name for the structure should be used in lowercase, with separators between it and its number. Further substructures can be appended to this. For example, Part IV to Schedule 9 of the Road Traffic Regulation Act 1984 should be referenced using:

`http://www.legislation.gov.uk/id/ukpga/1984/27/schedule/9/part/IV`

The allowed keywords here are:

* `group`
* `part`
* `chapter`
* `schedule`
* `crossheading`
* `title` (for EU documents only)
* `annex` (for EU documents only)
* `attachment` (for EU documents only)

Within schedules, sections are referred to by the keyword `paragraph`:

`http://www.legislation.gov.uk/id/ukpga/1984/27/schedule/4/paragraph/3`

Within EU annexes and attachments, sections are referred to by the keyword `division`—unusually, the keyword `division` is repeated for every nested division:

`http://www.legislation.gov.uk/eur/2006/1907/annex/II/part/A/division/0.2/division/0.2.1`

Note that these are URI keywords, and always in English regardless of the language used in the legislation. However, the numbers used for parts, chapters and so on reflect the numbers used within the legislation; some legislation may contain Part II while another contains Part 2, and the URIs will reflect this difference rather than normalising on decimal numbers.

Requesting a division that does not exist within the legislation will result in a `404 Not Found` response.

### Document URIs

Document URIs are used to refer to particular documents on the web: versions of the legislation. Document URIs follow the template:

<code>http://www.legislation.gov.uk/{<a href="#legislation-types">type</a>}/{<a href="#legislation-years">year</a>}/{<a href="#legislation-numbers">number</a>}[/{<a href="#legislation-sections">section</a>}][/{<a href="#legislation-extents">extent</a>}][/{<a href="#legislation-versions">version</a>}]</code>

#### Legislation extents

To reference legislation as it extends to a particular country, append `/{country}`, where country is:

*   `england`
*   `wales`
*   `scotland`
*   `ni`

For example, to get the Rent Act 1977 as it extends to England, you would use:

`http://www.legislation.gov.uk/ukpga/1977/42/england`

It is also possible to select a section based on more than one country by listing them with a + separator. For example,

`http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+scotland`

requests the versions of Section 6 of The Transport Act 1985 that are applicable to England and Scotland.

Requesting a piece of legislation, or a subsection of legislation, while specifying a country that the legislation or subsection does not extend to will result in a `404 Not Found` response.

URIs that do not specify an extent are assumed to refer to the legislation as it extends to all countries.

When a selection for an exact extent is needed, the '=' operator can precede the country list. For example,

`http://www.legislation.gov.uk/ukpga/1985/67/section/6/=england+wales`

which will request all version of Section 6 of The Transport Act 1985 that are applicable to both England and Wales.

#### Legislation versions

Legislation versions fall into three general categories: [enacted/made/adopted versions](#enactedmadeadopted-versions), [dated versions](#dated-versions) and [prospective versions](#prospective-versions).

##### Enacted/made/adopted versions

The enacted, made or adopted version of legislation reflects the text of the legislation when it became law. Primary legislation is “enacted”, while the majority of secondary legislation is “made” (United Kingdom Church Instruments and Ministerial Orders are simply “created”) and legislation originating from the EU was “adopted”.

Using the keyword `enacted`, `made`, `created` or `adopted` at the end of a document URI provides the enacted or made version of the legislation, if such is available. The enacted version of legislation is often unavailable for legislation prior to 1988<!-- TODO when origins is done (see our [origins](origins.md) page for an explanation)-->.

For example, the enacted version of the Childcare Act 2006 can be found at:

`http://www.legislation.gov.uk/ukpga/2006/21/enacted`

##### Dated versions

It is often helpful to know which parts of a piece of legislation are in force at a particular time. Often, particular sections of a piece of legislation do not come into force immediately (on the enactment date) but are brought into force later on, often through a commencement order (a particular kind of secondary legislation).

In addition, most legislation, particularly primary legislation, goes through multiple changes during its lifetime as other legislation inserts or repeals sections, paragraphs and phrases. Like the original, enacted, sections, inserted sections may not actually come into force until a separate order is made.

If no version is specified in a document URI, this is taken to refer to the version of the legislation that is currently in force. For example:

`http://www.legislation.gov.uk/ukpga/1985/67`

Indicates the current version of The Transport Act 1985, and will provide the most up to date version of the legislation available through the API. (This may not indicate the current state of the legislation, due to the [limitations](../what-we-have.md#limitations) of the content available through this site.) In this case, the result will be the legislation as it stood on 1st April 2003, which is also accessible at the URI:

`http://www.legislation.gov.uk/ukpga/1985/67/2003-04-01`

Any date can be used within the URI. For example:

`http://www.legislation.gov.uk/ukpga/1985/67/1997-06-01`

would refer to the version of The Transport Act 1985 that was in effect on 1st June 1997.

Requesting a date that is prior to the [base date](../glossary.md#base-date) of 1st February 1991 (or 1st January 2006 for NI legislation) will normally result in a redirection to the legislation as it was on the base date.

Requesting a date that was prior to the enactment of the legislation results in `404 Not Found` response. Requests for sections that did not exist within a particular version will return you that section though the fact that it was not in force on that date will be indicated.

##### Prospective versions

At any point in time, there may be prospective sections within or amendments to a piece of legislation: planned sections or changes that have not come into force. Using `/prospective` instead of a date within the URI refers to the legislation that would be in force were all prospective sections and amendments in effect. For example, Part II of the Road Traffic Regulation Act 1984 has a prospective amendment from the Railways and Transport Safety Act 2003 (sections 108 and 120) that adds a Section 22B. The prospective version of that Part would be:

`http://www.legislation.gov.uk/ukpga/1984/27/part/II/prospective`

Note that the URI

`http://www.legislation.gov.uk/ukpga/1984/27/section/22B`

will return the section but that it is marked as being prospective, as does specifically requesting the prospective version with

`http://www.legislation.gov.uk/ukpga/1984/27/section/22B/prospective`

##### Explanatory Notes

Explanatory Notes provide accessible information to readers who are not legally qualified and who have no specialised knowledge of the matters dealt with by the enacting legislation. They are intended to allow the reader to grasp what the Act sets out to achieve and place its effect in context. Using `/notes` at the end of a document URI provides the Explanatory Notes for that specific legislation. For example, the Explanatory Notes for the Communications Act 2003 would be:

`http://www.legislation.gov.uk/ukpga/2003/21/notes`

The explanatary Notes for a specific section within that legislation, for example section 50 of the Communications Act 2003 would be:

`http://www.legislation.gov.uk/ukpga/2003/21/section/50/notes`

If there are no Explanatory Notes or no Explanatory Note for a specific section exists then the uri will return a `404 Not Found` response, since it does not exist.

### Representation URIs

**Note that these URIs only apply to _dynamic_ representations of legislation and associated documents. For static PDFs and images, see the [static resources](#static-resources) section below.**

Each document is available in multiple [formats](../formats/overview.md). The URI for a particular format follows the template:

<code>http://www.legislation.gov.uk/{<a href="#legislation-types">type</a>}/{<a href="#legislation-years">year</a>}/{<a href="#legislation-numbers">number</a>}[/{<a href="#legislation-sections">section</a>}][/{<a href="#legislation-extents">extent</a>}][/{<a href="#legislation-versions">version</a>}]/data.[ext]</code>

for legislation and

<code>http://www.legislation.gov.uk/{<a href="#legislation-types">type</a>}/{<a href="#legislation-years">year</a>}/{<a href="#legislation-numbers">number</a>}[/{<a href="#legislation-sections">section</a>}]/notes/data.[ext]</code>

for explanatory notes.

In the above URI templates, `[ext]` is the extension for the particular format. Available formats and their extensions are listed on the [formats](../formats/overview.md) page.

<!-- PA 23/2/2023: Commenting this out as I think we want to discourage content negotiation using the Accept header

The format provided as the result of a particular request on a [document URI](#document-uris) is determined through content negotiation based on the content types the client provides in the `Accept` request header. -->

## Static resources

Legislation.gov.uk serves three categories of static document resources:

* static PDFs of legislation and associated documents;
* images included within legislation and explanatory notes; and
* static HTML versions of explanatory notes, where not generated dynamically from XML.

These resources do not use the same URI scheme as other resources on legislation.gov.uk. The below sections explain how to derive a URI for a resource of one of the above types.

### Static PDFs

Legislation.gov.uk provides static PDFs of:

* legislation documents;
* explanatory notes; and
* other associated documents.

These have URIs that do not follow a predictable pattern. The most reliable way to find a URI for one of the above types of resource is to extract it from a link in the metadata for the associated item of legislation.

#### Legislation PDFs

Legislation.gov.uk offers two types of static legislation PDFs:

* “Original” legislation PDFs, representing the legislation as enacted or made (usually this is the same as the text as it was first printed, although some PDFs may incorporate corrections made later to the text); and
* Revised legislation PDFs, representing the legislation as it stood at a particular point in time (these are rare and mostly only appear for selected social security legislation)

Links to static legislation PDFs (where available) appear in the metadata of the legislation item, specifically as children of the `<ukm:Alternatives>` child element of the `<ukm:Metadata>` element. The `URI` attribute of the `<ukm:Alternative>` element indicates the URI of the PDF, and the presence of the `Revised` attribute indicates that the PDF represents a revised version (its value indicates the date of the [point in time](../model/legislation.md#points-in-time) up to which the version is revised; the attribute’s absence indicates that the PDF is an original version).

The [XPath](../api/xml-intro.md#navigating-xml-with-xpath) that selects the URIs of original legislation PDFs from the metadata of a legislation document is:

`/leg:Legislation/ukm:Metadata/ukm:Alternatives/ukm:Alternative[not(@Revised)]/@URI`

The XPath that selects the URIs of revised legislation PDFs from the metadata of a legislation document is:

`/leg:Legislation/ukm:Metadata/ukm:Alternatives/ukm:Alternative[@Revised]/@URI`

#### Explanatory notes PDFs

Some items of legislation have a PDF version of their explanatory notes. A link to this PDF (where available) appears in the metadata of the legislation item, specifically as children of the `<ukm:Alternatives>` child element of the `<ukm:Notes>` element. As for legislation PDFs, the `URI` attribute of the `<ukm:Alternative>` element indicates the URI of the explanatory notes PDF.

The XPath that selects the URI of explanatory notes PDFs from the metadata of a legislation document is:

`/leg:Legislation/ukm:Metadata/ukm:Notes/ukm:Alternatives/ukm:Alternative/@URI`

#### PDFs for other associated documents

Legislation items often have other [associated documents](../glossary.md#associated-document). The metadata available via the API link to these in a variety of different ways.

The below table provides an [XPath expression](../api/xml-intro.md#navigating-xml-with-xpath) that identifies all the URIs in the metadata of a given legislation item for associated documents of the kind given in the first column:

|Associated document|XPath expression|
|---|---|
|Impact Assessments|`/leg:Legislation/ukm:Metadata/ukm:ImpactAssessments/ukm:ImpactAssessment/@URI`|
|Policy equality statements|`/leg:Legislation/ukm:Metadata/ukm:PolicyEqualityStatements/ukm:PolicyEqualityStatement/@URI`|
|Codes of practice|`/leg:Legislation/ukm:Metadata/ukm:CodesOfPractice/ukm:CodeOfPractice/@URI`|
|Codes of conduct|`/leg:Legislation/ukm:Metadata/ukm:CodesOfConduct/ukm:CodeOfConduct/@URI`|
|Tables of origins|`/leg:Legislation/ukm:Metadata/ukm:TablesOfOrigins/ukm:TableOfOrigins/@URI`|
|Tables of destinations|`/leg:Legislation/ukm:Metadata/ukm:TablesOfDestinations/ukm:TableOfDestinations/@URI`|
|Orders in Council|`/leg:Legislation/ukm:Metadata/ukm:OrdersInCouncil/ukm:OrderInCouncil/@URI`|
|Explanatory documents|`/leg:Legislation/ukm:Metadata/ukm:ExplanatoryDocuments/ukm:ExplanatoryDocument/@URI`|
|Transposition notes|`/leg:Legislation/ukm:Metadata/ukm:TranspositionNotes/ukm:TranspositionNote/@URI`|
|UK Regulatory Policy Committee opinions|`/leg:Legislation/ukm:Metadata/ukm:UKRPCOpinions/ukm:UKRPCOpinion/@URI`|
|Correction slips|`/leg:Legislation/ukm:Metadata/ukm:CorrectionSlips/ukm:CorrectionSlip/@URI`|  
|Correction slips for explanatory notes and memoranda|`/leg:Legislation/ukm:Metadata/ukm:Notes/ukm:CorrectionSlips/ukm:CorrectionSlip/@URI`|
|Other documents (not included in the other categories)|`/leg:Legislation/ukm:Metadata/ukm:OtherDocuments/ukm:OtherDocument/@URI`|

<!--### Images
TODO explain how to find images-->

### HTML explanatory notes

Static HTML versions of explanatory notes, where available, use the below URI pattern:

<code>http://www.legislation.gov.uk/{<a href="#legislation-types">type</a>}/{<a href="#legislation-years">year</a>}/{<a href="#legislation-numbers">number</a>}/notes/division/[number]/index.htm</code>

where `[number]` is a whole number starting from 1 for the first division of the notes and increasing by 1 for each subsequent division. 
