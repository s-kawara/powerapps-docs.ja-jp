---
title: 'グラフの理解: 基盤となるデータとグラフ表現 (モデル駆動型アプリ) | Microsoftのドキュメント'
description: グラフには、水平 (x) と垂直 (y) の 2 つの軸にテキスト値をマップすることでデータが視覚的に表示されます。 x 軸はカテゴリ軸と呼ばれ、y 軸は系列軸と呼ばれます。
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
# <a name="understand-charts-underlying-data-and-chart-representation"></a>グラフの理解: 基盤となるデータとグラフ表現

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/understand-charts-underlying-data-chart-representation -->

グラフには、水平 (x) と垂直 (y) の 2 つの軸にテキスト値をマップすることでデータが視覚的に表示されます。 x 軸は *カテゴリ* 軸と呼ばれ、y 軸は *series* 軸と呼ばれます。 カテゴリ軸には数値と数値以外を表示できますが、系列軸には数値のみ表示されます。  
  
 モデル駆動形アプリにおいて、グラフはさらに次のように分類できます。  
  
- **単一系列グラフ**: 単一の系列 (y) 値が単一のカテゴリ (x) 値にマップされたデータを表示するグラフ。  
  
- **複数系列グラフ**: 複数の系列値が単一のカテゴリ値にマップされたデータを表示するグラフ。 複数系列グラフには、積み上げ縦棒グラフ (全カテゴリ合計に対する各系列の貢献度を垂直方向に表示) と 100% 積み上げ縦棒グラフ (全カテゴリ合計に対する各系列の貢献率を比較) があります。 たとえば、縦棒グラフと横棒グラフ、棒グラフと折れ線グラフなど、複数系列グラフの、互換性のある別の種類のグラフと結合できます。  
  
> [!NOTE]
>  複数カテゴリ グラフは、Web アプリケーションで、またはここで説明するように XML 文字列を変更することで作成できます。  
  
 モデル駆動形アプリで SDK を使用してグラフを作成する際には、次の 2 つの要点を考慮する必要があります。  
  
- **グラフの基になるデータ**: *データ記述* XML 文字列を使用して指定します。  
  
- **データ表現 (外観)**: *プレゼンテーション記述* XML 文字列を使用してデータ プレゼンテーションを指定します。  
  
> [!NOTE]
> Microsoft Chart Controls を用いると、縦棒グラフ、横棒グラフ、面積グラフ、折れ線グラフ、円グラフ、じょうごグラフ、バブル チャート、レーダー チャートなど様々な種類のグラフを作成できます。 モデル駆動形アプリのグラフ デザイナーでは特定の種類のグラフのみを作成できます。 ただし SDK を用いることにより Microsoft Chart Controls でサポートされているほとんどの種類のグラフを作成できます。  
  
## <a name="use-the-data-description-xml-string-to-specify-chart-data"></a>データ記述 XML 文字列を使用してグラフ データを指定する  
 データ記述 XML 文字列は、グラフに表示されるデータを定義します。 XML 文字列のコンテンツは、ビジュアル化データ記述スキーマに照らして検証されます。 スキーマの詳細については、「[ビジュアル化データ記述スキーマ](visualization-data-description-schema.md)」を参照してください。  
  
 グラフを作成する際に、組織所有のグラフまたはユーザー所有のグラフでそれぞれ `SavedQueryVisualization.DataDescription` 属性と `UserQueryVisualization.DataDescription` 属性を使用してデータ記述 XML 文字列を指定できます。  
  
 データ記述 XML 文字列には、`<FetchCollection>` および `<CategoryCollection>` という 2 つの要素が含まれます。  
  
### <a name="the-fetchcollection-element"></a>\<FetchCollection> 要素 
 
 `<FetchCollection>` 要素は、FetchXML を使用してグラフのデータを取得します。 FetchXML クエリは、グラフに表示するデータのエンティティ属性、集計関数、およびグループ化句に関する情報を指定します。 すべての FetchXML 集計関数がグラフでサポートされます。 FetchXML の集計機能に関する詳細については、 [FetchXML 集計を使う](../common-data-service/use-fetchxml-aggregation.md) を参照してください。  
  
 FetchXML クエリでは、データをフィルター処理できます。 また、フィルターはビュー経由でもグラフに適用されます。 したがって、フィルター条件が `<FetchCollection>` 要素の FetchXML クエリで既に指定されており、追加のフィルターがビュー経由で適用される場合、グラフには、すべてのフィルターの適用後に返されたデータが表示されます。 FetchXML クエリでデータをフィルターする詳細な方法に関しては、 [クエリの構築に FetchXML を使用する](../common-data-service/use-fetchxml-construct-query.md)を参照してください。  
  
> [!NOTE]
>  データ記述 XML 文字列はビジュアル化データ記述スキーマに照らして検証されますが、`<FetchCollection>` 要素内の FetchXML クエリはこのスキーマに照らして検証されません。 FetchXML クエリは、FetchXML スキーマに照らして検証されます。 詳細については [FetchXML スキーマ](../common-data-service/fetchxml-schema.md) を参照してください。  
  
 グラフが比較グラフの場合、`<FetchCollection>` 要素には 2 つの*グループ化*句が含まれます。  
  
### <a name="the-categorycollection-element"></a>\<CategoryCollection> 要素  
 `<CategoryCollection>` 要素には、グラフのカテゴリ (水平) 軸と系列 (垂直) 軸に関する情報が含まれます。  
  
