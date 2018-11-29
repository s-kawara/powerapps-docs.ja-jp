---
title: ビジュアル化を使用したデータの表示 (グラフ) (モデル駆動型アプリ) | MicrosoftDocs
description: ビジュアル化を使用すると、ビジネス データを視覚的に表示することができます。 ビジュアル化は、アプリ用 Common Data Services のエンティティに添付されます。 複数のビジュアル化を1つのエンティティに添付できますが、1つのビジュアル化だけグリッドの横で一度に表示できます。 ダッシュボードを使用すると、同時に複数のビジュアル化を表示できます。
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
# <a name="view-data-with-visualizations-charts"></a>ビジュアル化を使用したデータの表示 (グラフ)

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/view-data-with-visualizations-charts -->


ビジュアル化を使用すると、ビジネス データを視覚的に表示することができます。 ビジュアル化は、アプリ用 Common Data Services のエンティティに添付されます。 複数のビジュアル化を1つのエンティティに添付できますが、1つのビジュアル化だけグリッドの横で一度に表示できます。 ダッシュボードを使用すると、同時に複数のビジュアル化を表示できます。 詳細情報: [ダッシュボードによるデータの分析](analyze-data-with-dashboards.md)  
  
 アプリ用 CDS ではグラフまたは Web リソースをビジュアル化として使用できます。 グラフの場合、モデル駆動型アプリのグラフ デザイナーを使用できます。 ただし、ビジュアル化で Web リソースを使用するには、SDK を使用するか、カスタム ビジュアル化 XML を モデル駆動型アプリにインポートする必要があります。
  
<a name="VisualizationTypes"></a>   
## <a name="visualization-ownership"></a>ビジュアル化の所有権  
 モデル駆動型アプリには、組織所有とユーザー所有の 2 種類のビジュアル化の所有権があります。  
  
- 組織所有のビジュアル化は組織が所有し、割り当てや共有を行うことはできません。 `SavedQueryVisualization` エンティティは組織所有のビジュアル化を表します。 このようなビジュアル化は、モデル駆動型アプリのソリューション対応のエンティティです。 保存されたクエリ ビジュアル化を更新するときは、<xref:Microsoft.Crm.Sdk.Messages.PublishAllXmlRequest> メッセージを使用して変更内容を公開し、組織全体で更新を使用できるようにする必要があります。 このエンティティは、モデル駆動型アプリの Web アプリケーションでは*システム グラフ*と呼ばれます。  
  
- ユーザー所有のビジュアル化は個々のユーザーが所有し、他のユーザーやチームとの間で割り当てや共有を行うことができます。 `UserQueryVisualization` エンティティはユーザー所有のビジュアル化を表します。 このエンティティは、モデル駆動型アプリの Web アプリケーションでは*ユーザー グラフ*と呼ばれ、グラフのドロップダウン リストで**自分のグラフ**の下に表示されます。  
  
  ユーザー クエリ ビジュアル化は、エンティティ名に反してユーザー クエリ (ビュー) には添付できません。 このエンティティのビューの部分は、フィルター条件の設定のみに使用されます。  
  
