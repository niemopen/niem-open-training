### Creating Complex Objects

![Complex Objects](/Req_Analysis_Graphics/11_Complex_Objects_CrashDriverClassDiagram.png)

- If you’re making a special kind of existing NIEM type:
	- Use that type as a base to extend from and add things to it, or
	- Create an Augmentation to hold your new things
- If you’re starting from scratch:
	- Use `structures:ObjectType` as a base to extend from and add things to it

Here we're making the root element that will hold everything else. We create `CrashDriverInfoType`, basing it on `structures:ObjectType` so that it's just an empty object.

To that empty object, we add all the major objects in our exchange, `nc:Person`, `j:Crash`, and `j:Charge`. We also add a `j:PersonChargeAssociation` which lets us link together people and charges. Finally, we add a couple metadata object, the built-in `j:Metadata`, and `ext:PrivacyMetadata`, which we create in the extension schema and is in the prior example.

```json
"ext:CrashDriverInfo": {
	"description": "A collection of information about the driver of a vehicle in a crash.",
	"anyOf": [
		{"$ref": "#/definitions/ext:CrashDriverInfoType"},
		{
			"type": "array",
			"items": {"$ref": "#/definitions/ext:CrashDriverInfoType"}
		}
	]
}
```
```json
"ext:CrashDriverInfoType": {
	"description": "A data type for a collection of information about the driver of a vehicle in a crash.",
	"type": "object",
	"properties": {
		"nc:Person": {"$ref": "#/properties/nc:Person"},
		"j:Crash": {"$ref": "#/properties/j:Crash"},
		"j:PersonChargeAssociation": {"$ref": "#/properties/j:PersonChargeAssociation"},
		"j:Charge": {"$ref": "#/properties/j:Charge"},
		"j:MetadataAugmentation": {"$ref": "#/properties/j:MetadataAugmentation"},
		"ext:PrivacyMetadata": {"$ref": "#/properties/ext:PrivacyMetadata"}
	},
	"required": [
		"nc:Person",
		"j:Crash"
	]
}
```

Another example is when we created `ext:LicenseAugmentation` and `ext:LicenseAugmentationType` when talking about augmentations.

### Adding New Content to the Exchange

To summarize, there are two major ways to add new content to an exchange. We've seen them both above.

If you're _already_ creating a new complex object and type, like `CrashDriverInfo` and `CrashDriverInfoType` above, you can simply add new elements to the new type, as we did with `ext:PrivacyMetadata`. 

But if you're not already creating the new type for other reasons, XML would use augmentations via substitution groups. However, JSON doesn't support substitution groups. That leaves us with two options:

1. Just add the new object to an existing NIEM type.
2. Make a new type extending an existing type, adding the new object to this new type. This is called "concrete extension."

In an XML context, NIEM schemas and user extension schemas are separate documents. You don't change the NIEM schemas directly to add new objects. That's where substitution groups are handy for extensions. But in a JSON context, it's all one big schema document. Changing NIEM types directly to add new elements makes the resulting JSON instance better match the equivalent XML instance.

The other option is concrete extensions. This is also done in an XML context, but not often as using augmentations via substitution groups is much cleaner. Concrete extensions are an option, but they come with a big drawback.

### Problems with Concrete Extensions

The issue with concrete extensions is that if the extension is happening deep inside an object, all the surrounding objects will also need to be extended. For example, if instead of adding `ext:LicenseAugmentation` directly to `j:DriverLicenseType` we extended `j:DriverLicenseType`, making a new `ext:DriverLicenseType` to hold our new object. Now we need a new element for it, `ext:DriverLicense`.

But `j:CrashDriver` doesn't hold an `ext:DriverLicense`, so we need to make a new `ext:CrashDriverType` and `ext:CrashDriver` that can hold an `ext:DriverLicense`.

But `j:CrashVehicle` doesn't hold a `ext:CrashDriver`, so we need to make a new `ext:CrashVehicleType` and `ext:CrashVehicle` that can hold an `ext:CrashDriver`.

But `j:Crash` doesn't hold an `ext:CrashVehicle`, so we need to make a new `ext:CrashType` and `ext:Crash` that can hold `ext:CrashVehicle`.

That's a lot of extra work and muddies the semantics of the elements.

### Artifacts

- [Creating New Objects - Complex Objects](/Text_Document/11_Creating_New_Objects_Complex_Objects.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/11_Creating_New_Objects_Complex_Objects.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/11_Creating_New_Objects_Complex_Objects.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/11_Creating_New_Objects_Complex_Objects.pdf)

___
