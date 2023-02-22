# An introduction to XML

The underlying format of most structured data on legislation.gov.uk is [XML](https://www.w3.org/XML/). We use XML because it is a good format for electronic publishing and for marking up text with metadata. XML allows a text document to contain arbitrary semantic markup and metadata, and there are many applications that support XML workflows for editing, validation against schemas and transformation into other formats (such as HTML and PDF).

## Structure of an XML document

An XML document consists of a tree of nodes. The most common of these are elements, attributes, and text nodes.

## Elements

An element is denoted by either a pair of tags (e.g. `<Text>Hello</Text>`) or a single “self-closing” tag (e.g. `<Character Name="NonBreakingSpace"/>`). 

An element may contain other nodes in between its opening and closing tags, such as text nodes (e.g. `Hello` in the first example above) or other elements. These child nodes may appear in an arbitrary order (e.g. `<A X="Y">1 <B>2 <C Z="/">3</C> 4</B></A>`). Elements cannot partially overlap with other elements (i.e. `<A>over<B></A>lap</B>` is not permitted in XML).

An element has a name, which consists of a local name (e.g. "Text") and optionally a namespace (see the section on [namespaces](#namespaces) below).

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
 
Note that different documents (and different elements within a document) may declare their own prefix for any namespace, or declare a namespace as the default one with no prefix. For example, various CLML documents use the `leg` and `ukl` namespaces to represent the `http://www.legislation.gov.uk/namespaces/legislation` namespace, but most declare it as the default namespace using `xmlns` and then do not use a prefix at all (and some documents use multiple prefixes for the same namespace in different places). Make sure when you parse XML that you are checking for both the local name and the actual *namespace*, not a prefix or just a local name.

## Parsing XML

We strongly recommend you use a proper XML parser to parse XML. XML has many complicated rules and it is easy to get them wrong if you try and write your own parsing code. Using a supported XML parser is the most reliable way to extract data from an XML document.

Some popular XML parser libraries and classes include:

 * For Python, the [ElementTree](https://docs.python.org/3/library/xml.etree.elementtree.html) module in the standard library, or the [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/) library
 * For Javascript, the [DOMParser class](https://developer.mozilla.org/en-US/docs/Web/API/DOMParser) (only in web browsers), or the [xml2js](https://www.npmjs.com/package/xml2js) module
 * For .NET (C#), the [System.Xml](https://docs.microsoft.com/en-us/dotnet/standard/data/xml/) classes in the standard library
 * For Java, the [DocumentBuilder](https://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/DocumentBuilder.html) or [SAXParser](https://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/SAXParser.html) classes in the `javax.xml.parsers` package
 * For Go, the [xml](https://pkg.go.dev/encoding/xml) package in the standard library
 * For Rust, the [minidom](https://crates.io/crates/minidom) or [quickxml](https://crates.io/crates/quick-xml) crates