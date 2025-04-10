![Inherited Properties](/Req_Analysis_Graphics/03_Inherited_Properties_CrashDriverClassDiagram.png)

- NIEM is a model, not a flat data dictionary
- Some concepts don’t exist as elements using the terms for the concept
- Instead, properties are inherited
- There is no “Crash Date” in NIEM ([SSGT](http://niem5.org/ssgt_redirect.php?query=crash+date)/[Wayfarer](http://niem5.org/wayfarer/search.php?option=both&query=crash+date))
- There _is_ an `ActivityDate` which can be inside a `Crash` object ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-44f)/[Wayfarer](http://niem5.org/wayfarer/j/Crash.html))

### Schemas

Here's [`j:Crash`](https://niemopen.github.io/niem-open-training/j.html#Crash) and its type, `j:CrashType`:

```xml
<xs:element name="Crash" type="j:CrashType" nillable="true">
	<xs:annotation>
		<xs:documentation>A traffic accident.</xs:documentation>
	</xs:annotation>
</xs:element>
```
[`j:CrashType`](https://niemopen.github.io/niem-open-training/j.html#CrashType) contains several things, but the important thing here is what it's based on, `j:DrivingIncidentType`:

```xml
<xs:complexType name="CrashType">
	<xs:annotation>
		<xs:documentation>A data type for a traffic accident.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="j:DrivingIncidentType">
			<xs:sequence>
				<xs:element ref="j:CrashServiceCall" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:CrashInformationSource" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="j:CrashAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

[`j:DrivingIncidentType`](https://niemopen.github.io/niem-open-training/j.html#DrivingIncidentType) is, in turn, based on an even more generic type, `nc:IncidentType`:

```xml
<xs:complexType name="DrivingIncidentType">
	<xs:annotation>
		<xs:documentation>A data type for details of an incident involving a vehicle.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:IncidentType">
			<xs:sequence>
				<xs:element ref="j:DrivingAccidentSeverityAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="j:DrivingIncidentCMVAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="j:DrivingIncidentAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

[`nc:IncidentType`](https://niemopen.github.io/niem-open-training/nc.html#IncidentType) is, also in turn, based on a very generic type, `nc:ActivityType`:

```xml
<xs:complexType name="IncidentType">
	<xs:annotation>
		<xs:documentation>A data type for an occurrence or an event that may require a response.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="nc:ActivityType">
			<xs:sequence>
				<xs:element ref="nc:IncidentEvent" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:IncidentJurisdictionalOrganization" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="nc:IncidentAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

And we finally get to [`nc:ActivityType`](https://niemopen.github.io/niem-open-training/nc.html#ActivityType), which contains [`nc:ActivityDate`](https://niemopen.github.io/niem-open-training/nc.html#ActivityDate):

```xml
<xs:complexType name="ActivityType">
	<xs:annotation>
		<xs:documentation>A data type for a single or set of related actions, events, or process steps.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:ActivityIdentification" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:ActivityActualDuration" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="nc:ActivityDate" minOccurs="0" maxOccurs="unbounded"/>
				<!-- A whole slew of objects removed for clarity -->
				<xs:element ref="nc:ActivityAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```

What this all means is that a `j:Crash` object can contain a `nc:ActivityDate`, which is, contextually, a Crash Date.

### Instance Documents

Instance in XML:

```xml
<j:Crash>
	<nc:ActivityDate>
		<nc:Date>1900-05-04</nc:Date>
	</nc:ActivityDate>
</j:Crash>
```

You need to understand this concept in order to know to look for these cases, which are very common, but just use tools to figure out the details, e.g:

- [`j:Crash` in the SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-44f)
- [`j:Crash` in Wayfarer](http://niem5.org/wayfarer/j/Crash.html)
	- Wayfarer has a new feature that does some level of [contextual searching](http://niem5.org/wayfarer/searchcontextuals.php)
	- [Search contextually for "crash date" in Wayfarer](http://niem5.org/wayfarer/searchcontextuals.php?query=crash+date)

### Artifacts

- [Inherited Properties](Text_Document/03_Inherited_Properties.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](Mapping_Spreadsheets/03_Inherited_Properties.numbers)
	- [Mapping Spreadsheet (Excel)](Mapping_Spreadsheets/03_Inherited_Properties.xlsx)
	- [Mapping Spreadsheet (PDF)](Mapping_Spreadsheets/03_Inherited_Properties.pdf)

___