# Overview of our dataset

We publish the following data on legislation.gov.uk:

 * The **original texts** of legislation as it was enacted, made, adopted or otherwise created
 * The **revised texts** of legislation, as updated by the legislation.gov.uk Editorial team
 * **Amendments** to legislation, where an item of legislation amends another item of legislation (or itself)

We **only publish some legislation and amendments** on legislation.gov.uk.

<!--
<table>
<thead><tr><th>Legislation we <b>do</b> publish<th>Legislation we <b>don't</b> publish</th></tr></thead>
<tbody>
<tr>
<td>
<ul>
<li>Newly published primary and secondary legislation</li>
<li>Most EU Regulations, Decisions and Directives</li>
<li>All UK Public General Acts since 1988</li>
<li>All UK Local Acts since 1991</li>
<li>All UK Statutory Instruments since 1987, except for Local Statutory Instruments and non-prints</li>
<li>All Local and non-print UK Statutory Instruments since 2011</li>
<li>All Welsh Statutory Instruments, except for Local Statutory Instruments and non-prints</li>
<li>All Local and non-print Welsh Statutory Instruments since 2011</li>
<li>All Scottish Statutory Instruments, except for Local Statutory Instruments and non-prints</li>
<li>All Local and non-print Scottish Statutory Instruments since 2007</li>
<li>All Northern Ireland Statutory Rules since 1996, except for Local Statutory Instruments and non-prints</li>
<li>All Local and non-print Northern Ireland Statutory Rules since 2011</li>
<li>All Acts of Senedd Cymru</li>
<li>All Acts and Measures of the National Assembly for Wales</li>
<li>All Acts of the Scottish Parliament</li>
<li>All Acts of the Northern Ireland Assembly</li>
<li>Some older UK Statutory Instruments and NI Statutory Rules</li>
<li>Some older Statutory Rules and Orders (UK and NI)</li>
<li>Some older Local and non-print Statutory Instruments and Rules</li>
<li>Some historical Acts from the UK, Great Britain, England, Scotland and Ireland</li>
</ul>
</td>
<td>
<ul>
<li>Most Local Statutory Instruments and Rules</li>
<li></li>
<li></li>
<li>Bye-laws</li>
</ul>
</td>
</tr>
</tbody>
</table>
-->

<!--TI 15/9/21: This is a general introduction to legislation.gov.uk – I guess it is not really needed here? -->

The www.legislation.gov.uk website, owned and maintained by The National Archives, provides public access to UK legislation online. All new legislation made by UK parliaments, and government departments, in England, Wales, Scotland and Northern Ireland is submitted to The National Archives’ systems for publication on the www.legislation.gov.uk website and in print.

In addition to publication of new legislation, The National Archives is also responsible for the provision of revised (consolidated) versions of existing UK legislation that incorporate legislative amendments. The Legislation Services Editorial Team has the task of identifying new amendments to existing legislation and creating revised versions of documents that incorporate these changes. These revised documents are made available on www.legislation.gov.uk alongside the original versions.

In this guide you can find information about how legislation.gov.uk works, what data we hold and how you can access and re-use our data. This guide is not only aimed at technical users or developers who want to get their hands on legislation data, but it is for anyone interested in understanding our data model and how the service works.

## What data is held on legislation.gov.uk

<!--TI 15/9/21: This whole section is already on the website, although I have slightly changed it – should we remove it? Keep the same version as the one online or change it considerably?-->

Legislation.gov.uk holds over 300,000 items of legislation and thousands of versions (both as enacted and revised), carrying most (but not all) types of legislation and their accompanying explanatory documents, such as impact assessments. 

We hold UK legislation from 1267 to present day, with all primary legislation from 1988 available on the site, and most pre-1988 primary legislation. In some cases we only have the original published (as enacted) version and no revised version. This occurs if the legislation was wholly repealed before 1991 and therefore was not included in the revised data set when it was extracted from Statutes in Force. In other cases we may only have a revised version if the original (as enacted) version is not available in a web-publishable format.

We also hold legislation originating from the European Union, including corrigenda (correction slips for EU legislation) and EU Directives published up to EU exit (see EU Legislation and UK Law for more information), published up to the end of the EU Exit Implementation Period at 11:00 p.m. on 31 December 2020 ("IP completion day").

