## Introduction to NIEM

- What is NIEM?
- The Scope of NIEM
- NIEM Harmonization and Organization
___
### What is NIEM? - Framework
- NIEM is a community-driven, government and jurisdiction-wide, standards-based approach to exchanging information
- Diverse communities can collectively leverage NIEM to increase efficiencies and improve decision-making
- NIEM is available to everyone, including public and private organizations
- NIEM includes a data model, governance, training, tools, technical support services, and an active community to assist users in adopting a standards-based approach to exchanging data

![NIEM Framework](Intro_Graphics/NIEM_Framework.png)
___
### What is NIEM? – Interop Problem
- If we don’t understand what each other means, we won’t be able to exchange info
- Need a common language for defining things

![Interop Problem](Intro_Graphics/Interop_Problem_scaled.png)
___
### What is NIEM? And what not?
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

![Exchanging Data and Components](Intro_Graphics/Exch_Data_Components.png)
___
### What is NIEM? – Simplified Exchanges
- When using NIEM, you only need to “speak” two languages: your own and NIEM

| Without NIEM | With NIEM |
| --- | --- |
|![Scrambled Exchanges](Intro_Graphics/Scrambled_Exchanges.png)|![Centralized Exchanges](Intro_Graphics/Centralized_Exchanges.png)|
___
### Scope of NIEM
- NIEM is a data layer standard and intentionally does not address all the necessary technologies needed for information sharing
- Exchange partners decide how to store and process the NIEM-conformant data being exchanged

![Scope of NIEM 01](Intro_Graphics/Scope_NIEM_01.png)

![Scope of NIEM 02](Intro_Graphics/Scope_NIEM_02.png)
___
### Scope of NIEM - Open Source Interconnection (OSI) model

**Detailed:**

![OSI Detailed](Intro_Graphics/OSI_01_clean.png)

**Simplified:**

![OSI Simplified](Intro_Graphics/OSI_02.png)
___
### Bottle of Liquid
**A bottle of liquid:**

| ![Bottle 01](Intro_Graphics/Bottle_01.png) | ![Bottle 02](Intro_Graphics/Bottle_02.png) |
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

![Domain Diagram](Intro_Graphics/Domain_Diagram_scaled.png)

| Existing Domains                              | Upcoming Domains             |
| --------------------------------------------- | ---------------------------- |
| Agriculture                                   | Learning and Development     |
| Biometrics                                    | International Human Services |
| Chemical, Biological, Radiological, & Nuclear |                              |
| Cyber (new in 5.1)                            |                              |
| Emergency Management                          |                              |
| Human Services                                |                              |
| Immigration                                   |                              |
| Infrastructure Protection                     |                              |
| Intelligence                                  |                              |
| International Trade                           |                              |
| Justice                                       |                              |
| Maritime                                      |                              |
| Military Operations                           |                              |
| Screening                                     |                              |
| Surface Transportation                        |                              |

**Domains hold objects specific to their domains:**

| Agriculture | Biometrics |
| --- | --- |
| ![Agriculture](Domain_Graphics/ag.png) | ![Biometrics](Domain_Graphics/biom.png) |

| Chemical, Biological, Radiological, & Nuclear | Emergency Management |
| --- | --- |
| ![CBRN](Domain_Graphics/cbrn.png) | ![Emergency Management](Domain_Graphics/em.png) |

| Human Services | Immigration |
| --- | --- |
| ![Human Services](Domain_Graphics/hs.png) | ![Immigration](Domain_Graphics/im.png) |

| Infrastructure Protection | Intelligence |
| --- | --- |
| ![Infrastructure Protection](Domain_Graphics/ip.png) | ![Intelligence](Domain_Graphics/intel.png) |

| International Trade | Justice |
| --- | --- |
| ![International Trade](Domain_Graphics/it.png) | ![Justice](Domain_Graphics/j.png) |

| Maritime | Military Operations |
| --- | --- |
| ![Maritime](Domain_Graphics/m.png) | ![Military Operations](Domain_Graphics/mo.png) |

| Screening  | Surface Transportation |
| --- | --- |
| ![Screening ](Domain_Graphics/scr.png) | ![Surface Transportation](Domain_Graphics/st.png) |


**NIEM Versioning**

- NIEM has major and minor versions, plus domain updates
- Major version releases, e.g. 4.2 to 5.0
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
	- NIEM 6.0 scheduled for end of 2023
- Minor version releases, e.g. 5.0 to 5.1:
	- Annually
	- **NIEM-Core does not change!**
		- **Neither does the underlying infrastructure**
	- Domains can change
	- Domains can be harmonized
	- Domains can be added, like Cyber in 5.1
	- Domains are not guaranteed to be backwards compatible with earlier minor releases
		- But they often are
	- NIEM 5.2 scheduled for end of 2022
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

![Org Chart](Intro_Graphics/Org_Chart.png)

**Move to OASIS**

The NIEM program is transitioning from being a solely government-funded project to an open source project under [OASIS Open](https://www.oasis-open.org). So here's a quick plug for OASIS Open...

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

For more information about supporting the NIEM OASIS Open Project, contact Dee Schur, dee.schur@oasis-open.org
