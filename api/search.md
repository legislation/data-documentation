# Search, lists and feeds

The Legislation website and API offer two types of searches for legislation:

 * listings enable you to find multiple items of legislation and information about them;
 * identifier searches enable you to work out the correct identifier to use for an item or section of legislation.

The website and API also allow you to get listings of [changes to legislation](#changes-to-legislation).

## Common features

### Formats

Every list on the website of search results, or of legislation or changes to legislation, is available as a feed in [Atom](formats/atom.md) XML format by appending `/data.feed` to the end of the path of the address of the search request or list page (before the "query string" part of the address, which if present begins with a `?` character). The HTML and Atom formats contain the same information, but presented differently. 

### Paging

The API *paginates* its responses to requests for lists or searches. This means that the API only returns a fixed number of items in each response. The default is 20, which you can change by adding `results-count=N` to the [query string](https://en.wikipedia.org/wiki/Query_string)). Where there are more pages left in the feed, the response will contain an `<atom:link rel="next">` element with a link to the next results page.

### Sorting

Lists and search results support various sort criteria. The lists of changes to legislation also allows you to specify the ordering of the results. The sections below describe the available sort criteria and ordering options.

Note that the default sort order differs between the HTML view and the Atom feed, so make sure that if you want a specific sort order that you specify it explicitly in your request.

## Listings

The legislation.gov.uk website allows a user to get a list of legislation filtered by criteria such as title, type, year and text content. There are two ways to use this feature: the search form and the "browse" list pages of legislation, which both use the same underlying search functionality.

* Search requests have a path beginning with `/search`, followed by a "query string" (beginning with `?`) that consists of a set of search parameters separated by the `&` character. For example, the list page of all UK Statutory Instruments and Northern Ireland Statutory Rules from 2009 numbered 1 to 100 with "amendment" in the title is `https://www.legislation.gov.uk/search?type=uksi&type=nisr&year=2009&start-number=1&end-number=100&title="amendment"`.
* List pages have a path consisting of components that specify the parameters for the list. In some cases they may also have a query string to further filter the results. For example, the list page of all UK Statutory Instruments and Northern Ireland Statutory Rules from 2009 numbered 1 to 100 with "amendment" in the title is `https://www.legislation.gov.uk/uksi+nisr/2009/1-100?title="amendment"`.

The address of the results of a search or of a list is always the same, so you can save the address and return to it later to get up-to-date results for that search or list.

For every search request, there is a corresponding list page that contains the results for that search. The response to a request for a valid `/search` URI is always a redirect to the corresponding list page. If possible, we recommend you directly request the list page for your search, as your application will need to make one less request to our API and thereby save time and bandwidth. However, we will continue to support both methods for searching for and listing legislation.

For search requests, append `/data.feed` immediately after `/search` and before the `?` character. For example, the following search requests a list of legislation with type `ukpga` and title containing the word "finance":

`https://www.legislation.gov.uk/search?type=ukpga&title=finance`

To retrieve the first page of the results as an Atom feed, append `/data.feed` to the end of the path like so:

`https://www.legislation.gov.uk/search/data.feed?type=ukpga&title=finance`

For list pages, append `/data.feed` to the end of the path, before the query string if present. For example, the first page of the list of all UK Statutory Instruments is:

`https://www.legislation.gov.uk/uksi`

To retrieve the first page as an Atom feed, append `/data.feed` to the end of the path like so:

`https://www.legislation.gov.uk/uksi`

For an example with a query string, the first page of the list of all UK Public General Acts with the word "finance" in the title is:

`https://www.legislation.gov.uk/ukpga?title=finance`

To retrieve the first page as an Atom feed, append `/data.feed` to the end of the path (before the `?` character) like so:

`https://www.legislation.gov.uk/ukpga/data.feed?title=finance`

If the address does not contain a `?` character, you can append `/data.feed` to the very end of the address.

Note that the default sort order on list web pages is different to that of feeds:

 * By default, list web pages are ordered by:
    * Legislation type in descending alphabetical order (the [internal type name](/model/uris/reference.md#legislation-types) is used for sorting)
    * Legislation year in descending order (most recent first)
    * Legislation number in descending order
 * By default, feeds are sorted by last modification date in descending order (where the last modification date is the last date any enacted or revised version of the item was created or changed)

A search address must always start with:

`https://www.legislation.gov.uk/search`

The address may then contain an optional subresource indicating the desired format of the results. Currently, the only available format is Atom, which is requested by the subresource `/data.feed`. If no subresource is specified, the API will return the preferred format specified by the `Accept` request header of the requesting application, or HTML if no preferred format is specified.

After the `/search` source and any subresource comes the query string, which begins with the `?` character and is then followed by a sequence of `name=value` pairs separated by the `&` character (for example, `?year=2000&number=13`).

A list page address has the following structure:

`https://www.legislation.gov.uk/[{type}][/{year} or {start-year}-{end-year}}][/{number} or {start-number}-{end-number}]/[/{extent}|{point-in-time}]`

A list page address may also have a query string, which may contain the `title`, `text` and/or `sort` parameters and, where a single type and year are specified in the path, additionally a `number` parameter. (If you want the API to return a *listing* with an item of legislation of a specific type, year and number you must specify the `number` parameter in the query string—otherwise the API will redirect you to the item of legislation itself.)

The parameters permit the following values:

|Parameter|Meaning|Permitted values (`/search`)|Permitted values (list page)|
|---|---|---|---|
|`type`|The type of the legislation (e.g. UK Public General Act)|Supports any of the [short type codes](/model/uris/reference.md#legislation-types), the super-categories `primary`, `secondary` and `eu-origin`, and the `all` wildcard type. To specify multiple values, use the parameter more than once (e.g. `type=ukpga&type=asp`)|Supports any of the [short type codes](/model/uris/reference.md#legislation-types), the super-categories `primary`, `secondary` and `eu-origin`, and the `all` wildcard type. To specify multiple values, separate them using the `+` character (e.g. `ukpga+asp`)|
|`year`|The calendar year of the enactment or registration of the item of legislation|Supports any four-digit year.||
|`start-year`|The lower limit of the desired range of calendar years of items of legislation|Supports any four-digit year. Must be less than or equal to `end-year`.||
|`end-year`|The upper limit of the desired range of calendar years of items of legislation|Supports any four-digit year. Must be greater than or equal to `start-year`.||
|`number`|The number of the item of legislation|Supports any [natural number](https://en.wikipedia.org/wiki/Natural_number) or `*` wildcard, as well as a natural number or `*` wildcard preceded by a [series number](/glossary.md#alternative-number) code (`c`, `l`, `w`, `s`, `ni`)||
|`start-number`|The lower limit of the desired range of numbers of items of legislation|Supports any natural number or `*` wildcard. If a natural number, must be less than or equal to `end-number`.||
|`end-number`|The upper limit of the desired range of numbers of items of legislation|Supports any natural number or `*` wildcard. If a natural number, must be greater than or equal to `start-number`.||
|`extent`|The geographical extent of an item of legislation|Supports the values `england`, `wales`, `scotland` and `ni`. To specify multiple values, use the parameter more than once (e.g. `extent=england&extent=wales`)|Supports the values `england`, `wales`, `scotland` and `ni`. To specify multiple values, separate them using the `+` character (e.g. `england+wales`)|
|`extent-match`|Whether to match any item with an extent that overlaps with the specified extent, or to only match items with the exact extent specified|Supports the values `applicable` (to specify that the extent of the item must overlap with the specified extent values) or `exact` (to specify that the extent of the item must exactly match the specified extent values)|Supports the value `=` to specify that the extent of the item must exactly match the specified extent values); otherwise treated as equivalent to `applicable`|
|`version`|Filters for the latest version that existed at the specified point in time|Supports a date in [ISO 8601 format](https://www.iso.org/iso-8601-date-and-time-format.html) (e.g. `2018-06-01`)||
|**Query string only parameters**||||
|`title`|A word, phrase or boolean search to match the title of the item of legislation|Supports any combination of words, phrases and boolean logic (see below)||
|`text`|A word, phrase or boolean search to match the text content of the item of legislation|Supports any combination of words, phrases and boolean logic (see below)||
|`sort`|The method to use to sort the list|Supports the values `published`, `title`, `modified`, `created`, `type` or any other value (e.g. `year` or `basic`) to sort by the "basic" sort order (see below). Defaults to `created` for feeds and the basic sort order on the website||

### Title and text search

Both the `title` and `text` parameters support simple text, phrase and Boolean queries, such as:

 * `boats` matches a document whose title/text contains the word "boats" (or "boat" - see [Stemming](#stemming) below)
 * `fishing boats` matches a document that contains the words "fishing" and "boats" (or "fish" or "boat" - see [Stemming](#stemming) below) anywhere within the title/text (not necessarily adjacent to or near one another)
 * `boats OR cars` matches a document that contains the words "boats" or "cars" (or "boat" or "car" - see [Stemming](#stemming) below) anywhere within the title/text
 * `"electric cars" AND batteries` matches a document that contains the exact phrase "electric cars" and the word "batteries" (or "battery" - see [Stemming](#stemming) below) anywhere within the title/text
 * `(fish AND dogs) OR ("electric cars" AND batteries)` matches a document that contains, anywhere within the title/text, either: 
    * the words "fish" and "dogs" (or "dog" - see [Stemming](#stemming) below), or 
    * the exact phrase "electric cars" and the word "batteries" (or "battery" - see [Stemming](#stemming) below)

Note that the Boolean operators `OR` and `AND` **must be in all-caps** or they will be treated as regular words.

If you specify a `text` search, the resulting feed will have a `<link rel="http://purl.org/dc/terms/tableOfContents">` element for each matching result with a URL for the item’s table of contents, containing the `text` parameter appended to the end. If you insert `/data.xml` before the `?` character in this URL and make a request to the resulting URL, the returned XML will contain the following information to identify the provisions/parts of the document with text that matches the query:

 * Each individual `<Contents*>` element may have a `MatchText="true"` attribute indicating that there is a text match within the corresponding part/provision of the document.
 * The `<Contents>` element may have a `MatchTextEntries` attribute, containing a space-separated list of the IDs of the provisions containing matching text, and/or one or more of the following pseudo-IDs:
    * `note` to indicate that there is matching text within the explanatory note (`<ExplanatoryNotes>`, available at `/note`)
    * `signature` to indicate that there is matching text within the signature (`<SignedSection>`, available at `/signature`)
    * `earlier-orders` to indicate that there is matching text within the "earlier orders" part of the document (`<EarlierOrders>`, available at `/earlier-orders`)
    * `introduction` to indicate that there is matching text within the introduction (`<IntroductoryText>`, available at `/introduction`)
    * `schedules` to indicate that there is matching text within the schedules (`<Schedules>`, available at `/schedules`)

#### Stemming

The search on legislation.gov.uk uses *stemming*, where words in a search and in the title and texts of documents are all mapped onto their common root word. By default, this means that:

 * searches containing a plural noun (dogs) will match the singular form of the noun (dog) and the singular form will match the plural
 * searches containing a verb will match all conjugations of that verb (i.e. “run” will match “ran” and “runs”, “protect” will match “protecting” and “protected”)

### Sort orders

You can specify the following sort orders for a legislation search/list using the `sort` query string parameter:

|Name|Order|
|---|---|
|`published`|<p>Sort by first publication date/time descending\*, then category (EU, then primary, then secondary), then year descending, then number descending, then enacted/made date descending <p>(\* If a correction slip has been issued for a document, the first publication date will be treated as the issuance date of the most recent correction slip for the document, not the date the document was originally published.)|
|`title`|Sort by title ascending in alphabetical order, then category (EU, then primary, then secondary), then year descending, then number descending, then enacted/made date descending|
|`modified`|Sort by last modified date descending, then category (EU, then primary, then secondary), then year descending, then number descending, then enacted/made date descending|
|`created`|Sort by category (EU, then primary, then secondary), then year descending, then enacted/made date descending|
|`type`|Sort by legislation type ascending in alphabetical order (using the [long type code](/model/uris/reference.md#legislation-types)), then year descending, then enacted/made date descending|
|"Basic" sort order|Default sort order for search result and list web pages. Also used if any other value apart from the above values is passed to the `sort` parameter, including an empty string. Sort by category (EU, then primary, then secondary), then year descending, then number descending, then enacted/made date descending)|

Note that the HTML and Atom view of the feeds have a different default sort order:

 * When viewing the HTML view, the default sort is "basic".
 * When viewing the Atom view, the default sort is `modified`.

## New legislation listings

The "new legislation" listings at [https://www.legislation.gov.uk/new](https://www.legislation.gov.uk/new) list newly published items of legislation by date and type, sorted in descending order of publication date and time. It does not include historical legislation newly uploaded to legislation.gov.uk, which is published with a “silent” flag that hides it from the new legislation listings.

The new legislation listings are available in Atom format at:

 * `https://www.legislation.gov.uk/new/data.feed`, which is equivalent to `https://www.legislation.gov.uk/all/data.feed?sort=published` but with all items hidden that were published with the "silent" flag;
 * `https://www.legislation.gov.uk/new/[yyyy-mm-dd]/data.feed`, which shows all items published on the specified date (except those with the "silent" flag);
 * `https://www.legislation.gov.uk/new/[type]/[yyyy-mm-dd]/data.feed` which shows all items of the specified type published on the specified date (except those with the "silent" flag).

These feeds support the same paging and sorting options as other legislation listings.

## Impact Assessment listings

The governments of the United Kingdom publish *impact assessments* (or IAs) for some items of legislation, and occasionally for policy areas where they plan to legislate.

IA searches and listings support some additional query string parameters:

|Parameter|Meaning|Permitted values|
|---|---|---|
|`stage`|The stage of the development of the legislation to which the IA relates.|One of `Options`, `Consultation`, `Development`, `Enactment`, `Final`, `Implementation`, `Post-Implementation`|
|`department`|The department that authored the IA.|The full name of the department, [URL-encoded](https://en.wikipedia.org/wiki/Percent-encoding) (e.g. DEFRA is specified as `Department%20for%20Environment%2C%20Food%20and%20Rural%20Affairs`)|

Note that UKIA listings and searches do not support the following parameters or parameter values:

 * extent (IAs do not have an extent as they are not legislation)
 * version (IAs are not amended)
 * number ranges (e.g. 1000-2000)
 * number or year wildcards (e.g. `/ukia/*/100` or `/ukia/2015/\*-100`)


## Identifier searches

The [identifier search page](https://www.legislation.gov.uk/id) is there to help you to find the correct identifier URI for a piece of legislation, particularly if you are trying to create links from other documents. For example, Hansard contains records of speeches which often quote legislation, such as the following contribution in a [debate on the 1993 Education Bill](https://hansard.parliament.uk/Lords/1993-06-14/debates/2624f9f9-3481-43f8-a80f-7b1dd595bba3/EducationBill?highlight=%22approved%20for%20appointment%20as%20auditors%20of%20that%20company%20by%20the%20audit%20commission%22#contribution-6bea8200-7902-46d2-8929-bc14dcc68e7a):

> There is nothing new in the concept that auditors shall, in appropriate circumstances, be approved by the Audit Commission. The Transport Act 1985 provides that a public transport company shall appoint only auditors who, in addition to being qualified under the Companies Act, shall be, “approved for appointment as auditors of that company by the Audit Commission”.

To mark up this information, it’s useful to be able to search based on the title of the legislation, with supporting information narrowing down the search. You can complete the form manually, or use it to create URIs of the form:

`http://www.legislation.gov.uk/id?title={title}&type={type}&year={year}&number={number}`

<!--TODO link to list of acceptable values for "type"-->

Any of the fields may be missing from the search, but the more you specify, the greater the likelihood of uniquely identifying the legislation. If a single item of legislation is identified by the query, the response will be a `301 Moved Permanently` that redirects you to the correct URI for the legislation. If multiple items are identified by the query, you will get a `300 Multiple Choices` response that lists the possibilities in an XHTML document.

Within the form, the title field should hold the query against which the title will be searched. The query is case-insenstive and punctuation sensitive. For example, the following will all return the same results:

`http://www.legislation.gov.uk/id?title=TRANSPORT`

`http://www.legislation.gov.uk/id?title=tRanSPort`

`http://www.legislation.gov.uk/id?title=transport`

The title query can take the `+`, `-` and `""` (double quote) operators. When a phrase is encapsulated in double quotes then that exact phrase is matched. For example, the following will match any title that contains the words 'Transport Act 1985' in that specific order:

`http://www.legislation.gov.uk/id?title="Transport+Act+1985"`

Words preceded by a '+' operator and not encapsulated in double quotes will match titles with those words though not in any given order. For example, the following two queries will return the same result:

`http://www.legislation.gov.uk/id?title=Act+Transport`

`http://www.legislation.gov.uk/id?title=Transport+Act`

Words preceded by a `-` operator and will match those titles that do not contain such a word. Multiple `-` operators will match those titles that do not contain all of the `-` operated words. For example, the folowing query will match any title that does not contain the word 'criminal' and the word 'law' but does contain the word 'act':

`http://www.legislation.gov.uk/id?title=Act -criminal -law`

These operators can be combined to form advanced queries. For example, the following will match any title that contains the phrase 'Greater london', the word 'Act' but does not contain the word 'criminal':

`http://www.legislation.gov.uk/id?title="Greater London" + Act -criminal`

If the result of the query is a single piece of legislation, you will be redirected to that piece of legislation.

On the other hand, if multiple items of legislation match the query, a list of possibilities will be returned with a 300 Multiple Choices response. For example:

`http://www.legislation.gov.uk/id?title=Companies+Act`

will result in a 300 Multiple Choices response containing

```
<ul>
  <li>
    <a href="http://www.legislation.gov.uk/id/uksi/1991/145">Act of Sederunt (Applications under Part VII of the Companies Act 1989) 1991</a>
  </li>
  <li>
    <a href="http://www.legislation.gov.uk/id/ukpga/Will4and1Vict/7/73">Chartered Companies Act 1837 (repealed 5.11.1993)</a>
  </li>
  <li>
    <a href="http://www.legislation.gov.uk/id/ukpga/Vict/47-48/56">Chartered Companies Act 1884 (repealed 5.11.1993)</a>
  </li>
  <li>
    <a href="http://www.legislation.gov.uk/id/apni/1960/22">Companies Act (Northern Ireland) 1960</a>
  </li>
  <li>
    <a href="http://www.legislation.gov.uk/id/ukpga/Geo6/10-11/47">Companies Act 1947</a>
  </li>
  ...
</ul>
```

The **type** and **year** parameters can help narrow down the search for legislation. For example, you might know that you are searching for a UK Public General Act, in which case type=ukpga will help narrow down the search. Searches over multiple types can be conducted by concatenating the type together with a '+' operator, in such a case type=ukpga+uksi will search on both UK Public General Act and UK Statutory Instruments. A wild card '*' operator type=* will search over all legislation. If the wild card and specific types are mixed (e.g. `type=*+uksi`), the result will be as per the wild card. The type parameter can take the same values as in the non-query URIs.

If you know the type, year and number of the legislation, perhaps through a more formal reference such as in:

> Ss. 6-9: power to modify conferred (E.W.) (1.8.2001 for W. and 26.10.2001 for E.) by 2000 c. 38, s. 134(2)(a); S.I. 2001/2788, art. 2, Sch. 1 para. 2; S.I. 2001/3342, art. 2, Sch.

then you can use the form to construct the URI for the item of legislation without having to be familiar with the template for URIs. For example:

`http://www.legislation.gov.uk/id?type=uksi&year=2001&number=2788`

This will redirect you directly to the correct URI for the item of legislation.

## Changes to legislation

You can retrieve a feed of changes to legislation using a URI of the following form:

`https://www.legislation.gov.uk/changes[/affected[/{type}[/{year}[/{number}]|{start-year}-{end-year}[/{number}]]]][/affecting[/{type}[/{year}[/{number}]|{start-year}-{end-year}[/{number}]]]]`

You can specify either one or both of the affected/affecting type, type and year, or type, year and number. Alternatively, you can substitute a range of years for the year.

Each `<entry>` in the feed contains a `<ukm:Effect>` element, which contains the following information:

 * the affected and affecting items of legislation, and optionally their titles
 * the affected and affecting provisions of the items
 * any items of legislation that the effect commenced in full or in part
 * the type of effect (e.g. "words substituted", "repealed", "restricted")
 * the in force date(s) of the effect
 * the commencement authority for the effect (the provision that specifies when the effect comes into force)
 * the geographical extent and territorial application of the effect
 * whether the effect has been applied or will be applied
 * any "savings" (provisions that qualify the application of the effect)

To interpret the contents of the `<ukm:Effect>` element, see the [Effects section of the CLML User Guide](https://legislation.github.io/clml-schema/userguide.html#effects).