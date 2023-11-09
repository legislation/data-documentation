# An introduction to XML

The underlying format of most structured data on legislation.gov.uk is [XML](https://www.w3.org/XML/). We use XML because it is a good format for electronic publishing and for marking up text with metadata. XML allows a text document to contain arbitrary semantic markup and metadata, and there are many applications that support XML workflows for editing, validation against schemas and transformation into other formats (such as HTML and PDF).

## Structure of an XML document

An XML document consists of a tree of nodes. The most common of these are elements, attributes, and text nodes.

## Elements

An element is denoted by either a pair of tags (e.g. `<Text>Hello</Text>`) or a single “self-closing” tag (e.g. `<Character Name="NonBreakingSpace"/>`). 

An element may contain other nodes in between its opening and closing tags, such as text nodes (e.g. `Hello` in the first example above) or other elements. These child nodes may appear in an arbitrary order (e.g. `<A X="Y">1 <B>2 <C Z="/">3</C> 4</B></A>`). Elements cannot partially overlap with other elements (i.e. `<A>over<B></A>lap</B>` is not permitted in XML).

An element has a name, which consists of a local name (e.g. “Text”) and optionally a namespace (see the section on [namespaces](#namespaces) below).

Every XML document must contain exactly one root element, which must be the first node to appear in an XML document (apart from the optional `<?xml ... ?>` processing instruction, which indicates the XML version and character encoding for the file).

## Attributes

An attribute is denoted by a name, followed by a `=` character and a value enclosed in double or single quotes (e.g. `id="section-1"`). An element may contain one or more attributes within the opening tag (e.g. `<P1 id="section-1"> ... </P1>` or `<Citation Class="WelshStatutoryInstrument" Year="2002" Number="47">W.S.I. 2002/31</Citation>`). 

An attribute can only contain text, and cannot contain other nodes. Attributes may only appear on the opening tag, not the closing tag.

The name of an attribute consists of a local name, and optionally a namespace (see below).

## Namespaces

A namespace is an arbitrary URI that can form part of the name of an element, or (less commonly) of an attribute. For example, most elements in XML documents on legislation.gov.uk have the namespace `http://www.legislation.gov.uk/namespaces/legislation`. Namespaces make it possible to create and use XML files that combine different XML languages, which can each specify their own namespace(s) to distinguish their elements and attributes from those of other languages. In the XML our API provides, almost all elements use namespaces.

An XML document can declare the namespace of an element using the `xmlns` attribute. Any child elements (but not attributes) inherit the same namespace, unless they declare their own namespace or use a prefix (see below). The below example shows an element with the local name `P1` in the namespace `http://www.legislation.gov.uk/namespaces/legislation`, with two child elements `Pnumber` and `P1para`, also both in the namespace `http://www.legislation.gov.uk/namespaces/legislation`:

```
<P1 xmlns="http://www.legislation.gov.uk/namespaces/legislation">
  <Pnumber>...</Pnumber>
  <P1para>...</P1para>
</P1>
```

### Common namespaces in our data

The legislation.gov.uk dataset uses multiple XML namespaces, including but not limited to the following:

|Namespace|Namespace URI|Default prefix*|
|---|---|---|
|Legislation|`http://www.legislation.gov.uk/namespaces/legislation`|`leg:`|
|Metadata|`http://www.legislation.gov.uk/namespaces/metadata`|`ukm:`|
|Publication Log|`http://www.legislation.gov.uk/namespaces/publication-log` (see [Publication Log](../api/publication-log.md))|`pbl:`|
|Dublin Core Elements|`http://purl.org/dc/elements/1.1/`|`dc:`|
|Dublin Core Terms|`http://purl.org/dc/terms/`|`dct:`|
|Atom|`http://www.w3.org/2005/Atom`|`atom:`|
|XHTML|`http://www.w3.org/1999/xhtml`|No prefix|

\* Although most legislation.gov.uk XML data uses the default prefixes for these namespaces, some XML data use a different prefix or none at all, and these prefixes may change in future or vary between different contexts, even within a single document. **You must not use prefixes to identify elements or attributes unless you are parsing the XML with a properly configured XML parser.** Read carefully the following sections on prefixes, particularly [Prefixes are context-dependent](#prefixes-are-context-dependent) and [A note on namespaces in XPath](#a-note-on-namespaces-in-xpath).

### Namespace prefixes

An XML document can also declare that a prefix represents a particular namespace using the `xmlns:[NS]` attribute, where `[NS]` is the prefix to be used. In the below example, the root element declares prefixes that are used by descendent elements, and both the root `Legislation` element and its child `Primary` element are in the namespace `http://www.legislation.gov.uk/namespaces/legislation`, despite having different prefixes:

```
<Legislation xmlns="http://www.legislation.gov.uk/namespaces/legislation"
             xmlns:leg="http://www.legislation.gov.uk/namespaces/legislation" 
             xmlns:ukm="http://www.legislation.gov.uk/namespaces/metadata" 
             xmlns:dct="http://purl.org/dc/terms/">
  <ukm:Metadata>
    <dct:valid>2022-09-30</dct:valid>
  </ukm:Metadata>
  <leg:Primary>...</leg:Primary>
</Legislation>
```

### Prefixes are context-dependent
 
Note that different documents (and different elements within a document) may declare their own prefix for any namespace, or declare a namespace as the default one with no prefix. 

For example, various CLML documents use the `leg` and `ukl` namespaces to represent the `http://www.legislation.gov.uk/namespaces/legislation` namespace, but most declare it as the default namespace using `xmlns` and then do not use a prefix at all (and some documents use multiple prefixes for the same namespace in different places). 

Make sure when you parse XML that you are checking for both the local name and the actual *namespace*, not a prefix or just a local name. When processing or querying XML, you may need to tell your XML processor which prefix corresponds to which namespace. For an example, see the [a note on XPath namespace prefixes](#a-note-on-xpath-namespace-prefixes) section below.

## Parsing XML

We strongly recommend you use a proper XML parser to parse XML. XML has many complicated rules and it is very easy to get them wrong if you try and write your own parsing code. Using a supported XML parser is the most reliable way to extract data from an XML document.

Some popular XML parser libraries and classes include:

 * For Python, the [ElementTree](https://docs.python.org/3/library/xml.etree.elementtree.html) module in the standard library, the [lxml](https://pypi.org/project/lxml/) library, or the [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/) library _(note that ElementTree does not fully support [XPath](#xpath))_
 * For Javascript, the [DOMParser class](https://developer.mozilla.org/en-US/docs/Web/API/DOMParser) (only in web browsers), or the [xmldom](https://www.npmjs.com/package/@xmldom/xmldom) package (which implements the DOMParser interface for Node and other non-browser JS runtimes)
 * For .NET (C#), the [System.Xml](https://docs.microsoft.com/en-us/dotnet/standard/data/xml/) classes in the standard library
 * For Java, the [DocumentBuilder](https://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/DocumentBuilder.html) or [SAXParser](https://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/SAXParser.html) classes in the `javax.xml.parsers` package
 * For Go, the [xml](https://pkg.go.dev/encoding/xml) package in the standard library _(note that this package does not provide support for [XPath](#xpath))_
 * For Rust, the [quickxml](https://crates.io/crates/quick-xml) crate _(note that this crate does not provide support for [XPath](#xpath))_

## Navigating XML with XPath<a id="xpath"></a>

The [XPath](https://en.wikipedia.org/wiki/XPath) language is a simple, flexible and powerful syntax for querying and transforming XML documents.

An XPath _location path_ is a type of XPath expression that identifies part(s) of an XML document. For example, the following location path identifies all `<P1>` elements with an `id` attribute that are the descendant of a `<Pblock>` element anywhere within a `<Secondary>` child of a `<Legislation>` element:

`/child::leg:Legislation/child::leg:Secondary/descendant::leg:Pblock/descendant::leg:P1[exists(@id)]`

This can be written in an abbreviated form as:

`/leg:Legislation/leg:Secondary//leg:Pblock//leg:P1[@id]`

XPath has many other features. Most XML parsers that provide XPath support only support XPath 1.0, which has fewer features than the latest versions. To find out more about the features of XPath 1.0, read the [XPath 1.0 specification](https://www.w3.org/TR/1999/REC-xpath-19991116/) and the [syntax and semantics section of the XPath article on Wikipedia](https://en.wikipedia.org/wiki/XPath#Syntax_and_semantics_(XPath_1.0)).

### A note on namespaces in XPath

In the above examples, each step of the XPath location path expression has a prefix ending with a colon (in those examples, the only prefix used is `leg:`). As explained above in the [namespaces](#namespaces) section, the names of XML elements (and sometimes attributes) may have a namespace. A prefix in an XML element/attribute name indicates that its namespace is the one the current element (or one of its ancestors) declares the prefix to represent.

The relationship between a prefix and a namespace is context-dependent and may vary between documents and even elements within a document, and an element may have a namespace without a prefix if a default namespace is declared. As a result, a namespace prefix in an XPath expression is meaningless unless the resolver of the expression is told what the prefix means, and a resolver will treat the absence of a prefix as indicating “no namespace“ unless told otherwise. If you fail to register namespaces prefixes with an XPath resolver before using it, you may find that either your XPath expressions fail to return the desired results or cause the application to complain that the expression contains an unrecognized prefix and stop.

To avoid writing XPath expressions that don’t work, make sure that you:

* know what the namespace URI is for each element you want to query—if there is a prefix look for the value of the `xmlns:[prefix]` attribute on the target element or one of its ancestors, and if there is no prefix look for the value of the `xmlns` attribute instead;
* provide the XPath resolver with a set of prefixes corresponding to the namespaces you need to use in your XPath expression—for example, the <code>[document.evaluate()](https://developer.mozilla.org/en-US/docs/Web/API/Document/evaluate)</code> method in Javascript takes a `namespaceResolver` parameter that accepts a function taking a prefix string and returning the namespace URI corresponding to that prefix (or returns the default namespace if `null` is provided); and
* use the prefix you’ve provided for each namespace in the appropriate places in your XPath expression.