# Welcome

## Open data

The information on legislation.gov.uk is available for you to reuse **free of charge**, under a [permissive licence](reuse-licence.md), for commercial and non-commercial uses.

You can download the following data from us, in a variety of formats:

 * legislation document data and text;
 * metadata (data about legislation); and
 * amendments (changes) to legislation.

You can also search or query for legislation, download lists of legislation or subscribe to feeds of new and updated content.

## Find out what data we have

Our dataset **is not yet complete** and only contains data for some items of legislation. You can read about [what data we have](what-we-have.md), including limitations of the data in our dataset.

We acquire new and historical legislation data from multiple sources. <!-- TODO add in when origins page is ready You can read about the [origins](origins.md) of the data in our dataset, including information about when we update our data. -->You can read about how to track [updates](api/publication-log.md) to our data.

## Understand our data

Our [data model](model/overview.md) overview explains what our data represent and how to interpret them.

## Start using our data

You can get our data via our website and **API**.

<!-- TODO: Replace above para with this one once bulk downloads available You can read get our data through one of two routes:

 * through our **[data downloads](#data-downloads)** service, if you want to download all or a subset of our documents, or
 * via our website and **[API](#api)**, if you want fine-grained control over which data you download or you want to search or query our dataset. -->
 
You can find more information about the different kinds of data we offer, including how to get and interpret them, in the [open data](#open-data) section above.

<!--If you want a solution for a specific problem, you can read our [How do I…]() section, which includes instructions on how to do the following:

 * [Get a list of all UK legislation]()
 * [Download all UK legislation as XML, PDF or plain text]()
 * [Get XML for an item of legislation or part of it]()-->

<!-- TODO: re-add when bulk downloads available ### Data downloads

Our data downloads service provides ZIP files containing the text of legislation. They are available in the [Data section of our Research website]().

The ZIP files are available in the following formats:

* [XML](formats/xml.md) (where available) in our CLML dialect and Akoma Ntoso
* [HTML](formats/html.md) as XHTML and HTML5 (transformed from the source XML, only where it is available)
* [PDF](formats/pdf.md) (where an enacted/made or revised PDF is available)
* Plain text, both in full and limited to only the operative text TODO link to explanation of the item (transformed from the source XML, only where it is available)

There are ZIPs available that contain all legislation available in the specified format, as well as smaller ZIPs that contain only legislation of a specific type, or type and year.-->

### Online access via our API and website<a name="api"></a>

Our website provides data for items of legislation in multiple formats, including [XML](formats/xml.md). You can try: 
 * appending `/data.xml` to the end of a legislation.gov.uk address to get the content as [XML](formats/xml.md) (e.g. `https://www.legislation.gov.uk/asc/2021/4/part/1/data.xml`), or 
 * appending `/data.feed` to the end of the address for a search or list page (before the `?` query string character, if it appears) to get the content of the results page as an [Atom](formats/atom.md) feed (e.g. `https://www.legislation.gov.uk/nia/2013/data.feed?title=budget`).

The website is usable as an [API](https://en.wikipedia.org/wiki/API) by applications that speak [HTTP](https://en.wikipedia.org/wiki/HTTP). All the features of the website are available via the API. 

If you want to find out more about our API, we provide an [overview of the API](api/overview.md) that explains how it works and what features it offers.

## Code, schemas and other resources

You can find details about our code and schemas on the [More Resources](more-resources.md) page.

## Contact us

If you have any questions about using our data or API, please contact [data.legislation@nationalarchives.gov.uk](mailto:data.legislation@nationalarchives.gov.uk). We’re happy to help with enquiries from individuals, business, organisations and government departments.

You can also follow us on X (formerly Twitter) at [@legislation](https://twitter.com/legislation).