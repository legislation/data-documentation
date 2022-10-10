# Limitations

This page describes the limitations of the Legislation API.

## Unapplied Effects

The legislation held within the API is sourced from the [Statute Law Database](http://www.statutelaw.gov.uk/) (SLD) and is a live version of the publishable data from that database. The legislation is somewhat out of date because the SLD itself is out of date; not all effects from recent years are reflected in the legislation that is made available.

Effects on legislation are only captured and incorporated into the text of certain types of legislation held on the API. For more information see [http://www.statutelaw.gov.uk/help/Primary\_Legislation\_(Revised).htm](http://www.statutelaw.gov.uk/help/Primary_Legislation_(Revised).htm). However, metadata about the content you access will tell you where there are known effects that have not yet been applied to the legislation. In the XML content, the `<ukm:UnappliedEffects>` element holds information about these unapplied effects.

## Content

The [history of the SLD](http://en.wikipedia.org/wiki/UK_Statute_Law_Database) is quite complex, but leads to the following limitations on the content held within the site:

*   [Secondary legislation](http://www.statutelaw.gov.uk/help/Secondary_Legislation.htm) is not revised (i.e amendments by subsequent legislation are not incorporated into the text) except for Northern Ireland Orders in Council. Although note that corrections (issued by correction slip) are applied to all legislation where applicable.
*   The originating text of SLD was derived from two earlier official hardcopy editions of revised primary legislation, Statutes in Force (SIF) and The Northern Ireland Statutes Revised (NISR). The final text of SIF was revised to 1 February 1991, and that of NISR to 1 January 2006. These dates form the basedates for SLD legislation, which means the dates from which revision work has been taken forward. There are two main implications of this:
    *   Only Primary Legislation (e.g. Public General Acts) at least partially in force at the basedate of 1 February 1991 is included and for Northern Ireland at the basedate of 1 January 2006
    *   No version history is available prior to these basedates
*   Only secondary legislation issued after the base date of 1 February 1991 is included. Note that Northern Ireland Statutory Rules and Orders in Council (that affect UK legislation) issued before the Northern Ireland base date of 1st January 2006 _are_ included back to 1991.

In addition, the data content of the API has not been through the full set of quality checks usually carried out on SLD data before documents are published therefore the completeness and accuracy of the data cannot be guaranteed.