-   各 `<Category>` サブ要素には、プレゼンテーション記述 XML 内の `<MeasureCollection>` 要素にマップされる `<Series>` という子要素があります。 単一系列グラフには単一の `<MeasureCollection>` 子要素があり、複数系列グラフには複数の `<MeasureCollection>` 子要素があります。それぞれ、プレゼンテーション記述 XML の `<Series>` 要素にマップされます。  
  
-   各 `<MeasureCollection>` 子要素には、カテゴリ (水平) 軸の各値に対応する系列 (垂直) 軸値に対応する `<Measure>` という要素があります。  
  
### <a name="example"></a>例  
 データ記述 XML 文字列の例を次に示します。  
  
```xml  
<datadefinition>  
  <fetchcollection>  
    <fetch mapping="logical" count="10">  
      <entity name="opportunity">  
        <attribute name="estimatedvalue" />  
        <order attribute="estimatedvalue" descending="true" />  
      </entity>  
    </fetch>  
  </fetchcollection>  
  <categorycollection>  
    <category>  
      <measurecollection>  
        <measure alias="estimatedvalue" />  
      </measurecollection>  
    </category>  
  </categorycollection></datadefinition>  
```  
  
 データ記述 XML 文字列のその他の例については、「[サンプル グラフ](sample-charts.md)」を参照してください。  
  
## <a name="use-the-presentation-description-xml-string-to-specify-data-representation"></a>プレゼンテーション記述 XML 文字列を使用してデータ プレゼンテーションを指定する  
 プレゼンテーション記述 XML 文字列には、グラフ タイトル、グラフの色、グラフの種類 (横棒、縦棒、折れ線など) など、グラフの外観に関する情報が含まれます。 この XML 文字列に対するスキーマ定義はありません。 ただし XML はシリアル化された Microsoft Chart Controls における [Chart](https://msdn.microsoft.com/library/system.web.ui.datavisualization.charting.chart.aspx) class です。 詳細: [グラフ コントロール](http://go.microsoft.com/fwlink/p/?LinkId=128301)  
  
 グラフを作成する際に、組織所有のグラフまたはユーザー所有のグラフでそれぞれ `SavedQueryVisualization.PresentationDescription` 属性と `UserQueryVisualization.PresentationDescription` 属性を使用してプレゼンテーション記述 XML 文字列を指定できます。  
  
### <a name="example"></a>例  
 プレゼンテーション記述 XML 文字列の例を次に示します。  
  
```xml  
<Chart Palette="BrightPastel">  
  <Series>  
    <Series _Template_="All" Color="153, 204, 255" BorderColor="164, 164, 164" BorderDashStyle="Solid" BorderWidth="1" ShadowColor="128, 128, 128, 128" ShadowOffset="1" IsValueShownAsLabel="true" Font="{0}, 6.75pt" BackGradientStyle="TopBottom" BackSecondaryColor="0, 102, 153" LabelForeColor="100, 100, 100" ChartType="Column">  
      <SmartLabelStyle Enabled="True" />  
      <Points />  
    </Series>  
  </Series>  
  <ChartAreas>  
    <ChartArea _Template_="All" BackColor="White" BorderColor="26, 59, 105" BorderWidth="0" BorderDashStyle="Solid">      <AxisY LineColor="204, 204, 204" TitleFont="{0}, 8pt, GdiCharSet=0" TitleForeColor="100, 100, 100" LabelAutoFitMaxFontSize="7" LabelAutoFitMinFontSize="7">  
        <MajorTickMark LineColor="Gray" />  
        <MajorGrid Enabled="false" />  
        <LabelStyle Font="{0}, 6.75pt, GdiCharSet=0" ForeColor="100, 100, 100" />  
      </AxisY>  
      <AxisX LineColor="204, 204, 204" TitleFont="{0}, 8pt, GdiCharSet=0" TitleForeColor="100, 100, 100" LabelAutoFitMaxFontSize="7" LabelAutoFitMinFontSize="7">        <MajorTickMark LineColor="Gray" />        <MajorGrid Enabled="false" />  
        <LabelStyle Font="{0}, 6.75pt, GdiCharSet=0" ForeColor="100, 100, 100" />  
      </AxisX>  
    </ChartArea>  
  </ChartAreas>  
  <Titles>  
    <Title _Template_="All" Font="{0}, 9pt, style=Bold, GdiCharSet=0" ForeColor="100, 100, 100"></Title>  
  </Titles>  
  <BorderSkin PageColor="Control" BackColor="CornflowerBlue" BackSecondaryColor="CornflowerBlue" />  
</Chart>  
```  
  
 プレゼンテーション記述 XML 文字列のその他の例については、「[サンプル グラフ](sample-charts.md)」を参照してください。  
  
### <a name="see-also"></a>関連項目  
 [ビジュアル化 (グラフ)](view-data-with-visualizations-charts.md)   
 [ビジュアル化に対するアクション (グラフ)](actions-visualizations-charts.md)   
 [グラフの作成](create-visualization-chart.md)   
 [FetchXML の使用によるクエリの作成](../common-data-service/use-fetchxml-construct-query.md)   
 [FetchXML スキーマ](../common-data-service/fetchxml-schema.md) [ビジュアル化データ記述スキーマ](visualization-data-description-schema.md)   
 [サンプル グラフ](sample-charts.md)   
 [Chart クラス (Microsoft Chart Controls)](https://msdn.microsoft.com/library/system.web.ui.datavisualization.charting.chart.aspx)
