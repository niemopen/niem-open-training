```xml
<?xml version="1.0" encoding="UTF-8"?>
<c:IEPDCatalog xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://reference.niem.gov/niem/resource/iepd/catalog/5.0/ ../IEPDCatalog/iepd-catalog.xsd"
    xmlns:c="http://reference.niem.gov/niem/resource/iepd/catalog/5.0/"
    xmlns:nc="http://release.niem.gov/niem/niem-core/5.0/"
    xmlns:structures="http://release.niem.gov/niem/structures/5.0/"
    xmlns:exch="http://example.com/CrashDriver/1.0/" c:iepdURI="http://example.com/CrashDriver/1.0/"
    c:iepdConformanceTargetIdentifierURIList="http://reference.niem.gov/niem/specification/model-package-description/5.0/#IEPD"
    c:iepdName="crash-driver-iepd" c:iepdVersionID="2.0">
    <c:IEPDInformation>
        <c:AuthoritativeSource>
            <nc:EntityOrganization>
                <nc:OrganizationName>Training Office</nc:OrganizationName>
                <nc:OrganizationPrimaryContactInformation>
                    <nc:ContactEntity>
                        <nc:EntityPerson>
                            <nc:PersonName>
                                <nc:PersonFullName>Tom Carlson</nc:PersonFullName>
                            </nc:PersonName>
                        </nc:EntityPerson>
                    </nc:ContactEntity>
                </nc:OrganizationPrimaryContactInformation>
            </nc:EntityOrganization>
        </c:AuthoritativeSource>
        <c:CreationDate>2014-08-04</c:CreationDate>
        <c:StatusText>Release Candidate</c:StatusText>
    </c:IEPDInformation>
    <c:IEPConformanceTarget structures:id="CRASH-DRIVER-IEP">
        <nc:DescriptionText>
            A sample IEP representing all major technical aspects of NIEM.
        </nc:DescriptionText>
        <c:HasDocumentElement c:qualifiedNameList="ext:CrashDriverInfo"/>
        <c:XMLSchemaValid>
            <c:XMLCatalog c:pathURI="xml-catalog.xml"/>
        </c:XMLSchemaValid>
        <c:IEPSampleXMLDocument c:pathURI="iep-sample/CrashDriverSample.xml"/>
    </c:IEPConformanceTarget>
    <c:ReadMe c:pathURI="README.md"/>
    <c:IEPDChangeLog c:pathURI="changelog.md"/>
    <c:ConformanceAssertion c:pathURI="conformance.md"/>
    <c:Wantlist c:pathURI="xsd/wantlist.xml"/>
    <c:ExtensionSchemaDocument c:pathURI="xsd/extension/extension.xsd"/>
    <c:ReferenceSchemaDocument c:pathURI="xsd/niem/niem-core.xsd"/>
    <c:ReferenceSchemaDocument c:pathURI="xsd/niem/geospatial.xsd"/>
    <c:ReferenceSchemaDocument c:pathURI="xsd/niem/niem-xs.xsd"/>
    <c:ReferenceSchemaDocument c:pathURI="xsd/niem/codes/aamva_d20.xsd"/>
    <c:ReferenceSchemaDocument c:pathURI="xsd/niem/domains/jxdm.xsd"/>
    <c:ReferenceSchemaDocument c:pathURI="xsd/niem/utility/appinfo.xsd"/>
    <c:ReferenceSchemaDocument c:pathURI="xsd/niem/utility/code-lists-instance.xsd"/>
    <c:ReferenceSchemaDocument c:pathURI="xsd/niem/utility/code-lists-schema-appinfo.xsd"/>
    <c:ReferenceSchemaDocument c:pathURI="xsd/niem/utility/conformanceTargets.xsd"/>
    <c:ReferenceSchemaDocument c:pathURI="xsd/niem/utility/structures.xsd"/>
    <c:ExternalSchemaDocument c:pathURI="xsd/niem/external/ogc/gml/3.2.1/gml.xsd"/>
    <c:ExternalSchemaDocument c:pathURI="xsd/niem/external/ogc/ols/1.1.0/dhs-gmo/2.1.0/ols.xsd"/>
    <c:ExternalSchemaDocument c:pathURI="xsd/niem/external/ogc/xlink/1.0.0/xlinks.xsd"/>
</c:IEPDCatalog>
```