Legislation on legislation.gov.uk is provided in multiple different formats, such as XML, HTML – if you interested in knowing more on the formats available on the website and how to access them, see XXXXXX.

 * We provide legislation in multiple formats – see the section on Formats.
 * We also hold a list of changes to legislation, both applied and unapplied.
 * We hold all legislation in English, and we also hold most Welsh legislation in Welsh
 * There are some limitations in the data we hold – for example we do not hold all UK or EU legislation. You can find out more in the Limitations section.

## History of our data collection

In the beginning, there was Her Majesty's Stationery Office (HMSO)&mdash;a government department with statutory responsibility for official publishing in hard copy, created by statute/law. Long before the appearance of computers, the office was created in the 1940s, thus only publishing in print.

Throughout the years, its responsibility has shifted several times: once part of the Treasury, it was then part of the Cabinet Office, the Home Office and the Treasury Solicitor’s office – the Government’s legal team before government legal service came into existence. 

Not only owning the press, HMSO published bound volumes, print copies of legislation, as well as other government publications. One of the publications that HMSO created was the Statutes in Force (SIFs), namely print copy of revised primary legislation.

In the late 1980s/early 1990s, the HMSO team was split: the publication of new legislation stayed in HMSO, with the team going to Cabinet Office, while the team that made the Statutes in Force (the editorial team) became the Statutory Publications Office (SPO), going to the Lord Chancellor’s department. In this way, the publication of new legislation was completely separate from the team who were making revised versions of the Statutes in Force.

At this point, computers and digitisation came into play/happened. 

HMSO were the first publishing their website with copies of new legislation online. In the mid 1990s, the HMSO website was privatised and HMSO became the Office of Public Sector Information (OPSI). The printing function of HMSO was privatised as The Stationary Office (TSO), but HMSO kept the statutory responsibility – they still had the responsibility to do registering of Statutory Instruments (SIs) and overseeing publications. In this context, the OPSI website was developed and launched, with new enacted data. As part of digitisation, OPSI also developed the first markup language for UK legislation – the Crown Legislative Markup Language (CLML) – initially as an SGML schema, then becoming an XML schema when they moved to digital online publishing in the 1990s. 

In the same way, in the early 1990s, SPO decided to digitise the Statutes in Force thus making online versions available. SPO built the Statutory Law Database (SLD) website (launched in 2006) and created their own schema. The databased contained English and Welsh primary legislation that was in force in 1991, except local acts and public general acts with “local character”, statute law repeals, pieces of legislation that applied exclusively to Scotland or Northern Ireland, and documents largely consisting of amendments. From 1991, they also acquired copies of all new primary (with the exception of Northern Ireland) and secondary legislation, so that they could start applying more amendments – meaning that the SLD collection replicated all enacted data from 1991 onwards that was available on the OPSI website. 

Therefore, at the time, two different websites were coexisting: the Statutory Law Database website containing enacted data and a collection of Public General Acts that were revised, and an OPSI website containing enacted data.

In the background, responsibility for publishing legislation in Northern Ireland was different/separate. In Norther Ireland there was the Northern Ireland Statutory Publication Office (NI SPO), responsible for publishing bound volumes and making revised versions. Before the SLD website launched, NI SPO teamed up with SPO, translating their data to SLD language and only publishing Northern Ireland Primary legislation on the SLD website (they did not update secondary legislation). Compared to other data, one major difference is that Northern Ireland data does not have the SIF date that most have, namely February 1991. On the contrary, their basedate is the 1st of January 2006.

At this point, there were the OPSI team publishing enacted on the OPSI website and the SPO team publishing on the SLD website. The Lord Chancellor’s Department became the Department of Constitutional Affairs and then part of the Ministry of Justice (MoJ). 

Finally, the two teams that had been split up re-joined themselves and moved department - respectively from the Cabinet Office and MoJ to The National Archives. As a consequence, also the two websites and databases merged, thus creating legislation.gov.uk which translated all the data from the two systems and maintained all of the links to them.

## Other data ingestion activities

