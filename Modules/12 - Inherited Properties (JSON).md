![Inherited Properties](/Req_Analysis_Graphics/03_Inherited_Properties_CrashDriverClassDiagram.png)

- NIEM is a model, not a flat data dictionary
- Some concepts don’t exist as elements using the terms for the concept
- Instead, properties are "inherited"
	- Scare quotes because JSON Schema doesn't really support inheritance
	- Instead, you combine groups of elements
	- End result is similar
- There is no “Crash Date” in NIEM ([SSGT](http://niem5.org/ssgt_redirect.php?query=crash+date)/[Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=crash+date))
- There _is_ an `ActivityDate` which can be inside a `Crash` object ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-44f)/[Wayfarer](http://niem5.org/wayfarer/j/Crash.html))

### Schemas

Here's [`j:Crash`](http://niem5.org/schemas/j.html#Crash) and its type, `j:CrashType`:

```json
"j:Crash": {
	"description": "A traffic accident.",
	"$ref": "#/definitions/j:CrashType"
}
```

[`j:CrashType`](http://niem5.org/schemas/j.html#CrashType) contains several things, but the important thing here is what it's based on, `j:DrivingIncidentType`:

```json
"j:CrashType": {
	"description": "A data type for a traffic accident.",
	"allOf": [
		{"$ref": "#/definitions/j:DrivingIncidentType"},
		{
			"type": "object",
			"properties": {
				"j:CrashVehicle": {"$ref": "#/properties/j:CrashVehicle"},
				"j:CrashPerson": {"$ref": "#/properties/j:CrashPerson"},
				"nc:Location": {"$ref": "#/properties/nc:Location"}
			},
			"required": [
				"j:CrashVehicle",
				"nc:Location"
			]
		}
	]
}
```

[`j:DrivingIncidentType`](http://niem5.org/schemas/j.html#DrivingIncidentType) is, in turn, based on an even more generic type, `nc:IncidentType`:

```json
"j:DrivingIncidentType": {
	"description": "A data type for details of an incident involving a vehicle.",
	"$ref": "#/definitions/nc:IncidentType"
}
```

[`nc:IncidentType`](http://niem5.org/schemas/nc.html#IncidentType) is, also in turn, based on a very generic type, `nc:ActivityType`:

```json
"nc:IncidentType": {
	"description": "A data type for an occurrence or an event that may require a response.",
	"$ref": "#/definitions/nc:ActivityType"
}
```

And we finally get to [`nc:ActivityType`](http://niem5.org/schemas/nc.html#ActivityType), which contains [`nc:ActivityDate`](http://niem5.org/schemas/nc.html#ActivityDate):

```json
"nc:ActivityType": {
	"description": "A data type for a single or set of related actions, events, or process steps.",
	"type": "object",
	"properties": {
		"nc:ActivityDate": {"$ref": "#/properties/nc:ActivityDate"}
	},
	"required": ["nc:ActivityDate"]
}
```

What this all means is that a `j:Crash` object can contain a `nc:ActivityDate`, which is, contextually, a Crash Date.

### Instance Documents

Instance in JSON:

```json
"j:Crash": {
	"nc:ActivityDate": {
		"nc:Date": "1900-05-04"
	}
}
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