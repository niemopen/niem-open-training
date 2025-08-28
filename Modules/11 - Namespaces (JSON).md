## An Aside about Namespaces

In our examples, you've seen objects with different prefixes, like `j:Crash` and `nc:ActivityDate`. The `j` and `nc` refer to different namespaces in JSON-LD.

- Namespaces organize elements by context
- Identified by prefix, a nickname for the namespace
- NIEM governance is organized along these lines

![Namespaces and Case](Mapping_Graphics/Namespace_Case.png)

JSON-LD maps JSON objects to NIEM namespaces in the `@context` object. Each of these entries maps a prefix to a NIEM namespace, providing a link back to the NIEM object. 

```json
"@context": {
	"ext": "http://training.niem.gov/CrashDriver/1.0/extension#",
	"j": "https://docs.oasis-open.org/niemopen/ns/model/domains/justice/6.0/#",
	"nc": "https://docs.oasis-open.org/niemopen/ns/model/niem-core/6.0/#"
}
```

The `@context` object does _not_ have to be included in every exchange. It's enough that it exists _somewhere_.

In an XML context, NIEM namespaces are mapped to individual files. Each XML Schema file defines a single namespace. In JSON, these can all be kept in a single JSON Schema file.
___
