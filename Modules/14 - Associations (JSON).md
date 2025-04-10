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

```json
"j:PersonChargeAssociation": {
	"description": "An association between a person and a charge issued to that person.",
	"type": "array",
	"items": {"$ref": "#/definitions/j:PersonChargeAssociationType"}
}
```

[`j:PersonChargeAssociationType`](https://niemopen.github.io/niem-open-training/j.html#PersonChargeAssociationType) includes a [`nc:Person`](https://niemopen.github.io/niem-open-training/nc.html#Person) and a [`j:Charge`](https://niemopen.github.io/niem-open-training/j.html#Charge), but also includes information _about_ the association itself, in this case [`j:JuvenileAsAdultIndicator`](https://niemopen.github.io/niem-open-training/j.html#JuvenileAsAdultIndicator). (Which isn't used in _this_ exchange.) `PersonChargeAssociationType` extends `nc:AssociationType`:

```json
"j:PersonChargeAssociationType": {
	"description": "A data type for an association between a person and a charge.",
	"allOf": [
		{"$ref": "#/definitions/nc:AssociationType"},
		{
			"type": "object",
			"properties": {
				"nc:Person": {"$ref": "#/properties/nc:Person"},
				"j:Charge": {"$ref": "#/properties/j:Charge"},
				"j:JuvenileAsAdultIndicator": {"$ref": "#/properties/j:JuvenileAsAdultIndicator"}
			},
			"required": [
				"nc:Person",
				"j:Charge"
			]
		}
	]
}
```
[`nc:AssociationType`](https://niemopen.github.io/niem-open-training/nc.html#AssociationType) adds in generic association information like a start and end date and a description. Remember that these are inherited by any type based on `nc:AssociationType`, so things of `j:PersonChargeAssociationType` automatically get these common objects.

```json
"nc:AssociationType": {
	"description": "A data type for an association, connection, relationship, or involvement somehow linking people, things, and/or activities together."
}
```

### Instance Documents

In the instance document, the association object can specify the objects being associated together by pointing to then with `ref` attributes, or by including the object inside the association object.

First, here's the association using referencing. The applicable `nc:Person` and `j:Charge` objects are external to `j:PersonChargeAssociation`. While shown next to the `j:PersonChargeAssociation` object, they could be _anywhere_ in the instance document.

This method is useful when the same `nc:Person` object is being used in multiple contexts. In the example Message Spec / IEPD, this `nc:Person` is also the `j:CrashDriver` and the `j:CrashPerson`. This method allows us to define the `nc:Person` once and refer to it multiple times.

This beings with it two advantages:

1. This `nc:Person` object is not being replicated; there is no duplication of data
2. We know that the `nc:Person` in the Association _and_ the `j:CrashDriver` _and_ the `j:CrashPerson` are the exact same person, and not three people with the same name

```json
"j:PersonChargeAssociation": {
	"nc:Person": {
		"@id": "#P01"
	},
	"j:Charge": {
		"@id": "#CH01"
	},
},
"nc:Person": {
	"@id": "#P01",
	"nc:PersonName": {
		"nc:PersonGivenName": "Peter"
	}
},
"j:Charge": {
	"@id": "#CH01",
	"j:ChargeDescriptionText": "Furious Driving",
	"j:ChargeFelonyIndicator": false
}
```


The disadvantage with using referencing is that it can be more difficult to implement. Implementations need to look for `ref` attributes and find matching `id` attributes.

The alternative to referencing is to just include the `nc:Person` and `j:Charge` information inside the association:

```json
"j:PersonChargeAssociation": {
	"nc:Person": {
		"nc:PersonName": {
			"nc:PersonGivenName": "Peter"
		}
	},
	"j:Charge": {
		"j:ChargeDescriptionText": "Furious Driving",
		"j:ChargeFelonyIndicator": false
	}
}

```

You can also mix and match. You could reference a `nc:Person` while including the `j:Charge` inside the association.

NIEM _never_ requires you to do referencing. If the trade-offs of duplicated data aren't an issue, you can have multiple identical `nc:Person` objects.

JSON-LD works similarly. `j:PersonChargeAssociation` contains a `nc:Person` object with an `@id`. `j:Charge` is the same. These IDs match the `@id` objects in the actual `nc:Person` and `j:Charge` object outside the association:


As with the XML version, you can also just include the `nc:Person` and `j:Charge` objects inside the association:


The same trade-offs apply as in XML, but JSON developers may lean more towards inclusion rather than referencing based on implementation effort required. Again, NIEM _never_ requires you to do referencing.

Additionally, while referencing is part of XML Schema, it is _not_ part of JSON Schema. Checking that the `@id` values match up needs to be done with a JSON-LD validator.

### Artifacts

- [Associations](/Text_Document/04_Associations.md)
- Mapping Spreadsheets
	- [Mapping Spreadsheet (Numbers)](/Mapping_Spreadsheets/04_Associations.numbers)
	- [Mapping Spreadsheet (Excel)](/Mapping_Spreadsheets/04_Associations.xlsx)
	- [Mapping Spreadsheet (PDF)](/Mapping_Spreadsheets/04_Associations.pdf)

___
