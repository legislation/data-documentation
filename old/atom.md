# Atom Feeds

We provide [lists](/developer/searching#listing) of legislation in [Atom](http://tools.ietf.org/html/rfc4287).

We use the [Feed Paging and Archiving](http://tools.ietf.org/html/rfc5005) link relations of 'first', 'previous', 'next' and 'last' to enable navigation through pages of results when there is more than one page available.

We use the [OpenSearch Response Elements:](http://www.opensearch.org/Specifications/OpenSearch/1.1#OpenSearch_response_elements)

*   `<opensearch:Query>` to indicate the query that was made; the `leg:*` attributes provide details of the search parameters
*   `<opensearch:totalResults>` to indicate the total number of results found
*   `<opensearch:startIndex>` to indicate the index of the first item in the current page
*   `<opensearch:itemsPerPage>` to indicate how many items are being displayed on a page

We also use some custom elements on the feed, in the `http://www.legislation.gov.uk/namespaces/legislation` namespace:

*   `<leg:page>` is the index number for the page itself
*   `<leg:morePages>` is an approximation of the number of pages that are left to display
*   `<leg:facets>` provides faceting information that can be used to guide further searches into the data. The `<leg:facetTypes>` child wraps possible further searches based on type, `<leg:facetYears>` on years and `<leg:facetHundreds>` on number. The items within these wrappers each have a `type`, `year` or `hundred` attribute that indicates the value for the facet; an `href` attribute that can be used to narrow the search; and a `value` attribute that indicates how many items of legislation have the given value. The `total` attribute on the `<leg:facetYear>` element indicates the total number of items within the year, regardless of the rest of the search.

As well as the usual information about each item of legislation that's listed, the following metadata is also provided within the `http://www.legislation.gov.uk/namespaces/metadata` namespace:

*   `<ukm:DocumentMainType>` gives the type of the legislation
*   `<ukm:Year>` gives the year of the legislation
*   `<ukm:Number>` gives the number of the legislation
*   `<ukm:CreationDate>` gives the enactment or made date of the legislation

For each entry, we provide links to the [XML](/developer/formats/xml), [RDF/XML](/developer/formats/rdf) and [HTML](/developer/formats/html) formats of the legislation as well as to the XML [table of contents](/developer/formats/xml#toc) for the legislation. For example:

```
<entry>
	<id>http://www.legislation.gov.uk/id/ukpga/1985/67</id>
	<title>Transport Act 1985</title>
	<link rel="self" href="http://www.legislation.gov.uk/id/ukpga/1985/67" />
	<link href="http://www.legislation.gov.uk/ukpga/1985/67" />
	<link rel="alternate" type="application/xml"
		href="http://www.legislation.gov.uk/ukpga/1985/67/data.xml" title="XML" />
	<link rel="alternate" type="application/rdf+xml"
		href="http://www.legislation.gov.uk/ukpga/1985/67/data.rdf" title="RDF/XML" />
	<link rel="alternate" type="application/xhtml+xml"
		href="http://www.legislation.gov.uk/ukpga/1985/67/data.htm" title="HTML snippet" />
	<link rel="alternate" type="application/pdf"
		href="http://www.legislation.gov.uk/ukpga/1985/67/data.pdf" title="PDF" />
	<link rel="http://purl.org/dc/terms/tableOfContents" type="application/xml"
		href="http://www.legislation.gov.uk/ukpga/1985/67/contents" />
	<author><name /></author>
	<updated>2010-07-21T01:00:00+01:00</updated>
	<ukm:DocumentMainType Value="UnitedKingdomPublicGeneralAct" />
	<ukm:Year Value="1985" />
	<ukm:Number Value="67" />
	<ukm:CreationDate Date="1985-10-30" />
	<category term="Taxi and minicab licences" />
	<category term="Bus operators" />
	<category term="Public transport" />
	<category term="Buses" />
	<category term="Transport for disabled people" />
	<summary>An Act to amend the law relating to road passenger transport; to make provision for the transfer of the operations of the National Bus Company to the private sector; to provide for the reorganisation of passenger transport in the public sector; to provide for local and central government financial support for certain passenger transport services and travel concessions; to make further provision with respect to the powers of London Regional Transport; to make new provision with respect to the constitution, powers and proceedings of the Transport Tribunal; to make provision with respect to grants payable under section 92 of the Finance Act 1965; to establish a Disabled Persons Transport Advisory Committee; and for connected purposes.</summary>
</entry>
```