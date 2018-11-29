---
title: 'ダッシュボードについて: ダッシュボード コンポーネントと FormXML (モデル駆動型アプリ) | Microsoftのドキュメント'
description: ダッシュボードはモデル駆動型アプリで使用される様々な種類のフォームのうちの 1 つです。 フォームがダッシュボードかどうかは、SystemForm.Type または UserForm.Type 属性を使用して確認できます。
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
# <a name="understand-dashboards-dashboard-components-and-formxml"></a>ダッシュボードについて: ダッシュボード コンポーネントと FormXML

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/understand-dashboards-dashboard-components-formxml -->

ダッシュボードはモデル駆動型アプリで使用される様々な種類のフォームのうちの 1 つです。 フォームがダッシュボードかどうかは、`SystemForm.Type` または `UserForm.Type` 属性を使用して確認できます。 フォームの種類がダッシュボードの場合は、プロパティ値が "0" になっています。  

 フォーム コンテンツとプレゼンテーションの定義は、FormXML 内に格納されます。 詳細: [フォーム XML スキーマ](form-xml-schema.md)  

 さまざまな種類のダッシュボードの FormXML 文字列の例については、「[サンプル ダッシュボード](sample-dashboards.md)」を参照してください。  

<a name="DashboardComponents"></a>   
## <a name="dashboard-components"></a>ダッシュボードのコンポーネント  
 ダッシュボードには、グラフ、グリッド、IFRAME、または Web リソースを含めることができます。 既定では、1 つのダッシュボードにこれらのコンポーネントを最大で 6 つ含めることができます。  

