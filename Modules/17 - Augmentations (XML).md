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

Does driver's license have what we need? Does it have an email address?

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

(Why not [`j:CrashDriverLicense`](http://niem5.org/wayfarer/j/CrashDriverLicense.html)? It doesn't go inside a `j:CrashDriver`. Why? The domain submitted it like this.)

### Schemas

`j:DriverLicense` is defined to be of `j:DriverLicenseType`:

```xml
<xs:element name="DriverLicense" type="j:DriverLicenseType" nillable="true">
	<xs:annotation>
		<xs:documentation>A license issued to a person granting driving privileges.</xs:documentation>
	</xs:annotation>
</xs:element>
```

`j:DriverLicenseType` contains `j:DriverLicenseAugmentationPoint` as a hook for a augmentation bags:

```xml
<xs:complexType name="DriverLicenseType">
	<xs:annotation>
		<xs:documentation>A data type for a license issued to a person granting driving privileges.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:LicenseType">
			<xs:sequence>
				<xs:element ref="j:DriverLicenseEnhancedIndicator" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseCommercialClassAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseCommercialStatusAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseNonCommercialClassText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseNonCommercialStatusAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseWithdrawal" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseWithdrawalPendingIndicator" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseCardIdentification" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DriverLicenseAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
(`j:DriverLicenseType` also inherits from `nc:LicenseType`, but nothing we use in our example.)

While NIEM does have some augmentations pre-defined, they're particularly useful for adding new objects, or just putting existing NIEM objects somewhere else. Here we do the latter, creating a bag called `LicenseAugmentation` with `nc:ContactInformation` inside. 

`ext:` is the nickname we're going to use for our own extension namespace, where we'll create our own objects. This is a separate file _we_ create. In it we build new objects, based on existing NIEM objects. We'll learn more about how these files fit together when we get to creating schemas.

We can now "hang" it on the `j:DriverLicenseAugmentationPoint` hook with nothing more than a `substitutionGroup` attribute:

```xml
<xs:complexType name="LicenseAugmentationType">
	<xs:annotation>
		<xs:documentation>
			A data type for additional information about a license.
		</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:AugmentationType">
			<xs:sequence>
				<xs:element ref="nc:ContactInformation"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>

<xs:element name="LicenseAugmentation" type="ext:LicenseAugmentationType" substitutionGroup="j:DriverLicenseAugmentationPoint">
	<xs:annotation>
		<xs:documentation>
			Additional information about a license.
		</xs:documentation>
	</xs:annotation>
</xs:element>
```

Our new `ext:LicenseAugmentationType` is based on the built-in [`structures:AugmentationType`](https://niemopen.github.io/niem-open-training/structures.html#AugmentationType). That base type merely adds in infrastructure support for linking objects together:

```xml
<xs:complexType name="AugmentationType" abstract="true">
	<xs:annotation>
		<xs:documentation>A data type for a set of properties to be applied to a base type.</xs:documentation>
	</xs:annotation>
	<xs:attribute ref="structures:id"/>
	<xs:attribute ref="structures:ref"/>
	<xs:attribute ref="structures:uri"/>
	<xs:anyAttribute namespace="urn:us:gov:ic:ism urn:us:gov:ic:ntk" processContents="lax"/>
</xs:complexType>
```

The resulting XML Instance Document looks like:

```xml
<j:DriverLicense>
	<j:DriverLicenseCardIdentification>
		<nc:IdentificationID>A1234567</nc:IdentificationID>
	</j:DriverLicenseCardIdentification>
	<ext:LicenseAugmentation>
		<nc:ContactInformation>
			<nc:ContactEmailID>peter@wimsey.org</nc:ContactEmailID>
		</nc:ContactInformation>
	</ext:LicenseAugmentation>
</j:DriverLicense>
```

### Artifacts

- [Augmentations](/Text_Document/08_Combining_Domains_Augmentations.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/08_Combining_Domains_Augmentations.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/08_Combining_Domains_Augmentations.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/08_Combining_Domains_Augmentations.pdf)

___
