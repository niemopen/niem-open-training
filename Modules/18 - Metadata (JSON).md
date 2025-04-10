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

```xml
<xs:element name="MetadataAugmentation" type="j:MetadataAugmentationType" substitutionGroup="nc:MetadataAugmentationPoint" nillable="true">
	<xs:annotation>
		<xs:documentation>Additional information about metadata.</xs:documentation>
	</xs:annotation>
</xs:element>
```

There's nothing special about [`j:MetadataAugmentationType`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentationType). It's just an object holding some other objects, in this case a couple booleans indicators, `j:CriminalInformationIndicator` and `j:IntelligenceInformationIndicator`. It's based on [`structures:AugmentationType`](https://niemopen.github.io/niem-open-training/structures.html#AugmentationType), which is just an empty container. Substituting it for `nc:MetadataAugmentationPoint` provides the linking infrastructure we've seen with associations and roles as part of the `nc:Metadata` parent object:

```xml
<xs:complexType name="MetadataAugmentationType">
	<xs:annotation>
		<xs:documentation>A data type for additional information about metadata.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:AugmentationType">
			<xs:sequence>
				<xs:element ref="j:CriminalInformationIndicator" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:IntelligenceInformationIndicator" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

There are multiple methods for creating metadata objects:

1. NIEM-supplied metadata objects can added to a subset and included in your exchange

```xml
<xs:complexType name="MetadataType">
	<xs:annotation>
		<xs:documentation>A data type for information that further qualifies primary data; data about data.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:AdministrativeID" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:CaveatText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:Comment" minOccurs="0" maxOccurs="unbounded"/>
				<!-- additional elements remvoed for clarity -->
				<xs:element ref="nc:MetadataAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>

<xs:element name="Metadata" type="nc:MetadataType" nillable="true">
	<xs:annotation>
		<xs:documentation>Information that further qualifies primary data; data about data.</xs:documentation>
	</xs:annotation>
</xs:element>

```
2. New metadata objects can be created in an extension as an augmentation or as a standalone object

```xml
<xs:element name="PrivacyMetadataAugmentation"
			type="ext:PrivacyMetadataAugmentationType"
			substitutionGroup="nc:MetadataAugmentationPoint">
	<xs:annotation>
		<xs:documentation>Additional information about Privacy.</xs:documentation>
	</xs:annotation>
</xs:element>
<xs:complexType name="PrivacyMetadataAugmentationType">
	<xs:annotation>
		<xs:documentation>A data type for Additional information about Privacy.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:AugmentationType">
			<xs:sequence>
				<xs:element ref="ext:PrivacyCode" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>

<xs:element name="InjuryPrivacyMetadataAugmentation"
			type="ext:InjuryPrivacyMetadataAugmentationType"
			substitutionGroup="nc:InjuryAugmentationPoint">
	<xs:annotation>
		<xs:documentation>Additional information about Privacy.</xs:documentation>
	</xs:annotation>
</xs:element>
<xs:complexType name="InjuryPrivacyMetadataAugmentationType">
	<xs:annotation>
		<xs:documentation>A data type for Additional information about Privacy.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:AugmentationType">
			<xs:sequence>
				<xs:element ref="ext:PrivacyCode" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>

```

```xml
<xs:element name="Injury" type="ext:InjuryType">
	<xs:annotation>
		<xs:documentation>A form of harm or damage sustained by a person.</xs:documentation>
	</xs:annotation>
</xs:element>
<xs:complexType name="InjuryType">
	<xs:annotation>
		<xs:documentation>A data type for a form of harm or damage sustained by a person.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:InjuryType">
			<xs:sequence>
				<xs:element ref="ext:PrivacyCode" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
### Instance Documents

There are also multiple methods to relate that metadata to objects in instance documents: 

1. Using a `nc:metadataRef` attribute, which allows simple data objects to point to a standalone metadata object

```xml
<nc:Person>
	<nc:PersonBirthDate>
		<nc:Date nc:metadataRef="PMD01">1890-05-04</nc:Date>
	</nc:PersonBirthDate>
</nc:Person>

<nc:Metadata structures:id="PMD01">
	<ext:PrivacyMetadataAugmentation>
		<ext:PrivacyCode>PII</ext:PrivacyCode>
	</ext:PrivacyMetadataAugmentation>
</nc:Metadata>
```

```xml
<j:Charge nc:metadataRef="JMD01">
	<j:ChargeDescriptionText>Furious Driving</j:ChargeDescriptionText>
	<j:ChargeFelonyIndicator>false</j:ChargeFelonyIndicator>
</j:Charge>

<nc:Metadata structures:id="JMD01">
	<j:MetadataAugmentation>
		<j:CriminalInformationIndicator>true</j:CriminalInformationIndicator>
	</j:MetadataAugmentation>
</nc:Metadata>
```
1. Extend an object to include a metadata object
2. Add a metadata augmentation to an object (metadata or otherwise) via the object's AugmentationPoint

```xml
<j:CrashPerson>
	<j:CrashPersonInjury>
		<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
		<j:InjurySeverityCode>3</j:InjurySeverityCode>
		<!-- replacing nc:InjuryAugmentationPoint -->
		<ext:InjuryPrivacyMetadataAugmentation>
			<ext:PrivacyCode>PII</ext:PrivacyCode>
		</ext:InjuryPrivacyMetadataAugmentation>
	</j:CrashPersonInjury>
	<ext:PersonDefenestrationIndicator>false</ext:PersonDefenestrationIndicator>
</j:CrashPerson>
```
JSON-LD doesn't support a specific metadata link, so for JSON we just use `@id` and rely on the term "Metadata".

```json
"j:Metadata" : {
	"@id": "#CH01",
	"j:CriminalInformationIndicator": true
},

"j:Charge": {
	"@id": "#CH01",
	"j:ChargeDescriptionText": "Furious Driving",
	"j:ChargeFelonyIndicator": false
}

```

### Artifacts

- [Metadata](/Text_Document/07_Metadata.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/07_Metadata.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/07_Metadata.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/07_Metadata.pdf)

___
