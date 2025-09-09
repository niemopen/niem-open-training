# Mapping and NIEM Technical Details

NIEM can be used with JSON via [JSON-LD](https://en.wikipedia.org/wiki/JSON-LD). JSON-LD extends JSON to allow for meaningfully linking data together. NIEM leverages JSON-LD in two ways:

1. NIEM uses `@context` to provide a mapping from JSON object names back to their counterparts in NIEM
2. NIEM uses `@id` and `@uri` to provide links between JSON objects

Linking is a topic for later in the class, but here is an example of the `@context`. This context tells us that `nc:Person` refers to the `Person` object in the NIEM-Core namespace.

```json
"@context": {
	"nc": "http://release.niem.gov/niem/niem-core/5.0/",
	"xs": "http://www.w3.org/2001/XMLSchema"
}
```

The structure of the JSON instances mirrors the structure of the XML instances, although the schemas for each may look quite different, as JSON Schema and XML Schema work quite differently.

JSON-LD and JSON Schema are separate concepts. NIEM does not _yet_ support JSON Schema as a canonical definition of NIEM, but tools support making JSON Schema subsets against which to validate your instances. Links to schemas will go to the XML Schema versions due to this.

## Understanding NIEM Objects

- JSON Schema uses properties and definitions, similar to XML Schema's elements and types
	- We'll call them "elements" and "types"
- What a property/element can hold is based on its definition/type
- What you are (your type) defines what you can hold

![What You Are Defines What You Hold](/Mapping_Graphics/WYADWYH.png)

### JSON Schema

The JSON Schema defining [`nc:Person`](https://niemopen.github.io/niem-open-training/nc.html#Person) includes a definition of the property and a "type".

Its type, [`nc:PersonType`](https://niemopen.github.io/niem-open-training/nc.html#PersonType), has a little more information. It includes a definition, one similar to `nc:Person`. It also includes a `type` of "object" and a list of objects that go _inside_ an `nc:Person` object. Each one is a reference to a declaration of each of those objects. JSON Schema cardinality is done via a combination of properties being listed as "required" and the "`type` of the element, whether the object holds one set of values or an array of values. Both are shown with `nc:Person` and `nc:PersonType`:

```json
"nc:PersonType": {
	"description": "A data type for a human being.",
	"type": "object",
	"properties": {
		"nc:PersonBirthDate": {"$ref": "#/properties/nc:PersonBirthDate"},
		"nc:PersonName": {"$ref": "#/properties/nc:PersonName"}
	},
	"required": ["nc:PersonName"]
}
```
```json
"nc:Person": {
	"description": "A human being.",
	"anyOf": [
		{
			"type": "array",
			"items": {"$ref": "#/definitions/nc:PersonType"}
		},
		{"$ref": "#/definitions/nc:PersonType"}
	]
}
```

The JSON Schema defining [`nc:PersonName`](https://niemopen.github.io/niem-open-training/nc.html#PersonName) and [`nc:PersonNameType`](https://niemopen.github.io/niem-open-training/nc.html#PersonNameType) looks like:

```json
"nc:PersonNameType": {
	"description": "A data type for a combination of names and/or titles by which a person is known.",
	"type": "object",
	"properties": {
		"nc:PersonGivenName": {"$ref": "#/properties/nc:PersonGivenName"},
		"nc:PersonMiddleName": {"$ref": "#/properties/nc:PersonMiddleName"},
		"nc:PersonSurName": {"$ref": "#/properties/nc:PersonSurName"},
		"nc:personNameCommentText": {"$ref": "#/properties/nc:personNameCommentText"}
	},
	"required": ["nc:PersonSurName"]
}
```
```json
"nc:PersonName": {
	"description": "A combination of names and/or titles by which a person is known.",
	"type": "array",
	"items": {"$ref": "#/definitions/nc:PersonNameType"}
}
```
The JSON Schema defining [`nc:PersonGivenName`](https://niemopen.github.io/niem-open-training/nc.html#PersonGivenName), [`PersonNameTextType`](https://niemopen.github.io/niem-open-training/nc.html#PersonNameTextType), and supporting types looks like:

```json
"nc:PersonNameTextType": {
	"description": "A data type for a name by which a person is known, referred, or addressed.",
	"$ref": "#/definitions/nc:ProperNameTextType"
},
"nc:ProperNameTextType": {
	"description": "A data type for a word or phrase by which a person or thing is known, referred, or addressed.",
	"$ref": "#/definitions/nc:TextType"
},
"nc:TextType": {
	"description": "A data type for a character string.",
	"type": "string"
}
```
```json
"nc:PersonGivenName": {
	"description": "A first name of a person.",
	"$ref": "#/definitions/nc:PersonNameTextType"
}
```
Finally, the definition for `nc:PersonBirthDate` is `nc:DateType` which holds a `nc:Date`:

```json
"nc:DateType": {
	"description": "A data type for a calendar date.",
	"type": "object",
	"properties": {
		"nc:Date": {"$ref": "#/properties/nc:Date"}
	},
	"required": ["nc:Date"]
}
```
```json
"nc:Date": {
	"description": "A full date.",
	"type": "string",
	"format": "date"
},
"nc:PersonBirthDate": {
	"description": "A date a person was born.",
	"$ref": "#/definitions/nc:DateType"
}
```

The resulting instance document that all this creates might look like this:

```json
"nc:Person": {
	"nc:PersonBirthDate": {"nc:Date": "1890-05-04"},
	"nc:PersonName": {
		"nc:PersonGivenName": "Peter",
		"nc:PersonMiddleName": [
			"Death",
			"Bredon"
		],
		"nc:PersonSurName": "Wimsey"
	}
}
```

(Who is [Peter Wimsey](https://en.wikipedia.org/wiki/Lord_Peter_Wimsey)?)
___

