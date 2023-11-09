# The legislation.gov.uk data model

Legislation.gov.uk provides many different kinds of data about different things. Our data model describes how the things relate to one another and how we represent information about them in our data.

The key concepts we represent in our data are:

 * Items and subdivisions of **[legislation](legislation.md)**, which represent in abstract a particular law or part independently of its text or any version of it;
 * **[Versions](legislation.md#versions)** of items of legislation and their subdivisions, which embody the text of an item or a given division as it stood at a particular point in time (and, for dual-language legislation, in a particular language);
 * **[Effects](effects.md)** and commencements, where an item of legislation either changes or brings into force one or more provisions of legislation.

## URIs (Uniform Resource Identifiers)

We identify things in our data using URIs (short for “uniform resource identifier”). A URI is an identifier that looks like an address of a page or resource on a website. In many cases these URIs *are* functioning web addresses: we say that it is possible to **resolve** these URIs, which means that if you open the URI in a web browser or other suitable application, you can get a page or resource that represents the thing that the URI identifies.

The following are examples of legislation.gov.uk URIs:

 * `http://www.legislation.gov.uk/id/ukpga/1985/67` identifies the [Transport Act 1985](http://www.legislation.gov.uk/id/ukpga/1985/67)
 * `http://www.legislation.gov.uk/uksi/2013/376/regulation/12/2015-03-27` identifies [regulation 12 of the Universal Credit Regulations 2013, as it stood on 27/3/2015](http://www.legislation.gov.uk/uksi/2013/376/regulation/12/2015-03-27)
 * `http://www.legislation.gov.uk/anaw/2016/3/part/3/enacted/welsh/data.pdf` identifies the [PDF manifestation of the Welsh enacted version of Part 3 of the Environment (Wales) Act 2016](http://www.legislation.gov.uk/anaw/2016/3/part/3/enacted/welsh/data.pdf)
 * `http://www.legislation.gov.uk/id/effect/key-f8ca0da7874670764680c0bcf1a72bbe` identifies an effect from article 59(9) of the Criminal Justice (Northern Ireland) Order 2008, substituting words in article 21(2) of the Road Traffic (Northern Ireland) Order 1995
 * `http://www.legislation.gov.uk/def/legislation/NorthernIrelandAct` identifies the legislation type “Act of the Northern Ireland Assembly”

A URI identifies the same item or resource across legislation.gov.uk. Whatever part of our data set you use, a given URI will always refer to the same thing.

All our URIs start with `http://www.legislation.gov.uk/` and follow a consistent **URI scheme**. You can find out more about the URIs for each type of data in the section for that type, and about the scheme in the [URI scheme reference](reference.md) section of the guide.
