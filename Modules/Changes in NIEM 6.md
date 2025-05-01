# Changes NIEM 5 to NIEM 6

## Common Model Format

- Canonical definition of NIEM
	- Alongside XML Schema
	- JSON Schema supported but _not_ as _definitional_ serialization
- Defines modeling concepts in modeling terms
	- Properties, classes, and data types
	- Replaces implied modeling concepts with XML Schema terms
- Presented in XML, but the concepts are serialization agnostic
	- That said, CMF is still somewhat XML-ish in how it instantiates concepts
	- Easily converted to XML Schema and back
	- Manageably converted to JSON Schema but _not_ back
	- Makes transformations to other serializations easier
- Allows for tool-based support for both XML and JSON (and RDF, et al) from a single "code base"
- CMF is normally hidden behind tooling
	- You can do CMF by hand, but it's recommended to use the tooling

For a more detailed look at CMF, see [[Intro to Common Model Format]].

## Elimination of Explicit Roles

- NIEM 5 used explicit role objects to denote when something was playing a role, e.g. `RoleOfPerson`
- NIEM 6 links objects and their roles with the `structures:uri` attribute

## Changes in Metadata

- Metadata now leverages Augmentations
	- Just normal objects now
	- Simpler to create and use
- Can also use the `nc:metadataRef` to reference Metadata objects from the things to which the metadata applies

## Highlights

The following is a summary of the major changes made in NIEM 6.0:

- Core and cross-domain harmonization
- Updates to support the transition of NIEM to an OASIS Open Project, including namespace URI changes.
- Updates to support upcoming NIEM-NDR-v6.0 changes, including:
	- **Adapter changes** - New representation terms and a simpler type syntax.
	- **Attribute augmentations** - Allows message designers to create semantically-named attribute references from simple data properties to supplemental content.
	- **Attribute wildcards** - Allows declared attributes to be added to any NIEM element property.
	- **Metadata changes** - Now treated like regular objects, can be included in types where applicable, and can be augmented and extended.
	- **Role changes** - Leverages standard type extension and the existing `structures:uri` attribute to relate different roles of the same entity in a message together, replacing the previous `RoleOf` construct.
- Updates related to new digital identity requirements led by the Emergency Management domain, including:
	- `nc:IdentificationType` and related augmentation types
	- `nc:LicenseType` _(new)_ to support other kinds of licenses with NIEM
	- `j:DriverLicenseType` and related types
	- `nc:PassportType`, which now extends `nc:IdentificationType`
	- `em:PersonIDCardType`, which has been refactored to augment `nc:IdentificationType`
	- `m:SeamanLicenseType`, which can now be represented by the new `nc:LicenseType`
	- `m:MerchantMarinerDocumentType`, which can now be represented by the new `nc:LicenseType`
- Code set updates, including:
	- Updates provided by the FBI for the National Crime Information Center (NCIC) codes
	- GENC codes, version 3-12
- Synchronized the Justice domain version number with the rest of the model: now Justice 6.0

Details:
https://github.com/niemopen/niem-model/blob/dev/README.md