<a name="Charts"></a>   
## <a name="chart-visualizations"></a>グラフのビジュアル化  
 グラフを使用して、グリッド データの概要を表示できます。 グラフは、Microsoft Chart Controls for Microsoft .NET Framework 3.5 を使用して構築されます。 Microsoft Chart Controls の詳細については、[ダウンロード: .NET Framework のグラフ コントロール](http://go.microsoft.com/fwlink/p/?LinkId=128852) を参照してください。  
  
 これらのグラフは、Web アプリケーションでグリッドと統合されます。 フィルター (クエリ) をグリッドのデータに適用すると、フィルターはグラフにも適用され、それに応じてグラフが更新されます。 同様に、グラフに対してドリルダウン操作を実行すると、グリッド データが自動的に更新されます。  
  
 エンティティに添付されているグラフは、そのエンティティのすべてのビューで使用できます。 グラフに表示されるデータは、エンティティの現在選択されている (表示されている) ビューに対応します。 グラフには、保存されたクエリ (組織所有のビュー) とユーザー クエリ (ユーザー所有のビュー) 両方のデータを表示できます。  
  
 グラフに表示されるデータは、保存されたクエリ (組織所有のビュー) で、FetchXML (`SavedQuery.FetchXml` 属性) を使用してレコードをフィルター処理しているもののみです。 保存されたクエリが、クエリ API (`SavedQuery.QueryAPI` 属性) を使用してレコードをフィルター処理している場合、その保存されたクエリのグラフは表示されません。 この制約はユーザー クエリ (ユーザー所有のビュー) には適用されません。ユーザー クエリ エンティティは、レコードのフィルター処理のために `QueryAPI` 属性を使用しないためです。  
  
 グラフの操作の詳細については、「[グラフの詳細: 基盤となるデータとグラフ表現](understand-charts-underlying-data-chart-representation.md)」を参照してください。  
  
<a name="ChartTypes"></a>   
### <a name="chart-types-in-microsoft-chart-controls"></a>Microsoft グラフ コントロールのグラフの種類  
 Microsoft Chart Controls はモデル駆動型アプリでグラフを構築するために使用されます。 Microsoft Chart Controls では、縦棒グラフ、横棒グラフ、面グラフ、積み上げ棒グラフ、折れ線グラフ、バブル チャート、円グラフなどさまざまな種類のグラフを作成できます。  
  
 アプリ用 CDS で標準的に使用できるグラフの種類は、*縦棒グラフ*、*面グラフ*、*横棒グラフ*、*折れ線グラフ*、*円グラフ*、*じょうご*グラフです。 ただし、データ記述とプレゼンテーション記述のための XML 文字列に、グラフに対応する適切な内容を指定することにより、多系列グラフ、積み上げ棒グラフ、および 100% 積み上げ (比較) グラフなどの、サポートされている他の Microsoft Chart Controls のグラフの種類を作成することで、機能を拡張することができます。 詳細: [グラフ データの指定](understand-charts-underlying-data-chart-representation.md)  
  
<a name="WebResources"></a>   
## <a name="web-resource-visualizations"></a>Web リソースのビジュアル化  
 Web リソースはモデル駆動型アプリ データベースに格納される仮想ファイルであり、固有の URL アドレスを使用して取得できます。 既存の Web リソースをビジュアル化として表示できます。エンティティの他のグラフと一緒に、モデル駆動型アプリの**グラフ**領域に表示されます。 Web リソースに関する詳細については、[モデル駆動型アプリの Web リソース](web-resources.md) を参照してください。  
  
 ビジュアル化では次の種類の Web リソースを使用できます: [Webpage (HTML) の Web リソース](webpage-html-web-resources.md) および [画像 (JPG、PNG、GIF、ICO) Web リソース](image-web-resources.md)。 Web リソースでビジュアル化を作成する方法の詳細については、[Web リソース ビジュアル化の作成](create-visualization-chart.md#create-a-web-resource-visualization) を参照してください。  
  
<a name="SupportedVisualizationEntities"></a>   
## <a name="entities-supported-for-visualizations"></a>ビジュアル化がサポートされているエンティティ  
 ビジュアル化を作成および添付できるのは、新しいリボン インターフェイスをサポートするアプリ用 CDS のエンティティに限られます。 これは、すべてのグラフ コントロールがアプリ用 CDS のリボン インターフェイスにのみ表示されるためです。 ユーザー定義エンティティもビジュアル化でサポートされています。 必要であれば、ユーザー定義エンティティでのビジュアル化のサポートを無効にすることができます。 ただし、既定のエンティティではビジュアル化のサポートを無効にすることはできません。  
  
 以下は、ビジュアル化でサポートされている既定エンティティの一覧です。  
  
 Account  
ActivityPointer  
予定​​  
BulkOperation  
キャンペーン   
CampaignActivity  
CampaignResponse  
競合企業  
つながり   
取引先担当者   
契約   
電子メールの送信  
権利  
EntitlementChannel  
EntitlementTemplateChannel  
FAX   
目標   
GoalRollupQuery  
インシデント  
請求書   
InvoiceDetail  
KbArticle  
リード​​  
レター   
一覧取得  
メールボックス  
指標  
営業案件​​  
OpportunityProduct  
PhoneCall  
ポジション  
PriceLevel  
製品   
ProductAssociation  
ProductSubstitute  
QueueItem  
見積もり   
QuoteDetail  
RecurringAppointmentMaster  
レポート   
SalesLiterature  
受注  
SalesOrderDetail  
Service  
ServiceAppointment  
SLAKPIInstance  
ソーシャル活動  
SocialProfile  
SystemUser  
タスク  
チーム  
担当地域  
UoMSchedule  
  
### <a name="see-also"></a>関連項目  
 [データのグラフ化と分析](customize-visualizations-dashboards.md)   
 [グラフ データの指定](understand-charts-underlying-data-chart-representation.md)   
 [グラフ上のアクション](actions-visualizations-charts.md)   
 [グラフの作成](create-visualization-chart.md)   
 [サンプル グラフ](sample-charts.md)   
 [SavedQueryVisualization エンティティ](../common-data-service/reference/entities/savedqueryvisualization.md)   
 [UserQueryVisualization エンティティ](../common-data-service/reference/entities/userqueryvisualization.md) [ダウンロード: .NET Framework 言語パック用 Chart Controls](http://www.microsoft.com/downloads/details.aspx?FamilyId=581FF4E3-749F-4454-A5E3-DE4C463143BD&displaylang=en)   
 [ダウンロード: Visual Studio 用 Chart Controls アドオン](http://www.microsoft.com/downloads/details.aspx?FamilyId=1D69CE13-E1E5-4315-825C-F14D33A303E9&displaylang=en)   
 [ダウンロード: .NET Framework ドキュメント用 Chart Controls](http://go.microsoft.com/fwlink/p/?LinkId=128301)   
 [Microsoft Chart Controls 用サンプル環境](http://code.msdn.microsoft.com/mschart)   
 [Chart Controls フォーラム](http://go.microsoft.com/fwlink/p/?LinkId=128713)