The majority of the data on legislation.gov.uk, therefore, came from these two collections. Everything that has been subsequently acquired has come from either donations or digitisation, with four major data ingestions activities that can be recalled:

1.	Before this point in history, enacted data on legislation.gov.uk only went back to 1988. There was thus an effort by The National Archives to try to increase the historical collection of enacted data for older documents from 1801 forwards, by providing scanned and OCRed PDFs, hence making sure that all revised versions available on the website had their corresponding enacted version. 
2.	A great amount of historical data (in CLML format) was donated to The National Archives as part of the Red Tape Challenge – a government initiative to review legislation and reduce burden, with the aim of making a list of all legislation that was in force and identifying law that was not needed. Selection of donated data was chosen by subject theme, with a mix of primary and secondary legislation. 
3.	Another major collection is the Department for Work and Pensions’ data (blue and orange volumes). DWP were maintaining social security legislation in their own system up until they joined up with the National Archives, which started digitising their data and including it into legislation.gov.uk.
4.	A very large dataset was digitised by Norther Ireland, as a result of an initiative to make all NI secondary legislation available online.

### EUR-Lex ingest

<!--TI 15/9/2021: This is just a general introduction, without any technicalities. Are we going to write a section on the technical process to achieve this? Or directly provide your article somewhere? -->

Even if for different reasons, another major data ingestion activity was the inclusion of EU legislation to legislation.gov.uk.

In fact, prior to January 2020, the UK was a member of the European Union (EU). As such, directly applicable EU legislation was law in the UK by virtue of the Treaties on European Union and the European Communities Act 1972, with the Publications Office of the European Union being responsible for the publication of EU legislation through the EUR-Lex website.

However, on 31 December 2020, EU legislation as published on EUR-Lex ceased to apply in the UK. To ensure legal continuity a UK Act of Parliament, the European Union (Withdrawal) Act 2018 (c.16), made provision for relevant EU legislation in force at the end of 2020 to become part of UK domestic law. This “retained direct EU legislation” initially replicates the legislation text, including amending legislation, as published on EUR-Lex. Over time the EU and UK versions will diverge as EU institutions modify EU laws and the UK parliament amends and replaces the retained direct EU legislation inherited from EUR-Lex.

Schedule 5 of the European Union (Withdrawal) Act 2018 (c.16) created a new duty for the Queen’s Printer of Acts of Parliament, an officer at The National Archives, to publish the EU legislation that was incorporated into UK domestic law. 

To fulfil this obligation, The National Archives identified relevant legislation documents on EUR-Lex, extracted underlying data and published this new dataset on www.legislation.gov.uk. 

This obligation resulted in a large-scale data migration exercise - over 150,000 EU legislation documents, with over 300,000 individual document versions and accompanying metadata files were identified and successfully migrated to the www.legislation.gov.uk database: a doubling of the previous www.legislation.gov.uk database collection.

## Data Completeness 

The datasets that we provide are:

 * Legislation document data
 * Associated documents and explanatory notes/memoranda  
 * Changes to legislation

### Limitations

As shown in the History of our Data Collection and Data Completeness sections, the legislation database is both large/big – with more than 300,000 items of legislation - and complex - with data collections deriving from different sources. These two factors lead to a number of limitations on the content held within the database:

-	Not all legislation on the website is up-to-date and not all changes to Secondary legislation are in the dataset.
-	Not all documents are available in all formats. For instance, some documents are only available in PDF format. For more information on the formats available on the website and how to access them, see XXXXXX.
-	Images within documents do not have ALT text, that is a text describing non-text content such as pictures. ALT text serves several purposes: to allow people with visual or cognitive impairments to read when utilising screen readers; to display a descriptive text in place of a non-loaded image; to provide a semantic meaning to non-text content for search engines.
-	Completeness and accuracy of the data of documents from before the base date cannot be guaranteed as documents might be missing (e.g.: no longer in force, non-print legislation before 2012) or have been rekeyed or OCRed and may contain errors. However, all other legislation - including older versions of revised legislation (post-basedate) - should be present. 

## Data Updates

