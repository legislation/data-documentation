# Fair Use Policy


Legislation.gov.uk supports a wide range of users to access legislation data in different ways, including

* people searching and browsing the site, whether in a professional or personal capacity,
* commercial and institutional use, and
* crawlers (automated programs which systematically scan websites).

The National Archives welcome anyone searching and browsing legislation, archiving the website or indexing it for search engines, and we encourage the downloading of data for re-use.

The non-human traffic to legislation.gov.uk falls into several categories:

* Crawlers for search indexes (e.g. web search engines)
* Site archiving (e.g. national and international web archives)
* Other commercial data re-users (e.g. legal data services)
* Academic/individual data re-users (e.g. independent researchers looking to extract data)

The legislation.gov.uk website contains over 300,000 documents and there are often many hundreds of ways users can view (segments of) each one. Some individual documents can also contain more than 10,000 pages worth of text. You can find information about our data and formats available through the legislation.gov.uk API on our the [Formats](formats/overview.md) page.

Some users can, accidentally or intentionally, place a greater demand on website services than others. For instance, users running automated scripts that request a very large number of pages within a short amount of time.

The aim of this policy is to ensure fair access to legislation.gov.uk for all users whilst providing a suitable level of performance. The
policy applies to all website users. There is no offer of priority or preferential treatment to any group of users or type of usage.

## Policies

Legislation.gov.uk must be as open as possible, but also safe, secure and available to everyone. For this reason, there are a few ground rules to follow when using the website. Failure to comply with these rules may lead to denied access to the website (see [Restrictions](#restrictions) for more information).

### Identify yourself

If you are not using a browser, you must identify yourself, your web scraper or crawler, with a legitimate user agent string in the `User-Agent` header of your request. Anonymous user agents are not accepted (see [Restrictions](#restrictions)), and so your user agent must contain a clear identifier.

It is strongly recommended you add contact details to your user agent—either an email address, or a URL for a page that explains what your bot does and how to contact you—so we can contact you if there is a problem with your bot. You can find more details on the information we collect about you online and your rights by reading the [Privacy Notice](https://www.legislation.gov.uk/privacynotice).

The following is an example of a user agent containing a good identifier with an email address:

`My-Bot (contact@yourdomain.net)`

The following is an example of a user agent containing a good identifier with a link to a web page:

`My-Bot (https://yourdomain.net/mybot.html)`

### Follow legislation.gov.uk's robots.txt file

You must follow the rules in the site's robots.txt file (http://www.legislation.gov.uk/robots.txt). The robots.txt may specify how frequently and which pages you can or cannot crawl. These rules may change over time as we review this policy (see [Changes to this policy](#changes-to-this-policy)), so make sure to check them regularly.

### Stay under the rate limit

You must not exceed our request rate limit of 1,500 requests in any 5 minute period. If you exceed the rate limit, the API may block your requests until the average number of requests over the previous 5 minutes falls below the rate limit. This limit applies to users not IP addresses, so you will  exceeding the limit if you use multiple IP addresses that collectively make more than 1,500 requests in a 5 minute period.

Use a reasonable crawl rate to prevent overloading the website with requests. Follow the crawl-delay setting in our robots.txt, if provided. If the crawl-delay setting is not provided, use a conservative crawl rate (e.g. 10 requests per 5-10 seconds).

### Consider using another way to get legislation.gov.uk data

If you want to:

* carry out a large, one-off crawl of all or part of our content, or
* you want to extract new legislation as it is published or republished,

you should [use a different way](#other-ways-to-use-our-website) to download content.

### Talk to us if you have concerns

If you believe that:

* either this policy or the rules in the robots.txt may prevent you from using, crawling or scraping legislation.gov.uk as you require, or
* your activity may have an impact on the performance or availability of legislation.gov.uk or its API,

please [contact us](#contact-us) prior to taking any action.

## Restrictions

To preserve the security, stability, availability and integrity of legislation.gov.uk, we reserve the right to suspend or modify any user’s access to our website if the user:

* fails to comply with this policy;
* uses an anonymous user agent;
* disrupts, interferes or attempts to interfere with the normal and proper working of legislation.gov.uk or takes any action that places an unreasonable load on legislation.gov.uk;
* deliberately attempts to circumvent this policy or otherwise uses legislation.gov.uk in a malicious way.

Furthermore, note that:

* we may temporarily decrease the rate limit or block users to deal with unexpected spikes in traffic;
* we will add a specific crawl delay to a user agent if the user’s total requests from multiple IP addresses causes excessive load on the legislation.gov.uk API;
* we may block or modify any user’s access to our website for any other reason at our sole discretion (see [Changes to this policy](#changes-to-this-policy)).

## Changes to this policy

We may revise this policy at any time, with or without notice, in order to maintain an acceptable level of functionality and performance of the legislation.gov.uk website and API (e.g. in the event of significant changes to traffic).

You may want to check this page and the robots.txt file from time to time to take notice of any changes we make.

Some of the statements contained in this policy may also be superseded by statements published elsewhere on our legislation.gov.uk.

## Other ways to use our website

If you find it difficult to follow our this policy, there may be an alternative way to get the content you need:

<!-- TODO: re-enable when bulk downloads online * Use the [bulk downloads](index.md#data-downloads) service if you are looking for a one-off data download or a significant sub-set of data. This service provides pre-packaged data downloads of all the data we hold on legislation.gov.uk.-->

* Use the [“New Legislation”](api/search.md#new-legislation-listings) feed if you are interested in extracting new published legislation.
* Use the [Publication Log](api/publication-log.md) feed if you are interested in extracting any kind of new or updated content, including updates to legislation or resources already published.

We encourage users to use these services where appropriate to their needs, instead of crawling the entire website or API. Doing so may save you time and money, and free up server resources for other users.

## Contact us

We are happy to assist data users to acquire our data in a responsible fashion.

If you need any further information about this policy, you feel you have been blocked in error or you are otherwise having difficulties, please [contact us](index.md#contact-us).