<!-- In the [!INCLUDE[pn_dynamics_crm](../../includes/pn-dynamics-crm.md)] on-premises version, you can change the number of components to be displayed on a dashboard using [!INCLUDE[pn_PowerShell](../../includes/pn-powershell.md)]. More information: [Set the Number of Dashboard Controls](understand-dashboards-dashboard-components-formxml.md#set_controls_limit)-->

<!--[!INCLUDE[cc_sdk_onpremises_note](../../includes/cc-sdk-onpremises-note.md)]-->

### <a name="charts"></a>グラフ  
 組織所有のダッシュボードには、組織所有のグラフのみを含めることができます。 ただし、ユーザー所有のダッシュボードには、ユーザー所有のグラフと組織所有のグラフを含めることができます。 詳細: [モデル駆動型アプリにおけるグラフ (ビジュアル化)](view-data-with-visualizations-charts.md)  

### <a name="grids"></a>グリッド  
 モデル駆動型アプリにおけるグリッドは、クエリ (ビュー) からデータをフェッチします。 組織所有のダッシュボードには、保存済みのクエリからデータをフェッチするグリッドのみを含めることができます。 ただし、ユーザー所有のダッシュボードには、ユーザー クエリと保存済みクエリからデータをフェッチするグリッドを含めることができます。 詳細: [SavedQuery エンティティ](../common-data-service/reference/entities/savedquery.md) 

### <a name="iframes"></a>IFRAME  
 IFRAME を組織所有のダッシュボードに追加する際には、クロスフレーム スクリプトを制限するか、または許可するかを指定できます。 これを行うには、FormXML 内の IFRAME コントロールで `<Security>` パラメーターを使用する必要があります。 ただし、ユーザー所有のダッシュボードについては、IFRAME のクロスフレーム スクリプトは制限され、これを変更することはできません。 クロスフレーム スクリプトが有効化された IFRAME を含むユーザー所有ダッシュボードを作成しようとすると、エラー メッセージが表示されます。  

### <a name="web-resources"></a>Web リソース  
 ダッシュボードには、フォーム対応の Web リソースのみを含めることができます。 この制限は Web アプリケーション内でダッシュボード デザイナーを使用して Web リソースを追加する際に適用されますが、SDK を使用してダッシュボードに Web リソースを追加する際には、このような制限は適用されません。 詳細: [モデル駆動型アプリの Web リソース](web-resources.md)

<a name="DashboardComponentsandFormXML"></a>   
## <a name="dashboard-components-and-formxml-elements"></a>ダッシュボード コンポーネントと FormXML 要素  
 ダッシュボード コンポーネントは FormXML で指定された値に基づいてモデル駆動型アプリに表示されます。 次の画像は、ダッシュボードの例を示しています。 各ダッシュボードには、複数のタブを含めることができます。 タブとは、ダッシュボードの本文を分割する垂直スタックで、展開したり閉じたりすることができます。 タブには、複数のセクションを含めることができます。 セクションを使用すると、ダッシュボード コンポーネントをグループ化およびレイアウトできます。 

 <!-- TODO: image not found ![Dashboard components layout](../media/crm-v5s-dashboards-components.png "Dashboard components layout")   -->

<a name="SupportedFormXMLElements"></a>   
## <a name="formxml-elements-supported-for-dashboards"></a>ダッシュボード用にサポートされている FormXML 要素  
 ダッシュボードはフォームの一種ですが、すべての FormXML 要素と属性がダッシュボードによってサポートされるわけではありません。 次の表は、ダッシュボードによってサポートされる FormXML 要素、下位要素、および属性に関する情報をまとめたものです。

 さまざまな種類のダッシュボードの FormXML の例については、「[サンプル ダッシュボード](sample-dashboards.md)」を参照してください。  


|    Element     |                                                                                                                                                                                                                          下位要素                                                                                                                                                                                                                          |                                          要素属性                                          |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
|    `<form>`    |                                                                                                                                                                                                                             `<tabs>`                                                                                                                                                                                                                             |                                                  -                                                   |
|    `<tabs>`    |                                                                                                                                                                                                                             `<tab>`                                                                                                                                                                                                                              |                                                  -                                                   |
|    `<tab>`     |                                                                                                                                                                                                               -   `<labels>`<br />-   `<columns>`                                                                                                                                                                                                                | -   ID<br />-   名前<br />-   展開<br />-   verticallayout<br />-   showlabel<br />-   locklevel |
|   `<labels>`   |                                                                                                                                                                                                                            `<label>`                                                                                                                                                                                                                             |                                                  -                                                   |
|   `<label>`    |                                                                                                                                                                                                                                -                                                                                                                                                                                                                                 |                                -   説明<br />-   languagecode                                 |
|  `<columns>`   |                                                                                                                                                                                                                            `<column>`                                                                                                                                                                                                                            |                                                  -                                                   |
|   `<column>`   |                                                                                                                                                                                                                           `<sections>`                                                                                                                                                                                                                           |                                                width                                                 |
|  `<sections>`  |                                                                                                                                                                                                                           `<section>`                                                                                                                                                                                                                            |                                               addedby                                                |
|  `<section>`   |                                                                                                                                                                                                                 -   `<labels>`<br />-   `<rows>`                                                                                                                                                                                                                 |              -   ID<br />-   名前<br />-   showlabel<br />-   showbar<br />-   列               |
|    `<rows>`    |                                                                                                                                                                                                                             `<row>`                                                                                                                                                                                                                              |                                               addedby                                                |
|    `<row>`     |                                                                                                                                                                                                                             `<cell>`                                                                                                                                                                                                                             |                                               addedby                                                |
|    `<cell>`    |                                                                                                                                                                                                               -   `<labels>`<br />-   `<control>`                                                                                                                                                                                                                |      -   自動<br />-   addedby<br />-   ID<br />-   showlabel<br />-   rowspan<br />-   colspan      |
|  `<control>`   |                                                                                                                                                                                                                          `<parameters>`                                                                                                                                                                                                                          |                                       -   id<br />-   classid                                        |
| `<parameters>` | -   `<Url>`<br />-  `<PassParameters>`<br />-   `<Security>`<br />-   `<Scrolling>`<br />-   `<Border>`<br />-   `<ViewIds>`<br />-   `<ViewId>`<br />-   `<IsUserView>`<br />-   `<IsUserChart>`<br />-   `<TargetEntityType>`<br />-   `<AutoExpand>`<br />-   `<RecordsPerPage>`<br />-   `<EnableQuickFind>`<br />-   `<EnableJumpBar>`<br />-   `<EnableChartPicker>`<br />-   `<EnableViewPicker>`<br />-   `<ChartGridMode>`<br />-   `<VisualizationId>` |                                                  -                                                   |

<a name="set_controls_limit"></a>   
## <a name="set-the-number-of-dashboard-controls"></a>ダッシュボード コントロール数の設定  
 ここに示すように Windows PowerShell を使用してダッシュボード コントロールの数を調整できます。 最大値は 20 です。  

#### <a name="to-retrieve-and-set-the-dashboard-limit"></a>ダッシュボード制限の取得と設定  

1. Windows PowerShell のコマンド ウィンドウを開きます。  

2. モデル駆動型アプリの Windows PowerShell スナップインを追加します:  

   ```powershell  
   Add-PSSnapin Microsoft.Crm.PowerShell  
   ```  

3. 現在の設定を取得します。  

   ```powershell  
   $setting = Get-CrmSetting -SettingType DashboardSettings  
   ```  

4. 現在の設定を変更します。  

   ```powershell  
   $setting.MaximumControlsLimit = 5  
   ```  

   ```powershell  
   Set-CrmSetting -Setting $setting  
   ```  

### <a name="see-also"></a>関連項目  
 [ダッシュボード](analyze-data-with-dashboards.md)   
 [ダッシュボードに対するアクション](actions-dashboards.md)   
 [ダッシュボードの作成](create-dashboard.md)   
