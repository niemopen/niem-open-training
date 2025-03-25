## JSON Schema in a Nutshell

JSON Schema defines what an JSON document needs to look like. (XML Schema does the same for XML documents.)

For example, this bit of JSON Schema defines what a `PersonName` object needs to look like.

```json
"nc:PersonNameType": {
	"description": "A data type for a combination of names and/or titles by which a person is known.",
	"type": "object",
	"properties": {
		"nc:PersonGivenName": {"type": "string"},
		"nc:PersonMiddleName": {
			"type": "array",
			"items": {"type": "string"}
		},
		"nc:PersonSurName": {"type": "string"},
		"nc:personNameCommentText": {"type": "string"}
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
And here's what the matching JSON _instance_ document might look like.

```json
"nc:PersonName": [
	{
		"nc:PersonGivenName": "Peter",
		"nc:PersonMiddleName": [
			"Death",
			"Bredon"
		],
		"nc:PersonSurName": "Wimsey"
	}
]
```