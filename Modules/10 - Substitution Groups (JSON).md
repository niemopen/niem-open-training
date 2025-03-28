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
