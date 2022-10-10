# RDF/XML Format

We are publishing RDF about the legislation that is provided here using the vocabularies:

|Vocabulary|Prefix|Namespace|
|--- |--- |--- |
|[RDF Schema](http://www.w3.org/TR/rdf-schema/)|`rdfs`|`http://www.w3.org/2000/01/rdf-schema#`|
|[OWL](http://www.w3.org/TR/owl-features/)|`owl`|`http://www.w3.org/2002/07/owl#`|
|[Dublin Core Terms](http://dublincore.org/documents/dcmi-terms/)|`dct`|`http://purl.org/dc/terms/`|
|[FOAF](http://xmlns.com/foaf/spec/)|`foaf`|`http://xmlns.com/foaf/0.1/`|
|[XHTML Vocabulary](http://www.w3.org/1999/xhtml/vocab/)|`xhv`|`http://www.w3.org/1999/xhtml/vocab#`|
|[FRBR](http://vocab.org/frbr/core.html)|`frbr`|`http://purl.org/vocab/frbr/core#`|
|[Metalex](http://www.metalex.eu/)|`metalex`|`http://purl.org/vocab/frbr/core#`|

We are using these vocabularies because they will provide high recognition and ability for reuse without developers having to understand a specific legislation ontology. We do intend to use a specific legislation ontology in addition.

The RDF/XML document that you get will contain descriptions of several resources. At the moment, these are:

*   A `frbr:Work`/`metalex:BibliographicWork` which is the abstract notion of an item of legislation, identified by an [identifier URI](uris#identifiers). This is only provided when you request the current version of an item of legislation.
*   A `frbr:Expression`/`metalex:BibliographicExpression` which is always the latest version of the item of legislation that's been requested. This is only provided when you request the current version of an item of legislation.
*   Some `frbr:Expression`s/`metalex:BibliographicExpression`s which are the latest version of the item of legislation that's been requested with particular extents (only relevant extents are listed), again only provided when you've requested the current version of the item.
*   A `frbr:Expression`/`metalex:BibliographicExpression` which is the particular version of the item of legislation that's been requested. This is usually the most recent version.
*   Some `frbr:Expression`s/`metalex:BibliographicExpression`s which are the particular version of the item of legislation that's been requested with particular extents. This is only relevant when there are multiple concurrent versions of the requested section.
*   Some `frbr:Manifestation`s/`metalex:BibliographicManifestation`s for the different formats of each of the `frbr:Expression`s described above.

Links between the item of legislation and the documents that are particular versions of legislation are provided using the properties `foaf:isPrimaryTopicOf`, `frbr:realization` and `metalex:realizedBy`, which point from the legislation item (the Work) to the documents (the Expressions); and `foaf:primaryTopic`, `frbr:realizationOf` and `metalex:realizes`, which point from the documents (the Expression) to the legislation item (the Work).

A `rdfs:isDefinedBy` link points from the item of legislation to the latest version of the legislation. The latest version has a `dct:hasVersion` pointer to the particular versioned (and dated) document, which reciprocates with a `dct:isVersionOf` property.

Versions without extents point to those versions within extents using `dct:hasPart`; `dct:isPartOf` provides the reverse link.

The versioned documents point to their manifestations with the properties `frbr:embodiment`, `metalex:embodiedBy` and `dct:hasFormat`. The reverse links are available through the `frbr:embodimentOf`, `metalex:embodies` and `dct:isFormatOf` properties.

For example:

```
<frbr:Work rdf:about="http://www.legislation.gov.uk/id/ukpga/1985/67">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicWork" />
  <rdfs:label>Transport Act 1985</rdfs:label>
  <rdfs:isDefinedBy rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67" />
  <foaf:isPrimaryTopicOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67" />
  <frbr:realization rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67" />
  <metalex:realizedBy rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67" />
  <foaf:isPrimaryTopicOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <frbr:realization rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <metalex:realizedBy rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI">http://www.legislation.gov.uk/id/ukpga/1985/67</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Transport Act 1985</dct:title>
  <dct:description>An Act to amend the law relating to road passenger transport; to make provision for the transfer 
    of the operations of the National Bus Company to the private sector; to provide for the reorganisation of passenger 
    transport in the public sector; to provide for local and central government financial support for certain passenger 
    transport services and travel concessions; to make further provision with respect to the powers of London Regional 
    Transport; to make new provision with respect to the constitution, powers and proceedings of the Transport Tribunal; 
    to make provision with respect to grants payable under section 92 of the Finance Act 1965; to establish a Disabled 
    Persons Transport Advisory Committee; and for connected purposes.</dct:description>
  ...
</frbr:Work>
<frbr:Expression rdf:about="http://www.legislation.gov.uk/ukpga/1985/67">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicExpression" />
  <rdfs:label>Transport Act 1985 currently in force</rdfs:label>
  <foaf:primaryTopic rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67" />
  <frbr:realizationOf rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67" />
  <metalex:realizes rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI">http://www.legislation.gov.uk/ukpga/1985/67</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Transport Act 1985</dct:title>
  <dct:description>An Act to amend the law relating to road passenger transport; to make provision for the transfer 
    of the operations of the National Bus Company to the private sector; to provide for the reorganisation of passenger 
    transport in the public sector; to provide for local and central government financial support for certain passenger 
    transport services and travel concessions; to make further provision with respect to the powers of London Regional 
    Transport; to make new provision with respect to the constitution, powers and proceedings of the Transport Tribunal; 
    to make provision with respect to grants payable under section 92 of the Finance Act 1965; to establish a Disabled 
    Persons Transport Advisory Committee; and for connected purposes.</dct:description>
  <dct:hasVersion rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <dct:publisher>
    <rdf:Description>
      <rdfs:label>Statute Law Database</rdfs:label>
    </rdf:Description>
  </dct:publisher>
  <dct:license rdf:resource="http://www.legislation.gov.uk/licence" />
</frbr:Expression>
...
<frbr:Expression rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicExpression" />
  <rdfs:label>Transport Act 1985</rdfs:label>
  <foaf:primaryTopic rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67" />
  <frbr:realizationOf rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67" />
  <frbr:embodiment rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.xml" />
  <frbr:embodiment rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.rdf" />
  <metalex:realizes rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67" />
  <metalex:embodiedBy rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.xml" />
  <metalex:embodiedBy rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.rdf" />
  <dct:hasFormat rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.xml" />
  <dct:hasFormat rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.rdf" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI">http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Transport Act 1985</dct:title>
  <dct:description>An Act to amend the law relating to road passenger transport; to make provision for the transfer 
  of the operations of the National Bus Company to the private sector; to provide for the reorganisation of passenger 
  transport in the public sector; to provide for local and central government financial support for certain passenger 
  transport services and travel concessions; to make further provision with respect to the powers of London Regional 
  Transport; to make new provision with respect to the constitution, powers and proceedings of the Transport Tribunal; 
  to make provision with respect to grants payable under section 92 of the Finance Act 1965; to establish a Disabled 
  Persons Transport Advisory Committee; and for connected purposes.</dct:description>
  <dct:isVersionOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67" />
  <dct:publisher>
    <rdf:Description>
      <rdfs:label>Statute Law Database</rdfs:label>
    </rdf:Description>
  </dct:publisher>
  <dct:license rdf:resource="http://www.legislation.gov.uk/licence" />
  ...
</frbr:Expression>
...
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.xml">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicManifestation" />
  <rdfs:label>XML version of Transport Act 1985</rdfs:label>
  <frbr:embodimentOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <metalex:embodies rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <dct:isFormatOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI">http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.xml</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Transport Act 1985</dct:title>
  <dct:description>An Act to amend the law relating to road passenger transport; to make provision for the transfer 
  of the operations of the National Bus Company to the private sector; to provide for the reorganisation of passenger 
  transport in the public sector; to provide for local and central government financial support for certain passenger 
  transport services and travel concessions; to make further provision with respect to the powers of London Regional 
  Transport; to make new provision with respect to the constitution, powers and proceedings of the Transport Tribunal; 
  to make provision with respect to grants payable under section 92 of the Finance Act 1965; to establish a Disabled 
  Persons Transport Advisory Committee; and for connected purposes.</dct:description>
  <dct:format>
    <dct:IMT>
      <rdf:value>application/xml</rdf:value>
      <rdfs:label>XML</rdfs:label>
    </dct:IMT>
  </dct:format>
  ...
</frbr:Manifestation>
<frbr:Manifestation
  rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.rdf">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicManifestation" />
  <rdfs:label>RDF/XML version of Transport Act 1985</rdfs:label>
  <frbr:embodimentOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <metalex:embodies rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <dct:isFormatOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI">http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.rdf</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Transport Act 1985</dct:title>
  <dct:description>An Act to amend the law relating to road passenger transport; to make provision for the transfer 
  of the operations of the National Bus Company to the private sector; to provide for the reorganisation of passenger 
  transport in the public sector; to provide for local and central government financial support for certain passenger 
  transport services and travel concessions; to make further provision with respect to the powers of London Regional 
  Transport; to make new provision with respect to the constitution, powers and proceedings of the Transport Tribunal; 
  to make provision with respect to grants payable under section 92 of the Finance Act 1965; to establish a Disabled
  Persons Transport Advisory Committee; and for connected purposes.</dct:description>
  <dct:format>
    <dct:IMT>
      <rdf:value>application/rdf+xml</rdf:value>
      <rdfs:label>RDF/XML</rdfs:label>
    </dct:IMT>
  </dct:format>
  ...
</frbr:Manifestation>
<frbr:Manifestation
  rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.htm">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicManifestation" />
  <rdfs:label>RDF/XML version of Transport Act 1985</rdfs:label>
  <frbr:embodimentOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <metalex:embodies rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <dct:isFormatOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI">http://www.legislation.gov.uk/ukpga/1985/67/sld/2003-04-01/data.htm</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Transport Act 1985</dct:title>
  <dct:description>An Act to amend the law relating to road passenger transport; to make provision for the transfer 
of the operations of the National Bus Company to the private sector; to provide for the reorganisation of passenger 
transport in the public sector; to provide for local and central government financial support for certain passenger 
transport services and travel concessions; to make further provision with respect to the powers of London Regional 
Transport; to make new provision with respect to the constitution, powers and proceedings of the Transport Tribunal; 
to make provision with respect to grants payable under section 92 of the Finance Act 1965; to establish a Disabled
Persons Transport Advisory Committee; and for connected purposes.</dct:description>
  <dct:format>
    <dct:IMT>
      <rdf:value>application/xhtml+xml</rdf:value>
      <rdfs:label>HTML snippet</rdfs:label>
    </dct:IMT>
  </dct:format>
  ...
</frbr:Manifestation>
```

## Aliases

There will also be descriptions of items of legislation that are the same as, or similar to, the one that you have requested. These point, using `owl:sameAs`, to the canonical identifier for the item of legislation. These 'alias' URIs are:

*   a title-based URI that looks like `http://www.legislation.gov.uk/id?title={title}`
*   as relevant for pre-1963 legislation, a calendar-year-based URI (the canonical URI uses the regnal year of the legislation); where the calendar-year-based URI is ambiguous, pointing to two items of legislation, `rdfs:seeAlso` is used rather than `owl:sameAs`
*   as relevant for Wales Statutory Instruments and Northern Ireland Orders in Council, a UK Statuatory Instrument URI
*   as relevant for secondary legislation with alternative numbering schemes, URIs that use those alternative numbering schemes

For example:

```
<rdf:Description rdf:about="http://www.legislation.gov.uk/id?title=THE%20CHILDCARE%20ACT%202006%20%28COMMENCEMENT%20NO.1%29%20%28WALES%29%20ORDER%202008">
  <owl:sameAs rdf:resource="http://www.legislation.gov.uk/id/wsi/2008/17" />
</rdf:Description>
<rdf:Description rdf:about="http://www.legislation.gov.uk/id/uksi/2008/17">
  <owl:sameAs rdf:resource="http://www.legislation.gov.uk/id/wsi/2008/17" />
</rdf:Description>
<rdf:Description rdf:about="http://www.legislation.gov.uk/id/wsi/2008/w6">
  <owl:sameAs rdf:resource="http://www.legislation.gov.uk/id/wsi/2008/17" />
</rdf:Description>
<rdf:Description rdf:about="http://www.legislation.gov.uk/id/wsi/2008/c1">
  <owl:sameAs rdf:resource="http://www.legislation.gov.uk/id/wsi/2008/17" />
</rdf:Description>
```

## Versions

Versions are a particular issue with this information. Each Work has a number of Expressions, each representing a different version of the legislation. These include dated versions, the current version, and a prospective version.

Dated versions may have a `dct:replaces` pointer to the previous version of the item and a `dct:isReplacedBy` pointer to the next version of the item. The first version will lack a `dct:replaces` property and the last will lack a `dct:isReplacedBy` property. The current version may have a `dct:isReplacedBy` pointer to the prospective version if there is one. The prospective version will have a `dct:replaces` pointer to the current version if there is one.

The following tables summarise how the Dublin Core date properties are used in primary and secondary legislation within this data. Note that the `dct:valid` property uses the [DCMI Period](http://dublincore.org/documents/dcmi-period/) notation for indicating the period during which the item of legislation, or the particular version being looked at, is valid. The "Expression" column in these tables refers to the dated version of the legislation document rather than the "latest" version, for which the relevant dates would always be changing.

<table xmlns="http://www.w3.org/1999/xhtml">
  <caption>Dates in Primary Legislation</caption>
  <col width="10%" />
  <col width="15%" />
  <col width="15%" />
  <col width="15%" />
  <col width="15%" />
  <col width="15%" />
  <tr>
    <th rowspan="2">Property</th>
    <th rowspan="2">Work</th>
    <th colspan="3">Expression</th>
    <th rowspan="2">Manifestation</th>
  </tr>
  <tr>
    <th>Enacted</th>
    <th>Dated</th>
    <th>Prospective</th>
  </tr>
  <tr>
    <td><code>dc:created</code></td>
    <td>date of enactment</td>
    <td>date of enactment</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
  </tr>
  <tr>
    <td><code>dc:dateAccepted</code></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
  </tr>
  <tr>
    <td><code>dc:modified</code></td>
    <td>last amendment date</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>last modified date</td>
  </tr>
  <tr>
    <td><code>dc:valid</code></td>
    <td>start=earliest start date (if post base date)</td>
    <td>-</td>
    <td>start=latest start date within section; end=earliest end date within section;</td>
    <td>-</td>
    <td>-</td>
  </tr>
</table>

<table xmlns="http://www.w3.org/1999/xhtml">
  <caption>Dates in Revised Secondary Legislation</caption>
  <col width="10%" />
  <col width="15%" />
  <col width="15%" />
  <col width="15%" />
  <col width="15%" />
  <col width="15%" />
  <tr>
    <th rowspan="2">Property</th>
    <th rowspan="2">Work</th>
    <th colspan="3">Expression</th>
    <th rowspan="2">Manifestation</th>
  </tr>
  <tr>
    <th>Enacted</th>
    <th>Dated</th>
    <th>Prospective</th>
  </tr>
  <tr>
    <td><code>dc:created</code></td>
    <td>made date</td>
    <td>made date</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
  </tr>
  <tr>
    <td><code>dc:dateAccepted</code></td>
    <td>laid date</td>
    <td>laid date</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
  </tr>
  <tr>
    <td><code>dc:modified</code></td>
    <td>last amendment date</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>last modified date</td>
  </tr>
  <tr>
    <td><code>dc:valid</code></td>
    <td>start=coming into force date</td>
    <td>-</td>
    <td>start=latest start date within section; end=earliest end date within section;</td>
    <td>-</td>
    <td>-</td>
  </tr>
</table>

<table xmlns="http://www.w3.org/1999/xhtml">
  <caption>Dates in Unrevised Secondary Legislation</caption>
  <col width="25%" />
  <col width="25%" />
  <col width="25%" />
  <col width="25%" />
  <tr>
    <th>Property</th>
    <th>Work</th>
    <th>Expression</th>
    <th>Manifestation</th>
  </tr>
  <tr>
    <td><code>dc:created</code></td>
    <td>made date</td>
    <td>made date</td>
    <td>-</td>
  </tr>
  <tr>
    <td><code>dc:dateAccepted</code></td>
    <td>laid date</td>
    <td>laid date</td>
    <td>-</td>
  </tr>
  <tr>
    <td><code>dc:modified</code></td>
    <td>-</td>
    <td>-</td>
    <td>last modified date</td>
  </tr>
  <tr>
    <td><code>dc:valid</code></td>
    <td>start=coming into force date</td>
    <td>start=coming into force date</td>
    <td>-</td>
  </tr>
</table>

## Extents

The countries covered by the version of legislation being looked at are provided using the `dct:extent` property. The references are to the upcoming Ordnance Survey identifiers for these countries; an `rdfs:label` has been supplied for each to make them easier to understand.

For example:

```
<frbr:Expression rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/2003-04-01">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicExpression"/>
  <rdfs:label>Transport Act 1985 Section 6 in force in Scotland on 1st April 2003</rdfs:label>
  ...
  <dct:valid rdf:datatype="http://dublincore.org/documents/dcmi-period/">start=2001-07-01;</dct:valid>
  <dct:spatial>
    <rdf:Description rdf:about="http://data.ordnancesurvey.co.uk/id/8000000000000003">
      <rdfs:label>Scotland</rdfs:label>
    </rdf:Description>
  </dct:spatial>
</frbr:Expression>
```

Navigating to particular extents is made possible through the `dct:hasPart` property, which links a generic `frbr:Expression` to `frbr:Expression`s with particular extents, as shown in the following example:

```
<frbr:Work rdf:about="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicWork" />
  <rdfs:label>Transport Act 1985 section 6</rdfs:label>
  <rdfs:isDefinedBy rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <foaf:isPrimaryTopicOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <frbr:realization rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <metalex:realizedBy rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <foaf:isPrimaryTopicOf
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england" />
  <frbr:realization rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england" />
  <metalex:realizedBy rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england" />
  <foaf:isPrimaryTopicOf
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/wales" />
  <frbr:realization rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/wales" />
  <metalex:realizedBy rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/wales" />
  <foaf:isPrimaryTopicOf
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland" />
  <frbr:realization rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland" />
  <metalex:realizedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland" />
  <foaf:isPrimaryTopicOf
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01" />
  <frbr:realization
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01" />
  <metalex:realizedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01" />
  <foaf:isPrimaryTopicOf
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01" />
  <frbr:realization
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01" />
  <metalex:realizedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01" />
  <foaf:isPrimaryTopicOf
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/2003-04-01" />
  <frbr:realization
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/2003-04-01" />
  <metalex:realizedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/2003-04-01" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI"
    >http://www.legislation.gov.uk/id/ukpga/1985/67/section/6</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Registration of local services</dct:title>
  ...
</frbr:Work>
...
<frbr:Expression rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicExpression" />
  <rdfs:seeAlso rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <rdfs:label>Transport Act 1985 section 6 currently in force</rdfs:label>
  <foaf:primaryTopic rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <frbr:realizationOf rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <frbr:embodiment rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.xml" />
  <frbr:embodiment rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.rdf" />
  <metalex:realizes rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <metalex:embodiedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.xml" />
  <metalex:embodiedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.rdf" />
  <dct:hasFormat rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.xml" />
  <dct:hasFormat rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.rdf" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI"
    >http://www.legislation.gov.uk/ukpga/1985/67/section/6</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Registration of local services</dct:title>
  <dct:publisher>
    <rdf:Description>
      <rdfs:label>Statute Law Database</rdfs:label>
    </rdf:Description>
  </dct:publisher>
  <dct:license rdf:resource="http://www.legislation.gov.uk/licence" />
  <dct:hasPart rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england" />
  <dct:hasPart rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/wales" />
  <dct:hasPart rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland" />
  <dct:hasVersion rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01" />
  <metalex:variant rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01"
  />
</frbr:Expression>
<frbr:Expression rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicExpression" />
  <rdfs:seeAlso rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <rdfs:label>Transport Act 1985 section 6 currently in force in England</rdfs:label>
  <foaf:primaryTopic rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <frbr:realizationOf rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <frbr:embodiment
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england/data.xml" />
  <frbr:embodiment
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england/data.rdf" />
  <metalex:realizes rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <metalex:embodiedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england/data.xml" />
  <metalex:embodiedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england/data.rdf" />
  <dct:hasFormat
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england/data.xml" />
  <dct:hasFormat
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england/data.rdf" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI"
    >http://www.legislation.gov.uk/ukpga/1985/67/section/6/england</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Registration of local services</dct:title>
  <dct:publisher>
    <rdf:Description>
      <rdfs:label>Statute Law Database</rdfs:label>
    </rdf:Description>
  </dct:publisher>
  <dct:license rdf:resource="http://www.legislation.gov.uk/licence" />
  <dct:spatial>
    <rdf:Description rdf:about="http://data.ordnancesurvey.co.uk/id/8000000000000002">
      <rdfs:label>England</rdfs:label>
    </rdf:Description>
  </dct:spatial>
  <dct:isPartOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <dct:hasVersion
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01" />
  <metalex:variant
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01"
  />
</frbr:Expression>
<frbr:Expression rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/wales">
  ...
</frbr:Expression>
<frbr:Expression rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland">
  ...
</frbr:Expression>
<frbr:Expression rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicExpression" />
  <rdfs:seeAlso rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <rdfs:label>Transport Act 1985 section 6 in force on 1st April 2003</rdfs:label>
  <foaf:primaryTopic rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <frbr:realizationOf rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <frbr:embodiment
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.xml" />
  <frbr:embodiment
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.rdf" />
  <metalex:realizes rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <metalex:embodiedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.xml" />
  <metalex:embodiedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.rdf" />
  <dct:hasFormat
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.xml" />
  <dct:hasFormat
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.rdf" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI"
    >http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Registration of local services</dct:title>
  <dct:publisher>
    <rdf:Description>
      <rdfs:label>Statute Law Database</rdfs:label>
    </rdf:Description>
  </dct:publisher>
  <dct:license rdf:resource="http://www.legislation.gov.uk/licence" />
  <dct:spatial>
    <rdf:Description rdf:about="http://data.ordnancesurvey.co.uk/id/8000000000000001">
      <rdfs:label>Great Britain</rdfs:label>
    </rdf:Description>
  </dct:spatial>
  <dct:hasPart
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01" />
  <dct:hasPart
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/2003-04-01" />
  <dct:isVersionOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <dct:valid rdf:datatype="http://dublincore.org/documents/dcmi-period/"
    >start=2001-07-01;</dct:valid>
  <metalex:variant rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2001-07-01" />
  ...
</frbr:Expression>
<frbr:Expression
  rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicExpression" />
  <rdfs:seeAlso rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <rdfs:label>Transport Act 1985 section 6 in force in England and Wales on 1st April 2003</rdfs:label>
  <foaf:primaryTopic rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <frbr:realizationOf rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <frbr:embodiment
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01/data.xml" />
  <frbr:embodiment
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01/data.rdf" />
  <metalex:realizes rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6" />
  <metalex:embodiedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01/data.xml" />
  <metalex:embodiedBy
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01/data.rdf" />
  <dct:hasFormat
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01/data.xml" />
  <dct:hasFormat
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01/data.rdf" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI"
    >http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Registration of local services</dct:title>
  <dct:publisher>
    <rdf:Description>
      <rdfs:label>Statute Law Database</rdfs:label>
    </rdf:Description>
  </dct:publisher>
  <dct:license rdf:resource="http://www.legislation.gov.uk/licence" />
  <dct:spatial>
    <rdf:Description rdf:about="http://data.ordnancesurvey.co.uk/id/8000000000000002">
      <rdfs:label>England</rdfs:label>
    </rdf:Description>
  </dct:spatial>
  <dct:spatial>
    <rdf:Description rdf:about="http://data.ordnancesurvey.co.uk/id/8000000000000004">
      <rdfs:label>Wales</rdfs:label>
    </rdf:Description>
  </dct:spatial>
  <dct:isPartOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01" />
  <dct:isVersionOf
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales" />
  <dct:valid rdf:datatype="http://dublincore.org/documents/dcmi-period/"
    >start=2001-07-01;</dct:valid>
  <metalex:variant
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2001-07-01" />
  ...
</frbr:Expression>
<frbr:Expression rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/2003-04-01">
  ...
</frbr:Expression>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.xml">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicManifestation" />
  <rdfs:label>XML version of Transport Act 1985 section 6 currently in force</rdfs:label>
  <frbr:embodimentOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <metalex:embodies rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <dct:isFormatOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI"
    >http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.xml</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Registration of local services</dct:title>
  <dct:modified rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime"
    >2009-10-05T12:37:47+01:00</dct:modified>
  <dct:format>
    <dct:IMT>
      <rdf:value>application/xml</rdf:value>
      <rdfs:label>XML</rdfs:label>
    </dct:IMT>
  </dct:format>
  <dct:hasVersion
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.xml" />
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.rdf">
  <rdf:type rdf:resource="http://www.metalex.eu/metalex/2008-05-02#BibliographicManifestation" />
  <rdfs:label>RDF/XML version of Transport Act 1985 section 6 currently in force</rdfs:label>
  <frbr:embodimentOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <metalex:embodies rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <dct:isFormatOf rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6" />
  <dct:identifier rdf:datatype="http://www.w3.org/2001/XMLSchema#anyURI"
    >http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.rdf</dct:identifier>
  <dct:type rdf:resource="http://purl.org/dc/dcmitype/Text" />
  <dct:title>Registration of local services</dct:title>
  <dct:modified rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime"
    >2009-10-05T12:37:47+01:00</dct:modified>
  <dct:format>
    <dct:IMT>
      <rdf:value>application/rdf+xml</rdf:value>
      <rdfs:label>RDF/XML</rdfs:label>
    </dct:IMT>
  </dct:format>
  <dct:hasVersion
    rdf:resource="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.rdf" />
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/data.htm">
...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england/data.xml">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england/data.rdf">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england/data.htm">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/wales/data.xml">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/wales/data.rdf">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/wales/data.htm">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/data.xml">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/data.rdf">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/data.htm">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.xml">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.rdf">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/2003-04-01/data.htm">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01/data.xml">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01/data.rdf">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/england+wales/2003-04-01/data.htm">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/2003-04-01/data.xml">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/2003-04-01/data.rdf">
  ...
</frbr:Manifestation>
<frbr:Manifestation rdf:about="http://www.legislation.gov.uk/ukpga/1985/67/section/6/scotland/2003-04-01/data.htm">
  ...
</frbr:Manifestation>
```

## Unapplied Effects

The [unapplied effects](/developer/formats/xml#unapplied-effects) that are listed within the XML version of the legislation are also reflected within the RDF/XML version of the legislation. Here, we use the Metalex ontology to describe the effects.

Because we do not know which version (Expression) of the legislation is going to be modified by a particular effect, the unapplied effects are listed using the logic:

*   This Work is realised by some (as yet unknown) Expression
*   That Expression is the matter of (the intial state of) some Legislative Modification
*   The Legislative Modification has a legislative competence ground (affecting legislation) of some other legislation

For example, Section 6(1) of the Transport Act 1985 (c. 67) is amended by Paragraph 2(2) of Schedule 10 of the Education and Inspections Act 2006 (c. 40). The effect is described with:

```
<metalex:BibliographicWork rdf:about="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6/1">
  <metalex:realizedBy>
    <metalex:BibliographicExpression rdf:nodeID="document4">
      <metalex:realizes rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67/section/6/1" />
      <metalex:matterOf>
        <metalex:LegislativeModification rdf:nodeID="modification4">
          <rdfs:comment>text amended</rdfs:comment>
          <metalex:matter rdf:nodeID="document4" />
          <metalex:legislativeCompetenceGround>
            <metalex:LegislativeCompetenceGround
              rdf:about="http://www.legislation.gov.uk/id/ukpga/2006/40/schedule/10/paragraph/2/2">
              <metalex:legislativeCompetenceGroundOf rdf:nodeID="modification4" />
            </metalex:LegislativeCompetenceGround>
          </metalex:legislativeCompetenceGround>
        </metalex:LegislativeModification>
      </metalex:matterOf>
    </metalex:BibliographicExpression>
  </metalex:realizedBy>
  ...
</metalex:BibliographicWork>
```

The RDF/XML for a commencement order is a little more complicated, because in this case the modification is brought about through the commencement of a third item of legislation (which unfortunately we do not currently reference in a machine-readable form). In this case the logic goes:

*   This Work is realised by some (as yet unknown) Expression
*   That Expression is the matter of (the intial state of) some Legislative Modification
*   The Legislative Modification has a legislative competence ground (affecting legislation) of some (unknown) legislation
*   That legislation is the patient of (affected by) a Legislative Commencement
*   The Legislative Commencement has a legislative competence ground (affecting legislation) of some (known) legislation

For example, changes to the Transport Act 1985 (c. 67) by the Private Hire Vehicles (London) Act 1998 (c. 34) were commenced by Article 2(2) of The Private Hire Vehicles (London) Act 1998 (Commencement No. 3) Order 2004. The RDF/XML that articulates this is:

```
<metalex:BibliographicWork rdf:about="http://www.legislation.gov.uk/id/ukpga/1985/67">
  <metalex:realizedBy>
    <metalex:BibliographicExpression rdf:nodeID="document1">
      <metalex:realizes rdf:resource="http://www.legislation.gov.uk/id/ukpga/1985/67" />
      <metalex:matterOf>
        <metalex:LegislativeModification rdf:nodeID="modification1">
          <rdfs:label>Commencement Order</rdfs:label>
          <metalex:matter rdf:nodeID="document1" />
          <metalex:legislativeCompetenceGround>
            <metalex:LegislativeCompetenceGround rdf:nodeID="legislation1">
              <metalex:legislativeCompetenceGroundOf rdf:nodeID="modification1" />
              <metalex:patientOf>
                <metalex:LegislativeCommencement rdf:nodeID="commencement1">
                  <rdfs:label>commencement order for 1998 c. 34</rdfs:label>
                  <metalex:patient rdf:nodeID="legislation1" />
                  <metalex:legislativeCompetenceGround>
                    <metalex:LegislativeCompetenceGround
                      rdf:about="http://www.legislation.gov.uk/id/uksi/2004/241/article/2/1">
                      <metalex:legislativeCompetenceGroundOf rdf:nodeID="commencement1" />
                    </metalex:LegislativeCompetenceGround>
                  </metalex:legislativeCompetenceGround>
                </metalex:LegislativeCommencement>
              </metalex:patientOf>
            </metalex:LegislativeCompetenceGround>
          </metalex:legislativeCompetenceGround>
        </metalex:LegislativeModification>
      </metalex:matterOf>
    </metalex:BibliographicExpression>
  </metalex:realizedBy>
  ...
</metalex:BibliographicWork>
```

## Document Navigation

Navigation around the item of legislation is provided at each level.

Within the Work, the `metalex:fragment` property points to other Works that are fragments of this one, such as a section's subsections. The `metalex:fragmentOf` property points to the Work that this is a fragment of, such as the item of legislation for a section. At the Work level, sections are considered to be direct fragments of the legislation rather than belonging to a particular Part, since sections can move around during the lifetime of an item of legislation.

Within an Expression, the `metalex:fragment` property points to Expressions that are fragments of this one, such as a section's subsections or a crossheading's sections. The `metalex:fragmentOf` property points to the Expression that this is a fragment of, such as the crossheading or Part that a section belongs to. At the Expression level, sections are considered to be fragments of the crossheading in which they appear in that particular version of the legislation.

Also within an Expression, the `xhv:prev` and `xhv:next` properties provide navigation between items at the same level within the document. From a section, `xhv:prev` and `xhv:next` will navigate to other sections, even if they are contained within other Parts. From a crossheading, however, `xhv:prev` and `xhv:next` will only navigate to the previous and next crossheadings within the same Part. Similarly, `xhv:next` and `xhv:prev` cannot be used to navigate out of a schedule, except from the schedule itself.