# Fair Use Policy

We aim to support a wide range of users accessing legislation data and using the website in different ways. From users using the site in a professional or personal capacity, to crawlers (namely automated programs which systematically scan the Web) and institutions, we welcome anyone searching and browsing legislation, archiving the website or indexing it for search engines, and we encourage the downloading of data for re-use.

The non-human traffic on the website falls into several categories:
-	Crawlers for search indexes, such as web search engines
-	Site archiving, for instance national and international web archives
-	Commercial data re-users (e.g.: legal data services)
-	Academic/Individual data re-users – usually independent researchers looking to extract data

The legislation.gov.uk website contains over 300,000 documents and there are often many hundreds of ways users can view (sections of) each one. Some individual documents can also contain more than 10,000 pages worth of text. You can find information about our data and formats available through our API on our [formats](/formats/overview.md) page.

Some users can, accidentally or intentionally, place a greater demand on website services than others. For instance, users running automated scripts that request a very large number of pages within a short amount of time.

The aim of this policy it to set out our management strategy to ensure a fair use of the website for all, as well as optimising its performance for users
We apply this usage policy to all website users. No users or types of usage are given any priority or preferential treatment.

## Guidelines 

We want our website to be as open and inclusive as possible, but we also want it to be safe, secure, and available to everyone. For this reason, we have established a few ground rules for you to follow when using our website. Failure to comply with these rules may lead to denying your access to the website (see “Restrictions“ for more information).

### Identify yourself

If you are not using a browser, you must identify yourself, your web scraper or crawler with a legitimate user agent string in the `User-Agent` header of your request. We do not accept anonymous user agents (see [Restrictions](#restrictions)), therefore you must provide a clear identifier. 

We strongly recommend that you add contact details to your user agent&mdash;either an email address or a URL for a page that explains what your bot does and how to contact you. This means that we can contact you if there is a problem with your bot. You can find more details on the information we collect about you online and your rights by reading our [Privacy Notice](https://www.legislation.gov.uk/privacynotice). 

An example of a good identifier with email address is the following:

`My-Bot (contact@yourdomain.net)`

An example of a good identifier together with the link to the page is the following:

`My-Bot (https://yourdomain.net/mybot.html)`

### Follow our robots.txt

You must follow the rules in our robots.txt file (http://www.legislation.gov.uk/robots.txt). The robots.txt may specify how frequently and which pages you can or cannot crawl. These rules may change over time as we review this policy (see [Changes to this policy](#changes-to-this-policy)), so make sure to check them regularly.

### Stay under the rate limit

You must not exceed our request rate limit of 3,000 requests in any 5 minute period for each user agent. If you exceed the rate limit, our API will block your IP address until the average number of requests over the previous 5 minutes falls below the rate limit. Note that we rate-limit by IP address, not by user agent.

Use a reasonable crawl rate, to prevent overloading the website with requests. Follow the crawl-delay setting in our robots.txt, if provided. If the crawl-delay setting is not provided, use a conservative crawl rate (e.g.: 10 requests per 5-10 seconds).

### Consider using another way to get our data

If you want to:

 * carry out a large, one-off crawl of all or part of our content, or
 * you want to extract new legislation as it is published<!--TODO or uploaded, when publog is launched-->,

you should [use a different way](#other-ways-to-use-our-website) to download content.

### Talk to us if you have concerns

If you believe that:

 * either this policy or our robots.txt may prevent you from using, crawling or scraping our website as you require, or
 * your activity may have an impact on the performance or availability of our website or API, 

please [contact us](#contact-us) prior to taking any action.

## Restrictions

In order to preserve the security, stability, availability or integrity of our website, we reserve the right to suspend or modify any user’s access to our website if the user:

1.	Fails to comply with this policy
2.	Uses an anonymous user agent
3.	Disrupts, interferes or attempts to interfere with the normal and proper working of our website or take any action that places an unreasonable load on our website
4.	Deliberately attempts to circumvent this policy or uses the website in a malicious way

Furthermore, note that:
1.	We may temporarily decrease the rate limit or block users to deal with unexpected spikes in traffic
2.	We will add a specific crawl delay to a user agent, if the user’s total requests from multiple IP addresses causes excessive load on our API.
3.	If a user is being blocked for more than XXX<!--TODO fix--> days/weeks/months, we will write a comment on robots.txt specifying which user has been blocked and for what reason.
4.	We may block or modify any user’s access to our website for any other reason in our sole discretion (see [Changes to this policy](#changes-to-this-policy))

## Changes to this policy

We may revise this policy at any time (with or without notice) and when needed, in order to retain the correct functionality of the website (e.g.: in the event of significant changes to traffic).

You may want to check this page and the robots.txt page from time to time to take notice of any changes we make.

Some of the statements contained in this policy may also be superseded by statements published elsewhere on our site.

## Other ways to use our website 

If you find it difficult to follow our fair use policy, there may be an alternative way to get the content you need:

 * Use the [bulk downloads](/index.md#data-downloads) service if you are looking for a one-off data download or a significant sub-set of data. This service provides pre-packaged data downloads of all the data we hold on legislation.gov.uk. 
 * Use the [&ldquo;New Legislation&rdquo;](/api/search.md#new-legislation-listings) page if you are interested in extracting new published legislation. 

We encourage users to use these services where appropriate, instead of crawling the entire website or API. Doing so may save you (and us) time and money and free up server resources for other users.

## Contact us

We are happy to assist legitimate data users to acquire required data in a responsible fashion.

For this reason, if you require any further information about this policy, you feel you have been blocked in error or you are otherwise having difficulties, please [contact us](index.md#contact-us).