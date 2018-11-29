---
title: サンプル グラフ (モデル駆動型アプリ) | MicrosoftDocs
description: このトピックには、サンプル グラフと、個々のデータ記述、およびプレゼンテーション XML 文字列が含まれています。
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
# <a name="sample-charts"></a>サンプル グラフ

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/sample-charts -->

このトピックには、サンプル グラフと、個々のデータ記述、およびプレゼンテーション XML 文字列が含まれています。 次の指定が可能です。  
  
-   組織所有またはユーザー所有のグラフの `SavedQueryVisualization.DataDescription` または `UserQueryVisualization.DataDescription` 属性を使用して、グラフの*データ記述 XML 文字列*を個々に指定する。  
  
-   組織所有またはユーザー所有のグラフの `SavedQueryVisualization.PresentationDescription` または`UserQueryVisualization. PresentationDescription` 属性を使用して、グラフの*プレゼンテーション記述 XML 文字列*を個々に指定する。  
  
<a name="ColumnChart"></a>   
## <a name="column-chart"></a>縦棒グラフ  
 次に示すのは、業種別の取引先企業を表示する縦棒グラフです。 モデル駆動型アプリで `Account` エンティティに使用できる既存の "業種別取引先企業" 既定グラフのプレゼンテーション記述を変更して、グラフを縦棒グラフに変更しました。  
  
 ![縦棒グラフのサンプル: 業種別取引先企業](media/charts-accounts-by-industry.gif "縦棒グラフのサンプル: 業種別取引先企業")  
  
### <a name="data-description"></a>データ記述  
 次に示すのは、このグラフのデータ記述 XML 文字列の内容です。  
  
```xml  
<datadefinition>  
  <fetchcollection>  
    <fetch mapping="logical" aggregate="true">  
      <entity name="account">  
        <attribute groupby="true" alias="groupby_column" name="industrycode" />  
        <attribute alias="aggregate_column" name="name" aggregate="count" />  
      </entity>  
    </fetch>  
  </fetchcollection>  
  <categorycollection>  
    <category>  
      <measurecollection>  
        <measure alias="aggregate_column" />  
      </measurecollection>  
    </category>  
  </categorycollection>  
</datadefinition>  
  
```  
  
### <a name="presentation-description"></a>プレゼンテーション記述  
 次に示すのは、このグラフのプレゼンテーション記述 XML 文字列の内容です。  
  
```xml  
<Chart>  
  <Series>  
    <Series ChartType="Column" IsValueShownAsLabel="True" Color="149, 189, 66" BackGradientStyle="TopBottom" BackSecondaryColor="112, 142, 50" Font="{0}, 9.5px" LabelForeColor="59, 59, 59" CustomProperties="MinPixelPointWidth=5, PointWidth=0.75, MaxPixelPointWidth=40">  
      <SmartLabelStyle Enabled="True" />  
    </Series>  
  </Series>  
  <ChartAreas>  
    <ChartArea BorderColor="White" BorderDashStyle="Solid">  
      <AxisY IsLabelAutoFit="False" TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181" IsReversed="False">  
        <MajorGrid LineColor="239, 242, 246" />  
        <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
      </AxisY>  
      <AxisX IsLabelAutoFit="True" TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181" IsReversed="False">  
        <MajorGrid Enabled="False" />  
        <MajorTickMark Enabled="False" />  
        <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
      </AxisX>  
    </ChartArea>  
  </ChartAreas>  
  <Titles>  
    <Title Name="Chart Title" DockingOffset="-3" Font="{0}, 13px" ForeColor="59, 59, 59" Alignment="TopLeft"></Title>  
  </Titles>  
</Chart>  
```  
  
<a name="BarChart"></a>   
## <a name="bar-chart"></a>横棒グラフ  
 次に示すのは、上位 10 件の顧客を表示する棒グラフです。 これは、MDA で `Opportunity` エンティティに使用できる既定のグラフの 1 つです。  
  
 ![横棒グラフのサンプル: 上位 10 件の顧客](media/charts-top-10-customers.gif "横棒グラフのサンプル: 上位 10 件の顧客")  
  
### <a name="data-description"></a>データ記述  
 次に示すのは、このグラフのデータ記述 XML 文字列の内容です。  
  
