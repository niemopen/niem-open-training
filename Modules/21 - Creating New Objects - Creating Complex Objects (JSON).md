### Creating Complex Objects

![Complex Objects](/Req_Analysis_Graphics/11_Complex_Objects_CrashDriverClassDiagram.png)

- If you’re making a special kind of existing NIEM type:
	- Use that type as a base to extend from and add things to it, or
	- Create an Augmentation to hold your new things
- If you’re starting from scratch:
	- Use `structures:ObjectType` as a base to extend from and add things to it

Here we're making the root element that will hold everything else. We create `CrashDriverInfoType`, basing it on `structures:ObjectType` so that it's just an empty object.

To that empty object, we add all the major objects in our exchange, `nc:Person`, `j:Crash`, and `j:Charge`. We also add a `j:PersonChargeAssociation` which lets us link together people and charges. Finally, we add a couple metadata object, the built-in `j:Metadata`, and `ext:PrivacyMetadata`, which we create in the extension schema and is in the prior example.

```xml
<xs:element name="CrashDriverInfo" type="exch:CrashDriverInfoType">
	<xs:annotation>
		<xs:documentation>A collection of information about the driver of a vehicle in a crash.</xs:documentation>
	</xs:annotation>
</xs:element>

<xs:complexType name="CrashDriverInfoType">
	<xs:annotation>
		<xs:documentation>A data type for a collection of information about the driver of a vehicle in a crash.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:Person"/>
				<xs:element ref="j:Crash"/>
				<xs:element ref="j:PersonChargeAssociation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:Charge" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:Metadata" minOccurs="0"/>
				<xs:element ref="ext:PrivacyMetadata" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

Another example is when we created `ext:LicenseAugmentation` and `ext:LicenseAugmentationType` when talking about augmentations.

### Adding New Content to the Exchange

To summarize, there are two major ways to add new content to an exchange. We've seen them both above.

If you're _already_ creating a new complex object and type, like `CrashDriverInfo` and `CrashDriverInfoType` above, you can simply add new elements to the new type, as we did with `ext:PrivacyMetadata`. This is called "concrete extension."

But if you're not already creating the new type for other reasons, you should use augmentations. We used added `j:CrashPersonAugmentationPoint` to our exchange and used it as a hook on which we hung `ext:PersonDefenestrationIndicator`.

### Problems with Concrete Extensions

The issue with concrete extensions is that if the extension is happening deep inside an object, all the surrounding objects will also need to be extended. For example, if instead of using `j:DriverLicenseAugmentationPoint`, suppose we extended `j:DriverLicenseType`, making a new `ext:DriverLicenseType` to hold our new object. Now we need a new element for it, `ext:DriverLicense`.

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
