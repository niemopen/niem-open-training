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

Create `PersonDefenestrationIndicator` using the existing NIEM type `niem-xs:boolean`. By giving it `j:CrashPersonAugmentationPoint` as a substitution group head, it can go inside of the `j:CrashPerson`:

```xml
<xs:element name="PersonDefenestrationIndicator" type="niem-xs:boolean"
	substitutionGroup="j:CrashPersonAugmentationPoint">
	<xs:annotation>
		<xs:documentation>True if this person was thrown through a window; false otherwise.</xs:documentation>
	</xs:annotation>
</xs:element>
```
The resulting XML instance is then:

```xml
<j:CrashPerson>
	<nc:RoleOfPerson structures:ref="P01" xsi:nil="true"/>
	<j:CrashPersonInjury structures:metadata="PMD01 PMD02">
		<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
		<j:InjurySeverityCode>3</j:InjurySeverityCode>
	</j:CrashPersonInjury>
	<ext:PersonDefenestrationIndicator>false</ext:PersonDefenestrationIndicator>
</j:CrashPerson>
```
And the equivalent JSON-LD is:

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

The actual codes are defined in the simple type, `ext:PrivacyCodeSimpleType`. Each `enumeration` defines a code. The `documentation` tags provide a longer text description of the code:

```xml
<xs:simpleType name="PrivacyCodeSimpleType">
	<xs:annotation>
		<xs:documentation>A data type for a code representing a kind of
			property.</xs:documentation>
	</xs:annotation>
	<xs:restriction base="xs:token">
		<xs:enumeration value="PII">
			<xs:annotation>
				<xs:documentation>Personally Identifiable Information</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="MEDICAL">
			<xs:annotation>
				<xs:documentation>Medical Information</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
	</xs:restriction>
</xs:simpleType>

```

The complex type `ext:PrivacyCodeType` is then extended from `ext:PrivacyCodeSimpleType`. All this does is add infrastructure attributes to allow things of this type to refer to other elements, or be referred to in turn:

```xml
<xs:complexType name="PrivacyCodeType">
	<xs:annotation>
		<xs:documentation>A data type for a code representing a kind of
			property.</xs:documentation>
	</xs:annotation>
	<xs:simpleContent>
		<xs:extension base="ext:PrivacyCodeSimpleType">
			<xs:attributeGroup ref="structures:SimpleObjectAttributeGroup"/>
		</xs:extension>
	</xs:simpleContent>
</xs:complexType>
```
Then `ext:PrivacyCode` is created to be of `ext:PrivacyCodeType`:

```xml
<xs:element name="PrivacyCode" type="ext:PrivacyCodeType">
	<xs:annotation>
		<xs:documentation>A code representing a kind of property.</xs:documentation>
	</xs:annotation>
</xs:element>
```

In this exchange, this code is metadata to be applied to other objects, so we can create `ext:PrivacyMetadata` to hold it:

```xml
<xs:element name="PrivacyMetadata" type="ext:PrivacyMetadataType">
	<xs:annotation>
		<xs:documentation>Metadata about Privacy.</xs:documentation>
	</xs:annotation>
</xs:element>
<xs:complexType name="PrivacyMetadataType">
	<xs:annotation>
		<xs:documentation>A data type for metadata about Privacy.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:MetadataType">
			<xs:sequence>
				<xs:element ref="ext:PrivacyCode" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

### Instance Documents

The resulting XML instance document is:

```xml
<ext:PrivacyMetadata structures:id="PMD01">  
	<ext:PrivacyCode>PII</ext:PrivacyCode>  
</ext:PrivacyMetadata>  

<ext:PrivacyMetadata structures:id="PMD02">  
	<ext:PrivacyCode>MEDICAL</ext:PrivacyCode>  
</ext:PrivacyMetadata>

<j:CrashPerson>
	<nc:RoleOfPerson structures:ref="P01" xsi:nil="true"/>
	<j:CrashPersonInjury structures:metadata="PMD01 PMD02">
		<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
		<j:InjurySeverityCode>3</j:InjurySeverityCode>
	</j:CrashPersonInjury>
	<ext:PersonDefenestrationIndicator>false</ext:PersonDefenestrationIndicator>
</j:CrashPerson>

```

An equivalent JSON document would be:

```json
"j:CrashPerson": {
	"nc:RoleOfPerson": {
	  "@id": "#P01"
	},
	"j:CrashPersonInjury": {
	  "nc:InjuryDescriptionText": "Broken Arm",
	  "j:InjurySeverityCode": "3",
	  "ext:PrivacyCode": [
		"PII", "MEDICAL"
	  ]
	},
	"ext:PersonDefenestrationIndicator": "false"
}
```

Instead of linking to two separate metadata objects, we've embedded those into the `j:CrashPeson`.

### Artifacts

- [Creating New Objects - Simple Data](/Text_Document/10_Creating_New_Objects_Simple_Data.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/10_Creating_New_Objects_Simple_Data.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/10_Creating_New_Objects_Simple_Data.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/10_Creating_New_Objects_Simple_Data.pdf)

___