```xml  
<datadefinition>  
  <fetchcollection>  
    <fetch mapping="logical" count="10" aggregate="true">  
      <entity name="opportunity">  
        <attribute name="estimatedvalue" aggregate="sum" alias="sum_estimatedvalue" />  
        <attribute name="customerid" groupby="true" alias="customerid" />  
        <order alias="sum_estimatedvalue" descending="true" />  
      </entity>  
    </fetch>  
  </fetchcollection>  
  <categorycollection>  
    <category>  
      <measurecollection>  
        <measure alias="sum_estimatedvalue" />  
      </measurecollection>  
    </category>  
  </categorycollection>  
</datadefinition>  
  
```  
  
### <a name="presentation-description"></a>プレゼンテーション記述  
 次に示すのは、このグラフのプレゼンテーション記述 XML 文字列の内容です。  
  
```xml  
<Chart>  
  <Series>  
    <Series ChartType="Bar" IsValueShownAsLabel="True" Color="149, 189, 66" BackGradientStyle="TopBottom" BackSecondaryColor="112, 142, 50" Font="{0}, 9.5px" LabelForeColor="59, 59, 59" CustomProperties="MinPixelPointWidth=5, PointWidth=0.75, MaxPixelPointWidth=40">  
      <SmartLabelStyle Enabled="True" />  
    </Series>  
  </Series>  
  <ChartAreas>  
    <ChartArea BorderColor="White" BorderDashStyle="Solid">  
      <AxisY IsLabelAutoFit="False" TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181" IsReversed="False">  
        <MajorGrid LineColor="239, 242, 246" />  
        <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
      </AxisY>  
      <AxisX IsLabelAutoFit="False" TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181" IsReversed="False">  
        <MajorGrid Enabled="False" />  
        <MajorTickMark Enabled="False" />  
        <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
      </AxisX>  
    </ChartArea>  
  </ChartAreas>  
  <Titles>  
    <Title DockingOffset="-3" Font="{0}, 13px" ForeColor="59, 59, 59" Alignment="TopLeft"></Title>  
  </Titles>  
</Chart>  
```  
  
<a name="AreaChart"></a>   
## <a name="area-chart"></a>領域グラフ  
 次はに示すのは、特定の日付範囲の間に作成されたレコード数が示す領域グラフです。  
  
 ![領域グラフのサンプル](media/charts-count-of-records-areachart.gif "領域グラフのサンプル")  
  
### <a name="data-description"></a>データ記述  
 次に示すのは、このグラフのデータ記述 XML 文字列の内容です。  
  
```xml
<datadefinition>  
      <fetchcollection>  
        <fetch mapping="logical" aggregate="true">  
          <entity name="incident">  
            <attribute name="createdon" groupby="true" alias="_CRMAutoGen_groupby_column_Num_0" dategrouping="day" />  
            <attribute name="incidentid" aggregate="count" alias="_CRMAutoGen_aggregate_column_Num_0" />  
          </entity>  
        </fetch>  
      </fetchcollection>  
      <categorycollection>  
        <category alias="_CRMAutoGen_groupby_column_Num_0">  
          <measurecollection>  
            <measure alias="_CRMAutoGen_aggregate_column_Num_0" />  
          </measurecollection>  
        </category>  
      </categorycollection>  
    </datadefinition>   
```  
  
### <a name="presentation-description"></a>プレゼンテーション記述  
 次に示すのは、このグラフのプレゼンテーション記述 XML の内容です。  
  
