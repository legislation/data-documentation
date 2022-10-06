# XML Format

We provide the content of legislation in XML format using a [Legislation Schema](/schema/legislation.xsd) that includes both metadata and the content of legislation. The Legislation Schema uses [Dublin Core](http://dublincore.org/documents/dces/) for metadata, [XHTML](http://www.w3.org/TR/xhtml1/) for tables and [MathML](http://www.w3.org/Math/) for formulae.

Both the table of contents and the full content of the legislation includes links to other parts of the legislation. The `IdURI` attribute provides the [identifier URI](/developer/uris#identifiers) for the section. This URI identifies the section, but not the particular version that should be linked to from the view of the legislation that you are looking at. The `DocumentURI` attribute provides the [document URI](/developer/uris#documents) for the section, which includes any selected extent and the currently viewed version.

## Entire Items

When an entire piece of legislation is requested using a URL that contains a version such as `http://www.legislation.gov.uk/ukpga/1985/67/2003-04-01`, the legislation will be returned in its entirety, including sections that were not in force on the given date, which will including any prospective sections. Using the keyword `prospective` in place of the date will indicate how the legislation will look if all prospective amendments are applied in the future. A URL without a date will give you the current version of the legislation, which is the same as using today's date in the URI.

Within the XML, any sections that aren't valid at the date requested have a `Match="false"` attribute. The `Status` attribute indicates the status of the section at the requested date, which can be `Prospective` (the section hasn't yet come into force on that date), `Repealed` or `Discarded` (a section which was never brought into force and was later repealed). Other attributes, such as `RestrictStartDate`, `RestrictEndDate` and `RestrictExtent` provide additional information about the validity of the section.

Some items of legislation are very large and therefore take a long time to retrieve. **We recommend avoiding requesting entire items of legislation.**

## Sections

When a section of legislation is requested using a URL such as `http://www.legislation.gov.uk/ukpga/1985/67/section/6`, the section will be provided in context, including basic information about its ancestors (such as the part and chapter that it's contained in), their numbers, titles and links to them through the `DocumentURI` and `IdentifierURI` attributes. This information can help in the construction of breadcrumb trails, for example. The metadata will only include unapplied effects that would apply to that section or to the entire piece of legislation.

Where there are concurrent sections with different geographical extents, the body of the XML will contain only one of the versions of the section, and an `AltVersionRefs` attribute will point to the alternative version for that section which is held in the `<Versions>` element.

## Tables of Contents

When a contents page is requested using a URL such as `http://www.legislation.gov.uk/ukpga/1985/67/contents` (which is the usual document retrieved after a request to an [identifier URI](/developer/uris#identifiers)), you will get back a table of contents for the legislation. The table of contents is a combination of the contents of the requested version, previous versions and, if you're looking at the current table of contents, prospective changes to the legislation.

Within the table of contents, any sections that aren't valid at the date requested have a `Match="false"` attribute. The `Status` attribute indicates the status of the section at the requested date, which can be `Prospective` (the section hasn't yet come into force on that date), `Repealed` or `Discarded` (a section which was never brought into force and was later repealed). Other attributes, such as `RestrictStartDate`, `RestrictEndDate` and `RestrictExtent` provide additional information about the validity of the section.

For example, the table of contents at `http://www.legislation.gov.uk/ukpga/1975/30/contents` includes a Part whose content has been repealed:

```
<ContentsPart ContentRef="part-II"
  DocumentURI="http://www.legislation.gov.uk/ukpga/1975/30/part/II"
  IdURI="http://www.legislation.gov.uk/id/ukpga/1975/30/part/II" RestrictExtent="S"
  RestrictStartDate="2002-10-23">
  <ContentsNumber>Part II</ContentsNumber>
  <ContentsTitle> Local Administration</ContentsTitle>
  <ContentsItem Match="false" Status="Repealed" ContentRef="section-21"
    DocumentURI="http://www.legislation.gov.uk/ukpga/1975/30/section/21/2002-10-22"
    IdURI="http://www.legislation.gov.uk/id/ukpga/1975/30/section/21" RestrictExtent="S"
    RestrictEndDate="2002-10-23" ConfersPower="true">
    <ContentsNumber>21</ContentsNumber>
    <ContentsTitle> Commissioner for Local Administration</ContentsTitle>
  </ContentsItem>
  <ContentsItem Match="false" Status="Repealed" ContentRef="section-22"
    DocumentURI="http://www.legislation.gov.uk/ukpga/1975/30/section/22/2002-10-22"
    IdURI="http://www.legislation.gov.uk/id/ukpga/1975/30/section/22" RestrictExtent="S"
    RestrictEndDate="2002-10-23" ConfersPower="true">
    <ContentsNumber>22</ContentsNumber>
    <ContentsTitle> Body to be designated by Secretary of State for purposes of Part II</ContentsTitle>
  </ContentsItem>
  ...
</ContentsPart>
```

The table of contents at `http://www.legislation.gov.uk/nisi/2007/288/contents` includes an Article that has not yet come into force:

```
<ContentsPart ContentRef="part-IV"
  DocumentURI="http://www.legislation.gov.uk/nisi/2007/288/part/IV"
  IdURI="http://www.legislation.gov.uk/id/nisi/2007/288/part/IV" RestrictStartDate="2007-03-01">
  <ContentsNumber>
    <Strong>PART IV</Strong>
  </ContentsNumber>
  <ContentsTitle>ARREST</ContentsTitle>
  ...
  <ContentsItem ContentRef="article-17"
    DocumentURI="http://www.legislation.gov.uk/nisi/2007/288/article/17"
    IdURI="http://www.legislation.gov.uk/id/nisi/2007/288/article/17"
    RestrictStartDate="2007-03-01">
    <ContentsNumber>17</ContentsNumber>
    <ContentsTitle>Search upon arrest</ContentsTitle>
  </ContentsItem>
  <ContentsItem Match="false" Status="Prospective" ContentRef="article-18"
    DocumentURI="http://www.legislation.gov.uk/nisi/2007/288/article/18/prospective"
    IdURI="http://www.legislation.gov.uk/id/nisi/2007/288/article/18">
    <ContentsNumber>18</ContentsNumber>
    <ContentsTitle>Arrested juveniles</ContentsTitle>
  </ContentsItem>
</ContentsPart>
```

The `DocumentURI` attribute always points to an existing version of the section. In the case of a section that has been repealed, it will point to the version of the section that was in force on the day before its repeal.

## Metadata

The `<ukm:Metadata>` element contains metadata about the item of legislation or section of legislation that's requested. Among other things, this includes `<atom:link>` elements that point to other interesting documents:

|Relation|Description|
|---|---|
|`self`|The representation URI for the provided XML representation|
|`alternate`|Representation URIs for alternative representations, such as the [RDF/XML](/developer/formats/rdf) representation|
|`http://purl.org/dc/terms/tableOfContents`|The document URI of the table of contents for the item of legislation|
|`http://www.legislation.gov.uk/def/navigation/act`|The document URI for the whole item of legislation|
|`http://www.legislation.gov.uk/def/navigation/introduction`|The document URI for the introduction of the item of legislation|
|`http://www.legislation.gov.uk/def/navigation/body`|The document URI for the body of the item of legislation|
|`http://www.legislation.gov.uk/def/navigation/schedules`|The document URI for the schedules of the item of legislation|
|`http://purl.org/dc/terms/hasPart`|Document URIs for any concurrent versions; the title indicates their extents|
|`http://purl.org/dc/terms/isPartOf`|If you've requested a particular extent, the document URI for the combined version|
|`http://purl.org/dc/terms/replaces`|The document URI of the previous version, or the current version if you're looking at the prospective version; the title provides the date or the keyword 'current'|
|`http://purl.org/dc/terms/isReplacedBy`|The document URI of the next version, or the prospective version if there is one; the title provides the date or the keyword 'prospective'|
|`up`|A link to the parent of the section (the item of legislation)|
|`prev`|A link to the previous section|
|`next`|A link to the next section|

## Unapplied Effects

The content of an item of legislation can, and often is, changed by other legislation. Most of these changes are reflected in the content of the XML that we publish. However, one of the [limitations](/developer/limitations) of this site is not all the changes we know about have been applied to the content. It is therefore out of date.

The effects that have not yet been applied to the content of the legislation are listed in the metadata of the XML, within the `<ukm:UnappliedEffects>` element. For example:

```
<ukm:UnappliedEffects>
  <ukm:UnappliedEffect Type="Commencement Order" Notes="commencement order for 2007 c. 15"
    CommencingClass="UnitedKingdomStatutoryInstrument" CommencingYear="2008" CommencingNumber="1653" 
    AffectingClass="UnitedKingdomPublicGeneralAct" AffectingYear="2007" AffectingNumber="15" 
    AffectedProvision="specified amended provision(s)" CommencingSectionRef="article-2" 
    AffectingURI="http://www.legislation.gov.uk/id/ukpga/2007/15" 
    CommencingURI="http://www.legislation.gov.uk/id/uksi/2008/1653/article/2"/>
  <ukm:UnappliedEffect Type="Commencement Order" Notes="commencement order for 2007 c. 28" 
    CommencingClass="UnitedKingdomStatutoryInstrument" CommencingYear="2008" CommencingNumber="172" 
    AffectingClass="UnitedKingdomPublicGeneralAct" AffectingYear="2007" AffectingNumber="28" 
    AffectedProvision="specified amended provision(s)" CommencingStartSectionRef="article-2" 
    CommencingEndSectionRef="article-9" AffectingURI="http://www.legislation.gov.uk/id/ukpga/2007/28" 
    CommencingURI="http://www.legislation.gov.uk/id/uksi/2008/172/article/2" 
    CommencingUpTo="http://www.legislation.gov.uk/id/uksi/2008/172/article/9"/>
  <ukm:UnappliedEffect Type="inserted" AffectingClass="UnitedKingdomPublicGeneralAct" AffectingYear="2008" 
    AffectingNumber="26" AffectedSectionRef="section-126-1-aa" AffectingSectionRef="section-52-3" 
    AffectingURI="http://www.legislation.gov.uk/id/ukpga/2008/26/section/52/3" 
    AffectedURI="http://www.legislation.gov.uk/id/ukpga/1985/67/section/126/1/aa"/>
  <ukm:UnappliedEffect Type="text amended" AffectingClass="UnitedKingdomPublicGeneralAct" AffectingYear="2008" 
    AffectingNumber="26" AffectedSectionRef="section-126-3" AffectingSectionRef="section-61-2" 
    AffectingURI="http://www.legislation.gov.uk/id/ukpga/2008/26/section/61/2" 
    AffectedURI="http://www.legislation.gov.uk/id/ukpga/1985/67/section/126/3"/>
  <ukm:UnappliedEffect Type="repealed" AffectingClass="ScottishAct" AffectingYear="2003" 
    AffectingNumber="1" AffectedStartSectionRef="section-89" AffectedEndSectionRef="section-91" 
    AffectingSectionRef="section-60-3-c" AffectingURI="http://www.legislation.gov.uk/id/asp/2003/1/section/60/3/c" 
    AffectedURI="http://www.legislation.gov.uk/id/ukpga/1985/67/section/89" 
    AffectedUpTo="http://www.legislation.gov.uk/id/ukpga/1985/67/section/91"/>		
  ...
</ukm:UnappliedEffects>
```

Each effect is listed with a `Type` and sometimes some `Notes`. A link to the affecting legislation is provided through the attributes:

*   `AffectingClass` - the class of the affecting legislation
*   `AffectingYear` - the year of the affecting legislation
*   `AffectingNumber` - the number of the affecting legislation
*   `AffectingSectionRef` - the id of the section within that legislation causing the effect
*   `AffectingURI` - the [identifier URI](/developer/uris#identifiers) of the section within the legislation causing the effect

Each effect can affect different parts of the legislation. These are indicated through the following attributes:

*   `AffectedSectionRef` - the id for the affected section
*   `AffectedStartSectionRef`/`AffectedEndSectionRef` - the ids for the start and end sections in a range of affected sections
*   `AffectedURI` - the [identifier URI](/developer/uris#identifiers) of the affected section, or the start of range of sections
*   `AffectedUpTo` - the [identifier URI](/developer/uris#identifiers) of the end of the range of affected sections

For effects of the type 'Commencemnt Order' then the following attributes are used:

*   `CommencingClass` - the class of the commencing legislation
*   `CommencingYear` - the year of the commencing legislation
*   `CommencingNumber` - the number of the commencing legislation
*   `CommencingSectionRef` - the id of the section within the commencing legislation
*   `CommencingStartSectionRef`/`CommencingEndSectionRef` - the ids for the start and end sections in a range of commencing sections
*   `CommencingURI` - the [identifier URI](/developer/uris#identifiers) of the section within the commencing legislation
*   `CommencingUpTo` - the [identifier URI](/developer/uris#identifiers) of the end of the range of commencing sections

Note that because the changes that these effects encode are about future changes to the legislation, not all the sections that are linked to necessarily exist in the current version of the legislation. For example, one unapplied effect might insert a section 6(1A) which is then later modified by another piece of legislation.