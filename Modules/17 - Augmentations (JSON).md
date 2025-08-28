## Combining Domains (Augmentations)

![Augmentations](/Req_Analysis_Graphics/09_Augmentations_CrashDriverClassDiagram.png)

- Sometimes you just want to add properties from other domains to an object without making a special kind of thing
- Augmentations are bags of stuff
- Augmentation Points are hooks onto which to hang the bags of stuff
- Examples:
	- `nc:Incident` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-rr))
	- `j:IncidentAugmentation` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-9l7))
- **Augmentations are an easy way to extend objects to meet your exchange needs**
	- We'll add an email address to a driver license using an augmentation we'll build
	- `j:DriverLicense` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-lb))
	- `j:DriverLicenseAugmentationPoint` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-11rg))

In XML, we would use substitution groups to add the augmentation to the exchange. _However_, JSON and JSON Schema lack this concept of substitution groups. (As do most other serializations.) So in JSON Schema, we will need to extend an existing type to hold the new information. This is one reason why NIEM transformations from XML to JSON are possible, but transformations the other direction are not. Transformations to JSON are _lossy_.

Our first step is to determine whether driver's license has what we need. Does it have an email address?

- Try searching for "drivers license":
	- [SSGT](http://niem5.org/ssgt_redirect.php?query=drivers+license)
	- [Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=drivers+license)
- Try searching for "driver license", singular:
	- [SSGT](http://niem5.org/ssgt_redirect.php?query=driver+license)
	- [Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=driver+license)
	- It's _usually_ a good idea to drop pluralization in search terms
- Check to see if it has an email address. (Spoiler, it doesn't.)
- But we should learn its structure while we're here:
	- Check what can contain it, specifically [`j:CrashDriver`](http://niem5.org/wayfarer/j/CrashDriver.html)
	- Follow up to [`j:CrashVehicle`](http://niem5.org/wayfarer/j/CrashVehicle.html)
	- Follow up to [`j:Crash`](http://niem5.org/wayfarer/j/Crash.html)

Follow a similar process for [`nc:ContactEmailID`](http://niem5.org/wayfarer/nc/ContactEmailID.html) and [`nc:ContactInformation`](http://niem5.org/wayfarer/nc/ContactInformation.html). Learn about the _object_, not just the individual elements.

The SSGT is best for learning overall structure, so check out [`j:Crash`](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-44f) and [`nc:ContactInformation`](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-eh) there, too!

(Why not [`j:CrashDriverLicense`](http://niem5.org/wayfarer/j/CrashDriverLicense.html)? It doesn't go inside a `j:CrashDriver`. Why? The domain submitted it like this. They'll review this for the next release.)

### Schemas

`j:DriverLicense` is defined to be of `j:DriverLicenseType`:

```json
"j:DriverLicense": {
	"description": "A license issued to a person granting driving privileges.",
	"$ref": "#/definitions/j:DriverLicenseType"
}
```

`j:DriverLicenseType` contains `j:DriverLicenseAugmentationPoint` as a hook for a augmentation bags, but this isn't usable in JSON due to the aforementioned XML-specific substitution groups:

```json
"j:DriverLicenseType": {
	"description": "A data type for a license issued to a person granting driving privileges.",
	"allOf": [
		{"$ref": "#/definitions/j:DriverLicenseBaseType"},
		{
			"type": "object",
			"properties": {
				"j:DriverLicenseCardIdentification": {"$ref": "#/properties/j:DriverLicenseCardIdentification"},
			},
			"required": ["j:DriverLicenseCardIdentification"]
		}
	]
}
```

While NIEM does have some augmentations pre-defined, they're particularly useful for adding new objects, or just putting existing NIEM objects somewhere else. Here we do the latter, creating a bag called `LicenseAugmentation` with `nc:ContactInformation` inside. 

`ext:` is the nickname we're going to use for our own extension namespace. This identifies our own objects apart from NIEM-supplied ones.

```json
"ext:LicenseAugmentationType": {
	"description": "A data type for additional information about a license.",
	"type": "object",
	"properties": {
		"nc:ContactInformation": {"$ref": "#/properties/nc:ContactInformation"}
	}
},

"ext:LicenseAugmentation": {
	"description": "Additional information about a license.",
	"$ref": "#/definitions/ext:LicenseAugmentationType"
}
```

Finally, we add it directly to `j:DriverLicenseType`. In XML, this would be done with a substitution, but those aren't available to JSON. XML would also put extensions like this into a separate file and namespace. In JSON, we just use one single schema document.

```json
"j:DriverLicenseType": {
	"description": "A data type for a license issued to a person granting driving privileges.",
	"allOf": [
		{"$ref": "#/definitions/j:DriverLicenseBaseType"},
		{
			"type": "object",
			"properties": {
				"j:DriverLicenseCardIdentification": {"$ref": "#/properties/j:DriverLicenseCardIdentification"},
				"ext:LicenseAugmentation": {"$ref": "#/properties/ext:LicenseAugmentation"}
			},
			"required": ["j:DriverLicenseCardIdentification"]
		}
	]
}
```

The resulting JSON instance looks like this:

```json
"j:DriverLicense": {
	"j:DriverLicenseCardIdentification": {
		"nc:IdentificationID": "A1234567"
	},
	"ext:LicenseAugmentation": {
		"nc:ContactInformation": {
			"nc:ContactEmailID": "peter@wimsey.org"
		}
	}
}
```

### Artifacts

- [Augmentations](/Text_Document/08_Combining_Domains_Augmentations.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/08_Combining_Domains_Augmentations.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/08_Combining_Domains_Augmentations.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/08_Combining_Domains_Augmentations.pdf)

___
