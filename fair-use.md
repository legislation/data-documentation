# Fair Use Policy

We aim to support a wide range of users to access legislation data and use legislation.gov.uk in different ways, including users using the site in a professional or personal capacity, institutional and commercial users, and crawlers (automated programs which systematically scan websites). We welcome anyone searching and browsing legislation, archiving the website or indexing it for search engines, and we encourage the downloading of data for re-use.

The non-human traffic we receive on legislation.gov.uk falls into several categories:

 *	Crawlers for search indexes, such as web search engines
 *	Site archiving, for instance national and international web archives
 *	Other commercial data re-users (e.g. legal data services)
 *	Academic/individual data re-users (usually independent researchers looking to extract data)

The legislation.gov.uk website contains over 300,000 documents and there are often many hundreds of ways users can view (sections of) each one. Some individual documents can also contain more than 10,000 pages worth of text. You can find information about our data and formats available through our API on our [formats](/formats/overview.md) page.

Some users can, accidentally or intentionally, place a greater demand on website services than others. For instance, users running automated scripts that request a very large number of pages within a short amount of time.

The aim of this policy is to ensure fair access to legislation.gov.uk for all users whilst providing a suitable level of performance. We apply this usage policy to all website users. We do not provide or offer priority or preferential treatment to any group of users or type of usage.

## Policies 

We want our website to be as open and inclusive as possible, but we also want it to be safe, secure, and available to everyone. For this reason, we have established a few ground rules for you to follow when using our website. Failure to comply with these rules may lead to denying your access to the website (see [Restrictions](#restrictions) for more information).

### Identify yourself

If you are not using a browser, you must identify yourself, your web scraper or crawler with a legitimate user agent string in the `User-Agent` header of your request. We do not accept anonymous user agents (see [Restrictions](#restrictions)), and so your user agent must contain a clear identifier. 

We strongly recommend that you add contact details to your user agent—either an email address, or a URL for a page that explains what your bot does and how to contact you. This means that we can contact you if there is a problem with your bot. You can find more details on the information we collect about you online and your rights by reading our [Privacy Notice](https://www.legislation.gov.uk/privacynotice). 

The following is an example of a user agent containing a good identifier with an email address:

`My-Bot (contact@yourdomain.net)`

The following is an example of a user agent containing a good identifier with a link to a web page:

`My-Bot (https://yourdomain.net/mybot.html)`

### Follow our robots.txt

You must follow the rules in our robots.txt file (http://www.legislation.gov.uk/robots.txt). The robots.txt may specify how frequently and which pages you can or cannot crawl. These rules may change over time as we review this policy (see [Changes to this policy](#changes-to-this-policy)), so make sure to check them regularly.

### Stay under the rate limit

You must not exceed our request rate limit of 3,000 requests in any 5 minute period for each IP address. If you exceed the rate limit, our API will block your IP address until the average number of requests over the previous 5 minutes falls below the rate limit.

Use a reasonable crawl rate to prevent overloading the website with requests. Follow the crawl-delay setting in our robots.txt, if provided. If the crawl-delay setting is not provided, use a conservative crawl rate (e.g. 10 requests per 5-10 seconds).

### Consider using another way to get our data

If you want to:

 * carry out a large, one-off crawl of all or part of our content, or
 * you want to extract new legislation as it is published or republished,

you should [use a different way](#other-ways-to-use-our-website) to download content.

### Talk to us if you have concerns

If you believe that:

 * either this policy or our robots.txt may prevent you from using, crawling or scraping our website as you require, or
 * your activity may have an impact on the performance or availability of our website or API, 

please [contact us](#contact-us) prior to taking any action.

## Restrictions

In order to preserve the security, stability, availability or integrity of our website, we reserve the right to suspend or modify any user’s access to our website if the user:

 * fails to comply with this policy;
 * uses an anonymous user agent;
 * disrupts, interferes or attempts to interfere with the normal and proper working of our website or takes any action that places an unreasonable load on our website; or
 * deliberately attempts to circumvent this policy or otherwise uses the website in a malicious way.

Furthermore, note that:

 * we may temporarily decrease the rate limit or block users to deal with unexpected spikes in traffic;
 * we will add a specific crawl delay to a user agent if the user’s total requests from multiple IP addresses causes excessive load on our API;
 * if a user is being blocked for more than XXX<!--TODO fix--> days/weeks/months, we will add a comment to our robots.txt file specifying which user has been blocked and for what reason; and
 * we may block or modify any user’s access to our website for any other reason at our sole discretion (see [Changes to this policy](#changes-to-this-policy)).

## Changes to this policy

We may revise this policy at any time, with or without notice, in order to maintain an acceptable level of functionality and performance of the website and API (e.g. in the event of significant changes to traffic).

You may want to check this page and the robots.txt page from time to time to take notice of any changes we make.

Some of the statements contained in this policy may also be superseded by statements published elsewhere on our site.

## Other ways to use our website 

If you find it difficult to follow our fair use policy, there may be an alternative way to get the content you need:

 * Use the [bulk downloads](/index.md#data-downloads) service if you are looking for a one-off data download or a significant sub-set of data. This service provides pre-packaged data downloads of all the data we hold on legislation.gov.uk. 
 * Use the [&ldquo;New Legislation&rdquo;](/api/search.md#new-legislation-listings) feed if you are interested in extracting new published legislation. 
 * Use the [Publication Log](/api/publication-log.md) feed if you are interested in extracting any kind of new or updated content, including updates to legislation or resources already published.

We encourage users to use these services where appropriate to their needs, instead of crawling the entire website or API. Doing so may save you (and us) time and money and free up server resources for other users.

## Contact us

We are happy to assist legitimate data users acquire our data in a responsible fashion.

If you need any further information about this policy, you feel you have been blocked in error or you are otherwise having difficulties, please [contact us](index.md#contact-us).