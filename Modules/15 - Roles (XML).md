## Roles

![Roles](/Req_Analysis_Graphics/05_Roles_CrashDriverClassDiagram.png)

- Modeling some objects as specialized things gets complicated
- Roles are roles that objects play
	- People, organizations, items are the major ones
- Roles and objects playing the roles are linked together using the `uri` attribute
	- An object can play multiple roles, because multiple role objects can have the same `uri` value
- Roles contain other information about the role
- Roles are _not_ explicitly defined as such
- Examples:
	- `j:CrashPerson` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-45q)/[Wayfarer](http://niem5.org/wayfarer/j/CrashPerson.html))
	- `j:CrashDriver`

### Searching for Injured Person

How do we find the match for "injured person"? Here's one way:

- Search for `injured person`
	- [SSGT](http://niem5.org/ssgt_redirect.php?query=injured+person)
	- [Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=injured+person)
- No results! How about `person injury`?
	- [SSGT](http://niem5.org/ssgt_redirect.php?query=person+injury)
	- [Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=person+injury)
- Notice that [`j:InjuryLocationCode`](http://niem5.org/wayfarer/j/InjuryLocationCode.html) looks like something an injured person would have
- That's inside of things of [`nc:InjuryType`](http://niem5.org/wayfarer/nc/InjuryType.html)
- [`j:CrashPersonInjury`](http://niem5.org/wayfarer/j/CrashPersonInjury.html) is one of the things of that type
- And that's inside of [`j:CrashPerson`](http://niem5.org/wayfarer/j/CrashPerson.html)


### Roles - Not Special Kinds of People

| Roles | Just a Guy |
| --- | --- |
| ![Role Hats](/Mapping_Graphics/Role_Hats_01.png) | ![Role Hats](/Mapping_Graphics/Role_Hats_02.png) |

### Roles – Allows an Object to Play Multiple Roles
![Role Hats](/Mapping_Graphics/Role_Hats_03.png)

### Roles - How They Work
Roles are linked to the Object playing the Role via the `uri` attribute:

![Role Hats](/Mapping_Graphics/Role_Hats_04.png)

Roles contain information about the Role:

![Role Hats](/Mapping_Graphics/Role_Hats_05.png)

### Schemas

[`j:CrashPerson`](https://niemopen.github.io/niem-open-training/j.html#CrashPerson) is of `j:CrashPersonType`:

```xml
<xs:element name="CrashPerson" type="j:CrashPersonType" nillable="true">
	<xs:annotation>
		<xs:documentation>A person involved in a traffic accident.</xs:documentation>
	</xs:annotation>
</xs:element>
```

[`j:CrashPersonType`](https://niemopen.github.io/niem-open-training/j.html#CrashPersonType) contains information specific to this role. In the sample Message Spec / IEPD, we're also using `j:CrashPersonInjury`:

```xml
<xs:complexType name="CrashPersonType">
	<xs:annotation>
		<xs:documentation>A data type for any person involved in a traffic accident.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="j:CrashPersonEMSTransportation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:CrashPersonInjury" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="j:CrashPersonAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```


### Instance Documents

Here we see a `j:CrashPerson` linked via `structures:uri` with an `nc:Person` object playing that role:

```xml
<j:CrashPerson structures:uri="http://some.uri/">
	<j:CrashPersonInjury>  
		<nc:InjuryDescriptionText>Broken Arm</nc:InjuryDescriptionText>  
	</j:CrashPersonInjury>
</j:CrashPerson>

<nc:Person structures:uri="http://some.uri/">
	<nc:PersonName>
		<nc:PersonGivenName>Peter</nc:PersonGivenName>
	</nc:PersonName>
</nc:Person>
```

### Artifacts

- [Roles](/Text_Document/05_Roles.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/05_Roles.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/05_Roles.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/05_Roles.pdf)

___
