# Message Spec / IEPD Overview
- "Information Exchange Package Documentation"
- Slowly changing to "Message Specification"
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

![IEPD Process](IEPD_Process_Graphics/IEPD_Process_scaled.png)

Each step produces artifacts used by subsequent steps:

1. A clue as to what you're doing...
2. UML Diagrams
3. Mapping Spreadsheet
4. Schemas and Instance Documents
5. Textual Documents
6. Code

![Message Spec / IEPD Process](IEPD_Process_Graphics/Process_Artifacts_scaled.png)

**Message Spec / IEPD Process – Idealized**

![Message Spec Seq Ideal](IEPD_Process_Graphics/Process_Seq_Ideal.png)

**Message Spec / IEPD Process – Real Life**

![Message Spec Seq Ideal](IEPD_Process_Graphics/Process_Seq_Real.png)
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
