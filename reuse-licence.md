# Licensing and copyright: re-using data

We encourage the use and re-use of legislation.gov.uk data, with only a few conditions. 

## Open Government Licence

All content on legislation.gov.uk, and on our [Github page](https://github.com/legislation), is available under the [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/). The licence grants a worldwide, royalty-free, perpetual, non-exclusive licence to:

 * copy, publish, distribute and transmit our content;
 * adapt our content;
 * exploit our content commercially and non-commercially (for example, by combining it with other data, or by including it in your own product or application).

If you publish, distribute or transmit our content or data you have adapted from it, the licence requires you to provide or link to an attribution statement within your content, product or application that acknowledges the copyright, source and licence. If possible, the attribution statement should also link to the original licence. The following wording for acknowledgement is suggested:

 > © Crown and database right. Derived from content available under the [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/) from [legislation.gov.uk](https://www.legislation.gov.uk).

Some content on legislation.gov.uk is dual-licensed, which means you must comply with both the OGLv3.0 and an additional licence. The types of content we publish under dual licences are:

 * Content derived from EUR-Lex
 * Content derived from Westlaw

The below sections explain how to identify this content and comply with the licences.

## Content derived from EUR-Lex

Some legislation on legislation.gov.uk [originates from the EU](https://www.legislation.gov.uk/eu-origin), and is published under the duty and powers to publish relevant EU instruments and agreements which are assigned to The Kings’s Printer in Part 1 of Schedule 5 to the European Union (Withdrawal) Act 2018 (c. 16).

Where we have described legislation as ‘originating from the EU’, the item has been derived from [EUR-Lex](https://eur-lex.europa.eu) and published on legislation.gov.uk. EU legislation is published subject to the EUR-Lex copyright notice.

In addition to the legislation itself, we publish associated documents such as corrigenda (correction slips), and PDF versions of legislation both as originally adopted by the EU and as revised. We have also published [amendments](model/effects.md) made by EU legislation prior to the UK’s exit from the EU, data which are derived from EUR-Lex’s CELLAR database. The CELLAR stores and disseminates all content and metadata created or disseminated by the Publications Office of the European Union. It also drives the Publications Office’s major portals, including EUR-Lex.

### Re-using data derived from EUR-Lex

Data derived from EUR-Lex and published on legislation.gov.uk originate from two sources and are made available under two licences, **both** of which apply simultaneously:

 * Legislation originating from the EU is available for re-use under the terms of the [Commission Decision 2011/833/EU](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32011D0833).
 * Legislation published on legislation.gov.uk is available for re-use under the terms of the Open Government Licence v3.0.

You may re-use data for legislation originating from the EU and published on legislation.gov.uk and comply with both licences by acknowledging both Crown and EU copyright and not claiming any official endorsement in any onward publication of your re-use.

The following wording for acknowledgement is suggested:

 > Crown © and database right material re-used under the Open Government Licence (Logo containing link). Material derived from the European Institutions © European Union, 1998-2020 and re-used under the terms of the Commission Decision 2011/833/EU.

### EUR-Lex Copyright notice

We have reproduced below the [original copyright notice from EUR-Lex](https://webarchive.nationalarchives.gov.uk/eu-exit/20201231140419/https://eur-lex.europa.eu/content/legal-notice/legal-notice.html#2.%20droits):

> © European Union, 1998-2020
>
> The Commission’s document reuse policy is based on [Decision 2011/833/EU](https://webarchive.nationalarchives.gov.uk/eu-exit/20201231140419mp_/https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32011D0833). Unless otherwise specified, you can re-use the legal documents published in EUR-Lex for commercial or non-commercial purposes.
>
> Some documents, like the International Accounting Standards, may be subject to special conditions of use; these are mentioned in the respective Official Journal/document. You can also consult the [rules on on reproducing euro coin/note images](https://webarchive.nationalarchives.gov.uk/eu-exit/20201231140419mp_/https://ec.europa.eu/info/business-economy-euro/euro-area/euro-coins-and-notes/copyright-and-reproduction-rules-euro-coins-and-notes_en#reproduction-rules-for-coins).
>
> The copyright for the editorial content of this website, the summaries of EU legislation and the consolidated texts, which is owned by the EU, is licensed under the [Creative Commons Attribution 4.0 International licence](https://creativecommons.org/licenses/by/4.0/). This means that you can re-use the content provided you acknowledge the source and indicate any changes you have made.
>
> You may be required to clear additional rights if certain content depicts identifiable private individuals or includes third-party works. To use or reproduce content not owned by the EU, you may need to seek permission directly from the rights holders. Software or documents covered by industrial property rights, such as patents, trademarks, registered designs, logos and names, are excluded from the Commission’s reuse policy and are not licensed to you.
>
> To use the EUR-Lex logo, you first need the prior consent of the Publications Office.
>
> EUR-Lex metadata is dedicated to the public domain in accordance with the [Creative Commons CC0 1.0 Universal Public Domain Dedication deed](https://creativecommons.org/publicdomain/zero/1.0/).

For all other copyright issues, please contact: [op-copyright@publications.europa.eu](mailto:op-copyright@publications.europa.eu).

## Content derived from Westlaw
 
Westlaw UK have contributed electronic versions of Statutory Instruments and Statutory Rules and Orders, as they were first made, to legislation.gov.uk. These are the original versions of the legislation, so do not show how the information has changed or how it stands today. The legislation contributed by Westlaw UK was all made prior to 1987 and is in its original form.

Westlaw UK provide a commercial (pay for) service which provides the current version of these Statutory Instruments, Rules and Orders, showing how they are currently in force. For more information about Westlaw’s commercial services, including an online demo and free trial, visit [the Westlaw UK website](https://uk.westlaw.com/). Other companies provide similar commercial services.

Westlaw UK’s contribution to legislation.gov.uk means that the government is able to make secondary legislation from before 1987 available to the public, free of charge. The National Archives thanks Westlaw UK for their significant and important contribution, enabling greater public access to legislation.

### Identifying content derived from Westlaw

All content provided by Westlaw contains the following element in the `<ukm:Metadata>` element of its [XML representation](formats/xml.md):

`<dc:publisher>Westlaw</dc:publisher>`

In [XHTML](formats/html.md) pages (the default pages served by the website), Westlaw legislation contains the following element in the `<head>` element:

`<meta name="DC.publisher" content="Westlaw"/>`

### Re-using data derived from Westlaw

You can re-use all the text of the legislation on legislation.gov.uk under the terms of the Open Government Licence. If you are re-using the data contributed by Westlaw, either the HTML webpage or from the legislation.gov.uk API, you should make the following attribution:

 > Westlaw UK derived from Crown Copyright material and contributed to legislation.gov.uk
