![Build and Validate](/IEPD_Process_Graphics/Process_Artifacts_3_scaled.png)

# Build and Validate
- Conformance
- Subsets
- Extension and Exchange Schemas
- How things fit together

## NIEM Conformance
- Follow the rules in the [Naming and Design Rules (NDR)](http://niem.github.io/reference/specifications/ndr/)
- Follow the rules in the [IEPD Spec](http://niem.github.io/reference/specifications/iepd/)
- Many NDR rules exist as Schematron
	- Can check these via the Conformance Testing Assistant (ConTesA)
	- Can run the Schematron directly oXygen, with a plug-in in XMLSpy

## Schema Subsets
- NIEM has ~13,000 elements
- You don’t want them all
- NIEM supports mini versions of NIEM
	- With the elements / types you want
	- Plus things needed to make the elements / types you want work
- Use the [SSGT](https://tools.niem.gov/niemtools/ssgt/index.iepd) for this! **Demo Time!**
- [MEP Builder](http://localhost:3000/) can also help!  **More Demo Time!**

## Extension Schema(s)
- Create new elements for your exchange
- Emulate how NIEM does it
- Utilize Augmentations to add your new objects to existing NIEM objects
	- Concrete extension is an alternative
- Can have multiple extension schemas
- Some folks put code tables into a separate extension schema

## Exchange Schema
- Entry point to the exchange
- Defines the root element of the exchange
- Some put the definition for the root element here
- Some put that in the extension schema
- Some lump exchange and extension together
- An exchange with multiple messages can have multiple exchange schemas, one per
	- Can share a common extension
	- Or not

## How Schemas Fit Together

![Schema Import 7](/Schema_Graphics/Schema_Import_7_scaled.png)


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
- JSON instances are more of a manual process because NIEM doesn't support JSON Schema
	- It's in the works
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

![Other Artifacts](/IEPD_Process_Graphics/Process_Artifacts_4_scaled.png)

___
