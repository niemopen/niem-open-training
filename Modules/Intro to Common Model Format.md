# Intro to Common Model Format

## Canonical definition of NIEM

Common Model Format is a canonical definition of the NIEM model, alongside XML Schema. CMF is presented in XML, but its concepts are serialization agnostic. That said, CMF is closely modeled after XML Schema and does many things in an XML Schema-esque way.

## Modeling Concepts

Earlier versions of NIEM embedded modeling concepts in XML Schema. The concepts were implied, complicating pulling those concepts out in order to use NIEM in other contexts, like with JSON or RDF. CMF defines these modeling concepts in modeling terms. Then CMF is transformed into XML Schema or other serializations.

### Properties

Properties define objects with a definition. They're analogous to XML elements. Just as XML elements have types, CMF properties have a Class. Here `nc.PersonName` is of Class `nc.PersonNameType`. Notice that the namespace is called out separately instead of being implied by an element name prefix. Again, CMF is designed to make these concepts clear and distinct to better enable supporting other serializations:

```xml
<Property structures:id="nc.PersonName">
	<Name>PersonName</Name>
	<Namespace structures:ref="nc" xsi:nil="true"/>
	<DefinitionText>A combination of names and/or titles by which a person is known.</DefinitionText>
	<Class structures:ref="nc.PersonNameType" xsi:nil="true"/>
</Property>
```

### Classes

Classes define what other properties an object can hold, just as types do in XML Schema. Here `nc.PersonNameType` is defined to hold four other properties, `nc.PersonGivenName`, `nc.PersonMiddleName`, `nc.PersonSurName`, and `nc.personNameCommentText`. How many of each can be inside of something of `nc.PersonNameType` is defined by the `MinOccursQuantity` and `MaxOccursQuantity` values. This design pattern is straight out of XML Schema, including the possible values. The `sequenceID` is used to make the conversions between CMF and XML Schema lossless. XML attributes are treated as Properties in CMF, as the concept of attributes, especially applied to simple data, is uncommon in other serializations:

```xml
<Class structures:id="nc.PersonNameType">
	<Name>PersonNameType</Name>
	<Namespace structures:ref="nc" xsi:nil="true"/>
	<DefinitionText>A data type for a combination of names and/or titles by which a person is known.</DefinitionText>
	<HasProperty structures:sequenceID="1">
		<Property structures:ref="nc.PersonGivenName" xsi:nil="true"/>
		<MinOccursQuantity>0</MinOccursQuantity>
		<MaxOccursQuantity>1</MaxOccursQuantity>
	</HasProperty>
	<HasProperty structures:sequenceID="2">
		<Property structures:ref="nc.PersonMiddleName" xsi:nil="true"/>
		<MinOccursQuantity>0</MinOccursQuantity>
		<MaxOccursQuantity>unbounded</MaxOccursQuantity>
	</HasProperty>
	<HasProperty structures:sequenceID="3">
		<Property structures:ref="nc.PersonSurName" xsi:nil="true"/>
		<MinOccursQuantity>1</MinOccursQuantity>
		<MaxOccursQuantity>1</MaxOccursQuantity>
	</HasProperty>
	<HasProperty>
		<Property structures:ref="nc.personNameCommentText" xsi:nil="true"/>
		<MinOccursQuantity>0</MinOccursQuantity>
		<MaxOccursQuantity>1</MaxOccursQuantity>
	</HasProperty>
</Class>
```

Classes can extend other classes, just as XML does. In this example, `j.CrashType` extends `j.DrivingIncidentType`. It can hold anything `j.DrivingIncidentType` can hold, but adds additional properties, `j.CrashVehicle` and `j.CrashPerson`. In turn, `j.DrivingIncidentType` can, and does, extend a more generic type. This inheritance chain can be arbitrarily long, but doesn't go past four levels in NIEM:

