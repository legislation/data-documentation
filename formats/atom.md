# Atom feeds

We provide lists of [legislation](/api/search.md#listings) and [effects](/api/search.md#changes) in [Atom](http://tools.ietf.org/html/rfc4287).

We also provide the [Publication Log](/api/publication-log.md), which is a feed of all updates to the website, including the publication and republication of individual versions of legislation, associated documents and effects, plus the withdrawal of legislation and associated documents.

## Common elements

We use the [Feed Paging and Archiving](http://tools.ietf.org/html/rfc5005) link relations of `first`, `previous`, `next` and `last` to enable navigation through pages of results when there is more than one page available.

We use the [OpenSearch Response Elements](https://github.com/dewitt/opensearch/blob/master/opensearch-1-1-draft-6.md#opensearch-response-elements):

* `<opensearch:Query>` to indicate the query that was made; the attributes provide details of the search parameters
* `<opensearch:startIndex>` to indicate the index of the first item in the current page
* `<opensearch:itemsPerPage>` to indicate how many items are being displayed on a page

We also use some custom elements on the feed, in the `http://www.legislation.gov.uk/namespaces/legislation` namespace:

* `<leg:page>` is the index number for the page itself
* `<leg:morePages>` is an approximation of the number of pages that are left to display

## Legislation feeds

The feeds of legislation (for example, https://www.legislation.gov.uk/uksi/2020 lists all UK Statutory Instruments with a year of 2020) additionally have the following extra elements:

* `<opensearch:totalResults>` to indicate the total number of results found
* `<leg:facets>` provides faceting information that can be used to guide further searches into the data. The `<leg:facetTypes>` child wraps possible further searches based on type, `<leg:facetYears>` on years and `<leg:facetHundreds>` on number. The items within these wrappers each have a type, year or hundred attribute that indicates the value for the facet; an href attribute that can be used to narrow the search; and a value attribute that indicates how many items of legislation have the given value. The total attribute on the `<leg:facetYear>` element indicates the total number of items within the year, regardless of the rest of the search.

The list also provides the following metadata in the `http://www.legislation.gov.uk/namespaces/metadata` namespace for each item of legislation:

* `<ukm:DocumentMainType>` gives the type of the legislation
* `<ukm:Year>` gives the year of the legislation
* `<ukm:Number>` gives the number of the legislation
* `<ukm:CreationDate>` gives the enactment or made date of the legislation

For each entry, we provide links to the [XML](formats/xml.md) (CLML and Akoma Ntoso) and [HTML](/developer/formats/html.md) (XHTML and HTML5) formats of the legislation as well as to the XML [table of contents](/developer/formats/xml#toc) for the legislation. For example:

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

## Changes to legislation feeds

The changes to legislation feeds list [effects](model/effects.md). Each entry contains a single effect, represented by a `<ukm:Effect>` element (in the `http://www.legislation.gov.uk/namespaces/metadata` namespace). You can find out more about the XML representation of effects in the [Effects section of the CLML user guide](https://legislation.github.io/clml-schema/userguide.html#effects).

For example, below is an effect from [paragraph 2(3) of Schedule 7 of the Occupational Pension Schemes (Collective Money Purchase Schemes) Regulations 2022](http://www.legislation.gov.uk/id/uksi/2022/255/schedule/7/paragraph/2/3), inserting a new regulation 32EA into the [Occupational and Personal Pension Schemes (Automatic Enrolment) Regulations 2010](http://www.legislation.gov.uk/id/uksi/2010/772):

```
<entry>
	<id>http://www.legislation.gov.uk/changes/affected/uksi/2010/772/affecting/uksi/2022/255/key-3d258ed3180029fce9dc520cd9666d80/modified/2022-10-12T10:34:35Z</id>
	<content type="text/xml">
		<ukm:Effect EffectId="key-3d258ed3180029fce9dc520cd9666d80" AffectedClass="UnitedKingdomStatutoryInstrument" AffectedURI="http://www.legislation.gov.uk/id/uksi/2010/772" AffectingURI="http://www.legislation.gov.uk/id/uksi/2022/255" AffectingClass="UnitedKingdomStatutoryInstrument" URI="http://www.legislation.gov.uk/id/effect/key-3d258ed3180029fce9dc520cd9666d80" Row="74" Type="inserted" Applied="false" RequiresApplied="true" AffectedProvisions="reg. 32EA" AffectingEffectsExtent="E+W+S" AffectingYear="2022" AffectingNumber="255" AffectingProvisions="Sch. 7 para. 2(3)" AffectedYear="2010" AffectedNumber="772" Modified="2022-10-12T10:34:35Z">
			<ukm:AffectedTitle>The Occupational and Personal Pension Schemes (Automatic Enrolment) Regulations 2010</ukm:AffectedTitle>
			<ukm:AffectedProvisions>
				<ukm:Section xmlns:err="http://www.legislation.gov.uk/namespaces/error" Ref="regulation-32EA" URI="http://www.legislation.gov.uk/id/uksi/2010/772/regulation/32EA" err:Ref="Section missing in legislation" Missing="true">reg. 32EA</ukm:Section>
			</ukm:AffectedProvisions>
			<ukm:AffectingTitle>The Occupational Pension Schemes (Collective Money Purchase Schemes) Regulations 2022</ukm:AffectingTitle>
			<ukm:AffectingProvisions>
				<ukm:Section Ref="schedule-7" URI="http://www.legislation.gov.uk/id/uksi/2022/255/schedule/7">Sch. 7 </ukm:Section>
				<ukm:Section Ref="schedule-7-paragraph-2-3" URI="http://www.legislation.gov.uk/id/uksi/2022/255/schedule/7/paragraph/2/3">para. 2(3)</ukm:Section>
			</ukm:AffectingProvisions>
			<ukm:CommencementAuthority>
				<ukm:Section Ref="regulation-1-3" URI="http://www.legislation.gov.uk/id/uksi/2022/255/regulation/1/3">reg. 1(3)</ukm:Section>
			</ukm:CommencementAuthority>
			<ukm:InForceDates>
				<ukm:InForce Applied="false" Date="2022-08-01" Qualification="wholly in force"/>
			</ukm:InForceDates>
		</ukm:Effect>
	</content>
	<title>The Occupational Pension Schemes (Collective Money Purchase Schemes) Regulations 2022 effect on The Occupational and Personal Pension Schemes (Automatic Enrolment) Regulations 2010</title>
	<updated>2022-10-12T10:34:35Z</updated>
	<author>
		<name>editorial.legislation.gov.uk</name>
	</author>
</entry>
```

## Publication Log

The Publication Log feeds list publication and withdrawal events for legislation and associated documents, and publication events for effects. Each entry relates to:

 * for legislation and associated documents, the (re)publication or withdrawal of an individual resource on legislation.gov.uk, such as the XML for the enacted/made version or a specific revised Point in Time for an item of legislation, or a PDF of an item of legislation or associated document;
 * for effects, the (re)publication of new or updated effects within or against an item of legislation

As well as the common feed elements listed above, the Publication Log also uses elements in the `http://www.legislation.gov.uk/namespaces/publication-log` namespace, normally using the prefix `pbl:`. For more information, refer to the [Publication Log](/api/publication-log.md) section of this documentation.

For example, below is an entry relating to the publication of the XML for the 21/7/2022 revised Point in Time of the Sentencing Act 2022:

```
<entry>
	<id>http://www.legislation.gov.uk/ukpga/2020/17/2022-07-21/data.xml/published/2023-07-06T00:39:45.931518+01:00</id>
	<dc:identifier>http://www.legislation.gov.uk/id/ukpga/2020/17</dc:identifier>
	<title>Sentencing Act 2020</title>
	<author>
		<name>editorial.legislation.gov.uk</name>
	</author>
	<published>2022-09-06T00:22:47.213567+01:00</published>
	<updated>2023-07-06T00:39:45.931518+01:00</updated>
	<ukm:DocumentCategory Value="primary"/>
	<ukm:DocumentMainType Value="UnitedKingdomPublicGeneralAct"/>
	<ukm:Year Value="2020"/>
	<ukm:Number Value="17"/>
	<pbl:ContentType>legislation</pbl:ContentType>
	<pbl:Event>published</pbl:Event>
	<pbl:Republished>true</pbl:Republished>
	<pbl:New>false</pbl:New>
	<pbl:Document>http://www.legislation.gov.uk/ukpga/2020/17/2022-07-21</pbl:Document>
	<link rel="alternate" type="application/rdf+xml" href="http://www.legislation.gov.uk/ukpga/2020/17/2022-07-21/data.rdf" title="RDF/XML"/>
	<link rel="alternate" type="application/akn+xml" href="http://www.legislation.gov.uk/ukpga/2020/17/2022-07-21/data.akn" title="AKN"/>
	<link rel="alternate" type="application/xhtml+xml" href="http://www.legislation.gov.uk/ukpga/2020/17/2022-07-21/data.xht" title="HTML snippet"/>
	<link rel="alternate" type="application/akn+xhtml" href="http://www.legislation.gov.uk/ukpga/2020/17/2022-07-21/data.html" title="HTML5 snippet"/>
	<link rel="alternate" type="text/html" href="http://www.legislation.gov.uk/ukpga/2020/17/2022-07-21/data.htm" title="Website (XHTML) Default View"/>
	<link rel="alternate" type="application/pdf" href="http://www.legislation.gov.uk/ukpga/2020/17/2022-07-21/data.pdf" title="PDF"/>
	<pbl:Item_Published>http://www.legislation.gov.uk/ukpga/2020/17/2022-07-21/data.xml</pbl:Item_Published>
	<pbl:Format>xml</pbl:Format>
	<dc:language>en</dc:language>
</entry>
```