## An Aside about Namespaces

Below you can see object with different prefixes, `j:Crash` and `nc:ActivityDate`. The `j` and `nc` refer to different namespaces in XML Schema.

- Namespaces organize elements by context
- Identified by prefix, a nickname for the namespace
- NIEM governance is organized along these lines

![Namespaces and Case](Mapping_Graphics/Namespace_Case.png)

JSON-LD maps JSON objects to NIEM namespaces in the `@context`. Each of these entries maps a prefix to a NIEM namespace, providing a link back to the NIEM object. 

```json
"@context": {
	"ext": "http://training.niem.gov/CrashDriver/1.0/extension#",
	"j": "http://release.niem.gov/niem/domains/jxdm/7.0/#",
	"nc": "http://release.niem.gov/niem/niem-core/5.0/#"
}
```

As mentioned earlier, NIEM doesn't support JSON Schema well yet. Using NIEM with JSON is currently focused on creating matching instance documents. Upcoming NIEM developments will greatly enhance the ability to work in JSON as a similar level as with XML and XML Schema.
___
