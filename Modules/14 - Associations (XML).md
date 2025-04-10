## Associations

![Associations](/Req_Analysis_Graphics/04_Associations_CrashDriverClassDiagram.png)

- Relationships can be complex
- NIEM provides powerful Association objects
- Trade-off can be implementation complexity
- Associations link objects together
	- Associations reference the associated objects
	- Can link to multiple objects
	- Can thus form many-to-many relationships between them
- Associations also hold information about the association itself
	- `Date` or `DateRange` is a common example
- Associations can also just include the things being associated, if desired
- Examples:
	- `j:PersonChargeAssociation` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-4qf)/[Wayfarer](http://niem5.org/wayfarer/j/PersonChargeAssociation.html))
	- Anything ending in “Association” ([SSGT](http://niem5.org/ssgt_redirect.php?query=association)/[Wayfarer](http://niem5.org/wayfarer/search.php?option=names&query=association))

### Schemas

[`j:PersonChargeAssociation`](https://niemopen.github.io/niem-open-training/j.html#PersonChargeAssociation) is used, as the name suggests, to link together a Person and a Charge. It's of `j:PersonChargeAssociationType`:

```xml
<xs:element name="PersonChargeAssociation" type="j:PersonChargeAssociationType" nillable="true">
	<xs:annotation>
		<xs:documentation>An association between a person and a charge issued to that person.</xs:documentation>
	</xs:annotation>
</xs:element>
```

[`j:PersonChargeAssociationType`](https://niemopen.github.io/niem-open-training/j.html#PersonChargeAssociationType) includes a [`nc:Person`](https://niemopen.github.io/niem-open-training/nc.html#Person) and a [`j:Charge`](https://niemopen.github.io/niem-open-training/j.html#Charge), but also includes information _about_ the association itself, in this case [`j:JuvenileAsAdultIndicator`](https://niemopen.github.io/niem-open-training/j.html#JuvenileAsAdultIndicator). (Which isn't used in _this_ exchange.) `PersonChargeAssociationType` extends `nc:AssociationType`:

```xml
<xs:complexType name="PersonChargeAssociationType">
	<xs:annotation>
		<xs:documentation>A data type for an association between a person and a charge.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:AssociationType">
			<xs:sequence>
				<xs:element ref="nc:Person" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:Charge" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:JuvenileAsAdultIndicator" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:PersonChargeAssociationAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
[`nc:AssociationType`](https://niemopen.github.io/niem-open-training/nc.html#AssociationType) adds in generic association information like a start and end date and a description. Remember that these are inherited by any type based on `nc:AssociationType`, so things of `j:PersonChargeAssociationType` automatically get these common objects.

```xml
<xs:complexType name="AssociationType">
	<xs:annotation>
		<xs:documentation>A data type for an association, connection, relationship,
			or involvement somehow linking people, things, and/or activities together.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:AssociationType">
			<xs:sequence>
				<xs:element ref="nc:AssociationDateRange" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:AssociationDescriptionText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:AssociationAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

### Instance Documents

In the instance document, the association object can specify the objects being associated together by pointing to then with `ref` attributes, or by including the object inside the association object.

First, here's the association using referencing. The applicable `nc:Person` and `j:Charge` objects are external to `j:PersonChargeAssociation`. While shown next to the `j:PersonChargeAssociation` object, they could be _anywhere_ in the instance document.

This method is useful when the same `nc:Person` object is being used in multiple contexts. In the example Message Spec / IEPD, this `nc:Person` is also the `j:CrashDriver` and the `j:CrashPerson`. This method allows us to define the `nc:Person` once and refer to it multiple times.

This beings with it two advantages:

1. This `nc:Person` object is not being replicated; there is no duplication of data
2. We know that the `nc:Person` in the Association _and_ the `j:CrashDriver` _and_ the `j:CrashPerson` are the exact same person, and not three people with the same name

```xml
<j:PersonChargeAssociation>
	<nc:Person structures:ref="P01" xsi:nil="true"/>
	<j:Charge structures:ref="CH01" xsi:nil="true"/>
</j:PersonChargeAssociation>
<nc:Person structures:id="P01">
	<nc:PersonName>
		<nc:PersonGivenName>Peter</nc:PersonGivenName>
	</nc:PersonName>
</nc:Person>
<j:Charge structures:id="CH01">
	<j:ChargeDescriptionText>Furious Driving</j:ChargeDescriptionText>
	<j:ChargeFelonyIndicator>false</j:ChargeFelonyIndicator>
</j:Charge>
```

The disadvantage with using referencing is that it can be more difficult to implement. Implementations need to look for `ref` attributes and find matching `id` attributes.

The alternative to referencing is to just include the `nc:Person` and `j:Charge` information inside the association:

```xml
<j:PersonChargeAssociation>
	<nc:Person>
		<nc:PersonName>
			<nc:PersonGivenName>Peter</nc:PersonGivenName>
		</nc:PersonName>
	</nc:Person>
	<j:Charge>
		<j:ChargeDescriptionText>Furious Driving</j:ChargeDescriptionText>
		<j:ChargeFelonyIndicator>false</j:ChargeFelonyIndicator>
	</j:Charge>
</j:PersonChargeAssociation>
```
You can also mix and match. You could reference a `nc:Person` while including the `j:Charge` inside the association.

NIEM _never_ requires you to do referencing. If the trade-offs of duplicated data aren't an issue, you can have multiple identical `nc:Person` objects.

### Artifacts

- [Associations](/Text_Document/04_Associations.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/04_Associations.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/04_Associations.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/04_Associations.pdf)

___
