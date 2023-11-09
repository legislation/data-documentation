# Legislation API

<!--
What is an API?
Every resource is available through the API (with some exceptions)
What can I use the API for? (CORS, crawling)
Where we have XML you can request resources in multiple formats
You can get information about changes to legislation through the API
You can search using the API
You can get lists using the API (including those of newly published legislation)
-->

## What is the Legislation API?

The legislation.gov.uk website is also an [API](https://en.wikipedia.org/wiki/API) (short for “application programming interface”), which means it is designed for software applications to use as well as human readers. Applications can use the API to search for and download legislation and information about it.

The API serves the pages you can view on legislation.gov.uk. This means that (almost) every page or resource on the website is also available via the API, often in multiple formats, and the content available via both routes is updated at the same time. 

## Features of the API

The API has the following features:

 * Access to legislation document content
 * Access to legislation metadata
 * Search, lists and feeds
 * Content negotation for multiple file formats

### Access to legislation document content

You can get the content of a legislation document (or part of it) through the API.

For example, you can get the content of the Pension Schemes Act 2021 through the following [URLs](../model/uris/introduction.md):

* [https://www.legislation.gov.uk/ukpga/2021/1/data.xml](https://www.legislation.gov.uk/ukpga/2021/1/data.xml) returns the content of the **latest version** of the Pension Schemes Act 2021 as [CLML](../formats/xml.md), our XML dialect for legislation.
* [https://www.legislation.gov.uk/ukpga/2021/1/enacted/data.xml](https://www.legislation.gov.uk/ukpga/2021/1/enacted/data.xml) returns the content of the **as enacted version** of the Pension Schemes Act 2021 as CLML.
* [https://www.legislation.gov.uk/ukpga/2021/1/part/1/data.xml](https://www.legislation.gov.uk/ukpga/2021/1/part/1/data.xml) returns the content of the **latest version of Part 1** of the Act as CLML.

The [CLML Reference Guide](https://legislation.github.io/clml-schema/) has guidance on how to interpret CLML.

Some documents are only available as PDF. For example, the Metropolis Water Act 1902 is (as of writing) only available as a PDF at [https://www.legislation.gov.uk/ukpga/Edw7/2/41/pdfs/ukpga_19020041_en.pdf](https://www.legislation.gov.uk/ukpga/Edw7/2/41/pdfs/ukpga_19020041_en.pdf). <!-- TODO You can find out if a document is available as PDF or as CLML by parsing the metadata for the document (see below). -->

<!-- TODO more sections, notes, etc. -->

### Access to legislation metadata

You can get metadata (information about an item of legislation) through the API.

#### Embedded document metadata

The `<ukm:Metadata>` element in CLML (see the section on [namespaces](xml-intro.md#namespaces) in our introduction to XML for an explanation of what `ukm:` means) contains information about the item of legislation and the version being viewed, including but not limited to:

* the title of the item;
* the item’s type, year and number;
* any “alternative” formats of the item, such as a PDF;
* any associated documents, such as Impact Assessments and Explanatory Memoranda;
* the date(s) of enactment, making, laying and/or coming into force of the item (where present in the data);
* any powers to make secondary legislation conferred by the item (present only in [revised data](../model/legislation.md#versions)); and
* any unapplied changes outstanding for the document.

The CLML Reference Guide has guidance on how to interpret [metadata in CLML](https://legislation.github.io/clml-schema/userguide.html#part-5-metadata).

If you only want the metadata for a document, the `/resources` sub-resource contains the metadata for the specified version of an item. For example: 

* [https://www.legislation.gov.uk/ukpga/1981/54/resources/data.xml](https://www.legislation.gov.uk/ukpga/1981/54/resources/1999-09-27/data.xml) contains the metadata for the current version of the Senior Courts Act 1981.
* [https://www.legislation.gov.uk/ukpga/1981/54/resources/1999-09-27/data.xml](https://www.legislation.gov.uk/ukpga/1981/54/resources/1999-09-27/data.xml) contains the metadata for the version of the Senior Courts Act 1981 dated 27/9/1999.

#### Legislation Linked Data via the SPARQL endpoint

We now have a SPARQL endpoint that allows for querying of core legislation data, including a near-complete list of all UK law, as well as of EU origin law up to the end of the implementation period. For more information, see the [SPARQL](sparql.md) section of this documentation.

### Changes to legislation

The API provides lists of [changes made to legislation](https://www.legislation.gov.uk/changes), also known as “effects”. You can request a list of changes to legislation by the type, year and number of the affected and/or affecting document, including information on:

 * the affected and affecting provisions of the items;
 * the type of effect (e.g. “words substituted”, “repealed”, “restricted”);
 * the in force date(s) of the effect;
 * the geographical extent of the effect; and/or
 * whether the effect has been applied or will be applied.

To get a list of effects, see the [changes to legislation](search.md#changes-to-legislation) sub-section of the “Search, lists and feeds” section.

<!--For more information on how to request lists of effects, see the changes section of our API reference.--> 

For more information on how to interpret effects, see the [effects section](https://legislation.github.io/clml-schema/userguide.html#effects) of the CLML reference guide.

### Search, lists and feeds

You can search for legislation through the API using any of the features available on the search interface on the website. You can also retrieve the same lists of legislation through the API as through the website. 

The API returns the search results as an [Atom](https://en.wikipedia.org/wiki/Atom_(web_standard)) feed. The list is paginated, which means that the API only returns a fixed number of items in each response (the default is 20, which you can change by adding `results-count=N` to the [query string](https://en.wikipedia.org/wiki/Query_string)). Where there are more pages left in the feed, the response will contain a `<link rel="next">` element with a link to the next results page. 

By default the API returns items in order of their last modification date (the date on which an enacted or revised version was most recently published), most recent first.

For example:

* [https://www.legislation.gov.uk/ukpga/data.feed](https://www.legislation.gov.uk/ukpga/data.feed) returns the first page of the feed of UK Public General Acts, maximum 20 items per page.
* [https://www.legislation.gov.uk/primary+secondary?title=help](https://www.legislation.gov.uk/primary+secondary?title=help) returns the first page of the feed of UK legislation with “help” in the title, maximum 20 items per page.
* [https://www.legislation.gov.uk/all/2002/1-100?page=2](https://www.legislation.gov.uk/all/2002/1-100?page=2) returns the second page of the feed of legislation of all types with a year of 2002 and a number between 1 and 100, maximum 20 items per page.
* [https://www.legislation.gov.uk/uksi+wsi+ssi+nisr/data.feed?text=dogs&results-count=5](https://www.legislation.gov.uk/uksi+wsi+ssi+nisr/data.feed?text=dogs&results-count=5) returns a feed of Statutory Instruments (UK, Welsh and Scottish) and Northern Ireland Statutory Rules with the word “dogs” in the text, maximum 5 items per page.

For more information, see the section on [search, lists and feeds](search.md).

## How can I use the API?

You can connect to our API using any HTTP client (such as a web browser, or an HTTP request library for your programming language). This page contains addresses for some example resources available through the API.

We encourage users to use our API in their own applications, including crawling and bulk access, and whether commercial or non-commercial. The data in the API are available under open licences. For more information on licensing, see the [licence](../reuse-licence.md) section of this guide.

### Fair Use Policy

We do have a [Fair Use Policy](../fair-use.md) for the API. To use the API, you must follow the requirements of the policy: 

 * If you make requests to the API, they must specify a **user agent** (if you are making requests from a web browser, it will specify a user agent automatically).<!-- TODO in future we may require that the user agent contains descriptive information such as a web address-->
 * We currently limit each IP address to 3,000 API requests every 5 minutes.<!-- TODO: add back in when Bulk Downloads is working; If you want to download a large amount of legislation data at once, it may be quicker to use our [bulk downloads]() service, which allows you to download all or part of our set of legislation as a ZIP file.-->

### URI scheme

Our API follows a consistent [URI scheme](../model/uris.md).

### CORS

The API has [CORS (cross-origin resource sharing)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) enabled, which means you can make requests to the API from client-side Javascript applications running in a web browser.

Note that only endpoints where the path ends in `/data.[ext]` (e.g. `/data.xml` or `/data.feed`) have CORS enabled. Endpoints ending in `/data.htm` (which correspond to web pages as returned by the website) currently do not have CORS enabled.

### Caching

We [cache](caching.md) the output of the API for performance reasons, so sometimes there may be a delay between an update to our data and its appearance on the website or API.

### Representations and content negotiation

#### Formats

The API offers multiple representations of some types of content:

 * The text content of legislation for which we hold structured XML data is available via the API as HTML, XML (in multiple dialects) and as PDF (dynamically generated). 
 * Search results and lists are available as HTML and as Atom feeds.
 
This means that any legislation available as HTML is also available as XML and in other formats.

The formats the API currently provides are:

|Format|MIME Type|Resource name|
|---|---|---|
|XML|`application/xml`|`/data.xml` (CLML) or `/data.akn` (Akoma Ntoso)|
|HTML|`application/xhtml+xml` (XHTML) or `text/html` (HTML5)|`/data.xht` (XHTML) or `/data.html` (HTML5)|
|PDF (dynamically generated)|`application/pdf`|`/data.pdf`|
|Atom|`application/atom+xml`|`/data.feed`|

The API returns legislation [XML](../formats/xml.md) in the CLML and Akoma Ntoso dialects.

The API also generates PDFs from items of legislation and any part or version of them.

The API can provide pre-generated XHTML and HTML5 snippets for you to use in your own applications.

For [lists of legislation](../search.md) and [effects](../model/effects.md), the API returns feeds in Atom format.

#### XML is the recommended format

We recommend you request responses in XML format as this is normally easier to parse. You can request XML for legislation (as CLML) by appending `/data.xml` to the end of the URI, and XML for search results and lists (as Atom) by appending `/data.feed` to the end of the URI.

If you are not familiar with XML, we strongly recommend you read our [introduction to XML](xml-intro.md) to learn about its main features.

#### Content negotiation

To request a different representation of a resource, you can specify a _subresource_ at the end of the URI path. For example, appending `/data.xml` to the end of the URI for a version of legislation requests that version as CLML (e.g. [https://www.legislation.gov.uk/anaw/2013/1/data.xml](https://www.legislation.gov.uk/anaw/2013/1/data.xml) requests the CLML version of 2013 anaw 1).

<!-- PA: I’m commenting this out because I think we want to discourage server side content negotiation, which the WHATWG advise against and reduces cache performance: https://wiki.whatwg.org/wiki/Why_not_conneg#Server-side_choice_is_worse_for_intermediate_caches_than_browser-side_choice

 2. Specify the desired content type in the `Accept` header of your request (e.g. make a request with the header `Accept: application/pdf` for `https://www.legislation.gov.uk/asp/2020/5/introduction` to get the introduction to 2020 asp 5 as a dynamically generated PDF).

We strongly recommend you specify a subresource to choose a representation, rather than vary the `Accept` header. The API may respond faster on average to requests that specify a subresource and use a common generic `Accept` header (e.g. `Accept: */*`) than those that use a specific `Accept` header because the API is more likely to be able to serve a response from the cache. (For an explanation of why this is the case, see the WHATWG article ["Why not content negotation?"]()-->

### Supported HTTP methods

The API currently only supports the `GET` HTTP method, which is the default for most applications that use HTTP, except for the SPARQL endpoint at [https://www.legislation.gov.uk/sparql](https://www.legislation.gov.uk/sparql), which also supports the `POST` HTTP method in accordance with the [support for `POST` in the SPARQL protocol](https://www.w3.org/TR/sparql11-protocol/#query-via-post-urlencoded).

### Response codes

The API uses HTTP response codes as specified in [RFC 9110 (HTTP Semantics)](https://www.rfc-editor.org/rfc/rfc9110.html#name-status-codes).

Most requests to the API should return `200 OK`. Some other common response codes the API returns are:

 * `202 Accepted`: The API will return this code if you make a request to a URI that identifies a resource that is dynamically generated, such as a [dynamically generated PDF](../formats/pdf.md#dynamically-generated-pdfs), to indicate that your request has been accepted but the resource is not yet available. You should repeat the request for the same URI after a short wait, until the API returns a `200 OK` response—we recommend you wait at least 10 seconds between each request to give the API sufficient time to generate the resource.
 * `300 Multiple Choices`: The API will return this code if you make a request to a URI that identifies more than one item or section of legislation (e.g. [http://www.legislation.gov.uk/id/ukpga/1955/18](http://www.legislation.gov.uk/id/ukpga/1955/18) identifies both the Army Act 1955 and the Aliens' Employment Act 1955). The response will contain an HTML list with links to the different options.
 * `400 Bad Request`: The API will return this code if you make a request for an item of legislation and specify a year or number that is out of the acceptable range for that type of legislation. The API may also return this code if your request is malformed.
 * `403 Forbidden`: The API will return this code if you exceed the rate limit (see the section on our [Fair Use Policy](#fair-use) above). Your application should slow down or stop making requests until it is under the rate limit again. The API also returns `403 Forbidden` if we have blocked requests from your IP address. If you continue to receive `403 Forbidden` responses to your requests, please [contact us](../index.md#contact-us). 
 * `500 Internal Server Error`: The API may return this code if there is a temporary error within the service, or if it cannot process the requested document due to an error in the data. If you get this response more than once for a request to a specific resource, please [contact us](../index.md#contact-us) with details of the resource.
 * `503 Service Unavailable` or `504 Gateway Timeout`: The API returns these codes if the legislation.gov.uk service is over capacity or is experiencing a temporary interruption of service. We recommend you wait at least 5 minutes before trying your request again. If you continue to receive this response for a request to a specific resource, please [contact us](../index.md#contact-us) with details of the resource.
