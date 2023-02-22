# PDF

We provide both dynamically generated PDFs of legislation content, and static PDFs of certain documents.

## Dynamically generated PDFs

Any item of legislation or subdivision of it that you can get as XML or HTML is also available as a dynamically generated PDF. To get an item or subdivision of legislation as PDF, append `/data.pdf` to a version URI.

The API dynamically generates a PDF the first time a user requests a PDF representation of a given resource, and then caches the generated PDF, which is returned instantly upon subsequent requests. If the PDF is not yet in the cache, the API will return a `202 Accepted` response, and you should repeat the request every 10 seconds or so until it returns a `200 OK` response containing the PDF (see the API documentation on [response codes](/api/overview.md#response-codes)).

For example, you can get the current version of the Education Act (Northern Ireland) 2014 as PDF at the following URI:

`http://www.legislation.gov.uk/nia/2014/12/data.pdf`

You can get the version of Part 4 of the Bankruptcy (Scotland) Regulations 2016 as it stood on 1/5/2017 at the following URI:

`http://www.legislation.gov.uk/ssi/2016/397/part/4/2017-05-01/data.pdf`

We also provide dynamically generated PDFs of the enacted, made or adopted version of an item or subdivision of legislation. You can get the enacted Welsh version of the cross-heading &ldquo;Cyffredinol&rdquo; of Part 3 of the Planning (Wales) Act 2015 at:

`http://www.legislation.gov.uk/anaw/2015/4/part/3/crossheading/cyffredinol/enacted/welsh/data.pdf`

However, if you want an entire enacted, made or adopted version of a whole item of legislation, you may find that there is a higher-quality static PDF of the enacted/made/adopted version

## Static PDFs

Some other documents are available as &ldquo;static&rdquo; PDFs. These are:

 * Original versions of legislation as printed
 * Revised PDF versions of legislation
 * Associated documents (such as Impact Assessments)
 * Correction slips and corrigenda

These documents do not follow a standardised URI scheme. You can find their URIs linked in the metadata of the document to which they are associated. The CLML user guide describes [how to identify associated documents in metadata]().