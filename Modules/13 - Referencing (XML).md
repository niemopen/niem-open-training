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
