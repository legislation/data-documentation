# Effects (amendments and commencements)

The text of a provision of legislation may *amend* (change) one or more provisions of another item, or items, of legislation (or, very rarely, itself). 

For example, [paragraph 7 of schedule 2 of the Civil Partnership (Scotland) Act 2020](https://www.legislation.gov.uk/asp/2020/15/schedule/2/paragraph/7) contains the following amendment to the Marriage and Civil Partnership (Scotland) Act 2014:

> (1) The Marriage and Civil Partnership (Scotland) Act 2014 is modified as follows.
>
> (2) In section 30 (renewed marriage or civil partnership following issue of full gender recognition certificate), in subsection (1)(b) for “both parties” substitute “a party (or both parties)”.

When a provision of legislation makes a change to one or more provisions of legislation, our editors record the change in our Editorial system as an *effect*. 

An effect is a record of the change that helps our editors track where (and when) to apply amendments and commencements. Effects help our readers and data re-users find changes made by legislation both before and after we have applied them.

Our API represents effects as XML using [CLML](../formats/xml.md). The [Effects section of the CLML User Guide](https://legislation.github.io/clml-schema/userguide.html#effects) contains more information on how to interpret effects in XML.

## Effect data

An effect contains information on the following:

|Field|Description|
|---|---|
|Effect type|The type of the effect, such as “inserted”, “words substituted”, “repealed”, “applied” or “modified”|
|Affecting provisions|The provision or provisions that contain the operative text of the amendment or commencement|
|Affected provisions|The provision or provisions that the amendment or commencement affects|
|Savings|One or more provisions that qualify the meaning of the effect, usually to preserve the previous meaning of the amended provisions in certain contexts|
|In force dates|This specifies one or more dates on which the amendment comes into force (if it is already in force or is due to come into force). An amendment may come wholly into force once, or may partly come into force one or many times for specific geographic extents or purposes|
|Commencement authority|One or more provisions that specify when the amendment comes into force (as an amending provision may come into force some time after it is enacted or made)|
|Extent and territorial application|The extent (see also the [geographical extent of provisions](legislation.md#geographical-extents)) and territorial application of the amending provision (or the amendment itself, if it has a different extent or TA) and of the amended provision (or the amended text or meaning, if that has a different extent or TA)|
|“Applied” and “requires applied” statuses|Indicates whether the amendment has been applied (to the English text, for dual-language items) and whether it needs to be applied. An amendment may not need to be applied if its amending or amended provisions were repealed before it came into force, or if we do not hold the text of the amended item. The Notes field will usually indicate why an effect does not need to be applied|
|“Welsh applied” and “requires Welsh applied” statuses|Indicates whether the amendment has been applied to the Welsh text of an item (where it exists) and whether it needs to be applied.|
|Effect notes|Explains to a reader any information relating to the effect, for example why it is marked as not to be applied|

An effect may also contain other information, such as the titles of the affecting and affected items, appended information for the amendment’s commentary (the `AppendedCommentary`` attribute), plus other information used internally within legislation.gov.uk.

The effect does not contain the amending text, and nor does it contain machine-readable instructions on how to apply the amendment to the amended provision (although our Editorial system can apply certain effects automatically, such as repeals, commencements and [non-textual amendments](../glossary.md#non-textual-amendment)).

The effect does link to the amending provision(s), which allows our editors to research how to apply the effect, and our readers to consult the text of any amendments themselves.

## URIs

An effect normally has a URI that contains the path `/id/effect/` followed by an unique identifer. For example, the URI for the revocation of S.I. 2000/1408 by [Schedule 1 of S.I. 2004/1315](http://www.legislation.gov.uk/id/uksi/2004/1315/schedule/I) is:

`http://www.legislation.gov.uk/id/effect/key-322c74ea5935adababe5cb5d4de686f6`

You can [view the data for this effect](http://www.legislation.gov.uk/changes/affected/uksi/2000/1408/affecting/uksi/2004/1315) on the legislation.gov.uk website, or as XML via the following API URI:

`http://www.legislation.gov.uk/changes/affected/uksi/2000/1408/affecting/uksi/2004/1315/data.feed`

The unique identifier for an effect may be any alphanumeric string containing dashes. For example, the URI for the substitution of words in section 26(5) of the Land Development Values (Compensation) Act (Northern Ireland) 1965 by [Schedule 4 of the Planning Act (Northern Ireland) 2011](http://www.legislation.gov.uk/id/nia/2011/25/schedule/4/paragraph/4) is:

`http://www.legislation.gov.uk/id/effect/upload-b7xquzz2-48`

In our [XML](../formats/xml.md) formats (including CLML and [feeds](../api/search.md)), the unique identifier normally appears on its own in the `EffectId` attribute of an `<Effect>` or `<UnappliedEffect>` element, rather than as a URI.

## Effects and the Editorial process

### Recording effects

When we publish a new item of legislation, our editors carry out research on the item to find out what amendments it contains, and then record those amendments as effects.

For example, [section 116 of the Adoption and Children Act 2002](http://www.legislation.gov.uk/id/ukpga/2002/38/section/116) contains the following amendments (note that according to [section 2(5)](http://www.legislation.gov.uk/id/ukpga/2002/38/section/2) of that Act, “the 1989 Act” refers to the [Children Act 1989 (c. 41)](http://www.legislation.gov.uk/id/ukpga/1989/41)):

 > **116 Accommodation of children in need etc.**
 >
 > (1) In section 17 of the 1989 Act (provision of services for children in need, their families and others), in subsection (6) (services that may be provided in exercise of the functions under that section) after “include” there is inserted “providing accommodation and”.
 > 
 > (2) In section 22 of that Act (general duty of local authority in relation to children looked after by them), in subsection (1) (looked after children include those provided with accommodation, with exceptions) before “23B” there is inserted “17”.
 > 
 > (3) In section 24A of that Act (advice and assistance for certain children and young persons aged 16 or over), in subsection (5), for “or, in exceptional circumstances, cash” there is substituted “and, in exceptional circumstances, assistance may be given—
 > 
 > &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(a) by providing accommodation, if in the circumstances assistance may not be given in respect of the accommodation under section 24B, or
 >
 > &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(b) in cash”.

Our editor read the whole document to identify the amendments and research the context for them, and noted the following:

*  The [introduction](https://www.legislation.gov.uk/ukpga/2002/38/introduction/enacted) of the Act states that the date of Royal Assent is the 7<sup>th</sup> November 2002, which is the date on which the Act’s provisions come into force unless otherwise stated.
*  [Section 148(1) of the Act](http://www.legislation.gov.uk/id/ukpga/2002/38/section/148/1) requires that the Secretary of State must bring the Act into force by order, but specifically excludes section 116 from that requirement. As there is no other provision specifying when section 116 comes into force, section 116 and its child provisions come wholly into force on the date of Royal Assent.
*  [Schedule 4](http://www.legislation.gov.uk/id/ukpga/2002/38/schedule/4) contains transitory provisions and [savings](../glossary.md#saving) (provisions that qualify effects in the Act). [Paragraphs 6-8](https://www.legislation.gov.uk/ukpga/2002/38/schedule/4#schedule-4-paragraph-6) of Schedule 4 all begin with “Nothing in this Act affects”, and so are treated as [savings](../glossary.md#saving) that qualify all effects in the Act.

The editor then recorded the amendments in the above section as the following effects:

|Affected Legislation|Affected provision(s)|Type of Effect|Affecting Extent|Affecting Legislation|Affecting Provision|Sav|Commencement Authority|IF Date1|IF Date1 Qualification|
|--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |
|1989 c. 41|s. 17(6)|words inserted|Same as affected|2002 c. 38|s. 116(1)|Sch. 4 para. 6-8|s. 148(1)|07/11/2002|wholly in force|
|1989 c. 41|s. 22(1)|word inserted|Same as affected|2002 c. 38|s. 116(2)|Sch. 4 para. 6-8|s. 148(1)|07/11/2002|wholly in force|
|1989 c. 41|s. 24A(5)|substituted|Same as affected|2002 c. 38|s. 116(3)|Sch. 4 para. 6-8|s. 148(1)|07/11/2002|wholly in force|

### Applying effects

When one of our editors update an item of legislation, they use our Editorial system to create a new version of the item. The Editorial system instructs the editor which amendments to apply to the version, and the editor then amends the text of the version using those instructions, as well as those contained in the amending provision of legislation from which the effect originates.

The Editorial system automatically adds [revision tags](https://legislation.github.io/clml-schema/userguide.html#revised-legislation) and [commentaries](https://legislation.github.io/clml-schema/userguide.html#commentaries) for the amendments that they apply. For recently applied amendments, both the revision tags and commentaries have identifiers that link them to the effect.

(Although most amendments are applied this way, some amendments either pre-date the current Editorial system or are applied manually. These have identifiers that do not correspond to an effect.)
