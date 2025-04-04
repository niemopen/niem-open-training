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

It doesn't make much sense to try and represent this in JSON in a NIEM-conformant way. NIEM doesn't (can't) provide rules for converting non-NIEM XML to JSON. This was auto-generated with an XML editor:

```json
"nc:Location": {
	"geo:LocationGeospatialPoint": {
		"gml:Point": {
			"gml:id": "point1",
			"gml:pos": {
				"srsName": "urn:ogc:def:crs:EPSG::4326",
				"srsDimension": 2,
				"#text": "40.689167 -74.044444"
			}
		}
	}
}
```

### Artifacts

- [External Standards](/Text_Document/09_External_Standards.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/09_External_Standards.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/09_External_Standards.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/09_External_Standards.pdf)

___
