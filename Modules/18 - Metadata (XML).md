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

- Objects can reference the metadata objects that apply to them
	- Can include them via Augmentations as well
- An object can reference more than one metadata object
- More than one object can reference the same metadata object
- Examples of NIEM Metadata: [`nc:Metadata`](https://niemopen.github.io/niem-open-training/nc.html#Metadata) and [`j:MetadataAugmentation`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentation)

### Schemas

The [`j:MetadataAugmentation`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentation) object is of `j:MetadataAugmentationType`. 

```xml
<xs:element name="MetadataAugmentation" type="j:MetadataAugmentationType"
	substitutionGroup="nc:MetadataAugmentationPoint" nillable="true">
	<xs:annotation>
		<xs:documentation>Additional information about metadata.</xs:documentation>
	</xs:annotation>
</xs:element>
```

There's nothing special about [`j:MetadataAugmentationType`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentationType). It's just an object holding some other objects, in this case a couple booleans, `j:CriminalInformationIndicator` and `j:IntelligenceInformationIndicator`. It's based on [`structures:AugmentationType`](https://niemopen.github.io/niem-open-training/structures.html#AugmentationType), which is just an empty container. Substituting it for `nc:MetadataAugmentationPoint` provides the linking infrastructure we've seen with associations and roles as part of the [`nc:Metadata`](https://niemopen.github.io/niem-open-training/nc.html#Metadata) parent object:

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

#### NIEM-supplied metadata objects can added to a subset and included in your exchange

Here's NIEM's [`nc:Metadata`](https://niemopen.github.io/niem-open-training/nc.html#Metadata) and [`nc:MetadataType`](https://niemopen.github.io/niem-open-training/nc.html#MetadataType):

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
Using a `nc:metadataRef` attribute allows objects to point to standalone metadata objects:

- Conceptually, an object is saying that this is the metadata that applies to itself, this is _my_ metadata
- Can contain multiple IDs, separated with spaces, based on `IDREFS`
- The matching `id`s must exist in the instance document'

This attribute is built into [nc:TextType](https://niemopen.github.io/niem-open-training/nc.html#TextType):

```xml
<j:CrashPersonInjury>
	<nc:InjuryDescriptionText nc:metadataRef="PMD01">Broken Arm</nc:InjuryDescriptionText>
</j:CrashPersonInjury>

<nc:Metadata structures:id="PMD01">
	<ext:PrivacyMetadataAugmentation>
		<ext:PrivacyCode>PII</ext:PrivacyCode>
	</ext:PrivacyMetadataAugmentation>
</nc:Metadata>
```

You could also extend other objects, both simple and complex, to include `nc:metadataRef`:
```xml
<ext:Charge nc:metadataRef="JMD01">
	<j:ChargeDescriptionText>Furious Driving</j:ChargeDescriptionText>
	<j:ChargeFelonyIndicator>false</j:ChargeFelonyIndicator>
</ext:Charge>

<nc:Metadata structures:id="JMD01">
	<j:MetadataAugmentation>
		<j:CriminalInformationIndicator>true</j:CriminalInformationIndicator>
	</j:MetadataAugmentation>
</nc:Metadata>
```

#### New metadata objects can be created in an extension as an augmentation

```xml
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
The Augmentation then gets swapped in, replacing `nc:InjuryAugmentationPoint`:

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

#### New metadata objects can be created in an extension added as a standalone object

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
This new object can then be used like any other object:

```xml
<ext:Injury>
	<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
	<j:InjurySeverityCode>3</j:InjurySeverityCode>
	<ext:PrivacyCode>PII</ext:PrivacyCode>
</ext:Injury>
```
So in our example, we're mapping `IsCriminalInformation`. Searching for "criminal information" brings up [`j:CriminalInformationIndicator`](https://niemopen.github.io/niem-open-training/j.html#CriminalInformationIndicator), which is inside of  [`j:MetadataAugmentation`](https://niemopen.github.io/niem-open-training/j.html#MetadataAugmentation), which can be substituted for [`nc:MetadataAugmentationPoint`](https://niemopen.github.io/niem-open-training/nc.html#MetadataAugmentationPoint), which is inside of [`nc:Metadata`](https://niemopen.github.io/niem-open-training/nc.html#Metadata)

### Artifacts

- [Metadata](/Text_Document/07_Metadata.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/08_Metadata.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/08_Metadata.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/08_Metadata.pdf)

___

