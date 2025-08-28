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

_However_, JSON Schema and JSON in general lack this concept of substitution groups. (So do most other serializations.) So in JSON Schema, `nc:Date` is directly inside of things of `nc:DateType`, with no substitution happening. This is one reason why NIEM transformations from XML to JSON are possible, but transformations the other direction are not. Transformations to JSON are _lossy_.

### Schemas

Here we see [`nc:PersonBirthDate`](https://niemopen.github.io/niem-open-training/nc.html#PersonBirthDate) and its type, `nc:DateType`:

```json
"nc:PersonBirthDate": {
	"description": "A date a person was born.",
	"$ref": "#/definitions/nc:DateType"
}
```
Unlike in XML, [`nc:DateType`](https://niemopen.github.io/niem-open-training/nc.html#DateType) contains `nc:Date`directly:

```json
"nc:DateType": {
	"description": "A data type for a calendar date.",
	"type": "object",
	"properties": {
		"nc:Date": {"$ref": "#/properties/nc:Date"}
	},
	"required": ["nc:Date"]
}
```


### Instance Documents

The matching JSON similarly just shows `nc:Date`:

```json
"nc:Person": {
	"nc:PersonBirthDate": {
		"nc:Date": "1890-05-04"
	},
	"nc:PersonName": {
		"nc:PersonGivenName": "Peter",
		"nc:PersonMiddleName": [
			"Death",
			"Bredon"
		],
		"nc:PersonSurName": "Wimsey"
	}
}
```

### Artifacts

- [Substitition Groups](/Text_Document/02_Substitution_Groups.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/02_Substitution_Groups.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/02_Substitution_Groups.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/02_Substitution_Groups.pdf)

___
