## Metadata
![Metadata](/Req_Analysis_Graphics/07_Metadata_CrashDriverClassDiagram.png)

![Jett](/Mapping_Graphics/Jett_scaled.png)

Metadata is Data about Data. What does that mean? Here's an example:

### Data About Jett

- _Name:_ **Jett**
- _Sex:_ **Female**
- _Weight:_ **8 pounds**

### Data About Data About Jett, e.g. Her Weight

- _Reporting Organization:_ **Ark Pet Hospital**
- _Reported Date:_ **2021-06-10**
- _Last Verified Date:_ **2025-02-21**

### Object Reference Metadata

- Objects reference the metadata objects that apply to them
- An object can reference more than one metadata object
- More than one object can reference the same metadata object
- Example: `j:Metadata` (containing `j:CriminalInformationIndicator`) ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-4qr)/[Wayfarer](http://niem5.org/wayfarer/j/Metadata.html))

### Connecting Metadata to Objects

| Connections | Diagram |
| --- | --- |
| Easy to apply multiple metadata objects to one object | ![One to Many](/Mapping_Graphics/Metadata_One_to_Many.png) |
| Easy to apply same metadata to many objects | ![Many to One](/Mapping_Graphics/Metadata_Many_to_One.png) |
| Many-to-many relationships can get messy | ![Many to Many](/Mapping_Graphics/Metadata_Many_to_Many.png) |


### Schemas

The [`j:MetadataAugmentation`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentation) object is of `j:MetadataAugmentationType`. 

```json
"j:MetadataAugmentation": {
	"description": "Information that further qualifies the kind of data represented.",
	"$ref": "#/definitions/j:Metadata## AugmentationType"
}
```

There's nothing special about [`j:MetadataAugmentationType`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentationType). It's just defines an object holding some other objects, in this case a couple booleans indicators, `j:CriminalInformationIndicator` and `j:IntelligenceInformationIndicator`:

```json
"j:MetadataAugmentationType": {
	"description": "A data type for information that further qualifies the kind of data represented.",
	"type": "object",
	"properties": {
		"j:CriminalInformationIndicator": {"$ref": "#/properties/j:CriminalInformationIndicator"},
		"j:IntelligenceInformationIndicator": {"$ref": "#/properties/j:IntelligenceInformationIndicator"}
	}
}
```

There are multiple methods for creating metadata objects:

1. NIEM-supplied metadata objects can added to a subset and included in your exchange

```json
"j:MetadataAugmentation": {
	"description": "Information that further qualifies the kind of data represented.",
	"$ref": "#/definitions/j:MetadataAugmentationType"
}
```
```json
"j:MetadataAugmentationType": {
	"description": "A data type for information that further qualifies the kind of data represented.",
	"type": "object",
	"properties": {
		"j:CriminalInformationIndicator": {"$ref": "#/properties/j:CriminalInformationIndicator"},
		"j:IntelligenceInformationIndicator": {"$ref": "#/properties/j:IntelligenceInformationIndicator"}
	}
}
```

2. New metadata objects can be created in an extension as an augmentation or as a standalone object

```json
"ext:PrivacyMetadataType": {
	"description": "A data type for Additional information about Privacy.",
	"type": "object",
	"properties": {
		"ext:PrivacyCode": {"$ref": "#/properties/ext:PrivacyCode"}
	}
}
```

```json
"ext:PrivacyMetadata": {
	"description": "Metadata about Privacy.",
	"type": "array",
	"items": {"$ref": "#/definitions/ext:PrivacyMetadataType"}
}
```

```json
"ext:PrivacyCode": {
	"description": "A code representing a kind of property.",
	"type": "array",
	"items": {"$ref": "#/definitions/ext:PrivacyCodeType"},
	"maxItems": 2
}
```

### Instance Documents

There are also multiple methods to relate that metadata to objects in instance documents: 

1. Extend an object to include a metadata object

```json
"nc:InjuryType": {
	"description": "A data type for a form of harm or damage sustained by a person.",
	"type": "object",
	"properties": {
		"nc:InjuryDescriptionText": {"$ref": "#/properties/nc:InjuryDescriptionText"},
		"j:InjurySeverityCode": {"$ref": "#/properties/j:InjurySeverityCode"},
		"nc:InjurySeverityText": {"$ref": "#/properties/nc:InjurySeverityText"},
		"ext:PrivacyMetadata": {"$ref": "#/properties/ext:PrivacyMetadata"}
	},
}
```
Giving us an instance like this:

```json
"j:CrashPersonInjury": [
	{
		"nc:InjuryDescriptionText": "Broken Arm",
		"j:InjurySeverityCode": "3",
		"ext:PrivacyMetadata": [{
			"ext:PrivacyCode": [
				"PII",
				"MEDICAL"
			]
		}]
	}
]
```
2. Link metadata objects and the data objects to which they apply

```json
"j:Charge": {
	"@id": "#CH01",
	"j:ChargeDescriptionText": "Furious Driving",
	"j:ChargeFelonyIndicator": false
},
"j:Metadata": {
	"@id": "#CH01",
	"j:CriminalInformationIndicator": true,
	"j:IntelligenceInformationIndicator": false
}
```

### Artifacts

- [Metadata](/Text_Document/07_Metadata.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/07_Metadata.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/07_Metadata.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/07_Metadata.pdf)

___
