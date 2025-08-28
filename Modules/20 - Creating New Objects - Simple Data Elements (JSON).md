## Creating New Objects

![New Element Flowchart](/Mapping_Graphics/New_Element_Flowchart.png)

___

### Creating Simple Data Elements

![Simple Elements](/Req_Analysis_Graphics/10_Simple_Elements_CrashDriverClassDiagram.png)

- Base them on whichever XML Schema data type is appropriate
	- They're all in the [niem-xs](https://niemopen.github.io/niem-open-training/niem-xs.html) schema
- Follow the flowchart for help
- Base on the `niem-xs` adapters if you need referencing
	- Folks generally do this anyway, for consistency
- Follow the naming format of existing NIEM elements of that type, especially regarding the last term, e.g. “Text”, “Code”, etc.

Create `PersonDefenestrationIndicator` using the existing NIEM type `niem-xs:boolean`:

```json
"ext:PersonDefenestrationIndicator": {
	"description": "True if this person was thrown through a window; false otherwise.",
	"type": "boolean"
}
```
Then we add it to `j:CrashPersonType` so that it can go inside of the `j:CrashPerson`:

```json
"j:CrashPersonType": {
	"description": "A data type for any person involved in a traffic accident.",
	"type": "object",
	"properties": {
		"nc:RoleOfPerson": {"$ref": "#/properties/nc:RoleOfPerson"},
		"j:CrashPersonInjury": {"$ref": "#/properties/j:CrashPersonInjury"},
		"ext:PersonDefenestrationIndicator": {"$ref": "#/properties/ext:PersonDefenestrationIndicator"}
	},
	"required": ["nc:RoleOfPerson"]
}
```


The resulting JSON is:

```json
"j:CrashPerson": {
	"nc:RoleOfPerson": {
	  "@id": "#P01"
	},
	"j:CrashPersonInjury": {
	  "nc:InjuryDescriptionText": "Broken Arm",
	  "j:InjurySeverityCode": "3",
	},
	"ext:PersonDefenestrationIndicator": "false"
}
```
Note the `@id` that links to an identical `@id` in the nc:Person object.

For a more complicated example, we can create the `ext:PrivacyCode` element along with a `ext:PrivacyMetadata` to hold it.

The actual codes are defined in `ext:PrivacyCodeSimpleType`. Each `const` defines a code. The `description` tags provide a longer text description of the code:

```json
"ext:PrivacyCodeType": {
	"description": "A data type for a code representing a kind of property.",
	"type": "string",
	"oneOf": [
		{
			"const": "PII",
			"description": "Personally Identifiable Information"
		},
		{
			"const": "MEDICAL",
			"description": "Medical Information"
		}
	]
}
```

Then `ext:PrivacyCode` is created to be of `ext:PrivacyCodeType`:

```json
"ext:PrivacyCode": {
	"description": "A code representing a kind of property.",
	"type": "array",
	"items": {"$ref": "#/definitions/ext:PrivacyCodeType"},
	"maxItems": 2
}
```

In this exchange, this code is metadata to be applied to other objects, so we can create `ext:PrivacyMetadata` and `ext:PrivacyMetadataType` to hold it:

```json
"ext:PrivacyMetadata": {
	"description": "Metadata about Privacy.",
	"type": "array",
	"items": {"$ref": "#/definitions/ext:PrivacyMetadataType"}
}
```
```json
"ext:PrivacyMetadataType": {
	"description": "A data type for metadata about Privacy.",
	"type": "object",
	"properties": {
		"ext:PrivacyCode": {"$ref": "#/properties/ext:PrivacyCode"}
	}
}
```

### Instance Documents

The resulting JSON instance document is:

```json
"j:CrashPerson": [
	{
		"nc:RoleOfPerson": {"@id": "#P01"},
		"j:CrashPersonInjury": [
			{
				"nc:InjuryDescriptionText": "Broken Arm",
				"j:InjurySeverityCode": "3",
				"ext:PrivacyMetadata": [
					{
						"ext:PrivacyCode": [
							"PII",
							"MEDICAL"
						]
					}
				]
			}
		],
		"ext:PersonDefenestrationIndicator": false
	}
]
```

Instead of linking to two separate metadata objects, we've embedded those into the `j:CrashPeson`. We could also have the `ext:PrivacyMetadata` object as a standalone object with an `@id` that we can link with other objects:

```json
"ext:PrivacyMetadata": [
	{
		"@id": "#PM01",
		"ext:PrivacyCode": ["PII"]
	}
]
```

### Artifacts

- [Creating New Objects - Simple Data](/Text_Document/10_Creating_New_Objects_Simple_Data.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/10_Creating_New_Objects_Simple_Data.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/10_Creating_New_Objects_Simple_Data.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/10_Creating_New_Objects_Simple_Data.pdf)

___