```xml
<Class structures:id="j.CrashType">
	<Name>CrashType</Name>
	<Namespace structures:ref="j" xsi:nil="true"/>
	<DefinitionText>A data type for a traffic accident.</DefinitionText>
	<ExtensionOfClass structures:ref="j.DrivingIncidentType" xsi:nil="true"/>
	<HasProperty structures:sequenceID="1">
		<Property structures:ref="j.CrashVehicle" xsi:nil="true"/>
		<MinOccursQuantity>1</MinOccursQuantity>
		<MaxOccursQuantity>1</MaxOccursQuantity>
	</HasProperty>
	<HasProperty structures:sequenceID="2">
		<Property structures:ref="j.CrashPerson" xsi:nil="true"/>
		<MinOccursQuantity>0</MinOccursQuantity>
		<MaxOccursQuantity>unbounded</MaxOccursQuantity>
	</HasProperty>
</Class>
```

### Datatypes

CMF also has simple data types, modeled on XML Schema's simple data types. 

```xml
<Datatype structures:id="nc.PersonNameTextType">
	<Name>PersonNameTextType</Name>
	<Namespace structures:ref="nc" xsi:nil="true"/>
	<DefinitionText>A data type for a name by which a person is known, referred, or addressed.</DefinitionText>
	<RestrictionOf>
		<Datatype structures:ref="nc.ProperNameTextType" xsi:nil="true"/>
	</RestrictionOf>
</Datatype>
<Datatype structures:id="nc.ProperNameTextType">
	<Name>ProperNameTextType</Name>
	<Namespace structures:ref="nc" xsi:nil="true"/>
	<DefinitionText>A data type for a word or phrase by which a person or thing is known, referred, or addressed.</DefinitionText>
	<RestrictionOf>
		<Datatype structures:ref="nc.TextType" xsi:nil="true"/>
	</RestrictionOf>
</Datatype>
<Datatype structures:id="nc.TextType">
	<Name>TextType</Name>
	<Namespace structures:ref="nc" xsi:nil="true"/>
	<DefinitionText>A data type for a character string.</DefinitionText>
	<RestrictionOf>
		<Datatype structures:ref="xs.string" xsi:nil="true"/>
	</RestrictionOf>
</Datatype>
<Datatype structures:id="xs.string">
	<Name>string</Name>
	<Namespace structures:ref="xs" xsi:nil="true"/>
</Datatype>
```
These types can be further restricted, to create enumerations. For example, here the `xs.token` data type is restricted to the values "PII" and "MEDICAL", forming a privacy code table called `ext.PrivacyCodeType`:

```xml
<Datatype structures:id="ext.PrivacyCodeType">
	<Name>PrivacyCodeType</Name>
	<Namespace structures:ref="ext" xsi:nil="true"/>
	<DefinitionText>A data type for a code representing a kind of property.</DefinitionText>
	<RestrictionOf>
		<Datatype structures:ref="xs.token" xsi:nil="true"/>
		<Enumeration>
			<StringValue>PII</StringValue>
			<DefinitionText>Personally Identifiable Information</DefinitionText>
		</Enumeration>
		<Enumeration>
			<StringValue>MEDICAL</StringValue>
			<DefinitionText>Medical Information</DefinitionText>
		</Enumeration>
	</RestrictionOf>
</Datatype>
```

- Defines modeling concepts in modeling terms
	- Properties, classes, and data types
	- Not implying modeling concepts with XML Schema terms
- Presented in XML, but the concepts are serialization agnostic
	- That said, CMF is still somewhat XML-ish in how it instantiates concepts
	- Easily converted to XML Schema, and back
	- Manageably converted to JSON Schema, but not back
- Allows for tool-based support for both XML and JSON (and RDF, et al) from a single "code base"

## Tooling

CMF is normally hidden behind tooling. You can do CMF by hand, since it's just XML, but it's recommended to use the available tooling.

### CMFTool

`CMFTool` is a command line tool that converts between XML Schema and CMF. This is a full deterministic transform, allowing for lossless round-tripping between the two formats. `CMFTool` can also transform CMF to JSON Schema, but cannot transform JSON Schema back into CMF. By using CMF as an intermediary, `CMFTool` can also transform NIEM-conformant XML Schema into JSON Schema.

JSON Schema is _not_ one of the canonical definitions of NIEM, but this support is provided to make NIEM more usable in a JSON context.

### NIEM Toolbox and NIEM API

The functionality of `CMFTool` is also embedded in the NIEM API. You can access this functionality via NIEM Toolbox, or through your own client, which can be as simple as an HTML form.


## More Information

For information on more advanced aspects of CMF, refer to the NIEM Naming and Design Rules (NDR).
