# History of our data collection

## HM Stationery Office

In the beginning, there was HM Stationery Office (HMSO)—a government department with statutory responsibility for official publishing in hard copy, created by statute. The office was created in the 1940s, long before the appearance of computers, and so only published legislation in print.

Throughout the years, its responsibility has shifted several times: once part of the Treasury, it then became part of the Cabinet Office, the Home Office and the Treasury Solicitor’s office (the Government’s legal service before the Government Legal Department came into being) in turn. 

HMSO owned its own presses and published bound volumes and individual print copies of legislation, as well as other government publications. One series of publications printed HMSO printed was Statutes in Force (SIF), which were printed volumes of revised primary legislation.

## HMSO splits

In the <!--TODO which??? -->late 1980s/early 1990s, the HMSO legislation function split across multiple departments. The printing of newly enacted legislation remained with HMSO; the team responsible for adminstering the submission and registration of legislation moved to the Cabinet Office<!--TODO is this right??? -->; and the editorial team that revised legislation for Statutes in Force became the Statutory Publications Office (SPO), moving to the Lord Chancellor’s department. As a result, the publication of new legislation was completely separate from the team who were making revised versions of the Statutes in Force.

## Electronic publication

Some time after this split began the electronic publication of legislation. 

HMSO were the first to electronically publish legislation online, uploading copies of new legislation to their website. In the mid-1990s, the printing function of HMSO was privatised as The Stationary Office (TSO), and the remainder of HMSO became the Office of Public Sector Information (OPSI), which kept the statutory responsibility to register Statutory Instruments (SIs) and oversee publication of legislation. 

OPSI developed and launched a new website onto which they published new enacted legislation, as HMSO had done before. <!--TODO is this right?? chronology doesn’t make sense to me-->As part of digitisation, OPSI also developed the first markup language for UK legislation—the Crown Legislative Markup Language (CLML). This initially came into being as an SGML schema, then becoming an XML schema when OPSI began digital online publishing of legislation in the 1990s. 

Around the same time in the early 1990s, SPO decided to digitise the Statutes in Force and make an online version available to government users. SPO built the Statutory Law Database (SLD) website, which they launched in 2006, and created their own XML schema. The database contained historical primary legislation that was still in force as of the 1<sup>st</sup> February 1991, except for local acts and public general acts with “local character”, statute law repeals, legislation items that applied exclusively to Scotland or Northern Ireland, and documents largely consisting of amendments. They also included copies of all new primary and secondary legislation published from 1991 onwards (with the exception of Northern Ireland legislation), which meant that the SLD collection replicated all enacted data from 1991 onwards that was available on the OPSI website.

This meant that, as of the late 2000s, two different government legislation websites coexisted: the Statutory Law Database website containing enacted legislation from 1991 onwards, as well as a collection of revised Public General Acts, and the OPSI website containing only enacted legislation.

## Northern Ireland legislation

OPSI and SPO were only responsible for publishing legislation for Great Britain. Responsibility for publishing legislation in Northern Ireland was granted separately to the Northern Ireland Statutory Publication Office (NI SPO), which was responsible for both publishing bound volumes and making revised versions. Before the launch of the Statue Law Database website, the NI SPO worked with SPO to translate NI SPO’s primary legislation data to the SLD format and publish it on the SLD website (as SLD did not publish secondary legislation). The data NI SPO provided for the SLD database was revised up to the 1<sup>st</sup> January 2006, and so Northern Ireland legislation data in SLD had no versions available before that date.

## OPSI and SPO join forces and legislation.gov.uk launches

In 2006, OPSI became part of the National Archives. SPO became part of the [Ministry of Justice (MOJ)](https://www.gov.uk/government/organisations/ministry-of-justice) in 2007, before it also moved to the National Archives in 2008. There, OPSI and SPO unified once more and merged into one team, known as Legislation Services, which is responsible for the publication of both enacted and revised legislation. As part of this merger, the teams merged their datasets into a single dataset using a common format. This became the initial dataset for legislation.gov.uk, which replaced both the SLD and the OPSI legislation websites.

## Post-merger data ingestion activities

The majority of the data on legislation.gov.uk came from the merger of the OPSI and SLD data collections. All legislation subsequently acquired by legislation.gov.uk (besides newly published legislation) has come from outside data donations or digitisation of print material, of which the five major data ingestion activities below are the most notable:

1.  At launch, enacted data on legislation.gov.uk only went back to 1988. There was thus an effort by The National Archives to try to increase the historical collection of enacted data for older documents from 1801 onwards by scanning printed legislation and uploading it as PDF, in order to ensure that all revised versions available on the website had their corresponding enacted version. 
2.	A great amount of historical data (in CLML format) was donated by Westlaw to The National Archives as part of the Red Tape Challenge, a government initiative to review legislation and reduce burden. The aim of the Red Tape Challenge was to make a list of all legislation that was in force and identify law that was not needed. The selection of donated data was chosen by subject theme, with a mix of primary and secondary legislation. 
3.	Another major collection is the Department for Work and Pensions’ legislation data, derived from a series of print volumes known after their colour as the “blue and orange volumes”. DWP maintained revised versions of social security legislation in their own systems up until 2020, when they joined up with the National Archives to digitise their data and maintain revised versions using legislation.gov.uk’s existing web publication and editorial systems.
4.	A very large dataset was digitised by Northern Ireland, as a result of an initiative to make all NI secondary legislation available online.
5.  As part of the United Kingdom’s exit from the European Union, legislation.gov.uk ingested hundreds of thousands of EU legislation documents from EUR-Lex, the website of the Publications Office of the EU (see below).

## EUR-Lex ingest

<!--TI 15/9/2021: This is just a general introduction, without any technicalities. Are we going to write a section on the technical process to achieve this? Or directly provide your article somewhere? -->

Prior to January 2020, the UK was a member of the European Union (EU). As such, directly applicable EU legislation was law in the UK by virtue of the [European Communities Act 1972](https://www.legislation.gov.uk/id/ukpga/1972/68), with the Publications Office of the European Union being responsible for the publication of EU legislation.

The UK left the EU on 31 January 2020, but during the “transition period” that ran for the remainder of 2020 almost all EU law continued to apply in the UK. On 31 December 2020, EU legislation entirely ceased to apply in the UK. To ensure legal continuity, a UK Act of Parliament, the [European Union (Withdrawal) Act 2018](https://www.legislation.gov.uk/id/ukpga/2018/16), made provision for relevant EU legislation in force at the end of 2020 to become part of UK domestic law. This “retained direct EU legislation” (or “assimilated direct legislation” from the end of 2023) initially replicated EU legislation as it was in force on exit day, including amending legislation made up until the end of the transition period. Over time, the EU and UK versions will diverge as EU institutions modify EU laws and the UK parliament repeals or replaces retained direct EU legislation inherited from EUR-Lex.

Schedule 5 of the European Union (Withdrawal) Act 2018 created a new duty for the King’s Printer of Acts of Parliament, an officer at The National Archives, to publish EU legislation that was incorporated into UK domestic law. 

To fulfil this obligation, The National Archives identified relevant legislation documents on EUR-Lex, extracted underlying data and published this new dataset on legislation.gov.uk. 

This obligation resulted in a large-scale data migration exercise. Over 150,000 EU legislation documents, with over 300,000 individual document versions and accompanying metadata files, were identified and successfully migrated to the legislation.gov.uk database—a doubling of the previous size of the collection.
