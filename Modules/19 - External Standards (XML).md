## External Standards

![External Standards](/Req_Analysis_Graphics/08_External_Standards_CrashDriverClassDiagram.png)

- NIEM supports external standards, if they’re XML
- Wraps them in NIEM-conformant adapters
- Example:
	- NIEM: `nc:LocationGeospatialCoordinateAbstract` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-125z)/[Wayfarer](http://niem5.org/wayfarer/nc/LocationGeospatialCoordinateAbstract.html))
	- NIEM-conformant adapter: `geo:LocationGeospatialPoint` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-m73))
	- External standard: `gml:Point` ([SSGT](https://tools.niem.gov/niemtools/ssgt/SSGT-GetProperty.iepd?propertyKey=o4-fux))
- You’ll probably never use this, but should know it’s there
- SSGT supports them; Wayfarer does not

### Schemas

`LocationType` contains a `nc:LocationGeospatialCoordinateAbstract`:

```xml
<xs:complexType name="LocationType">
	<xs:annotation>
		<xs:documentation>A data type for geospatial location.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="nc:LocationAddressAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationArea" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationCategoryAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationContactInformation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationDescriptionText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationDirectionsText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationGeospatialCoordinateAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationHeightAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationIdentification" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationLandmarkAbstract" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationLocale" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationMapLocation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationName" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationPart" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationRangeDescriptionText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationRelativeLocation" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationSurroundingAreaDescriptionText" minOccurs="0" maxOccurs="unbounded"/>
				<xs:element ref="nc:LocationAugmentationPoint" minOccurs="0" maxOccurs="unbounded"/>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
`nc:LocationGeospatialCoordinateAbstract` is the head of a substitution group:

```xml
<xs:element name="LocationGeospatialCoordinateAbstract" abstract="true">
	<xs:annotation>
		<xs:documentation>A data concept for a geospatial location.</xs:documentation>
	</xs:annotation>
</xs:element>
```

One of the members of that substitution group is `geo:LocationGeospatialPoint`, which is an adapter to the external standard:

```xml
<xs:element name="LocationGeospatialPoint" type="geo:PointType" substitutionGroup="nc:LocationGeospatialCoordinateAbstract" nillable="true">
	<xs:annotation>
		<xs:documentation>A 2D or 3D geometric point. A gml:Point is defined by a single coordinate tuple.
			The direct position of a point is specified by the gml:pos element which is of
			type gml:DirectPositionType.</xs:documentation>
	</xs:annotation>
</xs:element>
```
Its type is `geo:PointType`. We're still in NIEM, but `gml:Point` isn't:

```xml
<xs:complexType name="PointType" appinfo:externalAdapterTypeIndicator="true">
	<xs:annotation>
		<xs:documentation>A data type for a 2D or 3D geometric point. A gml:Point is defined by a single
			coordinate tuple. The direct position of a point is specified by the gml:pos element which is
			of type gml:DirectPositionType.</xs:documentation>
	</xs:annotation>
	<xs:complexContent>
		<xs:extension base="structures:ObjectType">
			<xs:sequence>
				<xs:element ref="gml:Point" minOccurs="1" maxOccurs="1">
					<xs:annotation>
						<xs:documentation>A gml:Point is defined by a single coordinate tuple.
							The direct position of a point is specified by the gml:pos element
							which is of type gml:DirectPositionType.</xs:documentation>
					</xs:annotation>
				</xs:element>
			</xs:sequence>
		</xs:extension>
	</xs:complexContent>
</xs:complexType>
```
And here is the `gml:Point` object from the external standard.

```xml
<element name="Point" type="gml:PointType" substitutionGroup="gml:AbstractGeometricPrimitive">
	<annotation>
		<documentation>A Point is defined by a single coordinate tuple. The direct position of a point is specified by the pos element which is of type DirectPositionType.</documentation>
	</annotation>
</element>

<complexType name="PointType">
	<complexContent>
		<extension base="gml:AbstractGeometricPrimitiveType">
			<sequence>
				<choice>
					<element ref="gml:pos"/>
					<element ref="gml:coordinates"/>
				</choice>
			</sequence>
		</extension>
	</complexContent>
</complexType>

```

The resulting XML instance looks like this:

```xml
<nc:Location>
	<geo:LocationGeospatialPoint>
		<gml:Point gml:id="point1">
			<gml:pos srsName="urn:ogc:def:crs:EPSG::4326" srsDimension="2">40.689167 -74.044444</gml:pos>
		</gml:Point>
	</geo:LocationGeospatialPoint>
</nc:Location>
```

### Artifacts

- [External Standards](/Text_Document/09_External_Standards.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/09_External_Standards.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/09_External_Standards.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/09_External_Standards.pdf)

___