New legislation is published on legislation.gov.uk simultaneously - as quickly as we can once we are authorised to publish it – which is generally within 48 hours of it being enacted, made or laid, and appears on the New Legislation page and feeds. Any document which is especially complex in terms of its size or its typography may take longer to prepare and, sometimes, we publish PDFs for some items of new legislation before XML is available. Data is sometimes altered after it is first published. This can occur in a few scenarios: a formal correction of the legislation (e.g. a correction slip); the correction of data versions to better represent the official PDF version; or a reprint/reissue of the relevant legislation item.

It is possible to subscribe to the legislation feeds to get details of the latest legislation as soon as it is published without having to check the new legislation page each day. You can find more details about this service by reading the New Legislation page. <!--TI 15/9/22: Do we need to explain here how to subscribe to the feed, considering that many users do not seem to understand how it works? Or should we just improve the guide on the New Legislation page? -->

For revised legislation, information about effects are extracted and added to the Changes to Legislation page as quickly as we can, although it can take up to six weeks if the document is large or if there is a high volume of new legislation (for more information see Our editorial practice and timescales). 

If you are interested in knowing when a document has last changed, it is possible to check this information by opening the XML format of the document and looking at the dc:modified value. To know how to access the XML format of a document, as well as other formats, see XXXXXX.

Usually, documents (either enacted or revised) are not removed from legislation.gov.uk except in rare cases with agreement of the originating department where the item was not valid law, e.g. if it was published because of administrative error or if a court judgment has ruled that it was invalid. If data are missing from legislation.gov.uk then this is usually because we do not yet hold it.

## Caching Strategy

Legislation.gov.uk, by nature of its content, is subjected to an extremely large volume of traffic on a daily basis. To address the need to improve performance and serve content quickly and efficiently, without overloading server and network architecture, legislation.gov.uk has been implementing a web cache solution. This cache is a temporary high-speed data storage layer of frequently accessed data, with the purpose of increasing data retrieval performance by reducing the need to access data’s primary slower storage location. 

On the website, a Time to Live (TTL) mechanism has been implemented which determines how long the content can be cached before a check needs to be made for an updated version.

New, as enacted legislation does not exist in the cache and therefore is always up to date, as well as all related summary pages on the website such as http://www.legislation.gov.uk/new, http://www.legislation.gov.uk/new/ukpga, http://www.legislation.gov.uk/ukpga, etc. where the cache is purged. <!--TI 15/9/22: Not sure whether is this indeed the case? Also, which is the current caching strategy for publishing changes to existing legislation? Is the cache purged every time there is an update? 
-->

However, other pages on the website have different Time to Live rules, such as search pages where the TTL is set to 1 hour. As a consequence, this means that it could take up to an hour for search results to be reflected on the relevant pages – leading to a temporary displaying of out of date information. In these cases, in order to bypass the cache and load the latest version of a page, it is recommended to perform a hard refresh of the browser in use. 

## Licensing and copyright: re-using data

We encourage the use and re-use of legislation.gov.uk data, with only a few conditions. In fact, all content on legislation.gov.uk is available under the Open Government Licence v3.0 except where otherwise stated (see below).

### Content derived from EUR-Lex

Some legislation on legislation.gov.uk originates from EUR-Lex, and is published under the duty and powers to publish relevant EU instruments and agreements which are assigned to The Queen’s Printer (and Chief Executive of The National Archives) in the European Union (Withdrawal) Act 2018 (c. 16) Schedule 5 Part 1.

Where we have described legislation as ‘originating from the EU’, the item has been derived from EUR-Lex and published on legislation.gov.uk. Browse all legislation originating from the EU to see the documents included in the dataset, which includes Regulations, Decisions, Directives and selected Treaties and Agreements. EU legislation is published subject to the EUR-Lex copyright notice.

Additional to the legislation types, there are associated documents published alongside the legislation such as Corrigendum (correction slips), and PDF versions of legislation both as originally adopted by the EU and as ‘revised’. We have also published amendment information relating to amendments between EU legislation documents prior to the UK’s exit from the EU, which is derived from the CELLAR. The CELLAR stores and disseminates all content and metadata created or disseminated by the Publications Office of the European Union. It also drives the Publications Office's major portals, including EUR-Lex.