```xml
<Chart Palette="None" PaletteCustomColors="149,189,66; 197,56,52; 55,118,193; 117,82,160; 49,171,204; 255,136,35; 168,203,104; 209,98,96; 97,142,206; 142,116,178; 93,186,215; 255,155,83">  
      <Series>  
        <Series ChartType="StackedArea" Font="{0}, 9.5px" LabelForeColor="59, 59, 59" CustomProperties="PointWidth=0.75, MaxPixelPointWidth=40" />  
      </Series>  
      <ChartAreas>  
        <ChartArea BorderColor="White" BorderDashStyle="Solid">  
          <AxisY LabelAutoFitMinFontSize="8" TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181" IntervalAutoMode="VariableCount">  
            <MajorGrid LineColor="239, 242, 246" />  
            <MajorTickMark LineColor="165, 172, 181" />  
            <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
          </AxisY>  
          <AxisX LabelAutoFitMinFontSize="8" TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181" IntervalAutoMode="VariableCount">  
            <MajorTickMark LineColor="165, 172, 181" />  
            <MajorGrid LineColor="Transparent" />  
            <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
          </AxisX>  
        </ChartArea>  
      </ChartAreas>  
      <Titles>  
        <Title Alignment="TopLeft" DockingOffset="-3" Font="{0}, 13px" ForeColor="59, 59, 59" />  
      </Titles>  
      <Legends>  
        <Legend Alignment="Center" LegendStyle="Table" Docking="right" IsEquallySpacedItems="True" Font="{0}, 11px" ShadowColor="0, 0, 0, 0" ForeColor="59, 59, 59" />  
      </Legends>  
    </Chart>  
```  
  
<a name="LineChart"></a>   
## <a name="line-chart"></a>折れ線グラフ  
 次に示すのは、過去 5 か月間に生成された潜在顧客の数を表す折れ線グラフです。 これは、MDA で `Lead` エンティティに使用できる既定のグラフの 1 つです。 
  
![折れ線グラフのサンプル: 潜在顧客の生成率折れ線グラフのサンプル](media/lead-generation-rate-chart.png "折れ線グラフのサンプル: 潜在顧客の生成率折れ線グラフのサンプル") --> 
  
### <a name="data-description"></a>データ記述  
 次に示すのは、このグラフのデータ記述 XML 文字列の内容です。  
  
```xml  
<datadefinition>  
  <fetchcollection>  
    <fetch mapping="logical" count="5" aggregate="true">  
      <entity name="lead">  
        <attribute name="leadid" aggregate="countcolumn" alias="count_leadid" />  
        <attribute name="createdon" groupby="true" dategrouping="month" usertimezone="false" alias="createdon" />  
        <order alias="createdon" descending="false" />  
      </entity>  
    </fetch>  
  </fetchcollection>  
  <categorycollection>  
    <category>  
      <measurecollection>  
        <measure alias="count_leadid" />  
      </measurecollection>  
    </category>  
  </categorycollection>  
</datadefinition>  
```  
  
### <a name="presentation-description"></a>プレゼンテーション記述  
 次に示すのは、このグラフのプレゼンテーション記述 XML 文字列の内容です。  
  
```xml  
<Chart>  
  <Series>  
    <Series IsValueShownAsLabel="True" BorderWidth="3" ChartType="Line" Color="49, 171, 204" MarkerStyle="Square" MarkerSize="9" MarkerColor="37, 128, 153"></Series>  
  </Series>  
  <ChartAreas>  
    <ChartArea BorderColor="White">  
      <AxisY LabelAutoFitMinFontSize="8" TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181">  
        <MajorGrid LineColor="239, 242, 230" />  
        <MajorTickMark LineColor="165, 172, 181" />  
        <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
      </AxisY>  
      <AxisX LabelAutoFitMinFontSize="8" TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181">  
        <MajorGrid Enabled="False" />  
        <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
      </AxisX>  
    </ChartArea>  
  </ChartAreas>  
  <Titles>  
    <Title DockingOffset="-3" Font="{0}, 13px" ForeColor="59, 59, 59" Alignment="TopLeft"></Title>  
  </Titles>  
</Chart>  
```  
  
<a name="PieChart"></a>   
## <a name="pie-chart"></a>円グラフ  
 次に示すのは、潜在顧客の総数とそれらの重要度を表す円グラフです。 これは、MDA で `Lead` エンティティに使用できる既定のグラフの 1 つです。  
  
 ![円グラフのサンプル: 評価別潜在顧客](media/leads-by-source-chart.png "円グラフのサンプル: 評価別潜在顧客")  
  
### <a name="data-description"></a>データ記述  
 次に示すのは、このグラフのデータ記述 XML 文字列の内容です。  
  
```xml  
<datadefinition>  
  <fetchcollection>  
    <fetch mapping="logical" aggregate="true">  
      <entity name="lead">  
        <attribute groupby="true" alias="groupby_column" name="leadqualitycode" />  
        <attribute alias="aggregate_column" name="fullname" aggregate="count" />  
      </entity>  
    </fetch>  
  </fetchcollection>  
  <categorycollection>  
    <category>  
      <measurecollection>  
        <measure alias="aggregate_column" />  
      </measurecollection>  
    </category>  
  </categorycollection>  
</datadefinition>  
  
```  
  
