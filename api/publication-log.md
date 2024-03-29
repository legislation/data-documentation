# Publication Log

The Legislation API provides a feed that records the publication and withdrawal of content on legislation.gov.uk. We call this feed the **Publication Log**.

The Publication Log feed contains one entry for every publication or republication of a resource to, or withdrawal of a resource from, the legislation.gov.uk website, for the following categories of content:

 * legislation;
 * associated documents;
 * UK Impact Assessments (which are a special kind of associated document that also exists as a standalone item); and
 * changes to legislation ([effects](../model/effects.md)).

The feed allows you to find out when we have:

 * published new items of legislation;
 * published new, updated Points in Time (revised versions) for an existing item of legislation;
 * published associated documents or Impact Assessments;
 * recorded changes to legislation (effects) from or to an item of legislation; and
 * republished or withdrawn any content already on the website.

The full feed, containing all entries, is available at [https://www.legislation.gov.uk/update/data.feed](https://www.legislation.gov.uk/update/data.feed). **We recommend that you do not directly request the full feed**, but instead request a filtered view of the feed as this will return results much faster. You can filter the feed for entries from a particular date, about a specific item, type or category of legislation, or use various other combinations of filters (see [Filtering](#filtering) below).

## Paging

The API *paginates* its responses to requests for Publication Log feeds. This means that the API returns a maximum number of items in each response to a request for a feed, and so it may be necessary to make multiple requests to get all the items in a feed.

Currently, the number of entries per page is fixed at 20 entries. The `page` query string parameter specifies the page of results the API will return.

## Fields

Each Publication Log entry has multiple fields describing its publication or withdrawal event. The Publication Log represents most of the fields using the `http://www.legislation.gov.uk/namespaces/publication-log` namespace (normally using the prefix `pbl:`), but also uses other namespaces. Note that the Atom namespace (`http://www.w3.org/2005/Atom`) is used without a prefix in the feeds and in the examples drawn from it below, but the table below uses the `atom:` prefix to show where a field uses the Atom namespace. (For more information about the namespaces, see the [Common namespaces in our data](../api/xml-intro.md#common-namespaces-in-our-data) section of the guide.)

The fields that appear in Publication Log entries are:

|Field|Representing element|Meaning|
|---|---|---|
|Entry ID|`<atom:id>`|{::nomarkdown}<p>A unique identifier for the event.<p><strong>Note:</strong> the Publication Log records the (dis)association of a UK Impact Assessment with an item of legislation as two separate entries (one for the UKIA-legislation association, and one for the legislation-UKIA association). These entries have the same Entry ID, but different Item IDs (one for the legislation item and the other for the UKIA){:/}|
|Item ID|`<dc:identifier>`|The identifier of the item of legislation or UK Impact Assessment which the resource manifests or to which it is associated.|
|Updated|`<atom:updated>`|The date and time at which the event (publication or withdrawal) occurred.|
|Published|`<atom:published>`|{::nomarkdown}<p>If present, the first date and time at which a resource was published at this URI.<p><strong>Note:</strong> Due to deficiencies in the admin log, which recorded publication events before the Publication Log was released, some resources were published to legislation.gov.uk without a log entry. If this field is absent, it means that the resource was not previously published on or after 5<sup>th</sup> July 2023, but might have been published before that date. If this field is present, the date may not be the true date and time of original publication if it is on or after 5<sup>th</sup> July 2023.{:/}|
|Title|`<atom:title>`|The title of the resource. This is usually the title of the legislation item, but for associated documents it will normally be the title of the associated legislation item followed by the type of the associated document.|
|Author|`<atom:author>`|{::nomarkdown}<p>The publisher of the resource.<p><strong>Note:</strong> the Publication Log always shows the author for XML versions of revised legislation as <code>editorial.legislation.gov.uk</code>, but in the XML for the revised legislation itself the value of <code>dc:publisher</code> is usually <code>Statute Law Database</code>.{:/}|
|Content type|`<pbl:ContentType>`|The type of content being published or withdrawn (`legislation`, `draft`, `associated-documents` or `changes`).|
|Event|`<pbl:Event>`|The type of event (`published` or `withdrawn`).|
|Republished|`<pbl:Republished>`|{::nomarkdown}<p>Indicates whether the resource has ever previously been published at this URI.<p><strong>Note:</strong> Due to deficiencies in the admin log, which recorded publication events before the Publication Log was released, some resources were published to legislation.gov.uk without a log entry. If the value of this field is `false`, it means that the resource was not previously published on or after 5<sup>th</sup> July 2023, but might have been published before that date{:/}|
|New|`<pbl:New>`|Indicates whether the item of legislation existed on legislation.gov.uk before this publication event.|
|Newly issued|`<pbl:NewlyIssued>`|Indicates whether a new item of legislation has just been issued (is actually “new”), or whether it was issued in the past but has only just been uploaded.|
|Document|`<pbl:Document>`|The [expression](../model/legislation.md#frbr-functional-requirements-for-bibliographic-records) (version) of the item that the resource manifests. For associated documents, this will normally be the same as the Item.|
|Link|`<atom:link>`|For XML resources, a link to an alternate representation of the resource.| 
|Item|{::nomarkdown}<code>&lt;pbl:Item_Published&gt;</code><br><code>&lt;pbl:Item_Withdrawn&gt;</code>{:/}|The URI of the resource being published or withdrawn.|
|Format|`<pbl:Format>`|The format of the resource (`xml`, `pdf` or `html5`).|
|Print|`<pbl:Print>`|Indicates whether a legislation PDF represents the version of the document that is to be printed.|
|Direction|`<pbl:Direction>`|For changes, indicates whether the effects were updated for the affecting or affected item.|
|Correction slip number|`<pbl:CorrectionSlipNumber>`|For correction slips, records the sequential number of the correction slip.|
|Document category|`<ukm:DocumentCategory>`|The category of the item of legislation to which the resource relates.|
|Document main type|`<ukm:DocumentMainType>`|The long name of the document type of the item to which the resource relates.|
|Year|`<ukm:Year>`|The year of the item to which the resource relates.|
|Number|`<ukm:Number>`|The number of the item (in its primary numbering series) to which the resource relates.|
|ISBN|`<ukm:ISBN>`|For legislation items that are not numbered, the ISBN of the item of legislation to which the resource relates.|
|Alternative number|`<ukm:AlternativeNumber>`|{::nomarkdown}<p>A number in an alternative numbering series for the item to which the resource relates.<p><strong>Note:</strong> this field does not appear for entries for associated documents or changes, even if it applies to the related item of legislation.{:/}|
|Supersedes|`<ukm:Supersedes>`|{::nomarkdown}<p>For legislation that supersedes other legislation, the item of legislation superseded by the item to which the resource relates.<p><strong>Note:</strong> this field does not appear for entries for associated documents or changes, even if it applies to the related item of legislation.{:/}|

## Filtering

You can filter the Publication Log by specifying various parameters in the feed URI path and query string.

### Paths

The Publication Log feeds support the following path parameters:

|Parameter|Filters|Permitted values|Examples|
|---|---|---|---|
|Date|The date on which the event occurred (from the `<atom:published>` field)|A date in `yyyy-mm-dd` format|[https://www.legislation.gov.uk/update/2023-07-07/data.feed](https://www.legislation.gov.uk/update/2023-07-07/data.feed)|
|Content type|The type of content to which the event relates|{::nomarkdown}One of the following values:<ul><li><code>legislation</code><li><code>draft</code><li><code>associated-documents</code><li><code>changes</code></li>{:/}|[https://www.legislation.gov.uk/update/draft/data.feed](https://www.legislation.gov.uk/update/draft/data.feed)|
|Direction|**For effects only:** Whether the effects were recorded against the affecting item or the affected item|{::nomarkdown}One of the following values:<ul><li><code>affecting</code><li><code>affected</code></li>{:/}|[https://www.legislation.gov.uk/update/changes/affected/data.feed](https://www.legislation.gov.uk/update/changes/affected/data.feed)|
|Document category|**For legislation and associated documents:** The category of legislation|{::nomarkdown}One of the following values:<ul><li><code>primary</code><li><code>secondary</code><li><code>eu-origin</code></li>{:/}|[https://www.legislation.gov.uk/update/legislation/eu-origin/data.feed](https://www.legislation.gov.uk/update/legislation/eu-origin/data.feed)|
|Document main type|The type of the document to which the resource relates|One of the values in the “Document Main Type” column of the [legislation types](../model/uris.md#legislation-types) table|[https://www.legislation.gov.uk/update/2023-07-05/wsi/data.feed](https://www.legislation.gov.uk/update/2023-07-05/wsi/data.feed) (Document main type = wsi)|
|Treaty name|**For EU treaties only:** The short name of the EU treaty|{::nomarkdown}One of the following values:<ul><li><code>teec</code><li><code>euratom</code><li><code>teu</code><li><code>eea-agreement</code><li><code>withdrawal-agreement</code></li>{:/}|[https://www.legislation.gov.uk/update/eut/withdrawal-agreement/data.feed](https://www.legislation.gov.uk/update/eut/withdrawal-agreement/data.feed)|
|Year|The year assigned to the document|A four digit year|[https://www.legislation.gov.uk/update/2014/data.feed](https://www.legislation.gov.uk/update/2014/data.feed)|
|Regnal year|**For regnal year-numbered items only:** The monarch and session assigned to the document|A regnal year string (see examples)|[https://www.legislation.gov.uk/update/legislation/ukpga/Eliz2/6-7/51/data.feed](https://www.legislation.gov.uk/update/legislation/ukpga/Eliz2/6-7/51/data.feed) (Regnal = Eliz2/6-7)|
|Number|The number assigned to the document in its main numbering series|A whole number greater than or equal to 0|[https://www.legislation.gov.uk/update/2023-07-06/2022/231/data.feed](https://www.legislation.gov.uk/update/2023-07-06/2022/231/data.feed) (Number = 231)|

### Query string parameters

The Publication Log feeds support the following query parameters:

|Parameter|Filters|Permitted values|
|---|---|---|
|event|The type of event|`published` or `withdrawn`|
|new|{::nomarkdown}<p><strong>For items of legislation and UK Impact Assessments:</strong> whether the item of legislation or UK Impact Assessment associated with the event is new to legislation.gov.uk.<p><strong>For other associated documents:</strong> whether the associated document has been published before at this URI.{:/}|`true` or `false`|
|format|The format of the resource.|`xml`, `pdf` or `html5`|
|language|A language of the resource.|`en` or `cy` (dual-language resources will match either value)|
|title|The title of the resource or the document to which it is associated, or any contiguous sequence of words within its title.|Any text string|
|republished|Whether the resource has been published before at this URI.|`true` or `false`|

The Publication Log feeds also support the `page` parameter for selecting a results page (see [Paging](#paging) above), and the `sort` and `sortorder` parameters for sorting (see below).

## Sorting

The Publication Log feeds support various sort criteria, and allow you to specify the ordering of the results. The table below lists the available sort criteria:

|Name|Sort|
|---|---|
|`date`|Sort by the date and time at which the event occurred.|
|`title`|Sort by title in alphabetical order.|
|`language`|Sort by the language of the resource.|
|`republished`|Sort by whether or not the resource was being republished in the event.|
|`format`|Sort by the format of the resource.|
|`new`|Sort by whether the event was for the first resource of a new item of legislation.|
|`event`|Sort by whether the resource was published or withdrawn.|
|`contenttype`|Sort by the type of the content of the resource being published or withdrawn.|
|`legislationtype`|Sort by the category of legislation (primary, secondary, EU).|
|`documenttype`|Sort by the type of the item for which the resource was published or withdrawn.|
|`year`|Sort by the year of the item for which the resource was published or withdrawn.|
|`number`|Sort by the number of the item for which the resource was published or withdrawn.|

You may only sort by a single sort criterion at any one time.

You can choose whether to order the sort in `ascending` or `descending` order using the `sortorder` parameter.

The default sort is `date` and the default sort order is `descending`.

## Content types

### Legislation

The Publication Log feed contains one entry for each publication, republication or withdrawal of an XML or PDF representation of an item of legislation, which may be for the enacted or made version or for a revised Point in Time (PiT).

The following is the example of the publication of XML for the 1/3/2021 revised PiT for Regulation (EU) 2019/2013 (from [https://www.legislation.gov.uk/update/2023-07-07/legislation/eu-origin/eur/2019/2013/data.feed?format=xml&republished=false](https://www.legislation.gov.uk/update/2023-07-07/legislation/eu-origin/eur/2019/2013/data.feed?format=xml&republished=false)):

```
<entry>
  <id>http://www.legislation.gov.uk/eur/2019/2013/2021-03-01/data.xml/published/2023-07-07T10:56:11.717977+01:00</id>
  <dc:identifier>http://www.legislation.gov.uk/id/eur/2019/2013</dc:identifier>
  <title>Commission Delegated Regulation (EU) 2019/2013 of 11 March 2019 supplementing Regulation (EU) 2017/1369 of the European Parliament and of the Council with regard to energy labelling of electronic displays and repealing Commission Delegated Regulation (EU) No 1062/2010 (Text with EEA relevance.)</title>
  <author>
    <name>editorial.legislation.gov.uk</name>
  </author>
  <updated>2023-07-07T10:56:11.717977+01:00</updated>
  <ukm:DocumentCategory Value="euretained"/>
  <ukm:DocumentMainType Value="EuropeanUnionRegulation"/>
  <ukm:Year Value="2019"/>
  <ukm:Number Value="2013"/>
  <pbl:ContentType>legislation</pbl:ContentType>
  <pbl:Event>published</pbl:Event>
  <pbl:Republished>false</pbl:Republished>
  <pbl:New>false</pbl:New>
  <pbl:Document>http://www.legislation.gov.uk/eur/2019/2013/2021-03-01</pbl:Document>
  <link rel="alternate" type="application/rdf+xml" href="http://www.legislation.gov.uk/eur/2019/2013/2021-03-01/data.rdf" title="RDF/XML"/>
  <link rel="alternate" type="application/akn+xml" href="http://www.legislation.gov.uk/eur/2019/2013/2021-03-01/data.akn" title="AKN"/>
  <link rel="alternate" type="application/xhtml+xml" href="http://www.legislation.gov.uk/eur/2019/2013/2021-03-01/data.xht" title="HTML snippet"/>
  <link rel="alternate" type="application/akn+xhtml" href="http://www.legislation.gov.uk/eur/2019/2013/2021-03-01/data.html" title="HTML5 snippet"/>
  <link rel="alternate" type="text/html" href="http://www.legislation.gov.uk/eur/2019/2013/2021-03-01/data.htm" title="Website (XHTML) Default View"/>
  <link rel="alternate" type="application/pdf" href="http://www.legislation.gov.uk/eur/2019/2013/2021-03-01/data.pdf" title="PDF"/>
  <pbl:Item_Published>http://www.legislation.gov.uk/eur/2019/2013/2021-03-01/data.xml</pbl:Item_Published>
  <pbl:Format>xml</pbl:Format>
  <dc:language>en</dc:language>
</entry>
```

The following is an example of the withdrawal of a non-print PDF of the made English version of W.S.I. 2023/754 (from [https://www.legislation.gov.uk/update/wsi/2023/754/data.feed?event=withdrawn&format=pdf&language=en](https://www.legislation.gov.uk/update/wsi/2023/754/data.feed?event=withdrawn&format=pdf&language=en)):

```
<entry>
  <id>http://www.legislation.gov.uk/wsi/2023/754/pdfs/wsi_20230754_en.pdf/withdrawn/2023-07-05T12:24:02.697007+01:00</id>
  <dc:identifier>http://www.legislation.gov.uk/id/wsi/2023/754</dc:identifier>
  <title>The Animal By-Products, Pet Passport and Animal Health (Fees) (Wales) (Amendment) Regulations 2023</title>
  <author>
    <name>King's Printer of Acts of Parliament</name>
  </author>
  <published>2023-07-04T19:03:59.45768+01:00</published>
  <updated>2023-07-05T12:24:02.697007+01:00</updated>
  <ukm:DocumentCategory Value="secondary"/>
  <ukm:DocumentMainType Value="WelshStatutoryInstrument"/>
  <ukm:Year Value="2023"/>
  <ukm:Number Value="754"/>
  <ukm:AlternativeNumber Category="W" Value="119"/>
  <pbl:ContentType>legislation</pbl:ContentType>
  <pbl:Event>withdrawn</pbl:Event>
  <pbl:Document>http://www.legislation.gov.uk/wsi/2023/754/made</pbl:Document>
  <pbl:Item_Withdrawn>http://www.legislation.gov.uk/wsi/2023/754/pdfs/wsi_20230754_en.pdf</pbl:Item_Withdrawn>
  <pbl:Format>pdf</pbl:Format>
  <pbl:Print>false</pbl:Print>
  <dc:language>en</dc:language>
</entry>
```

### Associated documents

The feed contains one entry for each publication, republication or withdrawal of a PDF, XML or HTML 5 version of an associated document for an item of legislation.

The following is an example of the publication of an Explanatory Note for a UKPGA (from [https://www.legislation.gov.uk/update/2023-07-07/associated-documents/ukpga/2023/data.feed](https://www.legislation.gov.uk/update/2023-07-07/associated-documents/ukpga/2023/data.feed)):

```
<entry>
  <id>http://www.legislation.gov.uk/ukpga/2023/28/pdfs/ukpgaen_20230028_en.pdf/published/2023-07-07T13:17:53.676278+01:00</id>
  <dc:identifier>http://www.legislation.gov.uk/id/ukpga/2023/28</dc:identifier>
  <title>Retained EU Law (Revocation and Reform) Act 2023 Explanatory Note</title>
  <author>
    <name>King's Printer of Acts of Parliament</name>
  </author>
  <updated>2023-07-07T13:17:53.676278+01:00</updated>
  <ukm:DocumentCategory Value="primary"/>
  <ukm:DocumentMainType Value="UnitedKingdomPublicGeneralAct"/>
  <ukm:Year Value="2023"/>
  <ukm:Number Value="28"/>
  <pbl:ContentType>associated-documents</pbl:ContentType>
  <pbl:Event>published</pbl:Event>
  <pbl:Republished>false</pbl:Republished>
  <pbl:New>true</pbl:New>
  <pbl:Document>http://www.legislation.gov.uk/ukpga/2023/28/pdfs/ukpgaen_20230028_en.pdf</pbl:Document>
  <pbl:Item_Published>http://www.legislation.gov.uk/ukpga/2023/28/pdfs/ukpgaen_20230028_en.pdf</pbl:Item_Published>
  <pbl:Format>pdf</pbl:Format>
  <dc:language>en</dc:language>
</entry>
```

### UK Impact Assessments

The feed contains one entry for each publication, republication or withdrawal of a PDF version of a UK Impact Assessment, plus entries for its association to (or disassociation from) items of legislation.

The following is an example of the publication of a UKIA associated with an item of legislation. There are two entries, one from the feed for the item of legislation with which it is associated, and one from the feed for the UKIA itself. Both entries have the same ID as they represent the same event, the same document (which represents the link between the two items) and the same metadata about the resource itself. However, the metadata in the feed entry for the item of legislation (the type, year, number and publisher) all relate to the item of legislation, whereas in the feed entry for the UKIA they relate to the UKIA.

The entry for the association to the item of legislation appears as follows (from [https://www.legislation.gov.uk/update/2023-07-05/associated-documents/uksi/2022/633/data.feed](https://www.legislation.gov.uk/update/2023-07-05/associated-documents/uksi/2022/633/data.feed)):

```
<entry>
  <id>http://www.legislation.gov.uk/ukia/2022/107/pdfs/ukia_20220107_en.pdf/published/2023-07-05T14:25:19.821972+01:00</id>
  <dc:identifier>http://www.legislation.gov.uk/id/uksi/2022/633</dc:identifier>
  <title>The Customs (Safety and Security Procedures) Regulations 2022 Impact Assessment</title>
  <author>
    <name>King's Printer of Acts of Parliament</name>
  </author>
  <updated>2023-07-05T14:25:19.821972+01:00</updated>
  <ukm:DocumentCategory Value="secondary"/>
  <ukm:DocumentMainType Value="UnitedKingdomStatutoryInstrument"/>
  <ukm:Year Value="2022"/>
  <ukm:Number Value="633"/>
  <pbl:ContentType>associated-documents</pbl:ContentType>
  <pbl:Event>published</pbl:Event>
  <pbl:Republished>false</pbl:Republished>
  <pbl:New>true</pbl:New>
  <pbl:Document>http://www.legislation.gov.uk/uksi/2022/633/impacts/2022/107</pbl:Document>
  <pbl:Item_Published>http://www.legislation.gov.uk/ukia/2022/107/pdfs/ukia_20220107_en.pdf</pbl:Item_Published>
  <pbl:Format>pdf</pbl:Format>
  <dc:language>en</dc:language>
</entry>
```

The entry for the association to the UKIA appears as follows (from [https://www.legislation.gov.uk/update/2023-07-05/ukia/2022/107/data.feed](https://www.legislation.gov.uk/update/2023-07-05/ukia/2022/107/data.feed)):

```
<entry>
  <id>http://www.legislation.gov.uk/ukia/2022/107/pdfs/ukia_20220107_en.pdf/published/2023-07-05T14:25:19.821972+01:00</id>
  <dc:identifier>http://www.legislation.gov.uk/id/ukia/2022/107</dc:identifier>
  <title>The Customs (Safety and Security Procedures) Regulations 2022 Impact Assessment</title>
  <author>
    <name>Better Regulation Executive</name>
  </author>
  <updated>2023-07-05T14:25:19.821972+01:00</updated>
  <ukm:DocumentMainType Value="UnitedKingdomImpactAssessment"/>
  <ukm:Year Value="2022"/>
  <ukm:Number Value="107"/>
  <pbl:ContentType>associated-documents</pbl:ContentType>
  <pbl:Event>published</pbl:Event>
  <pbl:Republished>false</pbl:Republished>
  <pbl:New>true</pbl:New>
  <pbl:Document>http://www.legislation.gov.uk/uksi/2022/633/impacts/2022/107</pbl:Document>
  <pbl:Item_Published>http://www.legislation.gov.uk/ukia/2022/107/pdfs/ukia_20220107_en.pdf</pbl:Item_Published>
  <pbl:Format>pdf</pbl:Format>
  <dc:language>en</dc:language>
</entry>
```

### Changes to legislation

The feed contains one entry for each publication or republication of the set of [effects](../model/effects.md) made by, or to, an item of legislation. The entry only specifies the item of legislation and whether it was the affecting or affected document in relation to the set of changes published—it does not list details of individual effects. (To view details of individual effects, you can retrieve a [feed of the effects](search.md#changes-to-legislation) for the item of legislation.)

Changes can only be republished, not withdrawn. However, a publication of a set of changes may delete some or all of the existing effects. This is still recorded as a “published” event.

Due to limitations in our API, changes entries do not have the following fields:

 * Document category
 * Alternative number
 * Supersedes

Changes entries also do not have a language, as each legislation item only has a single set of effects even if its text has multiple languages. However, they do contain both English and Welsh titles for dual-language documents.

The following is an example of a changes event relating to the publishing of effects made **by** W.S.I. 2020/1073 (from [https://www.legislation.gov.uk/update/changes/affecting/wsi/2020/1073/data.feed](https://www.legislation.gov.uk/update/changes/affecting/wsi/2020/1073/data.feed)):

```
<entry>
  <id>http://www.legislation.gov.uk/changes/affecting/wsi/2020/1073/published/2023-07-07T16:20:33.742931+01:00</id>
  <dc:identifier>http://www.legislation.gov.uk/id/wsi/2020/1073</dc:identifier>
  <title type="xhtml">
  <div xmlns="http://www.w3.org/1999/xhtml">
    <span xml:lang="en">The National Health Service (Pharmaceutical Services) (Wales) Regulations 2020</span>
    / 
    <span xml:lang="cy">Rheoliadau’r Gwasanaeth Iechyd Gwladol (Gwasanaethau Fferyllol) (Cymru) 2020</span>
  </div>
  </title>
  <author>
    <name>editorial.legislation.gov.uk</name>
  </author>
  <updated>2023-07-07T16:20:33.742931+01:00</updated>
  <ukm:DocumentMainType Value="WelshStatutoryInstrument"/>
  <ukm:Year Value="2020"/>
  <ukm:Number Value="1073"/>
  <pbl:ContentType>changes</pbl:ContentType>
  <pbl:Event>published</pbl:Event>
  <pbl:Direction>affecting</pbl:Direction>
</entry>
```
