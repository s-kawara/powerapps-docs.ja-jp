---
title: ビジュアル化データ記述スキーマ (モデル駆動型アプリ) | Microsoft Docs
description: 次に示すのは、ビジュアル化のグラフのデータ記述 XML 文字列のスキーマです。 グラフを作成する際に、データ記述 XML 文字列の内容を確認するのに使用できます。
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
# <a name="visualization-data-description-schema"></a>ビジュアル化データ記述スキーマ

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/visualization-data-description-schema -->

次に示すのは、ビジュアル化のグラフのデータ記述 XML 文字列のスキーマです。 グラフを作成する際に、データ記述 XML 文字列の内容を確認するのに使用できます。 詳細については、「[グラフの詳細: 基盤となるデータとグラフ表現](understand-charts-underlying-data-chart-representation.md)」を参照してください。 [!INCLUDE[schema_download](../../includes/schema-download.md)] およびフォルダーの `VisualizationDataDescription.xsd` ファイルを参照してください。  
  
## <a name="schema"></a>スキーマ  
  
```xml  
<?xml version='1.0' encoding='utf-8'?>  
<xs:schema attributeFormDefault='unqualified'  
           elementFormDefault='qualified'  
           xmlns:xs='http://www.w3.org/2001/XMLSchema'>  
 <xs:element name='datadefinition'>  
  <xs:complexType>  
   <xs:sequence>  
    <xs:element name='fetchcollection'>  
     <xs:complexType>  
      <xs:sequence>  
       <xs:element maxOccurs='unbounded'  
                   name='fetch'>  
        <xs:annotation>  
         <!--FetchXML goes here-->  
        </xs:annotation>  
       </xs:element>  
      </xs:sequence>  
     </xs:complexType>  
    </xs:element>  
    <xs:element name='categorycollection'>  
     <xs:complexType>  
      <xs:sequence>  
       <xs:element name='category'  
                   type='CategoryType'  
                   minOccurs='1'  
                   maxOccurs='unbounded' />  
      </xs:sequence>  
     </xs:complexType>  
    </xs:element>  
   </xs:sequence>  
  </xs:complexType>  
 </xs:element>  
 <xs:complexType name ='CategoryType'>  
  <xs:sequence>  
   <xs:element minOccurs='1'  
               maxOccurs='unbounded'  
               name='measurecollection'>  
    <xs:complexType>  
     <xs:sequence>  
      <xs:element minOccurs='1'  
                  maxOccurs='unbounded'  
                  name='measure'>  
       <xs:complexType>  
        <xs:attribute name='alias'  
                      type='xs:string'  
                      use='required' />  
       </xs:complexType>  
      </xs:element>  
     </xs:sequence>  
    </xs:complexType>  
   </xs:element>  
  </xs:sequence>  
  <xs:attribute name='alias'  
                type='xs:string'  
                use='optional' />  
 </xs:complexType>  
</xs:schema>  
```  
### <a name="see-also"></a>関連項目  
 [ビジュアル化とダッシュボードのカスタマイズ](customize-visualizations-dashboards.md)   
 [グラフの詳細: 基盤となるデータとグラフ表現](understand-charts-underlying-data-chart-representation.md)   
 [サンプル グラフ](sample-charts.md)   
 [FetchXML の使用によるクエリの作成](../common-data-service/use-fetchxml-construct-query.md)