### <a name="presentation-description"></a>プレゼンテーション記述  
 次に示すのは、このグラフのプレゼンテーション記述 XML 文字列の内容です。  
  
```xml  
<Chart Palette="None" PaletteCustomColors="97,142,206; 209,98,96; 168,203,104; 142,116,178; 93,186,215; 255,155,83; 148,172,215; 217,148,147; 189,213,151; 173,158,196; 145,201,221; 255,180,138">  
  <Series>  
    <Series ShadowOffset="0" IsValueShownAsLabel="true" Font="{0}, 9.5px" LabelForeColor="59, 59, 59" CustomProperties="PieLabelStyle=Inside, PieDrawingStyle=Default" ChartType="pie">  
      <SmartLabelStyle Enabled="True" />  
    </Series>  
  </Series>  
  <ChartAreas>  
    <ChartArea>  
      <Area3DStyle Enable3D="false" />  
    </ChartArea>  
  </ChartAreas>  
  <Legends>  
    <Legend Alignment="Center" LegendStyle="Table" Docking="right" Font="{0}, 11px" ShadowColor="0, 0, 0, 0" ForeColor="59, 59, 59" />  
  </Legends>  
  <Titles>  
    <Title Alignment="TopLeft" DockingOffset="-3" Font="{0}, 13px" ForeColor="0, 0, 0"></Title>  
  </Titles>  
</Chart>  
```  
  
<a name="FunnelChart"></a>   
## <a name="funnel-chart"></a>じょうごグラフ  
 次に示すのは、営業パイプラインの各ステージでの売上見込み合計を表すじょうごグラフです。 これは、MDA で `Opportunity` エンティティに使用できる既定のグラフの 1 つです。  
  
 ![じょうごグラフのサンプル: 営業パイプライン](media/charts-sales-pipeline-chart.png "じょうごグラフのサンプル: 営業パイプライン")  
  
### <a name="data-description"></a>データ記述  
 次に示すのは、このグラフのデータ記述 XML 文字列の内容です。  
  
```xml  
<datadefinition>  
  <fetchcollection>  
    <fetch mapping="logical" count="10" aggregate="true">  
      <entity name="opportunity">  
        <attribute name="estimatedvalue" aggregate="sum" alias="sum_estimatedvalue" />  
        <attribute name="stepname" groupby="true" alias="stepname" />  
        <order alias="stepname" descending="false" />  
      </entity>  
    </fetch>  
  </fetchcollection>  
  <categorycollection>  
    <category>  
      <measurecollection>  
        <measure alias="sum_estimatedvalue" />  
      </measurecollection>  
    </category>  
  </categorycollection>  
</datadefinition>  
```  
  
### <a name="presentation-description"></a>プレゼンテーション記述  
 次に示すのは、このグラフのプレゼンテーション記述 XML 文字列の内容です。  
  
```xml  
<Chart Palette="None" PaletteCustomColors="55,118,193; 197,56,52; 149,189,66; 117,82,160; 49,171,204; 255,136,35; 97,142,206; 209,98,96; 168,203,104; 142,116,178; 93,186,215; 255,155,83">  
  <Series>  
    <Series ShadowOffset="0" IsValueShownAsLabel="true" Font="{0}, 9.5px" LabelForeColor="59, 59, 59" ChartType="Funnel" CustomProperties="FunnelLabelStyle=Outside, FunnelNeckHeight=0, FunnelPointGap=1, FunnelNeckWidth=5">  
      <SmartLabelStyle Enabled="True" />  
    </Series>  
  </Series>  
  <ChartAreas>  
    <ChartArea>  
      <Area3DStyle Enable3D="True" />  
    </ChartArea>  
  </ChartAreas>  
  <Legends>  
    <Legend Alignment="Center" LegendStyle="Table" Docking="right" Font="{0}, 11px" ShadowColor="0, 0, 0, 0" ForeColor="59, 59, 59" />  
  </Legends>  
  <Titles>  
    <Title Alignment="TopLeft" DockingOffset="-3" Font="Segeo UI, 13px" ForeColor="0, 0, 0"></Title>  
  </Titles>  
</Chart>  
```  
  
