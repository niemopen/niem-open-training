## Code Tables

![Code Tables](/Req_Analysis_Graphics/06_Code_Tables_CrashDriverClassDiagram.png)

- Codes help ensure accurate information
- Codes are, essentially, strings, simple data
- A few in NIEM are integers
- Elements defined in the domains
- Types are often defined in their own namespaces
- Examples:
	- `j:InjurySeverityCode` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-45s)/[Wayfarer](http://niem5.org/wayfarer/j/InjurySeverityCode.html))
		- In the SSGT, the actual codes are viewable on the page for the base simple type, e.g. [`aamva_d20:AccidentSeverityCodeSimpleType`](https://tools.niem.gov/niemtools/ssgt/SSGT-GetType.iepd?typeKey=o4-c)
		- In Wayfarer, there should be a link on the element page bringing up the codes in a separate window, e.g. [`aamva_d20:AccidentSeverityCodeSimpleType`](http://niem5.org/wayfarer/aamva_d20/AccidentSeverityCodeSimpleType_codes.html)
	- Anything ending in "Code" ([SSGT](http://niem5.org/ssgt_redirect.php?query=code)/[Wayfarer](http://niem5.org/wayfarer/search.php?option=names&query=code))
- Codes nearly always have a text alternative

### Schemas

[`j:InjurySeverityCode`](https://niemopen.github.io/niem-open-training/j.html#InjurySeverityCode) is a code table, with its codes defined in another namespace, the one for [AAMVA](https://www.aamva.org/). Here's the schema for the element:

```json
"j:InjurySeverityCode": {
	"description": "A severity of an injury received by a person, such as in a traffic accident or crash.",
	"$ref": "#/definitions/aamva_d20:AccidentSeverityCodeType"
}
```

The actual codes are defined in  [`aamva_d20:AccidentSeverityCodeType`](https://niemopen.github.io/niem-open-training/aamva_d20.html#AccidentSeverityCodeType), as a `oneOf` construct listing one code per `const` below:

```json
"aamva_d20:AccidentSeverityCodeType": {
	"description": "A data type for severity levels of an accident.",
	"type": "string",
	"oneOf": [
		{
			"const": "1",
			"description": "Fatal Accident"
		},
		{
			"const": "2",
			"description": "Incapacitating Injury Accident"
		},
		{
			"const": "3",
			"description": "Non-incapacitating Evident Injury"
		},
		{
			"const": "4",
			"description": "Possible Injury Accident"
		},
		{
			"const": "5",
			"description": "Non-injury Accident"
		},
		{
			"const": "9",
			"description": "Unknown"
		}
	]
}
```
### Instance Documents

The code is what shows up in the instance document. The longer definition does not. If you want to know that "3" means "Non-incapacitating Evident Injury," you need to refer to the schema. JSON Schema validation _will_ verify that the value is one of the enumerated `const` values: 

```json
"j:CrashPersonInjury": {
	"nc:InjuryDescriptionText": "Broken Arm",
	"j:InjurySeverityCode": "3"
}
```

### Artifacts

- [Code Tables](/Text_Document/06_Code_Tables.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/06_Code_Tables.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/06_Code_Tables.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/06_Code_Tables.pdf)

___
