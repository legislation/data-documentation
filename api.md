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

The legislation.gov.uk website is also an [API](https://en.wikipedia.org/wiki/API) (short for "application programming interface"), which means it is designed for software applications to use as well as human readers. Applications can use the API to search for and download legislation and information about it.

The API serves the pages you can view on legislation.gov.uk. This means that (almost) every page or resource on the website is also available via the API, often in multiple formats.

## Features of the API

The API has the following features:

 * Access to legislation document content
 * Access to legislation metadata
 * Search, lists and feeds
 * Content negotation for multiple file formats

### Access to legislation document content

You can get the content of a legislation document (or part of it) through the API.

For example, you can get the content of the Pension Schemes Act 2021 through the following [URLs]():

* [https://www.legislation.gov.uk/ukpga/2021/1/data.xml](https://www.legislation.gov.uk/ukpga/2021/1/data.xml) returns the content of the **latest version** of the Pension Schemes Act 2021 as [CLML](), our XML dialect for legislation.
* [https://www.legislation.gov.uk/ukpga/2021/1/enacted/data.xml](https://www.legislation.gov.uk/ukpga/2021/1/enacted/data.xml) returns the content of the **as enacted version** of the Pension Schemes Act 2021 as CLML.
* [https://www.legislation.gov.uk/ukpga/2021/1/part/1/data.xml](https://www.legislation.gov.uk/ukpga/2021/1/part/1/data.xml) returns the content of the **latest version of Part 1** of the Act as CLML.

The [CLML Reference Guide]() has guidance on how to interpret CLML.

Some documents are only available as PDF. For example, the Metropolis Water Act 1902 is (as of writing) only available as a PDF at [https://www.legislation.gov.uk/ukpga/Edw7/2/41/pdfs/ukpga_19020041_en.pdf](https://www.legislation.gov.uk/ukpga/Edw7/2/41/pdfs/ukpga_19020041_en.pdf). <!-- TODO You can find out if a document is available as PDF or as CLML by parsing the metadata for the document (see below). -->

<!-- TODO more sections, notes, etc. -->

### Access to legislation metadata

You can get metadata (information about an item of legislation) through the API.

The `<ukm:Metadata>` element in CLML <!--TODO link to explanation of namespaces--> contains information about the item of legislation and the version being viewed, including but not limited to:

* the title of the item
* the item's type, year and number
* any "alternative" formats of the item, such as a PDF
* any associated documents, such as Impact Assessments and Explanatory Memoranda
* the date(s) of enactment, making, laying and/or coming into force of the item (where present in the data)
* any powers to make secondary legislation conferred by the item (present only in [revised data]())
* any unapplied changes outstanding for the document

The CLML Reference Guide has guidance on how to interpret [metadata in CLML]().

If you only want the metadata for a document, the `/resources` sub-resource contains the metadata for the specified version of an item. For example: 

* [https://www.legislation.gov.uk/ukpga/1981/54/resources/data.xml](https://www.legislation.gov.uk/ukpga/1981/54/resources/1999-09-27/data.xml) contains the metadata for the current version of the Senior Courts Act 1981.
* [https://www.legislation.gov.uk/ukpga/1981/54/resources/1999-09-27/data.xml](https://www.legislation.gov.uk/ukpga/1981/54/resources/1999-09-27/data.xml) contains the metadata for the version of the Senior Courts Act 1981 dated 27/9/1999.

### Changes to legislation

The API provides lists of [changes made to legislation](https://www.legislation.gov.uk/changes), also known as "effects". You can request a list of changes to legislation by the type, year and number of the affected and/or affecting document, including information on:

 * the affected and affecting provisions of the items
 * the type of effect (e.g. "words substituted", "repealed", "restricted")
 * the in force date(s) of the effect
 * the geographical extent of the effect
 * whether the effect has been applied or will be applied

To get a list of effects, see the [Changes to legislation](/search.html#changes) sub-section of the "Search, lists and feeds" section.

<!--For more information on how to request lists of effects, see the changes section of our API reference.--> For more information on how to interpret effects, see the [effects section of the CLML reference guide]().

### Search, lists and feeds

You can search for legislation through the API using any of the features available on the search interface on the website. You can also retrieve the same lists of legislation through the API as through the website. 

The API returns the search results as an [Atom](https://en.wikipedia.org/wiki/Atom_(web_standard)) feed. The list is paginated, which means that the API only returns a fixed number of items in each response (the default is 20, which you can change by adding `results-count=N` to the [query string](https://en.wikipedia.org/wiki/Query_string)). Where there are more pages left in the feed, the response will contain a `<link rel="next">` element with a link to the next results page. 

By default the API returns items in order of their last modification date (the date on which an enacted or revised version was most recently published), most recent first.

For example:

* [https://www.legislation.gov.uk/ukpga/data.feed](https://www.legislation.gov.uk/ukpga/data.feed) returns the first page of the feed of UK Public General Acts, maximum 20 items per page.
* [https://www.legislation.gov.uk/primary+secondary?title=help](https://www.legislation.gov.uk/primary+secondary?title=help) returns the first page of the feed of UK legislation with "help" in the title, maximum 20 items per page.
* [https://www.legislation.gov.uk/all/2002/1-100?page=2](https://www.legislation.gov.uk/all/2002/1-100?page=2) returns the second page of the feed of legislation of all types with a year of 2002 and a number between 1 and 100, maximum 20 items per page.
* [https://www.legislation.gov.uk/uksi+wsi+ssi+nisr/data.feed?text=dogs&results-count=5](https://www.legislation.gov.uk/uksi+wsi+ssi+nisr/data.feed?text=dogs&results-count=5) returns a feed of Statutory Instruments (UK, Welsh and Scottish) and Northern Ireland Statutory Rules with the word "dogs" in the text, maximum 5 items per page.

For more information, see the section on [search, lists and feeds](/search.md).

## How can I use the API?

You can connect to our API using any HTTP client (such as a web browser, or an HTTP request library for your programming language). This page contains addresses for some example resources available through the API. The API <!--TODO except for the SPARQL endpoint--> only supports `GET` requests. 

We encourage users to use our API in their own applications, including crawling and bulk access, and whether commercial or non-commercial. The data in the API are available under open licences. For more information on licensing, see the License section of this guide.

### Fair Use Policy

We do have a [Fair Use Policy]() for the API. To use the API, you must follow the requirements of the policy: 

 * If you make requests to the API, they must specify a **user agent** (if you are making requests from a web browser it will specify a user agent automatically). <!-- TODO in future we may require that the user agent contains descriptive information such as a web address -->
 * We currently limit each IP address to 3,000 API requests every 5 minutes. If you want to download a large amount of legislation data at once, it may be quicker to use our [bulk downloads]() service, which allows you to download all or part of our set of legislation as a ZIP file.

### CORS

The API has [CORS (cross-origin resource sharing)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) enabled, which means you can make requests to the API from client-side Javascript applications running in a web browser.

### Caching

We [cache](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching) the output of the API for performance reasons, so sometimes there may be a delay between an update to our data and its appearance on the website or API.

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

The API returns legislation XML in the [CLML]() and [Akoma Ntoso]() dialects.

The API also generates PDFs from items of legislation and any part or version of them.

The API can provide pre-generated XHTML and HTML 5 snippets for you to use in your own applications.

For [lists of legislation](/search.html) and [effects](), the API returns feeds in Atom format.

#### XML is the recommended format

We recommend you request responses in XML format as this is normally easier to parse. You can request XML for legislation (as CLML) by appending `/data.xml` to the end of the URI, and XML for search results and lists (as Atom) by appending `/data.feed` to the end of the URI.

If you are not familiar with XML, we strongly recommend you read the [introduction to XML](#xml-intro) below to learn about its main features.

#### Content negotiation

To request a different representation of a resource, you can either:

 1. Specify a _subresource_ at the end of the URI path. For example, appending /data.xml to the end of the URI for a version of legislation requests that version as CLML (e.g. https://www.legislation.gov.uk/anaw/2013/1/data.xml requests the CLML version of 2013 anaw 1)
 2. Specify the desired content type in the `Accept` header of your request (e.g. make a request with the header `Accept: application/pdf` for `https://www.legislation.gov.uk/asp/2020/5/introduction` to get the introduction to 2020 asp 5 as a dynamically generated PDF).

We strongly recommend you specify a subresource to choose a representation, rather than vary the `Accept` header. The API may respond faster on average to requests that specify a subresource and use a common generic `Accept` header (e.g. `Accept: */*`) than those that use a specific `Accept` header because the API is more likely to be able to serve a response from the cache. (For an explanation of why this is the case, see the WHATWG article ["Why not content negotation?"](https://wiki.whatwg.org/wiki/Why_not_conneg#Server-side_choice_is_worse_for_intermediate_caches_than_browser-side_choice))

### Supported HTTP methods

The API currently only supports the `GET` HTTP method, which is the default for most applications that use HTTP.

### Response codes

The API uses HTTP response codes as specified in [RFC 9110 (HTTP Semantics)](https://www.rfc-editor.org/rfc/rfc9110.html#name-status-codes).

Most requests to the API should return `200 OK`. Some other common response codes the API returns are:

 * `300 Multiple Choices`: The API will return this code if you make a request to a URI that identifies more than one item or section of legislation (e.g. http://www.legislation.gov.uk/id/ukpga/1955/18 identifies both the Army Act 1955 and the Aliens' Employment Act 1955). The response will contain an HTML list with links to the different options.
 * `403 Forbidden`: The API will return this code if you exceed the rate limit (see the section on our [Fair Use Policy](#fair-use) above). Your application should slow down or stop making requests until it is under the rate limit again. The API also returns `403 Forbidden` if we have blocked requests from your IP address. If you continue to receive `403 Forbidden` responses to your requests, please [contact us](). 
 * `400 Bad Request`: The API will return this code if you make a request for an item of legislation and specify a year or number that is out of the acceptable range for that type of legislation. The API may also return this code if the request is malformed.
 * `500 Internal Server Error`: The API may return this code if there is a temporary error within the service, or if it cannot process the requested document due to an error in the data. If you get this response more than once for a request to a specific resource, please [contact us]() with details of the resource.
 * `503 Service Unavailable` or `504 Gateway Timeout`: The API returns these codes if the legislation.gov.uk service is over capacity or is experiencing a temporary interruption of service. We recommend you wait at least 5 minutes before trying your request again. If you continue to receive this response for a request to a specific resource, please [contact us]() with details of the resource.

## An introduction to XML <a id="xml-intro"></a>

The underlying format of most structured data on legislation.gov.uk is [XML](https://www.w3.org/XML/). We use XML because it is a good format for electronic publishing: 

 * XML allows a text document to contain arbitrary semantic markup and metadata.
 * We can transform XML documents into HTML, PDF and other formats using [XSL](https://www.w3.org/Style/XSL/).

### Structure of an XML document

An XML document consists of a tree of nodes. The most common of these are elements, attributes, and text nodes.

### Elements

An element is denoted by either a pair of tags (e.g. `<Text>Hello</Text>`) or a single “self-closing” tag (e.g. `<Character Name="NonBreakingSpace"/>`). 

An element may contain other nodes in between its opening and closing tags, such as text nodes (e.g. `Hello` in the first example above) or other elements. These child nodes may appear in an arbitrary order (e.g. `<A X="Y">1 <B>2 <C Z="/">3</C> 4</B></A>`). Elements cannot partially overlap with other elements (i.e. `<A>over<B></A>lap</B>` is not possible in XML).

An element has a name, which consists of a local name (e.g. "Text") and optionally a namespace (see the section on [namespaces](#namespaces) below).

Every XML document must contain exactly one root element, which must be the first node to appear in an XML document (apart from the optional `<?xml ... ?>` processing instruction, which indicates the XML version and character encoding for the file).

### Attributes

An attribute is denoted by a name, followed by a `=` character and a value enclosed in double or single quotes (e.g. `id="section-1"`). An element may contain one or more attributes within the opening tag (e.g. `<P1 id="section-1"> ... </P1>` or `<Citation Class="WelshStatutoryInstrument" Year="2002" Number="47">W.S.I. 2002/31</Citation>`). 

An attribute can only contain text, and cannot contain other nodes. Attributes may only appear on the opening tag, not the closing tag.

The name of an attribute consists of a local name, and optionally a namespace (see below).

### Namespaces

A namespace is an arbitrary URI that can form part of the name of an element, or (less commonly) of an attribute. For example, most elements in XML documents on legislation.gov.uk have the namespace `http://www.legislation.gov.uk/namespaces/legislation`. Namespaces make it possible to create and use XML files that combine different XML languages, which can each specify their own namespace(s) to distinguish their elements and attributes from those of other languages. In the XML our API provides, almost all elements use namespaces.

An XML document can declare the namespace of an element using the `xmlns` attribute. Any child elements (but not attributes) inherit the same namespace, unless they declare their own namespace or use a prefix (see below). The below example shows an element with the local name `P1` in the namespace `http://www.legislation.gov.uk/namespaces/legislation`, with two child elements `Pnumber` and `P1para`, also both in the namespace `http://www.legislation.gov.uk/namespaces/legislation`:

```
<P1 xmlns="http://www.legislation.gov.uk/namespaces/legislation">
  <Pnumber>...</Pnumber>
  <P1para>...</P1para>
</P1>
```

An XML document can also declare that a prefix represents a particular namespace using the `xmlns:[NS]` attribute, where `[NS]` is the prefix to be used. In the below example, the root element declares prefixes that are used by descendent elements, and both the root `Legislation` element and its child `Primary` element are in the namespace `http://www.legislation.gov.uk/namespaces/legislation`, despite having different prefixes:

```
<Legislation xmlns="http://www.legislation.gov.uk/namespaces/legislation" xmlns:leg="http://www.legislation.gov.uk/namespaces/legislation" xmlns:ukm="http://www.legislation.gov.uk/namespaces/metadata" xmlns:dct="http://purl.org/dc/terms/">
  <ukm:Metadata>
    <dct:valid>2022-09-30</dct:valid>
  </ukm:Metadata>
  <leg:Primary>...</leg:Primary>
```
 
Note that different documents (and different elements within a document) may declare their own prefix for any namespace, or declare a namespace as the default one with no prefix. For example, various CLML documents use the `leg` and `ukl` namespaces to represent the `http://www.legislation.gov.uk/namespaces/legislation` namespace, but most declare it as the default namespace using `xmlns` and then do not use a prefix at all (and some documents use multiple prefixes for the same namespace in different places). Make sure when you parse XML that you are checking for both the local name and the actual *namespace*, not a prefix or just a local name.

### Parsing XML

We strongly recommend you use a proper XML parser to parse XML. XML has many complicated rules and it is easy to get them wrong if you try and write your own. Using a supported XML parser is the most reliable way to extract data from an XML document.

Some popular XML parser libraries and classes include:

 * For Python, the [ElementTree](https://docs.python.org/3/library/xml.etree.elementtree.html) module in the standard library, or the [BeautifulSoup]() library
 * For Javascript, the [DOMParser class](https://developer.mozilla.org/en-US/docs/Web/API/DOMParser) (only in web browsers), or the [xml2js](https://www.npmjs.com/package/xml2js) module
 * For .NET (C#), the [System.Xml](https://docs.microsoft.com/en-us/dotnet/standard/data/xml/) classes in the standard library
 * For Java, the [DocumentBuilder](https://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/DocumentBuilder.html) or [SAXParser](https://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/SAXParser.html) classes in the `javax.xml.parsers` package
 * For Go, the [xml](https://pkg.go.dev/encoding/xml) package in the standard library
 * For Rust, the [minidom](https://crates.io/crates/minidom) or [quickxml](https://crates.io/crates/quick-xml) crates