<a name="MultiSeriesChart"></a> 
  
## <a name="multi-series-chart"></a>複数系列グラフ  

 次に示すのは、月ごとの売上見込みと実売上の対比を示す複数系列グラフです。 MDA のグラフ デザイナー、または開発者ドキュメントに記載されているメソッドを使用して、これらの種類のグラフを作成できます。  
  
 複数系列グラフでは、データ記述に複数の `<measurecollection>` 要素が含まれ、そのそれぞれが、プレゼンテーション記述 XML 文字列内の対応する `<Series>` 要素にマッピングされています。  
  
 複数系列グラフでは、プレゼンテーション記述に複数の `<Series>` 要素が含まれます。`<Series>` 要素の数は、データ記述 XML 文字列内の `<measurecollection>` 要素の数と同じです。  
  
 ![複数系列グラフのサンプル](media/estimated-actual-revenue-chart.gif "複数系列グラフのサンプル")  
  
### <a name="data-description"></a>データ記述  
 次に示すのは、このグラフのデータ記述 XML 文字列の内容です。  
  
```xml  
<datadefinition>  
  <fetchcollection>  
    <fetch mapping="logical" aggregate="true">  
      <entity name="opportunity">  
        <attribute name="estimatedvalue" aggregate="sum" alias="estvalue" />  
        <attribute name="actualvalue" aggregate="sum" alias="actvalue" />  
        <attribute name="actualclosedate" groupby="true" alias="actclosedate" dategrouping="month" />  
      </entity>  
    </fetch>  
  </fetchcollection>  
  <categorycollection>  
    <category>  
      <measurecollection>  
        <measure alias="estvalue" />  
      </measurecollection>  
      <measurecollection>  
        <measure alias="actvalue" />  
      </measurecollection>  
    </category>  
  </categorycollection>  
</datadefinition>  
  
```  
  
### <a name="presentation-description"></a>プレゼンテーション記述  
 次に示すのは、このグラフのプレゼンテーション記述 XML 文字列の内容です。  
  
```xml  
<Chart Palette="BrightPastel">  
  <Series>  
    <Series _Template_="All" Color="112, 162, 213" BorderColor="164, 164, 164" BorderDashStyle="Solid" BorderWidth="1" ShadowColor="128, 128, 128, 128" ShadowOffset="1" IsValueShownAsLabel="true" Font="{0}, 6.75pt, GdiCharSet=0" BackGradientStyle="TopBottom" BackSecondaryColor="0, 102, 153" LabelForeColor="100, 100, 100" ChartType="Column">  
      <SmartLabelStyle Enabled="True" />  
      <Points />  
    </Series>  
    <Series _Template_="All" Color="204,0,0" BorderColor="204,0,0" BorderDashStyle="Solid" BorderWidth="1" ShadowColor="128, 128, 128, 128" ShadowOffset="1" IsValueShownAsLabel="true" Font="{0}, 6.75pt, GdiCharSet=0" BackSecondaryColor="0, 102, 153" LabelForeColor="100, 100, 100" ChartType="Column">  
      <SmartLabelStyle Enabled="True" />  
      <Points />  
    </Series>  
  </Series>  
  <ChartAreas>  
    <ChartArea _Template_="All" BackColor="White" BorderColor="26, 59, 105" BorderWidth="0" BorderDashStyle="Solid">  
      <AxisY LineColor="204, 204, 204" TitleFont="{0}, 8pt, GdiCharSet=0" TitleForeColor="100, 100, 100" LabelAutoFitMaxFontSize="7" LabelAutoFitMinFontSize="7">  
        <MajorTickMark LineColor="Gray" />  
        <MajorGrid Enabled="false" />  
        <LabelStyle Font="{0}, 6.75pt, GdiCharSet=0" ForeColor="100, 100, 100" />  
      </AxisY>  
      <AxisX LineColor="204, 204, 204" TitleFont="{0}, 8pt, GdiCharSet=0" TitleForeColor="100, 100, 100" LabelAutoFitMaxFontSize="7" LabelAutoFitMinFontSize="7">  
        <MajorTickMark LineColor="Gray" />  
        <MajorGrid Enabled="false" />  
        <LabelStyle Font="{0}, 6.75pt, GdiCharSet=0" ForeColor="100, 100, 100" />  
      </AxisX>  
      <Area3DStyle LightStyle="Realistic" IsClustered="True" />  
    </ChartArea>  
  </ChartAreas>  
  <Legends>  
    <Legend _Template_="All" Alignment="Center" LegendStyle="Table" Docking="Bottom" IsEquallySpacedItems="True" BackColor="White" BorderColor="228, 228, 228" BorderWidth="0" Font="{0}, 8pt, GdiCharSet=0" ShadowColor="0, 0, 0, 0" ForeColor="100, 100, 100"></Legend>  
  </Legends>  
  <Titles>  
    <Title _Template_="All" Font="{0}, 9pt, style=Bold, GdiCharSet=0" ForeColor="100, 100, 100"></Title>  
  </Titles>  
  <BorderSkin PageColor="Control" BackColor="CornflowerBlue" BackSecondaryColor="CornflowerBlue" />  
</Chart>  
  
```  
  