#### Re-using data derived from EUR-Lex

UK legislation is available for re-use under the terms of the Open Government Licence v3.0 (OGL).

EU legislation is available for re-use under the terms of the Commission Decision 2011/833/EU. You may re-use UK law derived from the EU (legislation originating from the EU) and comply with both licences by acknowledging these two sources and not claiming any official endorsement in any onward publication of your re-use. The following wording for acknowledgement is suggested:

 > Crown © and database right material re-used under the Open Government Licence (Logo containing link). Material derived from the European Institutions © European Union, 1998-2019 and re-used under the terms of the Commission Decision 2011/833/EU.

#### EUR-Lex Copyright notice

For reference the copyright notice from EUR-Lex copyright notice can be read below.

> Copyright notice
> 
> © European Union, 1998-2019
> 
> Except where otherwise stated, reuse of the EUR-Lex data for commercial or non-commercial purposes is authorised provided the source is acknowledged ('© European Union, https://eur-lex.europa.eu, 1998-2019').
>
> The reuse policy of the European Commission is implemented by the Commission Decision of 12 December 2011.
>
> Some documents, like the International Accounting Standards, may be subject to special conditions of use, which are mentioned in the respective Official Journal.
>
> The EUR-Lex logo may not be used without the prior consent of the Publications Office.
> 
> The reproduction rules of the Euro coins and notes are described here. <!-- TODO fix-->
>
> For all other copyright issues regarding EUR-Lex, please contact: op-copyright@publications.europa.eu.

### Content derived from Westlaw
 
To support the government's deregulation initiative, Westlaw UK have contributed electronic versions of Statutory Instruments, Statutory Rules and Orders, as they were first made, to legislation.gov.uk. These are the original versions of the legislation, so do not show how the information has changed or how it stands today. The legislation contributed by Westlaw UK was all made prior to 1987 and is in its original form.

Westlaw UK provide a commercial (pay for) service which provides the current version of these Statutory Instruments, Rules and Orders, showing how they currently in force. For more information about Westlaw's commercial services, including an online demo and free trial, visit www.westlaw.co.uk. Other companies provide similar commercial services.

Westlaw UK's contribution to legislation.gov.uk means that the government is able to make secondary legislation from before 1987 available to the public, free of charge. The National Archives thanks Westlaw UK for their significant and important contribution, enabling greater public access to legislation.

#### Re-using data derived from Westlaw

You can re-use all the text of the legislation on legislation.gov.uk under the terms of the Open Government Licence. If you are re-using the data contributed by Westlaw, either the HTML webpage or from the legislation.gov.uk API, you should make the following attribution.

"Westlaw UK derived from Crown Copyright material and contributed to legislation.gov.uk"

### How to identify contributors

It is possible to find out who contributed to a specific document by opening the XML format of the document and looking at the dc:publisher value within the Metadata section. For instance, XML data contributed by Westlaw shows “Westlaw” as value for the dc:publisher element. To know how to access the XML format of a document, as well as other formats, see XXXXXX.

## Fair Use Policy

We aim to support a wide range of users accessing legislation data and using the website in different ways. From users using the site in a professional or personal capacity, to crawlers (namely automated programs which systematically scan the Web) and institutions, we welcome anyone searching and browsing legislation, archiving the website or indexing it for search engines, and we encourage the downloading of data for re-use.

The non-human traffic on the website falls into several categories:
-	Crawlers for search indexes, such as web search engines
-	Site archiving, for instance national and international web archives
-	Commercial data re-users (e.g.: legal data services)
-	Academic/Individual data re-users – usually independent researchers looking to extract data

The legislation.gov.uk website contains over 300,000 documents and there are often many hundreds of ways users can view (sections of) each one; some individual documents can also contain more than 10,000 pages worth of text. You can find information about our data and formats available through our API at XXXX.

Some users can, accidentally or intentionally, place a greater demand on website services than others. For instance, users running automated scripts that request a very large number of pages within a short amount of time.

The aim of this policy it to set out our management strategy to ensure a fair use of the website for all, as well as optimising its performance for users
We apply this usage policy to all website users. No users or types of usage are given any priority or preferential treatment.

