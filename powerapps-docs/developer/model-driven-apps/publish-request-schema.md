---
title: Publish 要求スキーマ (モデル駆動型アプリ) | MicrosoftDocs
description: 次は、PublishXmlRequest メッセージのスキーマ定義です。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="publish-request-schema"></a>Publish 要求スキーマ

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/publish-request-schema -->

次は、<xref:Microsoft.Crm.Sdk.Messages.PublishXmlRequest> メッセージのスキーマ定義です。 詳細については、「[カスタマイズの公開](publish-customizations.md)」を参照してください。 [!INCLUDE[schema_download](../../includes/schema-download.md)]。  
  
## <a name="schema"></a>スキーマ  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema attributeFormDefault="unqualified"  
           elementFormDefault="qualified"  
           xmlns:xs="http://www.w3.org/2001/XMLSchema">  
 <xs:element name="importexportxml">  
  <xs:complexType>  
   <xs:sequence>  
    <xs:element name="entities"  
                minOccurs="0">  
     <xs:complexType>  
      <xs:sequence minOccurs="0"  
                   maxOccurs="unbounded">  
       <!-- Name of the entity to publish-->  
       <xs:element maxOccurs="unbounded"  
                   name="entity"  
                   type="xs:string" />  
      </xs:sequence>  
     </xs:complexType>  
    </xs:element>  
    <xs:element name="ribbons"  
                minOccurs="0">  
     <xs:complexType>  
      <xs:sequence minOccurs="0"  
                   maxOccurs="unbounded">  
       <!-- Application ribbon. : This value is not used. We publish the application ribbon if there is at least one <ribbon> node present -->  
       <xs:element maxOccurs="unbounded"  
                   name="ribbon"  
                   type="xs:string" />  
      </xs:sequence>  
     </xs:complexType>  
    </xs:element>  
    <xs:element name="dashboards"  
                minOccurs="0">  
     <xs:complexType>  
      <xs:sequence minOccurs="0"  
                   maxOccurs="unbounded">  
       <!-- Guid of the systemform to publish-->  
       <xs:element maxOccurs="unbounded"  
                   name="dashboard"  
                   type="xs:string" />  
      </xs:sequence>  
     </xs:complexType>  
    </xs:element>  
    <xs:element name="optionsets"  
                minOccurs="0">  
     <xs:complexType>  
      <xs:sequence minOccurs="0"  
                   maxOccurs="unbounded">  
       <!-- Name of the optionset to publish-->  
       <xs:element maxOccurs="unbounded"  
                   name="optionset"  
                   type="xs:string" />  
      </xs:sequence>  
     </xs:complexType>  
    </xs:element>  
    <xs:element name="sitemaps"  
                minOccurs="0">  
     <xs:complexType>  
      <xs:sequence minOccurs="0"  
                   maxOccurs="unbounded">  
       <!-- Guid of the sitemap to publish : This value is not used. We publish the sitemap if there is at least one <sitemap> node present-->  
       <xs:element maxOccurs="unbounded"  
                   name="sitemap"  
                   type="xs:string" />  
      </xs:sequence>  
     </xs:complexType>  
    </xs:element>  
    <xs:element name="webresources"  
                minOccurs="0">  
     <xs:complexType>  
      <xs:sequence minOccurs="0"  
                   maxOccurs="unbounded">  
       <!-- Guid of the web resource to publish -->  
       <xs:element maxOccurs="unbounded"  
                   name="webresource"  
                   type="xs:string" />  
      </xs:sequence>  
     </xs:complexType>  
    </xs:element>  
   </xs:sequence>  
  </xs:complexType>  
 </xs:element>  
</xs:schema>  
  
```  
  
### <a name="see-also"></a>関連項目  
 <xref:Microsoft.Crm.Sdk.Messages.PublishXmlRequest>   
 [カスタマイズの公開](publish-customizations.md)   
 [モデル駆動型アプリで使用するスキーマ](/dynamics365/customer-engagement/developer/schemas-used-dynamics-365)
