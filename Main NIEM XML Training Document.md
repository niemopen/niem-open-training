![NIEMOPEN Logo](/Intro_Graphics/NIEMOPEN_logo.png)

# Main NIEM 6 Training Document

# Introduction

## Purpose

Deliver a NIEM 101 course for executives and project managers as well as a techical course focused on preparing developers and implementers to use NIEM.

## Supporting Documents

All materials are available on the NIEM Training Github repo at [https://github.com/niemopen/niem-open-training](https://github.com/niemopen/niem-open-training). Specific materials used are listed on the README page and include:

- **Main NIEM Training Document**
	- [Main NIEM Training Document (XML)](https://github.com/niemopen/niem-open-training/blob/main/Main%20NIEM%20XML%20Training%20Document.md)
	- [Main NIEM Training Document (JSON)](https://github.com/niemopen/niem-open-training/blob/main/Main%20NIEM%20JSON%20Training%20Document.md)
- [Individual module documents](https://github.com/niemopen/niem-open-training/tree/main/Modules)
- [Mapping Spreadsheets](https://github.com/niemopen/niem-open-training/tree/main/Mapping_Spreadsheets)
- [Ersatz Textual Instances](https://github.com/niemopen/niem-open-training/tree/main/Text_Document)

## Sample Message Specification

- [Crash Driver Message Specification](https://github.com/niemopen/niem-open-training/tree/main/Crash%20Driver%20IEPD)

## Agenda

- Logistics
- Introduction to NIEM
- Introduction to Message Spec / IEPD Development
	- Scenario Planning
	- Requirements Analysis
	- Mapping
		- Intro to Mapping
			- Mapping to Existing Objects
		- Creating New Objects
		- External Standards
	- Creating and Validating Schemas
	- Assembly
	- Publishing
	- Implementation
- Resources
___
## Logistics and Background

- Major revamp of prior training programs
- Updated for NIEM 6
- Send questions to info@niemopen.org
- This document and supporting materials are at:
	- https://github.com/niemopen/niem-open-training/
___
## Introduction to NIEM

- What is NIEM?
- The Scope of NIEM
- NIEM Harmonization and Organization
- NIEMOpen and OASIS Open Projects
___
### What is NIEM? - Framework
- NIEM is a community-driven, government and jurisdiction-wide, standards-based approach to exchanging information
- Diverse communities can collectively leverage NIEM to increase efficiencies and improve decision-making
- NIEM is available to everyone, including public and private organizations
- NIEM includes a data model, governance, training, tools, technical support services, and an active community to assist users in adopting a standards-based approach to exchanging data

![NIEM Framework](/Intro_Graphics/NIEM_Framework.png)
___
### What is NIEM? – Interop Problem
- If we don’t understand what each other means, we won’t be able to exchange info
- Need a common language for defining things

![Interop Problem](/Intro_Graphics/Interop_Problem_scaled.png)
___
### What is NIEM? And what it's not?
**NIEM is:**
- a common vocabulary
- a means of enabling efficient information exchange across diverse public and private organizations

**NIEM is not:**
- a system or database
- a means of specifying how to transmit or store data
___
### What is NIEM? – Exchanging Data and Components
- Using NIEM, organizations come together to agree on a common vocabulary
- When additional organizations are added to the information exchange, the initial NIEM exchange can be reused, saving time and money

![Exchanging Data and Components](/Intro_Graphics/Exch_Data_Components.png)
___
### What is NIEM? – Simplified Exchanges
- When using NIEM, you only need to “speak” two languages: your own and NIEM

| Without NIEM | With NIEM |
| --- | --- |
|![Scrambled Exchanges](/Intro_Graphics/Scrambled_Exchanges.png)|![Centralized Exchanges](/Intro_Graphics/Centralized_Exchanges.png)|
___
### Scope of NIEM
- NIEM is a data layer standard and intentionally does not address all the necessary technologies needed for information sharing
- Exchange partners decide how to store and process the NIEM-conformant data being exchanged

![Scope of NIEM 01](/Intro_Graphics/Scope_NIEM_01.png)

![Scope of NIEM 02](/Intro_Graphics/Scope_NIEM_02.png)
___
### Scope of NIEM - Open Source Interconnection (OSI) model

**Detailed:**

![OSI Detailed](/Intro_Graphics/OSI_01_clean.png)

**Simplified:**

![OSI Simplified](/Intro_Graphics/OSI_02.png)
___
### Bottle of Liquid
**A bottle of liquid:**

| ![Bottle 01](/Intro_Graphics/Bottle_01.png) | ![Bottle 02](/Intro_Graphics/Bottle_02.png) |
| --- | --- |
| Has some combination of liquids inside | NIEM is the liquid inside, the payload document |
| Has a shape | NIEM doesn’t care about the shape |
| Made of certain materials | NIEM doesn’t care about what the bottle is made out of or how it's constructed |
| Can be opaque or transparent | NIEM doesn’t care about whether you can see into the bottle |
| Is moved around by various means | NIEM doesn’t care about how you move the bottle around |
| Can be filled and emptied | NIEM doesn’t care about how you filled it or what you do with the liquid later |

___
### NIEM Harmonization and Organization

- Think of the NIEM data model as a mature and stable data dictionary of agreed-upon terms, definitions, relationships, and formats independent of how information is stored in individual agency systems
- The data model consists of two sets of closely related vocabularies:
	- NIEM core
	- Individual NIEM domains
- NIEM core includes data elements commonly agreed upon across all NIEM domains (i.e., person, activity, location, and item, etc.)
- Individual NIEM domains contain mission-specific data components that build upon NIEM core concepts

![Domain Diagram](/Intro_Graphics/Domain_Diagram_scaled.png)

| Existing Domains                              | Upcoming Domains             |
| --------------------------------------------- | ---------------------------- |
| Agriculture                                   | International Human Services |
| Biometrics                                    |                              |
| Chemical, Biological, Radiological, & Nuclear |                              |
| Cyber                                         |                              |
| Emergency Management                          |                              |
| Human Services                                |                              |
| Immigration                                   |                              |
| Infrastructure Protection                     |                              |
| Intelligence                                  |                              |
| International Trade                           |                              |
| Justice                                       |                              |
| Learning and Development                      |                              |
| Maritime                                      |                              |
| Military Operations                           |                              |
| Screening                                     |                              |
| Surface Transportation                        |                              |

**Domains hold objects specific to their domains:**

| Agriculture | Biometrics |
| --- | --- |
| ![Agriculture](/Domain_Graphics/ag.png) | ![Biometrics](/Domain_Graphics/biom.png) |

| Chemical, Biological, Radiological, & Nuclear | Emergency Management |
| --- | --- |
| ![CBRN](/Domain_Graphics/cbrn.png) | ![Emergency Management](/Domain_Graphics/em.png) |

| Human Services | Immigration |
| --- | --- |
| ![Human Services](/Domain_Graphics/hs.png) | ![Immigration](/Domain_Graphics/im.png) |

| Infrastructure Protection | Intelligence |
| --- | --- |
| ![Infrastructure Protection](/Domain_Graphics/ip.png) | ![Intelligence](/Domain_Graphics/intel.png) |

| International Trade | Justice |
| --- | --- |
| ![International Trade](/Domain_Graphics/it.png) | ![Justice](/Domain_Graphics/j.png) |

| Maritime | Military Operations |
| --- | --- |
| ![Maritime](/Domain_Graphics/m.png) | ![Military Operations](/Domain_Graphics/mo.png) |

| Screening  | Surface Transportation |
| --- | --- |
| ![Screening ](/Domain_Graphics/scr.png) | ![Surface Transportation](/Domain_Graphics/st.png) |


**NIEM Versioning**

- NIEM has major and minor versions, plus domain updates
- Major version releases, e.g. 5.2 to 6.0
	- Every 3 years
	- All bets are off
	- NIEM-Core can and will change
		- Underlying infrastructure can also change
	- Domains can change
	- Domains are harmonized
		- Combination of tools and human collaboration to reach consensus
		- Repeated content is collapsed
		- Misplaced content is moved, either to other domains or to core
		- New content is added
	- _Nothing_ in a major version change is guaranteed to be backwards compatible with earlier major releases
	- NIEM 6.0 schemas out now, support documentation mid-2025
- Minor version releases, e.g. 5.1 to 5.2:
	- Annually
	- **NIEM-Core does not change!**
		- **Neither does the underlying infrastructure**
	- Domains can change
	- Domains can be harmonized
	- Domains can be added, like Cyber in 5.1
	- Domains are not guaranteed to be backwards compatible with earlier minor releases
		- But they often are
	- NIEM 6.1 is planned
- Domain updates are done per-domain
	- Domains can update their content in between minor releases
	- Those updates then are normally folded into the next minor release
- Older versions never go away
	- You can still use NIEM 1.0 (but shouldn't)
	- There are plenty of NIEM 2.0 exchanges in current use
- Migration
	- Don't have to migrate
	- May want to migrate if a newer version gives you functionality you need (and you're already making changes)
	- NIEM provides tools for migrating the NIEM objects, ~90% effective
	- Manual work is needed for things you've added for your exchange

**NIEM Administration and Organization**

Overall structure is always changing, but this is a simplifed snapshot at the time of recording.

- Project Governing Board (PGB)
- NIEM Business Architecture Committee (NBAC)
- NIEM Technical Architecture Committee (NTAC)

```mermaid
graph TD
PGB---nbac_chair[NBAC Chairs]
PGB---ntac_chair[NTAC Chairs]
PGB---dom1_chair[Domain A Chairs]
PGB---dom2_chair[Domain B Chairs]

subgraph NBAC
	nbac_chair---nbac_members[NBAC Members]
end

subgraph NTAC
	ntac_chair---ntac_members[NTAC Members]
end

subgraph Domains
	dom1_chair---dom1_members[Domain A Members]
	dom2_chair---dom2_members[Domain B Members]
end

```

### NIEMOpen and OASIS Open Projects

**Move to OASIS**

The NIEM program has transitioned from being a solely government-funded project to an open source project under [OASIS Open](https://www.oasis-open.org). So here's a quick plug for OASIS Open...

**About OASIS Open**

One of the most respected, nonprofit open source and open standards bodies in the world, OASIS Open advances the fair, transparent development of open source software and standards through the power of global collaboration and community.

**Why Should My Organization Join the NIEM OASIS Open Project?**

- Participate in the development of internationally recognized NIEM standards, ensuring your perspectives and use-cases are represented
- Unify fragmented efforts and encourage convergence
- Facilitate communication between private and public-sector
- Create partnerships and tap into brain trust of NIEM experts from the public sector
- Opportunity to become a steward with a seat on the NIEM Board
- Determine if/when approved work should be submitted to ITU, ICC, UN, ISO, etc.

**Get Involved!**

- Involvement is free!
- Decision-making powers require paid sponsorship
	- Sliding scale for different types of organizations

For more information about supporting the NIEM OASIS Open Project, contact info@niemopen.org.
___# Message Spec / IEPD Overview

- Old Name: "Information Exchange Package Documentation (IEPD)"
- New Name: "Message Specification"
- Defines an exchange
- Made up of a bunch of documents, "artifacts"
	- Some meant for humans
	- Some meant for computers
___

## Message Spec Process

Creating a Message Spec is a multi-step process:

1. Scenario Planning
2. Analyze Requirements
3. Map and Model
4. Build and Validate
5. Assemble and Document (and Publish) 
6. Implement

![IEPD Process](/IEPD_Process_Graphics/IEPD_Process_scaled.png)

Each step produces artifacts used by subsequent steps:

1. A clue as to what you're doing...
2. UML Diagrams
3. Mapping Spreadsheet
4. Schemas and Instance Documents
5. Textual Documents
6. Code

![Message Spec / IEPD Process](/IEPD_Process_Graphics/Process_Artifacts_scaled.png)

**Message Spec / IEPD Process – Idealized**

![Message Spec Seq Ideal](/IEPD_Process_Graphics/Process_Seq_Ideal.png)

**Message Spec / IEPD Process – Real Life**

![Message Spec Seq Ideal](/IEPD_Process_Graphics/Process_Seq_Real.png)
___

### Message Spec / IEPD Artifacts - Documentation

- Master Documentation (Word)
- Message Spec / IEPD catalog document (`iepd-catalog.xml`)
- Change log (text)
- README (text)
- Conformance assertion (text)
- Mapping Spreadsheet
___

### Message Spec / IEPD Artifacts - Definitional

- Wantlist (`wantlist.xml`)
- Schema subset schemas
- Extension schemas
- Exchange schemas
- Sample instances
- XML catalogs
___
## Scenario Planning

- Decide what the exchange is about
- Who are the exchange partners?
- Who are stakeholders?
- Communication is key

```mermaid
sequenceDiagram
	Sender ->> Receiver: So we send you A, B, and C.
	Receiver ->> Sender: We don't use C. We throw it away. We really need D.
	Sender ->> Receiver: What? C is hard to generate. D is easy!
	Receiver ->> Sender: ¯\_(ツ)_/¯
```

- Existing exchanges or other documentation can help
	- Within your organization
	- From NIEM repositories
		- https://www.niem.gov/about-niem/message-exchange-package-mep-registry-repository
	- There's a community to draw from

![Participants](/Scenario_Planning_Graphics/Participants.png)
___
### Existing Documentation

- Current technical architecture documents of all exchange partners
- Stakeholders that will be involved in the exchange
- Security, privacy, and other policy-related concerns associated with the exchange
- Technical characteristics of the exchange:
	- Types of data being shared
	- Number of data objects
		- Current structure of the data (logical, physical)
		- Use of external standards
___
## Analyze Requirements
- Diagrams
	- Use Case Diagrams
	- Business Process Diagrams
	- Sequence Diagrams
- Class Diagrams
- Spreadsheets
- Other documents

**Use Case Diagrams**

![Use Case Diagram](/Req_Analysis_Graphics/Use_Case_Diagram_scaled.png)

**Business Process Diagrams**

![Business Process Diagram](/Req_Analysis_Graphics/Business_Process_Diagram_scaled.png)

**Sequence Diagrams**

![Sequence Diagram](/Req_Analysis_Graphics/Seq_Diagram_scaled.png)
___
### UML Class Diagrams

- The bread and butter of Message Spec / IEPD business requirements
- Can be oriented towards business terms and objects
	- Better for consensus
- Can be oriented towards NIEM terms and objects
	- Pre-loads the mapping step
___
### Business Oriented Class Diagram

Representing objects in UML by their business names and relationships.

![Business Oriented Class Diagram](/Req_Analysis_Graphics/CrashDriverClassDiagram.png)

This vary depending on how your subject matter experts view objects and their relationships. For example, the charge to person relationship could be charge to the driver instead. Cardinality, which we will touch on later, could vary depending on the needs of the exchange. The important thing is reflecting how your business folks understand the data, not model purity.
___
### NIEM Oriented Class Diagram

![NIEM Oriented Class Diagram](/Req_Analysis_Graphics/CrashDriverClassDiagram-NIEM.png)

___
### UML Tools
- [ArgoUML](https://en.wikipedia.org/wiki/ArgoUML)
- [BOUML](https://en.wikipedia.org/wiki/BOUML)
- [MagicDraw](https://en.wikipedia.org/wiki/MagicDraw) / [Rational Rose](https://en.wikipedia.org/wiki/IBM_Rational_Rose_XDE) (\$\$\$)
- [Visio](https://en.wikipedia.org/wiki/Microsoft_Visio) / [OmniGraffle](https://en.wikipedia.org/wiki/OmniGraffle)
- [Graphviz](https://graphviz.org/) / [Mermaid](https://mermaid-js.github.io/mermaid/) / [PlantUML](https://plantuml.com/)
- Many more…
___
### Business Rules
- Some rules are _not_ easily represented in UML
- You can use whatever works for your needs
- Schematron for XML
	- e.g. Birth dates must be in the past, salutations matching gender
- Plain old textual descriptions are great!
___

### The Process from Here On…

We have choices on how to proceed:

- Step-by-step
	- Finish mapping entirely before starting schemas
- Concurrent
	- Building schemas and instances as you go
- We'll use something in-between
	- Build an ersatz matching instance document as we map ([Crash Driver Report Complete](/Text_Document/12_Crash_Driver_Report_Complete.md))
	- Sorta like YAML without data values
	- Save schemas for the end## XML Schema in a Nutshell

XML Schema defines what an XML document needs to look like. (JSON Schema does the same for JSON documents.)

For example, this bit of XML Schema defines what a `PersonName` object needs to look like.

```xml
<xs:complexType name="PersonNameType">
	<xs:annotation>
		<xs:documentation>A data type for a combination of names and/or titles by which a person is known.</xs:documentation>
	</xs:annotation>
	<xs:sequence>
		<xs:element name="PersonGivenName" type="xs:string" minOccurs="1" maxOccurs="1"/>
		<xs:element name="PersonMiddleName" type="xs:string" minOccurs="0" maxOccurs="unbounded"/>
		<xs:element name="PersonSurName" type="xs:string" minOccurs="1" maxOccurs="1"/>
	</xs:sequence>
	<xs:attribute name="personNameCommentText" type="xs:string" use="optional"/>
</xs:complexType>

<xs:element name="PersonName" type="PersonNameType" nillable="true">
	<xs:annotation>
		<xs:documentation>A combination of names and/or titles by which a person is known.</xs:documentation>
	</xs:annotation>
</xs:element>

```
And here's what the matching XML _instance_ document might look like.

```xml
<PersonName personNameCommentText="copied">
	<PersonGivenName>Peter</PersonGivenName>
	<PersonMiddleName>Bredon</PersonMiddleName>
	<PersonMiddleName>Death</PersonMiddleName>
	<PersonSurName>Wimsey</PersonSurName>
</PersonName>
```

We will see much more of this. This is just an initial glance at it.

![Map and Model](/IEPD_Process_Graphics/Process_Artifacts_2_scaled.png)

## Map and Model

For this entire mapping process, we'll look at various things in the mapping spreadsheet and show how to map them to NIEM or to new elements that we'll create later. As we move through, we'll cover all the major aspects of how NIEM works.
___
### Introduction to Mapping

- Mapping Spreadsheets Options
	- NIEM Mapping Template
	- Custom Spreadsheet
- Mapping Process
	- Document Business Objects
	- Map them to NIEM objects, existing or new
	- While maintaining an Ongoing Sample Instance Skeleton
___
### NIEM Mapping Template

- Primarily for submitting content for inclusion in NIEM
	- Eight different tabs
- Can also be used for mapping in a Message Spec / IEPD
	- Just need a few of the tabs, mainly Property and Type
- Is a bit overkill for a Message Spec
- Slight difference between the versions on the NIEM site and for use with MEP Builder
- [Mapping Spreadsheet Template](/Mapping_Spreadsheets/niem-mapping-template.xlsx)
___
### Custom Mapping Spreadsheet

- Has evolved over time
- Contains all the info needed to make schemas
- Not as overwhelming as the NIEM Mapping Template
- You can make your own custom one
	- The Message Spec / IEPD Spec doesn’t specify a required format, by design
- Fresh copy for our example Message Spec / IEPD
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/00_Crash_Driver_Report_Fresh.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/00_Crash_Driver_Report_Fresh.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/00_Crash_Driver_Report_Fresh.pdf)

___
### Basics of Searching NIEM

**Tools**

- [SSGT](https://tools.niem.gov/niemtools/ssgt/index.iepd) (will be replaced with NIEM Toolbox)
- [Wayfarer](http://niem5.org/wayfarer/) (will be replace with API-driven Wayfarer)
- NIEM Schemas
	- [Official Releases](https://niem.github.io/niem-releases/)
	- [Schemas as HTML](https://niemopen.github.io/niem-open-training/)
- Spreadsheet (included in the official releases)

**Techniques**

- Search for Terms
	- Simple vs Advanced
- Search for Synonyms
- Search for Word Roots
- Search for Containers
- Search for Properties

___
# Mapping and NIEM Technical Details

## Understanding NIEM Objects
- XML Schema uses elements and types
- What an element can hold is based on its type
- What you are (your type) defines what you can hold

![What You Are Defines What You Hold](/Mapping_Graphics/WYADWYH.png)

### XML Schema

The XML Schema defining [`nc:Person`](https://niemopen.github.io/niem-open-training/nc.html#Person) includes a definition and a type.

Its type, [`nc:PersonType`](https://niemopen.github.io/niem-open-training/nc.html#PersonType), has a little more information. It also includes a definition, one similar to `nc:Person`. It also includes a `base` that tells us what sort of thing it is. In this case, the base is [`structures:ObjectType`](https://niemopen.github.io/niem-open-training/structures.html#ObjectType), which is just an empty object (that has a few infrastructure pieces we'll learn about later). To that `base` it adds several objects. These are objects that go _inside_ an `nc:Person` object. Each one is a reference to a declaration of each of those objects. Each also has cardinality defined, which tells us how many of each can go inside of an `nc:Person`. `minOccurs` is the minimum number of times. Any non-negative integer can go here, but 0 and 1 are what you'll usually find. Zero essentially means "optional." `maxOccurs` is the maximum number of times. This can also be any non-negative number, but can also be "unbounded", which means "as many as you want." Typical values are 1 and unbounded. Here's the schema for `nc:PersonType` with some of the contained objects removed for clarity:

```xml
<xs:complexType name="PersonType">
	<xs:annotation>
		<xs:documentation>A data type for a human being.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:PersonAccentText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonAgeDescriptionText" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="nc:PersonLivingIndicator" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="nc:PersonName" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="nc:PersonHomeContactInformation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>

<xs:element name="Person" type="nc:PersonType" nillable="true">
	<xs:annotation>
		<xs:documentation>A human being.</xs:documentation>
	</xs:annotation>
</xs:element>

```

The XML Schema defining [`nc:PersonName`](https://niemopen.github.io/niem-open-training/nc.html#PersonName) and [`nc:PersonNameType`](https://niemopen.github.io/niem-open-training/nc.html#PersonNameType) looks like:

```xml
<xs:complexType name="PersonNameType">
	<xs:annotation>
		<xs:documentation>A data type for a combination of names and/or titles by which a person is known.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:PersonNamePrefixAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonGivenName" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonMiddleName" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonSurName" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonNameSuffixText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonMaidenName" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonFullName" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonNameCategoryAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonNameSalutationText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonOfficialGivenName" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonPreferredName" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonSurNamePrefixText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:EffectiveDate" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:PersonNameAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
			<xs:attribute ref="nc:personNameCommentText" use="optional"/>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>

<xs:element name="PersonName" type="nc:PersonNameType" nillable="true">
	<xs:annotation>
		<xs:documentation>A combination of names and/or titles by which a person is known.</xs:documentation>
	</xs:annotation>
</xs:element>

```

The XML Schema defining [`nc:PersonGivenName`](https://niemopen.github.io/niem-open-training/nc.html#PersonGivenName), [`PersonNameTextType`](https://niemopen.github.io/niem-open-training/nc.html#PersonNameTextType), and supporting types looks like:

```xml
<xs:complexType name="PersonNameTextType">
	<xs:annotation>
		<xs:documentation>A data type for a name by which a person is known, referred, or addressed.</xs:documentation>
	</xs:annotation>
	<xs:simpleContent>
		<xs:extension base="nc:ProperNameTextType">
			<xs:attribute ref="nc:personNameInitialIndicator" use="optional"/>
		</xs:extension>
	</xs:simpleContent>
</xs:complexType>

<xs:complexType name="ProperNameTextType">
	<xs:annotation>
		<xs:documentation>A data type for a word or phrase by which a person or thing is known, referred, or addressed.</xs:documentation>
	</xs:annotation>
	<xs:simpleContent>
		<xs:extension base="nc:TextType"/>
	</xs:simpleContent>
</xs:complexType>

<xs:complexType name="TextType">
	<xs:annotation>
		<xs:documentation>A data type for a character string.</xs:documentation>
	</xs:annotation>
	<xs:simpleContent>
		<xs:extension base="niem-xs:string">
			<xs:attribute ref="nc:partialIndicator" use="optional"/>
			<xs:attribute ref="nc:truncationIndicator" use="optional"/>
			<xs:attribute ref="xml:lang" use="optional"/>
		</xs:extension>
	</xs:simpleContent>
</xs:complexType>

<xs:element name="PersonGivenName" type="nc:PersonNameTextType" nillable="true">
	<xs:annotation>
		<xs:documentation>A first name of a person.</xs:documentation>
	</xs:annotation>
</xs:element>

```
Finally, the definition for [`nc:PersonLivingIndicator`](https://niemopen.github.io/niem-open-training/nc.html#PersonLivingIndicator) is very simple. It's a boolean value, `true` or `false`.

```xml
<xs:element name="PersonLivingIndicator" type="niem-xs:boolean" nillable="true">
	<xs:annotation>
		<xs:documentation>True if a person is alive; false if a person is dead.</xs:documentation>
	</xs:annotation>
</xs:element>
```

The resulting instance document that all this creates might look like this:

```xml
<nc:Person>
	<nc:PersonLivingIndicator>false</nc:PersonLivingIndicator>
	<nc:PersonName nc:personNameCommentText="copied">
		<nc:PersonGivenName>Peter</nc:PersonGivenName>
		<nc:PersonMiddleName>Death</nc:PersonMiddleName>
		<nc:PersonMiddleName>Bredon</nc:PersonMiddleName>
		<nc:PersonSurName>Wimsey</nc:PersonSurName>
	</nc:PersonName>
</nc:Person>
```

(Who is [Peter Wimsey](https://en.wikipedia.org/wiki/Lord_Peter_Wimsey)?)
___
## Native Properties

![Native Properties](/Req_Analysis_Graphics/01_Native_Properties_CrashDriverClassDiagram.png)

- Some things will be easy to find
- Will map directly to NIEM objects
- Examples:
	- `nc:Person`, `nc:PersonName`, `nc:PersonGivenName`, etc.
	- Search for `nc:Person` in the [SSGT](http://niem5.org/ssgt_redirect.php?query=person)
	- Search for `nc:Person` in [Wayfarer](http://niem5.org/wayfarer/search.php?option=exact&query=person)

We've already seen the schema for these in detail.

### Artifacts

- [Native Properties](/Text_Document/01_Native_Properties.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/01_Native_Properties.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/01_Native_Properties.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/01_Native_Properties.pdf)

___
## Substitution Groups

![Substitution Groups](/Req_Analysis_Graphics/02_Substitution_Groups_CrashDriverClassDiagram.png)

- Some concepts can be represented multiple ways
- Text / code combinations are common
- Date can be a date, datetime, or a range
- NIEM uses substitution groups to support both:
	- The single concept, and
	- Multiple representations of that concept
- Examples:
	- `nc:PersonBirthDate` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-11r)/[Wayfarer](http://niem5.org/wayfarer/nc/PersonBirthDate.html)) contains a `nc:DateRepresentation` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-92a)/[Wayfarer](http://niem5.org/wayfarer/nc/DateRepresentation.html))
	- Substitution group heads follow the form of: `SomethingRepresentation` or `WhateverAbstract`

### Schemas

Here we see [`nc:PersonBirthDate`](https://niemopen.github.io/niem-open-training/nc.html#PersonBirthDate) and its type, `nc:DateType`:

```xml
<xs:element name="PersonBirthDate" type="nc:DateType" nillable="true">
	<xs:annotation>
		<xs:documentation>A date a person was born.</xs:documentation>
	</xs:annotation>
</xs:element>
```

[`nc:DateType`](https://niemopen.github.io/niem-open-training/nc.html#DateType) contains `nc:DateRepresentation`, along with other date properties:

```xml
<xs:complexType name="DateType">
	<xs:annotation>
		<xs:documentation>A data type for a calendar date.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:DateRepresentation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:DateAccuracyAbstract" minOccurs="0" maxOccurs="1"/>
				<xs:element ref="nc:DateMarginOfErrorDuration" minOccurs="0" maxOccurs="1"/>
				<xs:element ref="nc:DateAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
[`nc:DateRepresentation`](https://niemopen.github.io/niem-open-training/nc.html#DateRepresentation) is _abstract_, meaning it has no type and must be substituted with another object:

```xml
<xs:element name="DateRepresentation" abstract="true">
	<xs:annotation>
		<xs:documentation>A data concept for a representation of a date.</xs:documentation>
	</xs:annotation>
</xs:element>
```
Those other objects are identified by having a `substitutionGroup` attribute set to the name of the substitution group head. The most common one you'll see for `nc:DateRepresentation` is [`nc:Date`](https://niemopen.github.io/niem-open-training/nc.html#Date):

```xml
<xs:element name="Date" type="niem-xs:date" substitutionGroup="nc:DateRepresentation" nillable="true">
	<xs:annotation>
		<xs:documentation>A full date.</xs:documentation>
	</xs:annotation>
</xs:element>
```

### Instance Documents

In the resulting instance document, you don't see `nc:DateRepresentation` at all. You just see `nc:Date`, which is taking its place:

```xml
<nc:Person>
	<nc:PersonBirthDate>
		<nc:Date>1890-05-04</nc:Date>
	</nc:PersonBirthDate>
	<nc:PersonName>
		<nc:PersonGivenName>Peter</nc:PersonGivenName>
		<nc:PersonMiddleName>Death</nc:PersonMiddleName>
		<nc:PersonMiddleName>Bredon</nc:PersonMiddleName>
		<nc:PersonSurName>Wimsey</nc:PersonSurName>
	</nc:PersonName>
</nc:Person>
```
### Artifacts

- [Substitition Groups](/Text_Document/02_Substitution_Groups.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/02_Substitution_Groups.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/02_Substitution_Groups.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/02_Substitution_Groups.pdf)

___
## An Aside about Namespaces

Below you can see object with different prefixes, `j:Crash` and `nc:ActivityDate`. The `j` and `nc` refer to different namespaces in XML Schema.

- Namespaces organize elements by context
- Identified by prefix, a nickname for the namespace
- NIEM governance is organized along these lines

![Namespaces and Case](/Mapping_Graphics/Namespace_Case.png)

```xml
<xs:schema   
	targetNamespace="http://training.niem.gov/CrashDriver/1.0/" version="1" xml:lang="en-US"  

	xmlns:ext="http://training.niem.gov/CrashDriver/1.0/"  
	xmlns:j="https://docs.oasis-open.org/niemopen/ns/model/domains/justice/6.0/"  
	xmlns:nc="https://docs.oasis-open.org/niemopen/ns/model/niem-core/6.0/">

	<xs:import schemaLocation="../domains/justice.xsd"
		namespace="https://docs.oasis-open.org/niemopen/ns/model/domains/justice/6.0/"/>
	<xs:import schemaLocation="../niem-core.xsd"
		namespace="https://docs.oasis-open.org/niemopen/ns/model/niem-core/6.0/"/>

```

___
![Inherited Properties](/Req_Analysis_Graphics/03_Inherited_Properties_CrashDriverClassDiagram.png)

- NIEM is a model, not a flat data dictionary
- Some concepts don’t exist as elements using the terms for the concept
- Instead, properties are inherited
- There is no “Crash Date” in NIEM ([SSGT](http://niem5.org/ssgt_redirect.php?query=crash+date)/[Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=crash+date))
- There _is_ an `ActivityDate` which can be inside a `Crash` object ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-44f)/[Wayfarer](http://niem5.org/wayfarer/j/Crash.html))

### Schemas

Here's [`j:Crash`](https://niemopen.github.io/niem-open-training/j.html#Crash) and its type, `j:CrashType`:

```xml
<xs:element name="Crash" type="j:CrashType" nillable="true">
	<xs:annotation>
		<xs:documentation>A traffic accident.</xs:documentation>
	</xs:annotation>
</xs:element>
```
[`j:CrashType`](https://niemopen.github.io/niem-open-training/j.html#CrashType) contains several things, but the important thing here is what it's based on, `j:DrivingIncidentType`:

```xml
<xs:complexType name="CrashType">
	<xs:annotation>
		<xs:documentation>A data type for a traffic accident.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="j:DrivingIncidentType">
			<xs:sequence>
				<xs:element ref="j:CrashServiceCall" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:CrashInformationSource" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="j:CrashAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

[`j:DrivingIncidentType`](https://niemopen.github.io/niem-open-training/j.html#DrivingIncidentType) is, in turn, based on an even more generic type, `nc:IncidentType`:

```xml
<xs:complexType name="DrivingIncidentType">
	<xs:annotation>
		<xs:documentation>A data type for details of an incident involving a vehicle.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:IncidentType">
			<xs:sequence>
				<xs:element ref="j:DrivingAccidentSeverityAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DrivingIncidentCMVAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="j:DrivingIncidentAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

[`nc:IncidentType`](https://niemopen.github.io/niem-open-training/nc.html#IncidentType) is, also in turn, based on a very generic type, `nc:ActivityType`:

```xml
<xs:complexType name="IncidentType">
	<xs:annotation>
		<xs:documentation>A data type for an occurrence or an event that may require a response.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:ActivityType">
			<xs:sequence>
				<xs:element ref="nc:IncidentEvent" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:IncidentJurisdictionalOrganization" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="nc:IncidentAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

And we finally get to [`nc:ActivityType`](https://niemopen.github.io/niem-open-training/nc.html#ActivityType), which contains [`nc:ActivityDate`](https://niemopen.github.io/niem-open-training/nc.html#ActivityDate):

```xml
<xs:complexType name="ActivityType">
	<xs:annotation>
		<xs:documentation>A data type for a single or set of related actions, events, or process steps.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:ActivityIdentification" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:ActivityActualDuration" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="nc:ActivityDate" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="nc:ActivityAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

What this all means is that a `j:Crash` object can contain a `nc:ActivityDate`, which is, contextually, a Crash Date.

### Instance Documents

Instance in XML:

```xml
<j:Crash>
	<nc:ActivityDate>
		<nc:Date>1900-05-04</nc:Date>
	</nc:ActivityDate>
</j:Crash>
```

You need to understand this concept in order to know to look for these cases, which are very common, but just use tools to figure out the details, e.g:

- [`j:Crash` in the SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-44f)
- [`j:Crash` in Wayfarer](http://niem5.org/wayfarer/j/Crash.html)
	- Wayfarer has a new feature that does some level of [contextual searching](http://niem5.org/wayfarer/searchcontextuals.php)
	- [Search contextually for "crash date" in Wayfarer](http://niem5.org/wayfarer/searchcontextuals.php?query=crash+date)

### Artifacts

- [Inherited Properties](Text_Document/03_Inherited_Properties.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](Mapping_Spreadsheets/03_Inherited_Properties.numbers)
	- [Mapping Spreadsheet (Excel)](Mapping_Spreadsheets/03_Inherited_Properties.xlsx)
	- [Mapping Spreadsheet (PDF)](Mapping_Spreadsheets/03_Inherited_Properties.pdf)

___
## Linking Things Together

- NIEM is relational in many senses
- Objects can refer to each other across an XML hierarchy
- Allows NIEM to represent real world, many-to-many relationships
- `structures` namespace provides the infrastructure to make this work

### NIEM Structural "Layers"

NIEM has several conceptual layers which build on top of each other:

- [`structures`](https://niemopen.github.io/niem-open-training/structures.html) provides infrastructure
	- All namespaces draw from it
- [`niem-core`](https://niemopen.github.io/niem-open-training/nc.html) provides common objects to be used or built upon
	- Domains draw from it
- Domains provide domain-specific content, often built from `niem-core`
	- Domains can draw from each other, although this is limited in practice
- Code table namespaces define many of the code tables, built with infrastructure from `structures`
	- Domains draw from it for code definitions
- Wrappers for external standards, built with infrastructure from `structures`

![Structural Diagram](/Mapping_Graphics/Structural_Diagram_scaled.png)

## Referencing - XML Schema

- NIEM lets you assign unique IDs to objects
- Other objects can then link to those objects by referencing the ID
- Everything in NIEM can have attributes for this:
	- [`id`](https://niemopen.github.io/niem-open-training/structures.html#id)
	- [`ref`](https://niemopen.github.io/niem-open-training/structures.html#ref)
	- [`uri`](https://niemopen.github.io/niem-open-training/structures.html#uri)
- These leverage built-in XML Schema attributes `ID`, `IDREF`, and `anyURI`
- `id` assigns an ID to an object
	- Just a string
	- _Must_ be unique within an instance document
	- Can't include a space
- `ref` references an ID of another object
	- Contains a single `id` to match
	- The matching `id` _must_ exist in the instance document
	- Validators do _not_ check that the linking makes sense
- `uri` links objects together that are the same thing
	- Used to avoid duplication
	- Also used to assign roles to objects
- Additionally, objects and simple types can have `metadataRef` attributes, based on `IDREFS`
	- More on this in the Metadata module

Examples of how NIEM uses these are the next few sections. Here's a very simple non-NIEM example:

**Plain Old XML:**

```xml
<Cat>
	<CatName>Jett</CatName>
	<CatOwner IDREF="owner01"/>
</Cat>
<Human ID="owner01">
	<HumanName>Tom</HumanName>
</Human>
```

**NIEM's renaming:**

```xml
<Cat>
	<CatName>Jett</CatName>
	<CatOwner ref="owner01"/>
</Cat>
<Human id="owner01">
	<HumanName>Tom</HumanName>
</Human>
```

We will see these attributes used extensively in the following modules dealing with Associations and Roles.

___
## Associations

![Associations](/Req_Analysis_Graphics/04_Associations_CrashDriverClassDiagram.png)

- Relationships can be complex
- NIEM provides powerful Association objects
- Trade-off can be implementation complexity
- Associations link objects together
	- Associations reference the associated objects
	- Can link to multiple objects
	- Can thus form many-to-many relationships between them
- Associations also hold information about the association itself
	- `Date` or `DateRange` is a common example
- Associations can also just include the things being associated, if desired
- Examples:
	- `j:PersonChargeAssociation` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-4qf)/[Wayfarer](http://niem5.org/wayfarer/j/PersonChargeAssociation.html))
	- Anything ending in “Association” ([SSGT](http://niem5.org/ssgt_redirect.php?query=association)/[Wayfarer](http://niem5.org/wayfarer/search.php?option=names&query=association))

### Schemas

[`j:PersonChargeAssociation`](https://niemopen.github.io/niem-open-training/j.html#PersonChargeAssociation) is used, as the name suggests, to link together a Person and a Charge. It's of `j:PersonChargeAssociationType`:

```xml
<xs:element name="PersonChargeAssociation" type="j:PersonChargeAssociationType" nillable="true">
	<xs:annotation>
		<xs:documentation>An association between a person and a charge issued to that person.</xs:documentation>
	</xs:annotation>
</xs:element>
```

[`j:PersonChargeAssociationType`](https://niemopen.github.io/niem-open-training/j.html#PersonChargeAssociationType) includes a [`nc:Person`](https://niemopen.github.io/niem-open-training/nc.html#Person) and a [`j:Charge`](https://niemopen.github.io/niem-open-training/j.html#Charge), but also includes information _about_ the association itself, in this case [`j:JuvenileAsAdultIndicator`](https://niemopen.github.io/niem-open-training/j.html#JuvenileAsAdultIndicator). (Which isn't used in _this_ exchange.) `PersonChargeAssociationType` extends `nc:AssociationType`:

```xml
<xs:complexType name="PersonChargeAssociationType">
	<xs:annotation>
		<xs:documentation>A data type for an association between a person and a charge.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:AssociationType">
			<xs:sequence>
				<xs:element ref="nc:Person" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:Charge" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:JuvenileAsAdultIndicator" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:PersonChargeAssociationAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
[`nc:AssociationType`](https://niemopen.github.io/niem-open-training/nc.html#AssociationType) adds in generic association information like a start and end date and a description. Remember that these are inherited by any type based on `nc:AssociationType`, so things of `j:PersonChargeAssociationType` automatically get these common objects.

```xml
<xs:complexType name="AssociationType">
	<xs:annotation>
		<xs:documentation>A data type for an association, connection, relationship,
			or involvement somehow linking people, things, and/or activities together.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:AssociationType">
			<xs:sequence>
				<xs:element ref="nc:AssociationDateRange" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:AssociationDescriptionText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:AssociationAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

### Instance Documents

In the instance document, the association object can specify the objects being associated together by pointing to then with `ref` attributes, or by including the object inside the association object.

First, here's the association using referencing. The applicable `nc:Person` and `j:Charge` objects are external to `j:PersonChargeAssociation`. While shown next to the `j:PersonChargeAssociation` object, they could be _anywhere_ in the instance document.

This method is useful when the same `nc:Person` object is being used in multiple contexts. In the example Message Spec / IEPD, this `nc:Person` is also the `j:CrashDriver` and the `j:CrashPerson`. This method allows us to define the `nc:Person` once and refer to it multiple times.

This beings with it two advantages:

1. This `nc:Person` object is not being replicated; there is no duplication of data
2. We know that the `nc:Person` in the Association _and_ the `j:CrashDriver` _and_ the `j:CrashPerson` are the exact same person, and not three people with the same name

```xml
<j:PersonChargeAssociation>
	<nc:Person structures:ref="P01" xsi:nil="true"/>
	<j:Charge structures:ref="CH01" xsi:nil="true"/>
</j:PersonChargeAssociation>
<nc:Person structures:id="P01">
	<nc:PersonName>
		<nc:PersonGivenName>Peter</nc:PersonGivenName>
	</nc:PersonName>
</nc:Person>
<j:Charge structures:id="CH01">
	<j:ChargeDescriptionText>Furious Driving</j:ChargeDescriptionText>
	<j:ChargeFelonyIndicator>false</j:ChargeFelonyIndicator>
</j:Charge>
```

The disadvantage with using referencing is that it can be more difficult to implement. Implementations need to look for `ref` attributes and find matching `id` attributes.

The alternative to referencing is to just include the `nc:Person` and `j:Charge` information inside the association:

```xml
<j:PersonChargeAssociation>
	<nc:Person>
		<nc:PersonName>
			<nc:PersonGivenName>Peter</nc:PersonGivenName>
		</nc:PersonName>
	</nc:Person>
	<j:Charge>
		<j:ChargeDescriptionText>Furious Driving</j:ChargeDescriptionText>
		<j:ChargeFelonyIndicator>false</j:ChargeFelonyIndicator>
	</j:Charge>
</j:PersonChargeAssociation>
```
You can also mix and match. You could reference a `nc:Person` while including the `j:Charge` inside the association.

NIEM _never_ requires you to do referencing. If the trade-offs of duplicated data aren't an issue, you can have multiple identical `nc:Person` objects.

### Artifacts

- [Associations](/Text_Document/04_Associations.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/04_Associations.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/04_Associations.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/04_Associations.pdf)

___
## Roles

![Roles](/Req_Analysis_Graphics/05_Roles_CrashDriverClassDiagram.png)

- Modeling some objects as specialized things gets complicated
- Roles are roles that objects play
	- People, organizations, items are the major ones
- Roles and objects playing the roles are linked together using the `uri` attribute
	- An object can play multiple roles, because multiple role objects can have the same `uri` value
- Roles contain other information about the role
- Roles are _not_ explicitly defined as such
	- This is a change from NIEM 5, which included explicit `RoleOf` objects
- Examples:
	- `j:CrashPerson` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-45q)/[Wayfarer](http://niem5.org/wayfarer/j/CrashPerson.html))
	- `j:CrashDriver`

### Searching for Injured Person

How do we find the match for "injured person"? Here's one way:

- Search for `injured person`
	- [SSGT](http://niem5.org/ssgt_redirect.php?query=injured+person)
	- [Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=injured+person)
- No results! How about `person injury`?
	- [SSGT](http://niem5.org/ssgt_redirect.php?query=person+injury)
	- [Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=person+injury)
- Notice that [`j:InjuryLocationCode`](http://niem5.org/wayfarer/j/InjuryLocationCode.html) looks like something an injured person would have
- That's inside of things of [`nc:InjuryType`](http://niem5.org/wayfarer/nc/InjuryType.html)
- [`j:CrashPersonInjury`](http://niem5.org/wayfarer/j/CrashPersonInjury.html) is one of the things of that type
- And that's inside of [`j:CrashPerson`](http://niem5.org/wayfarer/j/CrashPerson.html)


### Roles - Not Special Kinds of People

| Roles | Just a Guy |
| --- | --- |
| ![Role Hats](/Mapping_Graphics/Role_Hats_01.png) | ![Role Hats](/Mapping_Graphics/Role_Hats_02.png) |

### Roles – Allows an Object to Play Multiple Roles
![Role Hats](/Mapping_Graphics/Role_Hats_03.png)

### Roles - How They Work
Roles are linked to the Object playing the Role via the `uri` attribute:

![Role Hats](/Mapping_Graphics/Role_Hats_04.png)

Roles contain information about the Role:

![Role Hats](/Mapping_Graphics/Role_Hats_05.png)

### Schemas

[`j:CrashPerson`](https://niemopen.github.io/niem-open-training/j.html#CrashPerson) is of `j:CrashPersonType`:

```xml
<xs:element name="CrashPerson" type="j:CrashPersonType" nillable="true">
	<xs:annotation>
		<xs:documentation>A person involved in a traffic accident.</xs:documentation>
	</xs:annotation>
</xs:element>
```

[`j:CrashPersonType`](https://niemopen.github.io/niem-open-training/j.html#CrashPersonType) contains information specific to this role. In the sample Message Spec / IEPD, we're using `j:CrashPersonInjury`:

```xml
<xs:complexType name="CrashPersonType">
	<xs:annotation>
		<xs:documentation>A data type for any person involved in a traffic accident.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="j:CrashPersonEMSTransportation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:CrashPersonInjury" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="j:CrashPersonAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```


### Instance Documents

Here we see a `j:CrashPerson` linked via `structures:uri` with an `nc:Person` object playing that role:

```xml
<j:CrashPerson structures:uri="http://some.uri/">
	<j:CrashPersonInjury>  
		<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>  
	</j:CrashPersonInjury>
</j:CrashPerson>

<nc:Person structures:uri="http://some.uri/">
	<nc:PersonName>
		<nc:PersonGivenName>Peter</nc:PersonGivenName>
	</nc:PersonName>
</nc:Person>
```

### Artifacts

- [Roles](/Text_Document/05_Roles.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/05_Roles.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/05_Roles.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/05_Roles.pdf)

___
## Code Tables

![Code Tables](/Req_Analysis_Graphics/06_Code_Tables_CrashDriverClassDiagram.png)

- Codes help ensure accurate information
- Codes are, essentially, strings, simple data
- A few in NIEM are integers
- Elements defined in the domains
- Types are often defined in their own namespaces
- NIEM wraps them in a complex type in order to apply some attributes needed for infrastructure
- Examples:
	- `j:InjurySeverityCode` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-45s)/[Wayfarer](http://niem5.org/wayfarer/j/InjurySeverityCode.html))
		- In the SSGT, the actual codes are viewable on the page for the base simple type, e.g. [`aamva_d20:AccidentSeverityCodeSimpleType`](https://tools.niem.gov/niemtools/ssgt/SSGT-GetType.iepd?typeKey=o4-c)
		- In Wayfarer, there should be a link on the element page bringing up the codes in a separate window, e.g. [`aamva_d20:AccidentSeverityCodeSimpleType`](http://niem5.org/wayfarer/aamva_d20/AccidentSeverityCodeSimpleType_codes.html)
	- Anything ending in "Code" ([SSGT](http://niem5.org/ssgt_redirect.php?query=code)/[Wayfarer](http://niem5.org/wayfarer/search.php?option=names&query=code))
- Codes nearly always have a text alternative

### Schemas

[`j:InjurySeverityCode`](https://niemopen.github.io/niem-open-training/j.html#InjurySeverityCode) is a code table, with its codes defined in another namespace, the one for [AAMVA](https://www.aamva.org/). Here's the schema for the element:

```xml
<xs:element name="InjurySeverityCode" type="aamva_d20:AccidentSeverityCodeType" substitutionGroup="nc:InjurySeverityAbstract" nillable="true">
	<xs:annotation>
		<xs:documentation>A severity of an injury received by a person, such as in a traffic accident or crash.</xs:documentation>
	</xs:annotation>
</xs:element>
```

The actual codes are defined in a pair of types. The first, [`aamva_d20:AccidentSeverityCodeSimpleType`](https://niemopen.github.io/niem-open-training/aamva_d20.html#AccidentSeverityCodeSimpleType), defines the actual codes and their definitions, one per `enumeration` below:

```xml
<xs:simpleType name="AccidentSeverityCodeSimpleType">
	<xs:annotation>
		<xs:documentation>A data type for severity levels of an accident.</xs:documentation>
	</xs:annotation>
	<xs:restriction base="xs:token">
		<xs:enumeration value="1">
			<xs:annotation>
				<xs:documentation>Fatal Accident</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="2">
			<xs:annotation>
				<xs:documentation>Incapacitating Injury Accident</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="3">
			<xs:annotation>
				<xs:documentation>Non-incapacitating Evident Injury</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="4">
			<xs:annotation>
				<xs:documentation>Possible Injury Accident</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="5">
			<xs:annotation>
				<xs:documentation>Non-injury Accident</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="9">
			<xs:annotation>
				<xs:documentation>Unknown</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
	</xs:restriction>
</xs:simpleType>
```

This simple type is then wrapped in a complex type, [`aamva_d20:AccidentSeverityCodeType`](https://niemopen.github.io/niem-open-training/aamva_d20.html#AccidentSeverityCodeType), to add infrastructure attributes that we've seen used in associations and roles. The two types are grouped together in the [`aamva_d20`](https://niemopen.github.io/niem-open-training/aamva_d20.html) namespace so they can be governed by AAMVA without needing to change the `j` domain:

```xml
<xs:complexType name="AccidentSeverityCodeType">
	<xs:annotation>
		<xs:documentation>A data type for severity levels of an accident.</xs:documentation>
	</xs:annotation>
	<xs:simpleContent>
		<xs:extension base="aamva_d20:AccidentSeverityCodeSimpleType">
			<xs:attributeGroup ref="structures:SimpleObjectAttributeGroup"/>
		</xs:extension>
	</xs:simpleContent>
</xs:complexType>
```
### Instance Documents

The code is what shows up in the instance document. The longer definition does not. If you want to know that "3" means "Non-incapacitating Evident Injury," you need to refer to the schemas. Schema validation _will_ verify that the value is one of the enumerations. Here's the XML:

```xml
<j:CrashPersonInjury>
	<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
	<j:InjurySeverityCode>3</j:InjurySeverityCode>
</j:CrashPersonInjury>
```

### Artifacts

- [Code Tables](/Text_Document/06_Code_Tables.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/06_Code_Tables.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/06_Code_Tables.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/06_Code_Tables.pdf)

___
## Combining Domains (Augmentations)

![Augmentations](/Req_Analysis_Graphics/09_Augmentations_CrashDriverClassDiagram.png)

- Sometimes you just want to add properties from other domains to an object without making a special kind of thing
- Augmentations are bags of stuff
- Augmentation Points are hooks onto which to hang the bags of stuff
- Examples:
	- `nc:Incident` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-rr))
	- `j:IncidentAugmentation` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-9l7))
- **Augmentations are an easy way to extend objects to meet your exchange needs**
	- We'll add an email address to a driver license using an augmentation we'll build
	- `j:DriverLicense` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-lb))
	- `j:DriverLicenseAugmentationPoint` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-11rg))

Does driver's license have what we need? Does it have an email address?

- Try searching for "drivers license":
	- [SSGT](http://niem5.org/ssgt_redirect.php?query=drivers+license)
	- [Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=drivers+license)
- Try searching for "driver license", singular:
	- [SSGT](http://niem5.org/ssgt_redirect.php?query=driver+license)
	- [Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=driver+license)
	- It's _usually_ a good idea to drop pluralization in search terms
- Check to see if it has an email address. (Spoiler, it doesn't.)
- But we should learn its structure while we're here:
	- Check what can contain it, specifically [`j:CrashDriver`](http://niem5.org/wayfarer/j/CrashDriver.html)
	- Follow up to [`j:CrashVehicle`](http://niem5.org/wayfarer/j/CrashVehicle.html)
	- Follow up to [`j:Crash`](http://niem5.org/wayfarer/j/Crash.html)

Follow a similar process for [`nc:ContactEmailID`](http://niem5.org/wayfarer/nc/ContactEmailID.html) and [`nc:ContactInformation`](http://niem5.org/wayfarer/nc/ContactInformation.html). Learn about the _object_, not just the individual elements.

The SSGT is best for learning overall structure, so check out [`j:Crash`](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-44f) and [`nc:ContactInformation`](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-eh) there, too!

(Why not [`j:CrashDriverLicense`](http://niem5.org/wayfarer/j/CrashDriverLicense.html)? It doesn't go inside a `j:CrashDriver`. Why? The domain submitted it like this.)

### Schemas

`j:DriverLicense` is defined to be of `j:DriverLicenseType`:

```xml
<xs:element name="DriverLicense" type="j:DriverLicenseType" nillable="true">
	<xs:annotation>
		<xs:documentation>A license issued to a person granting driving privileges.</xs:documentation>
	</xs:annotation>
</xs:element>
```

`j:DriverLicenseType` contains `j:DriverLicenseAugmentationPoint` as a hook for a augmentation bags:

```xml
<xs:complexType name="DriverLicenseType">
	<xs:annotation>
		<xs:documentation>A data type for a license issued to a person granting driving privileges.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:LicenseType">
			<xs:sequence>
				<xs:element ref="j:DriverLicenseEnhancedIndicator" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseCommercialClassAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseCommercialStatusAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseNonCommercialClassText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseNonCommercialStatusAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseWithdrawal" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseWithdrawalPendingIndicator" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseCardIdentification" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
(`j:DriverLicenseType` also inherits from `nc:LicenseType`, but nothing we use in our example.)

While NIEM does have some augmentations pre-defined, they're particularly useful for adding new objects, or just putting existing NIEM objects somewhere else. Here we do the latter, creating a bag called `LicenseAugmentation` with `nc:ContactInformation` inside. 

`ext:` is the nickname we're going to use for our own extension namespace, where we'll create our own objects. This is a separate file _we_ create. In it we build new objects, based on existing NIEM objects. We'll learn more about how these files fit together when we get to creating schemas.

We can now "hang" it on the `j:DriverLicenseAugmentationPoint` hook with nothing more than a `substitutionGroup` attribute:

```xml
<xs:complexType name="LicenseAugmentationType">
	<xs:annotation>
		<xs:documentation>
			A data type for additional information about a license.
		</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:AugmentationType">
			<xs:sequence>
				<xs:element ref="nc:ContactInformation"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>

<xs:element name="LicenseAugmentation" type="ext:LicenseAugmentationType" substitutionGroup="j:DriverLicenseAugmentationPoint">
	<xs:annotation>
		<xs:documentation>
			Additional information about a license.
		</xs:documentation>
	</xs:annotation>
</xs:element>
```

Our new `ext:LicenseAugmentationType` is based on the built-in [`structures:AugmentationType`](https://niemopen.github.io/niem-open-training/structures.html#AugmentationType). That base type merely adds in infrastructure support for linking objects together:

```xml
<xs:complexType name="AugmentationType" abstract="true">
	<xs:annotation>
		<xs:documentation>A data type for a set of properties to be applied to a base type.</xs:documentation>
	</xs:annotation>
	<xs:attribute ref="structures:id"/>
	<xs:attribute ref="structures:ref"/>
	<xs:attribute ref="structures:uri"/>
	<xs:anyAttribute namespace="urn:us:gov:ic:ism urn:us:gov:ic:ntk" processContents="lax"/>
</xs:complexType>
```

The resulting XML Instance Document looks like:

```xml
<j:DriverLicense>
	<j:DriverLicenseCardIdentification>
		<nc:IdentificationID>A1234567</nc:IdentificationID>
	</j:DriverLicenseCardIdentification>
	<ext:LicenseAugmentation>
		<nc:ContactInformation>
			<nc:ContactEmailID>peter@wimsey.org</nc:ContactEmailID>
		</nc:ContactInformation>
	</ext:LicenseAugmentation>
</j:DriverLicense>
```

### Artifacts

- [Augmentations](/Text_Document/08_Combining_Domains_Augmentations.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/07_Combining_Domains_Augmentations.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/07_Combining_Domains_Augmentations.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/07_Combining_Domains_Augmentations.pdf)

___
## Metadata
![Metadata](/Req_Analysis_Graphics/07_Metadata_CrashDriverClassDiagram.png)

![Jett](/Mapping_Graphics/Jett_scaled.png)

Metadata is Data about Data. What does that mean? Here's an example:

### Data About Jett

- _Name:_ **Jett**
- _Sex:_ **Female**
- _Weight:_ **8 pounds**

### Data About Data About Jett, e.g. Her Weight

- _Reporting Organization:_ **Ark Pet Hospital**
- _Reported Date:_ **2021-06-10**
- _Last Verified Date:_ **2025-02-21**

### Object Reference Metadata

- Objects can reference the metadata objects that apply to them
	- Can include them via Augmentations as well
- An object can reference more than one metadata object
- More than one object can reference the same metadata object
- Examples of NIEM Metadata: [`nc:Metadata`](https://niemopen.github.io/niem-open-training/nc.html#Metadata) and [`j:MetadataAugmentation`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentation)

### Schemas

The [`j:MetadataAugmentation`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentation) object is of `j:MetadataAugmentationType`. 

```xml
<xs:element name="MetadataAugmentation" type="j:MetadataAugmentationType"
	substitutionGroup="nc:MetadataAugmentationPoint" nillable="true">
	<xs:annotation>
		<xs:documentation>Additional information about metadata.</xs:documentation>
	</xs:annotation>
</xs:element>
```

There's nothing special about [`j:MetadataAugmentationType`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentationType). It's just an object holding some other objects, in this case a couple booleans, `j:CriminalInformationIndicator` and `j:IntelligenceInformationIndicator`. It's based on [`structures:AugmentationType`](https://niemopen.github.io/niem-open-training/structures.html#AugmentationType), which is just an empty container. Substituting it for `nc:MetadataAugmentationPoint` provides the linking infrastructure we've seen with associations and roles as part of the [`nc:Metadata`](https://niemopen.github.io/niem-open-training/nc.html#Metadata) parent object:

```xml
<xs:complexType name="MetadataAugmentationType">
	<xs:annotation>
		<xs:documentation>A data type for additional information about metadata.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:AugmentationType">
			<xs:sequence>
				<xs:element ref="j:CriminalInformationIndicator" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:IntelligenceInformationIndicator" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

There are multiple methods for creating metadata objects:

#### NIEM-supplied metadata objects can added to a subset and included in your exchange

Here's NIEM's [`nc:Metadata`](https://niemopen.github.io/niem-open-training/nc.html#Metadata) and [`nc:MetadataType`](https://niemopen.github.io/niem-open-training/nc.html#MetadataType):

```xml
<xs:complexType name="MetadataType">
	<xs:annotation>
		<xs:documentation>A data type for information that further qualifies primary data; data about data.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:AdministrativeID" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:CaveatText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:Comment" minOccurs="0" maxOccurs="unbounded"/>
				<!-- additional elements remvoed for clarity -->
				<xs:element ref="nc:MetadataAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>

<xs:element name="Metadata" type="nc:MetadataType" nillable="true">
	<xs:annotation>
		<xs:documentation>Information that further qualifies primary data; data about data.</xs:documentation>
	</xs:annotation>
</xs:element>

```
Using a `nc:metadataRef` attribute allows objects to point to standalone metadata objects:

- Conceptually, an object is saying that this is the metadata that applies to itself, this is _my_ metadata
- Can contain multiple IDs, separated with spaces, based on `IDREFS`
- The matching `id`s must exist in the instance document'

This attribute is built into [nc:TextType](https://niemopen.github.io/niem-open-training/nc.html#TextType):

```xml
<j:CrashPersonInjury>
	<nc:InjuryDescriptionText nc:metadataRef="PMD01">Broken Arm</nc:InjuryDescriptionText>
</j:CrashPersonInjury>

<nc:Metadata structures:id="PMD01">
	<ext:PrivacyMetadataAugmentation>
		<ext:PrivacyCode>PII</ext:PrivacyCode>
	</ext:PrivacyMetadataAugmentation>
</nc:Metadata>
```

You could also extend other objects, both simple and complex, to include `nc:metadataRef`:
```xml
<ext:Charge nc:metadataRef="JMD01">
	<j:ChargeDescriptionText>Furious Driving</j:ChargeDescriptionText>
	<j:ChargeFelonyIndicator>false</j:ChargeFelonyIndicator>
</ext:Charge>

<nc:Metadata structures:id="JMD01">
	<j:MetadataAugmentation>
		<j:CriminalInformationIndicator>true</j:CriminalInformationIndicator>
	</j:MetadataAugmentation>
</nc:Metadata>
```

#### New metadata objects can be created in an extension as an augmentation

```xml
<xs:element name="InjuryPrivacyMetadataAugmentation"
			type="ext:InjuryPrivacyMetadataAugmentationType"
			substitutionGroup="nc:InjuryAugmentationPoint">
	<xs:annotation>
		<xs:documentation>Additional information about Privacy.</xs:documentation>
	</xs:annotation>
</xs:element>
<xs:complexType name="InjuryPrivacyMetadataAugmentationType">
	<xs:annotation>
		<xs:documentation>A data type for Additional information about Privacy.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:AugmentationType">
			<xs:sequence>
				<xs:element ref="ext:PrivacyCode" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
The Augmentation then gets swapped in, replacing `nc:InjuryAugmentationPoint`:

```xml
<j:CrashPerson>
	<j:CrashPersonInjury>
		<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
		<j:InjurySeverityCode>3</j:InjurySeverityCode>
		<!-- replacing nc:InjuryAugmentationPoint -->
		<ext:InjuryPrivacyMetadataAugmentation>
			<ext:PrivacyCode>PII</ext:PrivacyCode>
		</ext:InjuryPrivacyMetadataAugmentation>
	</j:CrashPersonInjury>
	<ext:PersonDefenestrationIndicator>false</ext:PersonDefenestrationIndicator>
</j:CrashPerson>
```

#### New metadata objects can be created in an extension added as a standalone object

```xml
<xs:element name="Injury" type="ext:InjuryType">
	<xs:annotation>
		<xs:documentation>A form of harm or damage sustained by a person.</xs:documentation>
	</xs:annotation>
</xs:element>
<xs:complexType name="InjuryType">
	<xs:annotation>
		<xs:documentation>A data type for a form of harm or damage sustained by a person.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:InjuryType">
			<xs:sequence>
				<xs:element ref="ext:PrivacyCode" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
This new object can then be used like any other object:

```xml
<ext:Injury>
	<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
	<j:InjurySeverityCode>3</j:InjurySeverityCode>
	<ext:PrivacyCode>PII</ext:PrivacyCode>
</ext:Injury>
```
So in our example, we're mapping `IsCriminalInformation`. Searching for "criminal information" brings up [`j:CriminalInformationIndicator`](https://niemopen.github.io/niem-open-training/j.html#CriminalInformationIndicator), which is inside of  [`j:MetadataAugmentation`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentation), which can be substituted for [`nc:MetadataAugmentationPoint`](https://niemopen.github.io/niem-open-training/nc.html#MetadataAugmentationPoint), which is inside of [`nc:Metadata`](https://niemopen.github.io/niem-open-training/nc.html#Metadata)

### Artifacts

- [Metadata](/Text_Document/07_Metadata.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/08_Metadata.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/08_Metadata.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/08_Metadata.pdf)

___

## External Standards

![External Standards](/Req_Analysis_Graphics/08_External_Standards_CrashDriverClassDiagram.png)

- NIEM supports external standards, if they’re XML
- Wraps them in NIEM-conformant adapters
- Example:
	- NIEM: `nc:LocationGeospatialCoordinateAbstract` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-125z)/[Wayfarer](http://niem5.org/wayfarer/nc/LocationGeospatialCoordinateAbstract.html))
	- NIEM-conformant adapter: `geo:LocationGeospatialPoint` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-m73))
	- External standard: `gml:Point` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-fux))
- You’ll probably never use this, but should know it’s there
- SSGT supports them; Wayfarer does not

### Schemas

`LocationType` contains a `nc:LocationGeospatialCoordinateAbstract`:

```xml
<xs:complexType name="LocationType">
	<xs:annotation>
		<xs:documentation>A data type for geospatial location.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:LocationAddressAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationArea" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationCategoryAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationContactInformation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationDescriptionText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationDirectionsText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationGeospatialCoordinateAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationHeightAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationIdentification" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationLandmarkAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationLocale" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationMapLocation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationName" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationPart" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationRangeDescriptionText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationRelativeLocation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationSurroundingAreaDescriptionText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
`nc:LocationGeospatialCoordinateAbstract` is the head of a substitution group:

```xml
<xs:element name="LocationGeospatialCoordinateAbstract" abstract="true">
	<xs:annotation>
		<xs:documentation>A data concept for a geospatial location.</xs:documentation>
	</xs:annotation>
</xs:element>
```

One of the members of that substitution group is `geo:LocationGeospatialPoint`, which is an adapter to the external standard:

```xml
<xs:element name="LocationGeospatialPoint" type="geo:PointType" substitutionGroup="nc:LocationGeospatialCoordinateAbstract" nillable="true">
	<xs:annotation>
		<xs:documentation>A 2D or 3D geometric point. A gml:Point is defined by a single coordinate tuple.
			The direct position of a point is specified by the gml:pos element which is of
			type gml:DirectPositionType.</xs:documentation>
	</xs:annotation>
</xs:element>
```
Its type is `geo:PointType`. We're still in NIEM, but `gml:Point` isn't:

```xml
<xs:complexType name="PointType" appinfo:externalAdapterTypeIndicator="true">
	<xs:annotation>
		<xs:documentation>A data type for a 2D or 3D geometric point. A gml:Point is defined by a single
			coordinate tuple. The direct position of a point is specified by the gml:pos element which is
			of type gml:DirectPositionType.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="gml:Point" minOccurs="1" maxOccurs="1">
					<xs:annotation>
						<xs:documentation>A gml:Point is defined by a single coordinate tuple.
							The direct position of a point is specified by the gml:pos element
							which is of type gml:DirectPositionType.</xs:documentation>
					</xs:annotation>
				</xs:element>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
And here is the `gml:Point` object from the external standard.

```xml
<element name="Point" type="gml:PointType" substitutionGroup="gml:AbstractGeometricPrimitive">
	<annotation>
		<documentation>A Point is defined by a single coordinate tuple. The direct position of a point is specified by the pos element which is of type DirectPositionType.</documentation>
	</annotation>
</element>

<complexType name="PointType">
	<complexContent>
		<extension base="gml:AbstractGeometricPrimitiveType">
			<sequence>
				<choice>
					<element ref="gml:pos"/>
					<element ref="gml:coordinates"/>
				</choice>
			</sequence>
		</extension>
	</complexContent>
</complexType>

```

The resulting XML instance looks like this:

```xml
<nc:Location>
	<geo:LocationGeospatialPoint>
		<gml:Point gml:id="point1">
			<gml:pos srsName="urn:ogc:def:crs:EPSG::4326" srsDimension="2">40.689167 -74.044444</gml:pos>
		</gml:Point>
	</geo:LocationGeospatialPoint>
</nc:Location>
```
NIEM has its own way of tagging coordinates. It's more verbose and starts with [`nc:Location2DGeospatialCoordinate`](https://niemopen.github.io/niem-open-training/nc.html#Location2DGeospatialCoordinate). We'll include both methods in our example.

### Artifacts

- [External Standards](/Text_Document/09_External_Standards.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/09_External_Standards.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/09_External_Standards.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/09_External_Standards.pdf)

___
## Creating New Objects

![New Element Flowchart](/Mapping_Graphics/New_Element_Flowchart.png)

___

### Creating Simple Data Elements

![Simple Elements](/Req_Analysis_Graphics/10_Simple_Elements_CrashDriverClassDiagram.png)

- Base them on whichever XML Schema data type is appropriate
	- They're all in the [niem-xs](https://niemopen.github.io/niem-open-training/niem-xs.html) schema
- Follow the flowchart for help
- Base on the `niem-xs` adapters if you need referencing
	- Folks generally do this anyway, for consistency
- Follow the naming format of existing NIEM elements of that type, especially regarding the last term, e.g. “Text”, “Code”, etc.

Create `PersonDefenestrationIndicator` using the existing NIEM type `niem-xs:boolean`. By giving it `j:CrashPersonAugmentationPoint` as a substitution group head, it can go inside of the `j:CrashPerson`:

```xml
<xs:element name="PersonDefenestrationIndicator" type="niem-xs:boolean"
	substitutionGroup="j:CrashPersonAugmentationPoint">
	<xs:annotation>
		<xs:documentation>True if this person was thrown through a window; false otherwise.</xs:documentation>
	</xs:annotation>
</xs:element>
```
The resulting XML instance is then:

```xml
<j:CrashPerson>
	<j:CrashPersonInjury>
		<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
		<j:InjurySeverityCode>3</j:InjurySeverityCode>
	</j:CrashPersonInjury>
	<ext:PersonDefenestrationIndicator>false</ext:PersonDefenestrationIndicator>
</j:CrashPerson>
```
For a more complicated example, we can create the `ext:PrivacyCode` element along with a `ext:PrivacyMetadataAugmentation` to hold it.

The actual codes are defined in the simple type, `ext:PrivacyCodeSimpleType`. Each `enumeration` defines a code. The `documentation` tags provide a longer text description of the code:

```xml
<xs:simpleType name="PrivacyCodeSimpleType">
	<xs:annotation>
		<xs:documentation>A data type for a code representing a kind of
			privacy.</xs:documentation>
	</xs:annotation>
	<xs:restriction base="xs:token">
		<xs:enumeration value="PII">
			<xs:annotation>
				<xs:documentation>Personally Identifiable Information</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="MEDICAL">
			<xs:annotation>
				<xs:documentation>Medical Information</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
	</xs:restriction>
</xs:simpleType>

```

The complex type `ext:PrivacyCodeType` is then extended from `ext:PrivacyCodeSimpleType`. All this does is add infrastructure attributes to allow things of this type to refer to other elements, or be referred to in turn:

```xml
<xs:complexType name="PrivacyCodeType">
	<xs:annotation>
		<xs:documentation>A data type for a code representing a kind of
			privacy.</xs:documentation>
	</xs:annotation>
	<xs:simpleContent>
		<xs:extension base="ext:PrivacyCodeSimpleType">
			<xs:attributeGroup ref="structures:SimpleObjectAttributeGroup"/>
		</xs:extension>
	</xs:simpleContent>
</xs:complexType>
```
Then `ext:PrivacyCode` is created to be of `ext:PrivacyCodeType`:

```xml
<xs:element name="PrivacyCode" type="ext:PrivacyCodeType">
	<xs:annotation>
		<xs:documentation>A code representing a kind of privacy.</xs:documentation>
	</xs:annotation>
</xs:element>
```

In this exchange, this code is metadata to be applied to other objects, so we can create `ext:PrivacyMetadataAugmentation` to hold it:

```xml
<xs:complexType name="PrivacyMetadataAugmentationType">
	<xs:annotation>
		<xs:documentation>A data type for metadata about Privacy.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:AugmentationType">
			<xs:sequence>
				<xs:element ref="ext:PrivacyCode" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>

<xs:element name="PrivacyMetadataAugmentation" type="ext:PrivacyMetadataAugmentationType"
	substitutionGroup="nc:MetadataAugmentationPoint">
	<xs:annotation>
		<xs:documentation>Metadata about Privacy.</xs:documentation>
	</xs:annotation>
</xs:element>
```
And then we need to make an extended `ext:CrashPersonInjury` to point to it:

```xml
<xs:complexType name="InjuryType">
	<xs:annotation>
		<xs:documentation>A data type for a form of harm or damage sustained by a person.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:InjuryType">
			<xs:attribute ref="nc:metadataRef" use="optional"/>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>

<xs:element name="CrashPersonInjury" type="ext:InjuryType">
	<xs:annotation>
		<xs:documentation>An injury received by a person involved in a traffic accident.</xs:documentation>
	</xs:annotation>
</xs:element>
```

### Instance Documents

The resulting XML instance document includes:

```xml
<ext:CrashPersonInjury nc:metadataRef="PMD01">
	<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
	<j:InjurySeverityCode>3</j:InjurySeverityCode>
</ext:CrashPersonInjury>

<nc:Metadata structures:id="PMD01">
	<ext:PrivacyMetadataAugmentation>
		<ext:PrivacyCode>PII</ext:PrivacyCode>
	</ext:PrivacyMetadataAugmentation>
</nc:Metadata>
```
Of course, we could have alternatively defined it to hook onto `nc:InjuryAugmentationPoint` by changing the `substitutionGroup` attribute instead of extending `CrashPersonInjury`. This allows us to put it inside `j:CrashPersonInjury` but it can't be referred to by other objects:

```xml
<j:CrashPersonInjury>
	<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
	<j:InjurySeverityCode>3</j:InjurySeverityCode>
	<ext:PrivacyMetadataAugmentation>
		<ext:PrivacyCode>MEDICAL</ext:PrivacyCode>
	</ext:PrivacyMetadataAugmentation>
</j:CrashPersonInjury>
```
We'll use this latter method in our example.

### Artifacts

- [Creating New Objects - Simple Data](/Text_Document/10_Creating_New_Objects_Simple_Data.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/10_Creating_New_Objects_Simple_Data.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/10_Creating_New_Objects_Simple_Data.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/10_Creating_New_Objects_Simple_Data.pdf)

___
### Creating Complex Objects

![Complex Objects](/Req_Analysis_Graphics/11_Complex_Objects_CrashDriverClassDiagram.png)

- If you’re making a special kind of existing NIEM type:
	- Use that type as a base to extend from and add things to it
- If you're just adding things to an existing NIEM type:
	- Create an Augmentation to hold your new things and hook it on the existing type's AugmentationPoint
- If you’re starting from scratch:
	- Use `structures:ObjectType` as a base to extend from and add things to it

Here we're making the root element that will hold everything else. We create `CrashDriverInfoType`, basing it on `structures:ObjectType` so that it's just an empty object.

To that empty object, we add all the major objects in our exchange, `nc:Person`, `j:Crash`, and `ext:Charge`. We also add a `j:PersonChargeAssociation` which lets us link together people and charges. Finally, we add a metadata object, the built-in  `nc:Metadata`.

```xml
<xs:element name="CrashDriverInfo" type="exch:CrashDriverInfoType">
	<xs:annotation>
		<xs:documentation>A collection of information about the driver of a vehicle in a crash.</xs:documentation>
	</xs:annotation>
</xs:element>

<xs:complexType name="CrashDriverInfoType">
	<xs:annotation>
		<xs:documentation>A data type for a collection of information about the driver of a vehicle in a crash.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:Person" minOccurs="1" maxOccurs="1"/>
				<xs:element ref="j:Crash" minOccurs="1" maxOccurs="1"/>
				<xs:element ref="j:PersonChargeAssociation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="ext:Charge" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:Metadata" minOccurs="0"maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

Another example is when we created `ext:LicenseAugmentation` and `ext:LicenseAugmentationType` when talking about augmentations.

### Adding New Content to the Exchange

To summarize, there are two major ways to add new content to an exchange.

If you're _already_ extending to make a new complex object and type, like `CrashDriverInfo` and `CrashDriverInfoType` above, you can simply add new elements to the new type. This is called "concrete extension."

But if you're not already creating the new type for other reasons, you should use augmentations. We used `j:CrashPersonAugmentationPoint` in our exchange and used it as a hook on which we hung `ext:PersonDefenestrationIndicator`.

### Problems with Concrete Extensions

The issue with concrete extensions is that if the extension is happening deep inside an object, all the surrounding objects will also need to be extended. For example, if instead of using `j:DriverLicenseAugmentationPoint`, suppose we extended `j:DriverLicenseType`, making a new `ext:DriverLicenseType` to hold our new object. Now we need a new element for it, `ext:DriverLicense`.

But `j:CrashDriver` doesn't hold an `ext:DriverLicense`, so we need to make a new `ext:CrashDriverType` and `ext:CrashDriver` that can hold an `ext:DriverLicense`.

But `j:CrashVehicle` doesn't hold a `ext:CrashDriver`, so we need to make a new `ext:CrashVehicleType` and `ext:CrashVehicle` that can hold an `ext:CrashDriver`.

But `j:Crash` doesn't hold an `ext:CrashVehicle`, so we need to make a new `ext:CrashType` and `ext:Crash` that can hold `ext:CrashVehicle`.

That's a lot of extra work and muddies the semantics of the elements.

### Artifacts

- [Creating New Objects - Complex Objects](/Text_Document/11_Creating_New_Objects_Complex_Objects.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/11_Creating_New_Objects_Complex_Objects.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/11_Creating_New_Objects_Complex_Objects.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/11_Creating_New_Objects_Complex_Objects.pdf)

___
## Mapping Completed!

- [Crash Driver Report Complete](/Text_Document/12_Crash_Driver_Report_Complete.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/12_Crash_Driver_Report_Complete.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/12_Crash_Driver_Report_Complete.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/12_Crash_Driver_Report_Complete.pdf)

| Started With | Ended With |
| --- | --- |
| ![Business UML](/Req_Analysis_Graphics/CrashDriverClassDiagram.png) | ![NIEM UML](/Req_Analysis_Graphics/CrashDriverClassDiagram-NIEM.png) |

___
![Build and Validate](/IEPD_Process_Graphics/Process_Artifacts_3_scaled.png)

# Build and Validate
- Conformance
- Subsets
- Extension Schemas
- How things fit together

## NIEM Conformance
- Follow the rules in the [Naming and Design Rules (NDR)](http://niem.github.io/reference/specifications/ndr/) (NIEM 5)
	- Available in draft form for NIEM 6 on [Github](https://github.com/niemopen/niem-naming-design-rules/blob/dev/ndr6src.md)
- Follow the rules in the [IEPD Spec](http://niem.github.io/reference/specifications/iepd/) (NIEM 5)
	- Coming eventually for NIEM 6
- Many NDR rules exist as Schematron
	- Can check these via the Conformance Testing Assistant (ConTesA) for NIEM 5
	- Can run the Schematron directly oXygen, with a plug-in in XMLSpy
		- See below
	- NIEM Toolbox will provide this functionality for NIEM 6 soon

## Schema Subsets
- NIEM has ~13,000 elements
- You don’t want them all
- NIEM supports mini versions of NIEM
	- With the elements / types you want
	- Plus things needed to make the elements / types you want work
- Use the [SSGT](https://tools.niem.gov/niemtools/ssgt/index.iepd) for this for NIEM 5
	- NIEM Toolbox will provide this functionality for NIEM 6 soon

## Extension Schema(s)
- Create new elements for your exchange
- Defines the root element of the exchange
- Emulate how NIEM does it
- Utilize Augmentations to add your new objects to existing NIEM objects
	- Concrete extension is an alternative
- Can have multiple extension schemas
- Some folks put code tables into a separate extension schema

## How Schemas Fit Together

```mermaid
flowchart LR
	extension.xsd --> geospatial.xsd
	extension.xsd --> justice.xsd
	extension.xsd --> niem-xs.xsd
	extension.xsd --> structures.xsd
	extension.xsd --> niem-core.xsd
	
	niem-core.xsd --> structures.xsd
	niem-core.xsd --> niem-xs.xsd
	
	niem-xs.xsd --> structures.xsd
	
	justice.xsd --> niem-xs.xsd
	justice.xsd --> structures.xsd
	justice.xsd --> aamva_d20.xsd
	justice.xsd --> niem-core.xsd
	
	aamva_d20.xsd --> structures.xsd
	
	geospatial.xsd --> gml.xsd
	geospatial.xsd --> niem-core.xsd
	geospatial.xsd --> structures.xsd
	gml.xsd --> xlinks.xsd
```


## Help with Schemas
- Use a good validating XML editor
	- XMLSpy
		- Windows
	- oXygen
		- Windows, macOS, Linux
- Declare a conformance target
	- Just use the same one I am
- Declare and import all schemas used
	- Watch out for schemas incorporated only via substitution groups
	- Group heads don’t know who the members are
	- Still need to declare and import those

## Example Instances
- Required
- Validating against your schemas ensures your intent
- Some XML editors can create them from schemas
	- But you’ll always need to tweak those
- Other tools are out there…

## Tips and Tricks
- Christina’s [oXygen Snippets](https://niem.github.io/reference/tools/oxygen/snippets/)
	- oXygen only
- Use [Schematron](https://niem.github.io/reference/tools/oxygen/ndr/) to check your work as you go
	- oXygen
	- XMLSpy with plug-in
- [MEP Builder](https://sourceforge.net/projects/niem-mep-builder/)
	- Work on mapping spreadsheets
	- Generate subsets

___
![Other Artifacts](/IEPD_Process_Graphics/Process_Artifacts_4_scaled.png)

# Assemble and Document
- IEPD Catalog ([[iepd-catalog.xml]])
	- Metadata about the Message Spec / IEPD
	- What file is what
	- What the root element is
- Readme ([[Crash Driver IEPD/README|README]])
- Changelog ([[changelog]])
- Conformance Assertion ([[conformance]])
- Mapping Spreadsheet
- Main Documentation

## Main Documentation
- Just a Word document
	- Or another document format, e.g. Markdown, PDF, etc.
- A NIEM Message Spec / IEPD master document should (at a minimum) describe:
	- Message Spec / IEPD purpose
	- Scope
	- Business value
	- Exchange information
	- Senders/receivers
	- Interactions
	- References to other documentation, if applicable
- Don’t paste schemas into them!

## Message Spec / IEPD Assembly
- Message Specs / IEPDs are just ZIP files full of artifacts
- Can organize how you like
	- The IEPD Catalog is the guide to your organization
	- Generally, keep it simple
- MEP Builder can help with this
___
# Publishing

## NIEM Repos

- NIEM used to have a problem with existing repositories being out of date
	- IEPD Clearinghouse (old material)
	- Work With IEPDs (currently not working)
- New repository is here!
	- [Message Exchange Package (MEP) Registry & Repository](https://www.niem.gov/about-niem/message-exchange-package-mep-registry-repository)
	- Has all the archival material from the old Clearinghouse
	- Has all the material from "Work With IEPDs"
	- Has new material as well

## Other Websites

- Other entities can list their own
	- Example: [ACF](https://acf.gov/completed-information-exchange-packet-documentation-iepd)

___

![Implementation](IEPD_Process_Graphics/Process_Artifacts_5_scaled.png)

# Implementation

- Remember that NIEM is just the payload
	- It’s just plain old XML
		- Well, okay, with referencing
	- Or it’s just plain JSON
		- Well, okay, with JSON-LD
- Remember the scope of NIEM
	- Things outside the payload aren't NIEM
	- You don’t have to do anything special for NIEM outside NIEM’s scope

## Skill level to Implement NIEM
- Developers with the skills to design and implement a data exchange can learn the NIEM approach in a matter of hours
- Developer training is available
- Plenty of example IEPDs to follow
	- New repository!
- Don’t start from scratch, leverage shared IEPDs
- The NIEM technical specifications are complex, however
	- Most developers do not need to read them
	- Free tools can perform most of the conformance checking
		- Schematron directly
		- [Conformance Testing Assistant (ConTesA)](https://tools.niem.gov/contesa/)
		- NIEM Toolbox is coming for NIEM 6!

___
# Resources

## Documentation

- Prior NIEM Releases
	- [http://niem.github.io/niem-releases/](http://niem.github.io/niem-releases/)
- Current NIEM Specifications
        -[https://github.com/niemopen#specifications/](https://github.com/niemopen#specifications/)
- Prior NIEM Specifications
	- [http://niem.github.io/reference/specifications/](http://niem.github.io/reference/specifications/)
- Materials from this course:
	- [https://github.com/niemopen/niem-open-training/](https://github.com/niemopen/niem-open-training/)
- NIEMOpen.org Contact Page
	- [https://www.niemopen.org/contact](https://niemopen.org/contact/)

## Tools
- NIEM Toolbox
	- [https://niemopen.github.io/niem-toolbox/](https://niemopen.github.io/niem-toolbox/)
- SSGT:
	- [https://tools.niem.gov/niemtools/ssgt/index.iepd](https://tools.niem.gov/niemtools/ssgt/index.iepd)
- Conformance Testing Assistant (ConTesA)
	- [https://tools.niem.gov/contesa/](https://tools.niem.gov/contesa/)
- NDR Schematron
	- [https://niem.github.io/reference/tools/oxygen/ndr/](https://niem.github.io/reference/tools/oxygen/ndr/)
- MEP Builder
	- [https://mep.niemopen.org/]((https://mep.niemopen.org/)/)
- Wayfarer:
	- [http://niem5.org/wayfarer/](http://niem5.org/wayfarer/)
- oXygen Snippets
	- [https://niem.github.io/reference/tools/oxygen/snippets/](https://niem.github.io/reference/tools/oxygen/snippets/)

## Repositories
- Message Exchange Package (MEP) Registry & Repository
	- https://www.niem.gov/about-niem/message-exchange-package-mep-registry-repository

___
Generated on: 
Fri May  9 18:17:59 UTC 2025
