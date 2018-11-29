---
title: ダッシュボードを作成する (モデル駆動型アプリ) | MicrosoftDocs
description: 組織所有のダッシュボードは、アプリ用 Common Data Service Webサービス (SDK) を使用するか、customizations.xml ファイルを編集して アプリ用 Common Data Service でエンティティ フォームをカスタマイズすることで作成できます。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: da41f997-1f61-7ea8-db83-5d670d708d67
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

# <a name="create-a-dashboard"></a>ダッシュボードを作成する

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/create-dashboard -->

組織所有のダッシュボードは、アプリ用 Common Data Service を使用するか、customizations.xml ファイルを編集して アプリ用 Common Data Service でエンティティ フォームをカスタマイズすることで作成できます。  
  
> [!NOTE]
>  SDK を使用して、またはエンティティ フォームをカスタマイズして作成される一部のダッシュボードは、Web アプリケーションのダッシュボード デザイナーではサポートされません。 詳細については、このトピックの後半の [制限: SDKを使用するかまたはフォーム カスタマイズによってダッシュボードを作成](#Limitations) を参照してください。  
  
 ダッシュボードを作成する前に、次の項目を検討します。  
  
- **ダッシュボードの種類**: ダッシュボードを組織全体で利用できるようにし、より詳細なレベルでのアクセス レベル管理を行わない場合は、通常、組織所有のダッシュボードを作成します。 ただし、ダッシュボードのアクセス特権やセキュリティについて考慮する必要がある場合は、アクセスするユーザーをより厳密に制御できる、ユーザー所有のダッシュボードの作成を検討してください。  
  
     組織所有のダッシュボードを作成するには、システム管理者ロールまたはシステム カスタマイザー ロールが必要です。  
  
- **ダッシュボードのレイアウト**: ダッシュボードを作成する場合は、FormXML を使用して、ダッシュボード コンポーネントとレイアウトを定義する必要があります。 ダッシュボードを定義するための FormXML の操作については、「[ダッシュボードコンポーネントおよび FormXML要素](understand-dashboards-dashboard-components-formxml.md#DashboardComponentsandFormXML)」を参照してください。 さまざまな種類のダッシュボードの FormXML の例については、[Sample Dashboards](sample-dashboards.md) を参照してください。  
  
<a name="UsingSDK"></a>   
## <a name="create-a-dashboard-by-using-the-sdk"></a>SDK を使用したダッシュボードの作成  
 ダッシュボードを作成するには、組織所有のダッシュボードの `SystemForm` のインスタンス、またはユーザー所有のダッシュボードの `UserForm` のインスタンスを作成します。 次の例は、組織所有のダッシュボードを作成する方法を示しています。  
  
 ```csharp
 //This is the language code for U.S. English. If you are running this code
//in a different locale, you will need to modify this value.
int languageCode = 1033;

//We set up our dashboard and specify the FormXml. Refer to the
//FormXml schema in the Microsoft Dynamics CRM SDK for more information.
SystemForm dashboard = new SystemForm
{
    Name = "Sample Dashboard",
    Description = "Sample organization-owned dashboard.",
    FormXml = String.Format(@"<form>
            <tabs>
                <tab name='Test Dashboard' verticallayout='true'>
                    <labels>
                        <label description='Sample Dashboard' languagecode='{0}' />
                    </labels>
                    <columns>
                        <column width='100%'>
                            <sections>
                                <section name='Information Section'
                                    showlabel='false' showbar='false'
                                    columns='111'>
                                    <labels>
                                        <label description='Information Section'
                                            languagecode='{0}' />
                                    </labels>
                                    <rows>
                                        <row>
                                            <cell colspan='1' rowspan='10' 
                                                showlabel='false'>
                                                <labels>
                                                    <label description='Top Opportunitiess - 1'
                                                    languagecode='{0}' />
                                                </labels>
                                                <control id='TopOpportunities'
                                                    classid='{{E7A81278-8635-4d9e-8D4D-59480B391C5B}}'>
                                                    <parameters>
                                                        <ViewId>{1}</ViewId>
                                                        <IsUserView>false</IsUserView>
                                                        <RelationshipName />
                                                        <TargetEntityType>opportunity</TargetEntityType>
                                                        <AutoExpand>Fixed</AutoExpand>
                                                        <EnableQuickFind>false</EnableQuickFind>
                                                        <EnableViewPicker>false</EnableViewPicker>
                                                        <EnableJumpBar>false</EnableJumpBar>
                                                        <ChartGridMode>Chart</ChartGridMode>
                                                        <VisualizationId>{2}</VisualizationId>
                                                        <EnableChartPicker>false</EnableChartPicker>
                                                        <RecordsPerPage>10</RecordsPerPage>
                                                    </parameters>
                                                </control>
                                            </cell>
                                            <cell colspan='1' rowspan='10' 
                                                showlabel='false'>
                                                <labels>
                                                    <label description='Top Opportunities - 2'
                                                    languagecode='{0}' />
                                                </labels>
                                                <control id='TopOpportunities2'
                                                    classid='{{E7A81278-8635-4d9e-8D4D-59480B391C5B}}'>
                                                    <parameters>
                                                        <ViewId>{1}</ViewId>
                                                        <IsUserView>false</IsUserView>
                                                        <RelationshipName />
                                                        <TargetEntityType>opportunity</TargetEntityType>
                                                        <AutoExpand>Fixed</AutoExpand>
                                                        <EnableQuickFind>false</EnableQuickFind>
                                                        <EnableViewPicker>false</EnableViewPicker>
                                                        <EnableJumpBar>false</EnableJumpBar>
                                                        <ChartGridMode>Grid</ChartGridMode>
                                                        <VisualizationId>{2}</VisualizationId>
                                                        <EnableChartPicker>false</EnableChartPicker>
                                                        <RecordsPerPage>10</RecordsPerPage>
                                                    </parameters>
                                                </control>
                                            </cell>
                                        </row>
                                        <row />
                                        <row />
                                        <row />
                                        <row />
                                        <row />
                                        <row />
                                        <row />
                                        <row />
                                        <row />
                                    </rows>
                                </section>
                            </sections>
                        </column>
                    </columns>
                </tab>
            </tabs>
        </form>",
    languageCode,
    defaultOpportunityQuery.SavedQueryId.Value.ToString("B"),
    visualization.SavedQueryVisualizationId.Value.ToString("B")),
    IsDefault = false
};
_dashboardId = _serviceProxy.Create(dashboard);
 ``` 
  
 完成サンプルについては、[サンプル: ダッシュボードを作成、取得、更新、および削除 (CRUD) する方法](/dynamics365/customer-engagement/developer/customize-dev/sample-create-retrieve-update-delete-dashboard) を参照してください。 ユーザー所有のダッシュボードを作成して別のユーザーに割り当てるサンプルについては、 [サンプル: 他のユーザーにユーザー所有のダッシュボードを割り当てる](/dynamics365/customer-engagement/developer/customize-dev/sample-assign-user-owned-dashboard-another-user)を参照してください。  <!-- TODO relevant powerapps repo topic must be linked> 
  
<a name="UsingFormCustomization"></a>   
## <a name="create-an-organization-owned-dashboard-by-customizing-the-entity-form"></a>エンティティ フォームのカスタマイズによる組織所有のダッシュボードの作成  
 アンマネージド ソリューションと共にエクスポートされた customizations.xml ファイルには、エンティティ フォームとダッシュボードの定義が含まれています。 customizations.xml ファイルを追加または変更して、ダッシュボードを追加または更新できます。  
  
#### <a name="create-a-dashboard-by-customizing-an-entity-form"></a>エンティティ フォームをカスタマイズしたダッシュボードの作成  
  
1. アプリ用 Common Data Service にログオンします。  
  
2. ソリューションをエクスポートします。 これを行う際の詳細については、" [エクスポート、編集の準備、およびリボンのインポート](export-prepare-edit-import-ribbon.md)を参照してください。  
  
3. エクスポートしたソリューション フォルダーで customizations.xml ファイルを参照し、編集用に開きます。  
  
4. `</Dashboards>` タグを検索することで、customizations.xml ファイル内のダッシュボード領域の終わりを参照します。  
  
5. `</Dashboards>` タグの前に、次のコードを追加して新しいダッシュボードを定義します。  
  
   ```xml  
   <Dashboard>  
      <LocalizedNames>  
         <LocalizedName description="Dashboard_Name" languagecode="1033" />  
      </LocalizedNames>     
      <IsCustomizable>1</IsCustomizable>  
      <IsDefault>0</IsDefault>  
      <FormXml>  
         <forms type="dashboard">  
   *** Dashboard definition goes here. *** // See “Sample Dashboards” topic for the FormXML content to be used here.  
         </forms>  
      </FormXml>  
   </Dashboard>  
   ```  
  
6. customizations.xml ファイルを保存します。   
  
7. .zip ファイルをアプリ用 CDS にソリューションとしてインポートします。 詳細: [Eリボンのエクスポート、編集の準備、およびインポート](export-prepare-edit-import-ribbon.md)。  
  
<a name="Limitations"></a>   

## <a name="limitations-creating-dashboards-by-using-the-sdk-or-through-form-customization"></a>制限事項: SDK を使用してまたはフォームのカスタマイズを使用してダッシュボードを作成すること  

 アプリ用 CDS を使用して、またはフォームのカスタマイズを通じて作成または変更された特定のダッシュボードは、Web アプリケーションのダッシュボード デザイナーではサポートされません。 SDK を使用するかフォーム カスタマイズを通じてダッシュボードを作成または変更する場合は、次の操作を避けてください。  
  
### <a name="general"></a>全般  
  
- **問題**: FormXML で定義されたセクションのないタブを含むダッシュボードを作成できます。  
  
  **解決方法**: FormXML の各タブに対して定義されたセクションが少なくとも 1 つあるダッシュボードを作成してください。  
  
- **問題**: あるセクションの `<row>` 要素の数が、FormXML のそのセクションの `<cell>` 要素の `rowspan` プロパティで指定された数と同じではないダッシュボードを作成できます。 理想としては、1 つのセクション内の `<cell>` 要素の `rowspan` プロパティ値と `<row>` 要素の数が同じである必要があります。  
  
  **解決方法**: あるセクションの `<row>` 要素の数が、そのセクションの `<cell>` 要素の `rowspan` プロパティで指定された数と同じであるダッシュボードを作成してください。  
  
### <a name="grids"></a>グリッド  
 **問題**: グリッドの `<AutoExpand>` パラメーター値が `Auto` に設定されたグリッドを含むダッシュボードを作成できます。  
  
 **解決方法**: ダッシュボードの作成時に、FormXML でグリッドの `<AutoExpand>` パラメーター値を `Fixed` として指定してください。  
  
### <a name="iframes"></a>IFRAME  
 **問題**: IFRAME を含むダッシュボードを作成できます。 この状況は、FormXML で IFRAME コントロールの `<Url>` パラメーターの値を指定しない場合に発生します。  
  
 **解決方法**: FormXML で IFRAME を作成する場合は、`<Url>` パラメーターの値を必ず指定してください。  
  
### <a name="see-also"></a>関連項目  
 [ダッシュボード](analyze-data-with-dashboards.md)   
 [ダッシュボード用FormXMLを使用](understand-dashboards-dashboard-components-formxml.md)   
 [ダッシュボードに対するアクション](actions-dashboards.md)   
 [サンプル ダッシュボード](sample-dashboards.md)   
 [サンプル: ダッシュボードの作成、取得、更新および削除(CRUD)](/dynamics365/customer-engagement/developer/customize-dev/sample-create-retrieve-update-delete-dashboard)   <!-- TODO relevant powerapps repo topic must be linked--> [エンティティ フォームのカスタマイズ](customize-entity-forms.md)
