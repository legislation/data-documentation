# History of our data collection

In the beginning, there was Her Majesty's Stationery Office (HMSO)&mdash;a government department with statutory responsibility for official publishing in hard copy, created by statute. Long before the appearance of computers, the office was created in the 1940s, thus only publishing in print.

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

# Other data ingestion activities

The majority of the data on legislation.gov.uk, therefore, came from these two collections. Everything that has been subsequently acquired has come from either donations or digitisation, with four major data ingestions activities that can be recalled:

1.	Before this point in history, enacted data on legislation.gov.uk only went back to 1988. There was thus an effort by The National Archives to try to increase the historical collection of enacted data for older documents from 1801 forwards, by providing scanned and OCRed PDFs, hence making sure that all revised versions available on the website had their corresponding enacted version. 
2.	A great amount of historical data (in CLML format) was donated to The National Archives as part of the Red Tape Challenge – a government initiative to review legislation and reduce burden, with the aim of making a list of all legislation that was in force and identifying law that was not needed. Selection of donated data was chosen by subject theme, with a mix of primary and secondary legislation. 
3.	Another major collection is the Department for Work and Pensions’ data (blue and orange volumes). DWP were maintaining social security legislation in their own system up until they joined up with the National Archives, which started digitising their data and including it into legislation.gov.uk.
4.	A very large dataset was digitised by Norther Ireland, as a result of an initiative to make all NI secondary legislation available online.

## EUR-Lex ingest

<!--TI 15/9/2021: This is just a general introduction, without any technicalities. Are we going to write a section on the technical process to achieve this? Or directly provide your article somewhere? -->

Even if for different reasons, another major data ingestion activity was the inclusion of EU legislation to legislation.gov.uk.

In fact, prior to January 2020, the UK was a member of the European Union (EU). As such, directly applicable EU legislation was law in the UK by virtue of the Treaties on European Union and the European Communities Act 1972, with the Publications Office of the European Union being responsible for the publication of EU legislation through the EUR-Lex website.

However, on 31 December 2020, EU legislation as published on EUR-Lex ceased to apply in the UK. To ensure legal continuity a UK Act of Parliament, the European Union (Withdrawal) Act 2018 (c.16), made provision for relevant EU legislation in force at the end of 2020 to become part of UK domestic law. This “retained direct EU legislation” initially replicates the legislation text, including amending legislation, as published on EUR-Lex. Over time the EU and UK versions will diverge as EU institutions modify EU laws and the UK parliament amends and replaces the retained direct EU legislation inherited from EUR-Lex.

Schedule 5 of the European Union (Withdrawal) Act 2018 (c.16) created a new duty for the Queen’s Printer of Acts of Parliament, an officer at The National Archives, to publish the EU legislation that was incorporated into UK domestic law. 

To fulfil this obligation, The National Archives identified relevant legislation documents on EUR-Lex, extracted underlying data and published this new dataset on www.legislation.gov.uk. 

This obligation resulted in a large-scale data migration exercise - over 150,000 EU legislation documents, with over 300,000 individual document versions and accompanying metadata files were identified and successfully migrated to the www.legislation.gov.uk database: a doubling of the previous www.legislation.gov.uk database collection.