<a name="ComparisonChart"></a>   
## <a name="comparison-chart-stacked-chart"></a>比較グラフ (積み上げグラフ)  
 次に示すのは、活動の数を種類と重要度ごとに表す比較グラフです。 MDA のグラフ デザイナー、または開発者ドキュメントに記載されているメソッドを使用して、これらの種類のグラフを作成できます。  
  
 比較グラフには、データ記述 XML 内に 2 つの `groupby` 句があります。  
  
 ![比較グラフのサンプル](media/charts-activities-by-type-and-priority-comparison-chart.gif "比較グラフのサンプル")  
  
### <a name="data-description"></a>データ記述  
 次に示すのは、このグラフのデータ記述 XML 文字列の内容です。  
  
```xml  
<datadefinition>  
  <fetchcollection>  
    <fetch mapping="logical" aggregate="true">  
      <entity name="activitypointer">  
        <attribute alias="aggregate_column" name="subject" aggregate="count" />  
        <attribute groupby="true" alias="groupby_column" name="activitytypecode" />  
        <attribute groupby="true" alias="groupby_priority" name="prioritycode" />  
      </entity>  
    </fetch>  
  </fetchcollection>  
  <categorycollection>  
    <category>  
      <measurecollection>  
        <measure alias="aggregate_column" />  
      </measurecollection>  
    </category>  
  </categorycollection>  
</datadefinition>  
  
```  
  
### <a name="presentation-description"></a>プレゼンテーション記述  
 次に示すのは、このグラフのプレゼンテーション記述 XML 文字列の内容です。  
  
```xml  
<Chart Palette="None" PaletteCustomColors="41,88,145; 147, 42, 39; 112,142,50; 88,62,120; 37,128,153; 194,103,28; 74,107,155; 155,77,73; 126,153,79; 107,88,134; 71,140,162; 199,118,64; 112,131,162;164,112,111; 143,161,115;131,120,148;111,152,167; 195,137,106">  
  <Series>  
    <Series Name="Series1" ChartType="StackedColumn" ChartArea="ChartArea1" IsValueShownAsLabel="True" Font="{0}, 9.5px" LabelForeColor="59, 59, 59" CustomProperties="MinPixelPointWidth=5, PointWidth=0.75, PixelPointWidth=26, MaxPixelPointWidth=40"></Series>  
  </Series>  
  <ChartAreas>  
    <ChartArea BorderColor="Transparent" BorderDashStyle="Solid" Name="ChartArea1">  
      <AxisY TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181" IntervalAutoMode="VariableCount">  
        <MajorGrid LineColor="239, 242, 246" />  
        <MajorTickMark LineColor="165, 172, 181" />  
        <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
      </AxisY>  
      <AxisX TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181" IntervalAutoMode="VariableCount">  
        <MajorGrid LineColor="Transparent" />  
        <MajorTickMark LineDashStyle="NotSet" />  
        <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
      </AxisX>  
    </ChartArea>  
  </ChartAreas>  
  <Legends>  
    <Legend Alignment="Center" LegendStyle="Table" Docking="Bottom" IsEquallySpacedItems="True" Font="{0}, 11px" ShadowColor="0, 0, 0, 0" ForeColor="59,59,59"></Legend>  
  </Legends>  
  <Titles>  
    <Title Alignment="TopLeft" Name="Title1" DockingOffset="-3" Font="{0}, 13px" ForeColor="59, 59, 59"></Title>  
  </Titles>  
</Chart>  
  
```  
  
