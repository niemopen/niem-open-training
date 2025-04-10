## Substitution Groups

![Substitution Groups](/Req_Analysis_Graphics/02_Substitution_Groups_CrashDriverClassDiagram.png)

- Some concepts can be represented multiple ways
- Text / code combinations are common
- Date can be a date, datetime, or a range
- NIEM uses substitution groups to support both:
	- The single concept, and
	- Multiple representations of that concept
- Examples:
	- `nc:PersonBirthDate` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-11r)/[Wayfarer](http://niem5.org/wayfarer/nc/PersonBirthDate.html)) contains a `nc:DateRepresentation` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-92a)/[Wayfarer](http://niem5.org/wayfarer/nc/DateRepresentation.html))
	- Substitution group heads follow the form of: `SomethingRepresentation` or `WhateverAbstract`

### Schemas

Here we see [`nc:PersonBirthDate`](https://niemopen.github.io/niem-open-training/nc.html#PersonBirthDate) and its type, `nc:DateType`:

```xml
<xs:element name="PersonBirthDate" type="nc:DateType" nillable="true">
	<xs:annotation>
		<xs:documentation>A date a person was born.</xs:documentation>
	</xs:annotation>
</xs:element>
```

[`nc:DateType`](https://niemopen.github.io/niem-open-training/nc.html#DateType) contains `nc:DateRepresentation`, along with other date properties:

```xml
<xs:complexType name="DateType">
	<xs:annotation>
		<xs:documentation>A data type for a calendar date.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:DateRepresentation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:DateAccuracyAbstract" minOccurs="0" maxOccurs="1"/>
				<xs:element ref="nc:DateMarginOfErrorDuration" minOccurs="0" maxOccurs="1"/>
				<xs:element ref="nc:DateAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
[`nc:DateRepresentation`](https://niemopen.github.io/niem-open-training/nc.html#DateRepresentation) is _abstract_, meaning it has no type and must be substituted with another object:

```xml
<xs:element name="DateRepresentation" abstract="true">
	<xs:annotation>
		<xs:documentation>A data concept for a representation of a date.</xs:documentation>
	</xs:annotation>
</xs:element>
```
Those other objects are identified by having a `substitutionGroup` attribute set to the name of the substitution group head. The most common one you'll see for `nc:DateRepresentation` is [`nc:Date`](https://niemopen.github.io/niem-open-training/nc.html#Date):

```xml
<xs:element name="Date" type="niem-xs:date" substitutionGroup="nc:DateRepresentation" nillable="true">
	<xs:annotation>
		<xs:documentation>A full date.</xs:documentation>
	</xs:annotation>
</xs:element>
```

### Instance Documents

In the resulting instance document, you don't see `nc:DateRepresentation` at all. You just see `nc:Date`, which is taking its place:

```xml
<nc:Person>
	<nc:PersonBirthDate>
		<nc:Date>1890-05-04</nc:Date>
	</nc:PersonBirthDate>
	<nc:PersonName>
		<nc:PersonGivenName>Peter</nc:PersonGivenName>
		<nc:PersonMiddleName>Death</nc:PersonMiddleName>
		<nc:PersonMiddleName>Bredon</nc:PersonMiddleName>
		<nc:PersonSurName>Wimsey</nc:PersonSurName>
	</nc:PersonName>
</nc:Person>
```
### Artifacts

- [Substitition Groups](/Text_Document/02_Substitution_Groups.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/02_Substitution_Groups.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/02_Substitution_Groups.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/02_Substitution_Groups.pdf)

___