### Guidelines 

We want our website to be as open and inclusive as possible, but we also want it to be safe, secure, and available to everyone. For this reason, we have established a few ground rules for you to follow when using our website. Failure to comply with these rules may lead to denying your access to the website (see “Restrictions“ for more information).

1.	If you are not using a browser, you must identify yourself, your web scraper or crawler with a legitimate user agent string. We do not accept anonymous user agents (see “Restrictions”), therefore you must provide a clear identifier. An example of a good identifier is the following: 
EXAMPLE
In addition, we recommend that you add an email address to your identifier.
This means that we can contact you if there is any problem with your user agent.
You can find more details on the information we collect about you online and your rights by reading our Privacy Notice. An example of a good identifier with email address is the following:
EXAMPLE Furthermore, we recommend that you create a page that explains what you are doing and why, and link back to the page in your user agent string. 
An example of a good identifier together with the link to the page is the following:
EXAMPLE MY-BOT (https://yoursite.com/mybot.html)

2.	Respect the rules of our robots.txt (http://www.legislation.gov.uk/robots.txt). The robots.txt may specify how frequently and which pages you can or cannot crawl.
­	These rules may change over time, as we review this policy (see section “Changes to this policy”), so make sure to check them regularly.

3.	Respect our request rate limit of XXX requests per second for each user agent. Note that we rate-limit by IP address, regardless of browser/agent type.

4.	Use a reasonable crawl rate, to prevent overloading the website with requests.
­	Respect the crawl-delay setting in robots.txt, if provided.
­	If the crawl-delay setting is not provided, use a conservative crawl rate (e.g.: X request per XX-XX seconds).

5.	If you are (1) looking for a one-off data download or (2) interested in extracting new published legislation, use our dedicated services rather than scraping/crawling the whole website (see “Other ways to use our website” section).

6.	If you believe that (1) this policy or the robots.txt prevent you from using, crawling or scraping our website or that (2) your activity may have an impact on our website, contact us prior to taking any action (see “Contact us” section).

### Restrictions

In order to preserve the security, stability, availability or integrity of our website, we reserve the right to suspend or modify any user’s access to our website if the user:

1.	Fails to comply with this policy
2.	Uses an anonymous user agent
3.	Disrupts, interferes or attempts to interfere with the normal and proper working of our website or take any action that places an unreasonable load on our website
4.	Deliberately attempts to circumvent this policy or uses the website in a malicious way

Furthermore, note that:
1.	We may temporarily decrease the rate limit or block users to deal with unexpected spikes in traffic
2.	We will add a specific crawl delay to a user agent, if the user’s total requests from multiple IP addresses exceeds XXX.
3.	If a user is being blocked for more than XXX days/weeks/months, we will write a comment on robots.txt specifying which user has been blocked and for what reason.
4.	We may block or modify any user’s access to our website for any other reason in our sole discretion (see “Changes to this policy” section)

### Changes to this policy

We may revise this policy at any time (with or without notice) and when needed, in order to retain the correct functionality of the website (e.g.: in the event of significant changes to traffic).

You may want to check this page and the robots.txt page from time to time to take notice of any changes we make.

Some of the statements contained in this policy may also be superseded by statements published elsewhere on our site.

## Other ways to use our website 

You can access data on www.legislation.gov.uk using the legislation API, but you can also access our data using the bulk-download service and the ‘new legislation’ page.
­
Use the bulk download service if you are looking for a one-off data download or a significant sub-set of data. This service provides pre-packaged data downloads of all the data we hold on legislation.gov.uk. You can find more details about this service by reading [page]
­
Use the ‘New Legislation’ page if you are interested in extracting new published legislation. 

You can find more details about this service by reading the New Legislation page.

We encourage all users to use these services which make the access to specific types of data easier, instead of scraping/crawling the whole website to get the same type of information.

## Contact us

We are happy to assist legitimate data users to acquire required data in a responsible fashion.

For this reason, if you require any further information about this policy, if you feel you have been blocked in error or are having difficulties, please email data.legislation@nationalarchives.gov.uk with your enquiry and a member of our team will respond to you as soon as possible. 