<a name="StackedChart"></a>   

## <a name="comparison-chart-100-stacked-chart"></a>比較グラフ (100% 積み上げグラフ)  

 次に示すのは、任意の日付に開かれたサポート案件の数を重要度ごとに表す比較グラフです。 MDA のグラフ デザイナー、または Web サービスで使用可能なメソッドを使用して、これらの種類のグラフを作成できます。  
  
 比較グラフには、データ記述 XML 内に 2 つの `groupby` 句があります。  
  
 ![100% 積み上げグラフのサンプル](media/charts-numberofcases-anydate-bypriority-100stackedchart.gif "100% 積み上げグラフのサンプル")  
  
### <a name="data-description"></a>データ記述  
 次に示すのは、このグラフのデータ記述 XML 文字列の内容です。  
  
```xml  
<datadefinition>  
      <fetchcollection>  
        <fetch mapping="logical" aggregate="true">  
          <entity name="incident">  
            <order alias="groupby_column" descending="false" />  
            <attribute alias="aggregate_column" name="incidentid" aggregate="count" />  
            <attribute groupby="true" alias="groupby_column" dategrouping="day" name="createdon" />  
            <attribute groupby="true" alias="groupby_priority" name="prioritycode" />  
          </entity>  
        </fetch>  
      </fetchcollection>  
      <categorycollection>  
        <category>  
          <measurecollection>  
            <measure alias="aggregate_column" />  
          </measurecollection>  
        </category>  
      </categorycollection>  
    </datadefinition>  
  
```  
  
### <a name="presentation-description"></a>プレゼンテーション記述  
 次に示すのは、このグラフのプレゼンテーション記述 XML 文字列の内容です。  
  
```xml  
<Chart Palette="None" PaletteCustomColors="149,189,66; 197,56,52; 55,118,193; 117,82,160; 49,171,204; 255,136,35; 168,203,104; 209,98,96; 97,142,206; 142,116,178; 93,186,215; 255,155,83">  
      <Series>  
        <Series ChartType="StackedBar100" Font="{0}, 9.5px" LabelForeColor="59, 59, 59" CustomProperties="PointWidth=0.75, MaxPixelPointWidth=40">  
          <SmartLabelStyle Enabled="True" />  
        </Series>  
      </Series>  
      <ChartAreas>  
        <ChartArea BorderColor="White" BorderDashStyle="Solid">  
          <AxisY LabelAutoFitMinFontSize="8" TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181" IntervalAutoMode="VariableCount">  
            <MajorGrid LineColor="239, 242, 246" />  
            <MajorTickMark LineColor="165, 172, 181" />  
            <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
          </AxisY>  
          <AxisX LabelAutoFitMinFontSize="8" TitleForeColor="59, 59, 59" TitleFont="{0}, 10.5px" LineColor="165, 172, 181" IntervalAutoMode="VariableCount">  
            <MajorGrid Enabled="False" />  
            <MajorTickMark Enabled="False" />  
            <LabelStyle Font="{0}, 10.5px" ForeColor="59, 59, 59" />  
          </AxisX>  
        </ChartArea>  
      </ChartAreas>  
      <Titles>  
        <Title Alignment="TopLeft" DockingOffset="-3" Font="{0}, 13px" ForeColor="0, 0, 0" />  
      </Titles>  
    </Chart>  
```  
  
### <a name="see-also"></a>関連項目  
 [データのビジュアル化および分析](customize-visualizations-dashboards.md)   
 [ビジュアル化データ記述スキーマ](visualization-data-description-schema.md)   
 [グラフの作成](create-visualization-chart.md)   
 [ビジュアル化を使用したデータの表示 (グラフ)](view-data-with-visualizations-charts.md)   
 [グラフのサンプル コード (ビジュアル化)](/dynamics365/customer-engagement/developer/customize-dev/sample-code-charts-visualizations)

