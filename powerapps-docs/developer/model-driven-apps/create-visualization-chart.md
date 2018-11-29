---
title: ビジュアル化の作成 (グラフ) (モデル駆動型アプリ) | Microsoft Docs
description: このトピックではグラフのビジュアル化と Web リソースのビジュアル化の作成方法を説明します。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 9dbed5ee-21a4-ab86-fc4c-08c3838e42f2
author: JimDaly
ms.author: jdaly
manager: shilpas
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="create-a-visualization-chart"></a>ビジュアル化の作成 (グラフ)

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/create-visualization-chart -->

ビジュアル化をプログラムで作成するには、[SavedQueryVisualization Entity](../common-data-service/reference/entities/savedqueryvisualization.md) または [UserQueryVisualization Entity](../common-data-service/reference/entities/userqueryvisualization.md) エンティティのレコードを作成して、組織所有またはユーザー所有のグラフをそれぞれ作成する必要があります。 このトピックでは、グラフ ビジュアル化と Web リソース ビジュアル化の作成方法を説明します。  
  
<a name="Before"></a>   

## <a name="before-you-create-a-visualization"></a>ビジュアル化を作成する前に  

 ビジュアル化を作成する前に、次のことを確認してください。  
  
- **ビジュアル化の種類**: ビジュアル化を組織全体で利用できるようにし、より詳細なレベルでのアクセス レベル管理を行わない場合は、通常、組織所有のビジュアル化を作成します。 ただし、ビジュアル化のアクセス特権やセキュリティについて考慮する必要がある場合は、アクセスするユーザーをより厳密に制御する、ユーザー所有のビジュアル化の作成を検討してください。  
  
    > [!NOTE]
    >  組織所有のビジュアル化は、システム管理者またはシステム カスタマイザー ロールを持つユーザーだけが作成できます。  
  
- **ビジュアル化エンティティ**: ビジュアル化はエンティティに添付されます。 詳細: [ビジュアル化でサポートされているエンティティ](view-data-with-visualizations-charts.md#SupportedVisualizationEntities)。 [SavedQueryVisualization.PrimaryEntityTypeCode](../common-data-service/reference/entities/savedqueryvisualization.md#BKMK_PrimaryEntityTypeCode) または [UserQueryVisualization.PrimaryEntityTypeCode](../common-data-service/reference/entities/userqueryvisualization.md#BKMK_PrimaryEntityTypeCode) 属性を使用して、サポートされるエンティティにグラフをアタッチすることができます。  
  
<a name="CreateChart"></a>   

## <a name="create-a-chart-visualization"></a>グラフ ビジュアル化の作成  

 グラフのビジュアル化を作成するには、グラフの基盤データとグラフの外観を、*データ記述*および*プレゼンテーション記述* XML 文字列として指定する必要があります。 詳細: [グラフ データの指定](understand-charts-underlying-data-chart-representation.md)および[サンプル グラフ](sample-charts.md)。  
  
 組織所有のグラフの作成方法の完全なサンプルについては、[サンプル: グラフの作成、取得、更新、および削除 (CRUD)](/dynamics365/customer-engagement/developer/customize-dev/sample-create-retrieve-update-delete-chart) を参照してください。  <!-- TODO need to replace the link with powerapps -->
  
### <a name="create-a-multi-series-chart"></a>複数系列グラフの作成  

 複数系列グラフとは、1 つのカテゴリ (水平方向) 軸値に複数の系列 (垂直方向) 軸値をマップするグラフです。 単一系列グラフとの唯一の違いは、XML 文字列内に、複数の `<measurecollection>` と、対応する `<series>` 要素が指定されている点です。 各 `<measurecollection>` 要素には、同じカテゴリ (水平方向) 値に対する系統 (垂直方向) 軸値を定義する、`<measure>` という子要素がふくまれています。 詳細: [グラフの詳細: 基盤となるデータとグラフ表現](understand-charts-underlying-data-chart-representation.md)。  
  
 サンプルの複数系列グラフと、対応するデータ記述およびプレゼンテーション記述 XML 文字列については、[TODO: 複数系列グラフ]<!--(sample-charts.md#MultiSeriesChart)-->を参照してください。
  
<a name="CreateWRVisualization"></a>   

## <a name="create-a-web-resource-visualization"></a>Web リソース ビジュアル化の作成  

 Web リソースを含んだビジュアル化では、データ Description およびプレゼンテーション Description XML 文字列を指定する必要はありません。 次のサンプルでは、SDK を使用して、Web リソースを含んだ組織所有のビジュアル化を作成する方法を示しています。  
  
```csharp  
SavedQueryVisualization newWebResourceVisualization = new SavedQueryVisualization()  
{  
   Name = "Sample Dashboard Visualization",  
   Description = "Sample organization-owned visualization",  
                           PrimaryEntityTypeCode = Account.EntityLogicalName,  
   WebResourceId = new EntityReference(WebResource.EntityLogicalName, _webResourceId))  
  
};  
_orgOwnedVisualizationId = _serviceProxy.Create(newWebResourceVisualization);  
  
```  
  
 Dynamics 365 Common Data Service for Apps Web アプリケーションを使用して Web リソース ビジュアル化を作成する場合は、次の形式の XML ファイルを作成し、その後、リボン内の**グラフのインポート**を使用してビジュアル化をインポートする必要があります。  
  
```xml  
<visualization>  
  <name>Visualization_Name</name>  
  <description>Description</description>  
  <webresourcename>Name_Of_An_Existing_Web_Resource</webresourcename>  
  <primaryentitytypecode>Entity_Logical_Name</primaryentitytypecode>  
  <isdefault>Value: true or false</isdefault>  
</visualization>  
```  
  
 たとえば、*new_TestWebResource* という名前の既存の Web リソースを表示する *サンプル ビジュアル化* を作成し、そのビジュアル化を *取引先企業* エンティティにアタッチするには、XML は以下のようになります。  
  
```xml  
<visualization>  
  <name>Sample Visualization</name>  
  <description>Sample Web Resource Visualization.</description>  
  <webresourcename>new_TestWebResource</webresourcename>  
  <primaryentitytypecode>account</primaryentitytypecode>  
  <isdefault>false</isdefault>  
</visualization>  
```  
  
### <a name="see-also"></a>関連項目  
 [グラフ](view-data-with-visualizations-charts.md)   
 [グラフ データの指定](understand-charts-underlying-data-chart-representation.md)   
 [グラフ上のアクション](actions-visualizations-charts.md)   
 [サンプル グラフ](sample-charts.md)   
 [データのビジュアル化および分析](customize-visualizations-dashboards.md)   
 [サンプル: グラフの作成、取得、更新、および削除 (CRUD) ](/dynamics365/customer-engagement/developer/customize-dev/sample-create-retrieve-update-delete-chart)<!-- TODO need to replace the link with powerapps -->