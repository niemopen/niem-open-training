## An Aside about Namespaces

Below you can see object with different prefixes, `j:Crash` and `nc:ActivityDate`. The `j` and `nc` refer to different namespaces in XML Schema.

- Namespaces organize elements by context
- Identified by prefix, a nickname for the namespace
- NIEM governance is organized along these lines

![Namespaces and Case](/Mapping_Graphics/Namespace_Case.png)

```xml
<xs:schema targetNamespace="http://training.niem.gov/CrashDriver/1.0/extension" version="1" xml:lang="en-US"  
    xmlns:ext="http://training.niem.gov/CrashDriver/1.0/extension"  
    xmlns:j="http://release.niem.gov/niem/domains/jxdm/7.0/"  
    xmlns:nc="http://release.niem.gov/niem/niem-core/5.0/">

    <xs:import schemaLocation="../niem/domains/jxdm.xsd"  
        namespace="http://release.niem.gov/niem/domains/jxdm/7.0/"/>
	<xs:import schemaLocation="../niem/niem-core.xsd"  
        namespace="http://release.niem.gov/niem/niem-core/5.0/"/>
```
___
