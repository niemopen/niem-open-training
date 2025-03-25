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
	- Save schemas for the end