## Code Tables

![Code Tables](/Req_Analysis_Graphics/06_Code_Tables_CrashDriverClassDiagram.png)

- Codes help ensure accurate information
- Codes are, essentially, strings, simple data
- A few in NIEM are integers
- Elements defined in the domains
- Types are often defined in their own namespaces
- NIEM wraps them in a complex type in order to apply some attributes needed for infrastructure
	- Which we will need in the next section…
- Examples:
	- `j:InjurySeverityCode` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-45s)/[Wayfarer](http://niem5.org/wayfarer/j/InjurySeverityCode.html))
		- In the SSGT, the actual codes are viewable on the page for the base simple type, e.g. [`aamva_d20:AccidentSeverityCodeSimpleType`](https://tools.niem.gov/niemtools/ssgt/SSGT-GetType.iepd?typeKey=o4-c)
		- In Wayfarer, there should be a link on the element page bringing up the codes in a separate window, e.g. [`aamva_d20:AccidentSeverityCodeSimpleType`](http://niem5.org/wayfarer/aamva_d20/AccidentSeverityCodeSimpleType_codes.html)
	- Anything ending in "Code" ([SSGT](http://niem5.org/ssgt_redirect.php?query=code)/[Wayfarer](http://niem5.org/wayfarer/search.php?option=names&query=code))
- Codes nearly always have a text alternative

### Schemas

[`j:InjurySeverityCode`](https://niemopen.github.io/niem-open-training/j.html#InjurySeverityCode) is a code table, with its codes defined in another namespace, the one for [AAMVA](https://www.aamva.org/). Here's the schema for the element:

```xml
<xs:element name="InjurySeverityCode" type="aamva_d20:AccidentSeverityCodeType" substitutionGroup="nc:InjurySeverityAbstract" nillable="true">
	<xs:annotation>
		<xs:documentation>A severity of an injury received by a person, such as in a traffic accident or crash.</xs:documentation>
	</xs:annotation>
</xs:element>
```

The actual codes are defined in a pair of types. The first, [`aamva_d20:AccidentSeverityCodeSimpleType`](https://niemopen.github.io/niem-open-training/aamva_d20.html#AccidentSeverityCodeSimpleType), defines the actual codes and their definitions, one per `enumeration` below:

```xml
<xs:simpleType name="AccidentSeverityCodeSimpleType">
	<xs:annotation>
		<xs:documentation>A data type for severity levels of an accident.</xs:documentation>
	</xs:annotation>
	<xs:restriction base="xs:token">
		<xs:enumeration value="1">
			<xs:annotation>
				<xs:documentation>Fatal Accident</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="2">
			<xs:annotation>
				<xs:documentation>Incapacitating Injury Accident</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="3">
			<xs:annotation>
				<xs:documentation>Non-incapacitating Evident Injury</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="4">
			<xs:annotation>
				<xs:documentation>Possible Injury Accident</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="5">
			<xs:annotation>
				<xs:documentation>Non-injury Accident</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
		<xs:enumeration value="9">
			<xs:annotation>
				<xs:documentation>Unknown</xs:documentation>
			</xs:annotation>
		</xs:enumeration>
	</xs:restriction>
</xs:simpleType>
```

This simple type is then wrapped in a complex type, [`aamva_d20:AccidentSeverityCodeType`](https://niemopen.github.io/niem-open-training/aamva_d20.html#AccidentSeverityCodeType), to add infrastructure attributes that we've seen used in associations and roles. The two types are grouped together in the [`aamva_d20`](https://niemopen.github.io/niem-open-training/aamva_d20.html) namespace so they can be governed by AAMVA without needing to change the `j` domain:

```xml
<xs:complexType name="AccidentSeverityCodeType">
	<xs:annotation>
		<xs:documentation>A data type for severity levels of an accident.</xs:documentation>
	</xs:annotation>
	<xs:simpleContent>
		<xs:extension base="aamva_d20:AccidentSeverityCodeSimpleType">
			<xs:attributeGroup ref="structures:SimpleObjectAttributeGroup"/>
		</xs:extension>
	</xs:simpleContent>
</xs:complexType>
```
### Instance Documents

The code is what shows up in the instance document. The longer definition does not. If you want to know that "3" means "Non-incapacitating Evident Injury," you need to refer to the schemas. Schema validation _will_ verify that the value is one of the enumerations. Here's the XML:

```xml
<j:CrashPersonInjury>
	<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>
	<j:InjurySeverityCode>3</j:InjurySeverityCode>
</j:CrashPersonInjury>
```

And here's the JSON. Note that NIEM does not yet support JSON Schema, so there's no means for validating the value of the code short of writing your own JSON Schema:

```json
"j:CrashPersonInjury": {
	"nc:InjuryDescriptionText": "Broken Arm",
	"j:InjurySeverityCode": "3"
}
```

### Artifacts

- [Code Tables](/Text_Document/06_Code_Tables.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/06_Code_Tables.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/06_Code_Tables.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/06_Code_Tables.pdf)

___
