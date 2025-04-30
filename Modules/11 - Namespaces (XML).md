## An Aside about Namespaces

Below you can see object with different prefixes, `j:Crash` and `nc:ActivityDate`. The `j` and `nc` refer to different namespaces in XML Schema.

- Namespaces organize elements by context
- Identified by prefix, a nickname for the namespace
- NIEM governance is organized along these lines

![Namespaces and Case](/Mapping_Graphics/Namespace_Case.png)

```xml
<xs:schema   
	targetNamespace="http://training.niem.gov/CrashDriver/1.0/" version="1" xml:lang="en-US"  

	xmlns:ext="http://training.niem.gov/CrashDriver/1.0/"  
	xmlns:j="https://docs.oasis-open.org/niemopen/ns/model/domains/justice/6.0/"  
	xmlns:nc="https://docs.oasis-open.org/niemopen/ns/model/niem-core/6.0/">

	<xs:import schemaLocation="../domains/justice.xsd"
		namespace="https://docs.oasis-open.org/niemopen/ns/model/domains/justice/6.0/"/>
	<xs:import schemaLocation="../niem-core.xsd"
		namespace="https://docs.oasis-open.org/niemopen/ns/model/niem-core/6.0/"/>

```

___
