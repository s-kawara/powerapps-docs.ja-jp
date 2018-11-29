---
title: エンティティ ビューのカスタマイズ (モデル駆動型アプリ) | MicrosoftDocs
description: エンティティ ビューのカスタマイズについて学習します。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: da2a9b57-fcd2-38c5-c670-63acf1767efa
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

# <a name="customize-entity-views"></a>エンティティ ビューのカスタマイズ

エンティティ ビューは、特定のフィルターを使用することによってデータを取得する特殊な保存済みクエリです。 このビューには、アプリケーションでのビュー内のデータの表示方法に関する情報も含まれます。 エンティティ ビューは、プログラム的に作成できる `SavedQuery` レコードです。 また、XML として定義し、アンマネージド ソリューションでインポートすることもできます。  
  
 エンティティ ビューは `UserQuery`とは異なります。 ユーザー クエリ (アプリケーションでは保存されているビューと呼ばれる) は、個々のユーザーによって所有され、他のユーザーに割り当てたり、他のユーザーと共有することができます。また、クエリのアクセス特権に応じて、他のユーザーがクエリを表示することもできます。 これは、頻繁に使用される、複数のエンティティの種類にまたがるクエリや、集計を実行するクエリに適しています。 詳細: [保存済みクエリ](../common-data-service/saved-queries.md) 
  
 カスタマイズ ツールを使用して、ビューをカスタマイズすることもできます。 詳細: [ビューの作成および編集](../../maker/model-driven-apps/create-edit-views.md)
  
<a name="BKMK_TypesOfViews"></a>   
## <a name="types-of-views"></a>ビューの種類  
 次の表には、カスタマイズがサポートされている 5 種類のビューが示されています。 ビューの種類コードは、`SavedQuery.QueryType` 属性に保存されます。 このエンティティは、Office Outlook フィルターおよびテンプレートの保存にも使用されているため、`QueryType`属性に対してこの一覧に記載されていない有効な値が他にもあります。 詳細については、[オフラインと Outlook のフィルターおよびテンプレート](../common-data-service/outlook-client/offline-outlook-filters-templates.md) を参照してください。 
  
 特定のエンティティに対してビューが定義されている場合、`SavedQuery.ReturnedTypeCode` 属性はエンティティの論理名を返します。  
  
|ビューの種類|種類コード|説明|  
|---------------|---------------|-----------------|  
|**公開企業**|0|- **出現回数**: 複数<br />- **アクション**: 作成、更新、削除<br />- **コメント**:`SavedQuery.IsDefault`を true に設定することによって、これらのビューの 1 つを既定の共有ビューとして設定できます。|  
|**高度な検索**|1|- **出現回数**: 1<br />- **アクション**: 更新のみ。<br />- **コメント**: 既定では、このビューは結果が**高度な検索**に表示されるときに表示されます。|  
|**関連**|2|- **出現回数**: 1<br />- **アクション**: 更新のみ。<br />- **コメント**: 既定では、このビューは関連するレコードのグリッドがレコードのナビゲーション ウィンドウに表示されるときに表示されます。|  
|**簡易検索**|4|- **出現回数**: 1<br />- **アクション**: 更新のみ。<br />- **コメント**:このビューは、ユーザーがこのリストビューで検索フィールドを使用してレコードを検索するときに、検索される列を定義します。|  
|**検索**|64|- **出現回数**: 1<br />- **アクション**: 更新のみ。<br />- **コメント**:これは、検索フィールドに他のビューが構成されていないときにレコードを検索するために使用される既定のビューです。|  
  
<a name="BKMK_CreateViews"></a>   
## <a name="create-views"></a>ビューの作成  
 共有ビューを作成するには、次のプロパティを指定します。
  
- `SavedQuery.Name`: 保存済みクエリの一意の識別子。
  
- `SavedQuery.ReturnedTypeCode`: エンティティの論理名に一致します。 
  
- `SavedQuery.FetchXml`: [FetchXML の使用によるクエリの作成](../common-data-service/use-fetchxml-construct-query.md) を参照してください。  
  
- `SavedQuery.LayoutXml`: 有効な要素については、[カスタマイズ ソリューション ファイルのスキーマ](../common-data-service/customization-solutions-file-schema.md) の `layoutxml` 要素を参照してください。
  
- `SavedQuery.QueryType`: 常にゼロ (0) である必要があります。  
  
  次のサンプルでは、営業案件エンティティの新しい共有ビューを作成します。  
  
  ```csharp
  System.String layoutXml =
  @"<grid name='resultset' object='3' jump='name' select='1' 
    preview='1' icon='1'>
    <row name='result' id='opportunityid'>
    <cell name='name' width='150' /> 
    <cell name='customerid' width='150' /> 
    <cell name='estimatedclosedate' width='150' /> 
    <cell name='estimatedvalue' width='150' /> 
    <cell name='closeprobability' width='150' /> 
    <cell name='opportunityratingcode' width='150' /> 
    <cell name='opportunitycustomeridcontactcontactid.emailaddress1' 
        width='150' disableSorting='1' /> 
    </row>
  </grid>";

  System.String fetchXml =
  @"<fetch version='1.0' output-format='xml-platform' 
    mapping='logical' distinct='false'>
    <entity name='opportunity'>
    <order attribute='estimatedvalue' descending='false' /> 
    <filter type='and'>
        <condition attribute='statecode' operator='eq' 
        value='0' /> 
    </filter>
    <attribute name='name' /> 
    <attribute name='estimatedvalue' /> 
    <attribute name='estimatedclosedate' /> 
    <attribute name='customerid' /> 
    <attribute name='opportunityratingcode' /> 
    <attribute name='closeprobability' /> 
    <link-entity alias='opportunitycustomeridcontactcontactid' 
        name='contact' from='contactid' to='customerid' 
        link-type='outer' visible='false'>
        <attribute name='emailaddress1' /> 
    </link-entity>
    <attribute name='opportunityid' /> 
    </entity>
  </fetch>";

  SavedQuery sq = new SavedQuery
    {
      Name = "A New Custom Public View",
      Description = "A Saved Query created in code",
      ReturnedTypeCode = "opportunity",
      FetchXml = fetchXml,
      LayoutXml = layoutXml,
      QueryType = 0
    };
                    
  _customViewId = _serviceProxy.Create(sq);
  Console.WriteLine("A new view with the name {0} was created.", sq.Name);
  ```  
  
<a name="BKMK_UpdateViews"></a>   
## <a name="update-views"></a>ビューの更新  
 `SavedQuery.IsCustomizable` 管理プロパティがビューの更新を許可する場合、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*> メソッドまたは <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> メッセージを使用してビューを更新することができます。  
  
<a name="BKMK_DeleteViews"></a>   
## <a name="delete-views"></a>ビューの削除  
 保存済みクエリの削除は、自分で作成したもののみについて行ってください。 ソリューション コンポーネントまたはアプリケーションの一部が、特定の保存済みクエリに依存している場合があります。 アプリケーションに表示する必要がないクエリがある場合は、非アクティブ化する必要があります。  
  
<a name="BKMK_RetrieveViews"></a>   
## <a name="retrieve-views"></a>ビューの取得  
 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMultipleRequest> または <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*> を使用して保存済みのクエリ レコードを取得します。  
  
 次のサンプルでは、営業案件エンティティのすべての共有ビューを取得します。  
  
 ```csharp
 QueryExpression mySavedQuery = new QueryExpression
        {
            ColumnSet = new ColumnSet("savedqueryid", "name", "querytype", "isdefault", "returnedtypecode", "isquickfindquery"),
            EntityName = SavedQuery.EntityLogicalName,
            Criteria = new FilterExpression
            {
                Conditions =
{
    new ConditionExpression
    {
        AttributeName = "querytype",
        Operator = ConditionOperator.Equal,
        Values = {0}
    },
    new ConditionExpression
    {
        AttributeName = "returnedtypecode",
        Operator = ConditionOperator.Equal,
        Values = {Opportunity.EntityTypeCode}
    }
}
            }
        };
        RetrieveMultipleRequest retrieveSavedQueriesRequest = new RetrieveMultipleRequest { Query = mySavedQuery };

        RetrieveMultipleResponse retrieveSavedQueriesResponse = (RetrieveMultipleResponse)_serviceProxy.Execute(retrieveSavedQueriesRequest);

        DataCollection<Entity> savedQueries = retrieveSavedQueriesResponse.EntityCollection.Entities;

        //Display the Retrieved views
        foreach (Entity ent in savedQueries)
        {
            SavedQuery rsq = (SavedQuery)ent;
            Console.WriteLine("{0} : {1} : {2} : {3} : {4} : {5},", rsq.SavedQueryId, rsq.Name, rsq.QueryType, rsq.IsDefault, rsq.ReturnedTypeCode, rsq.IsQuickFindQuery);
        }
```
  
<a name="BKMK_DeactivateViews"></a>   
## <a name="deactivate-views"></a>ビューの非アクティブ化  
 アプリケーションに表示する必要がない共有ビューは、非アクティブ化できます。 既定のビューとして設定されている共有ビューは、非アクティブ化できません。 次のサンプルでは、営業案件エンティティの**現在の会計年度中にクローズされた営業案件**ビューを非アクティブ化します。  
  
 ```csharp
 System.String SavedQueryName = "Closed Opportunities in Current Fiscal Year";
QueryExpression ClosedOpportunitiesViewQuery = new QueryExpression
{
    ColumnSet = new ColumnSet("savedqueryid", "statecode", "statuscode"),
    EntityName = SavedQuery.EntityLogicalName,
    Criteria = new FilterExpression
    {
        Conditions =
        {
            new ConditionExpression
            {
                AttributeName = "querytype",
                Operator = ConditionOperator.Equal,
                Values = {0}
            },
            new ConditionExpression
            {
                AttributeName = "returnedtypecode",
                Operator = ConditionOperator.Equal,
                Values = {Opportunity.EntityTypeCode}
            },
                            new ConditionExpression
            {
                AttributeName = "name",
                Operator = ConditionOperator.Equal,
                Values = {SavedQueryName}
            }
        }
    }
};

RetrieveMultipleRequest retrieveOpportuntiesViewRequest = new RetrieveMultipleRequest { Query = ClosedOpportunitiesViewQuery };

RetrieveMultipleResponse retrieveOpportuntiesViewResponse = (RetrieveMultipleResponse)_serviceProxy.Execute(retrieveOpportuntiesViewRequest);

SavedQuery OpportunityView = (SavedQuery)retrieveOpportuntiesViewResponse.EntityCollection.Entities[0];
_viewOriginalState = (SavedQueryState)OpportunityView.StateCode;
_viewOriginalStatus = OpportunityView.StatusCode;


SetStateRequest ssreq = new SetStateRequest
{
    EntityMoniker = new EntityReference(SavedQuery.EntityLogicalName, (Guid)OpportunityView.SavedQueryId),
    State = new OptionSetValue((int)SavedQueryState.Inactive),
    Status = new OptionSetValue(2)
};
_serviceProxy.Execute(ssreq);
 ```  
  
<a name="BKMK_EditFilterOrSorting"></a>   
## <a name="edit-filter-criteria-or-configure-sorting"></a>フィルター条件の編集または並べ替えの構成  
 フィルターの編集、またはデータの並べ替え方法の編集を行うには、`SavedQuery.FetchXml` 属性を設定する必要があります。 詳細については、[FetchXML でデータをクエリする](/powerapps/developer/common-data-service/use-fetchxml-construct-query)を参照してください。  
  
> [!TIP]
>  FetchXML に慣れていない場合は、メッセージ <xref:Microsoft.Crm.Sdk.Messages.QueryExpressionToFetchXmlRequest> および <xref:Microsoft.Crm.Sdk.Messages.FetchXmlToQueryExpressionRequest> を使用して、QueryExpression と FetchXML の間で変換できます。  
  
<a name="BKMK_EditColumns"></a>   
## <a name="edit-columns"></a>列の編集  
 ビューに表示する列は、エンティティまたは関連するエンティティから取得できます。 表示する列の指定方法の詳細については、[カスタマイズ ソリューション ファイルのスキーマ](../common-data-service/customization-solutions-file-schema.md) の `layoutxml` 要素を参照してください。  
  
<a name="BKMK_CustomIcons"></a>   
## <a name="add-custom-icons-with-tooltip-for-a-column"></a>列に対するユーザー定義アイコンのツールヒントの追加  
 列の値により列に表示するツールヒントのテキストを含むユーザー定義アイコンを追加できます; ローカライズされたツールヒント テキストを指定することもできます。 これにより、インスタンス内のイメージ Web リソースとしてユーザー定義アイコンを追加し、JavaScript Web リソースを使用して列の値によるアイコンを表示するための列の JavaScript コードを追加することができるようになります。  
  
> [!NOTE]
>  ユーザー定義アイコンのツールヒントの追加は読み取り専用グリッドでのみサポートされます。この機能は編集可能なグリッドではサポートされません。 編集可能なグリッドの詳細については、「[編集可能グリッドの使用](/powerapps/developer/model-driven-apps/use-editable-grids)」を参照してください。  
  
 2 つの新しい属性`imageproviderwebresource`および`imageproviderfunctionname`は、savedquery の layoutxml の`cell`要素に追加されます。これらを使用すると Web リソース名および JavaScript 関数名を指定して、列にカスタム アイコンおよびツールヒント テキストを表示することができます。 ページが読み込まれると、JavaScript コードが実行されます。  
  
 新しい **Web リソース**および**列のプロパティ**ページ内の**関数名**フィールドを使用しながら、Web クライアント名と JavaScript 関数名の定義を表示する属性 (列) のプロパティを変更することができます。  
  
 次のサンプルコードは、layoutxml 内の`opportunityratingcode`列に対するユーザー定義アイコンとツールヒントを追加するための Web リソースと JavaScript 関数名をプログラムで指定する方法を示します。  
  
```csharp  
System.String layoutXml =  
@"<grid name='resultset' object='3' jump='name' select='1'  
  preview='1' icon='1'>  
  <row name='result' id='opportunityid'>  
    <cell name='name' width='150' />  
    <cell name='customerid' width='150' />  
    <cell name='estimatedclosedate' width='150' />  
    <cell name='estimatedvalue' width='150' />  
    <cell name='closeprobability' width='150' />  
    <cell name='opportunityratingcode' width='150' imageproviderwebresource='new_SampleWebResource'  
          imageproviderfunctionname='displayIconTooltip' />  
    <cell name='opportunitycustomeridcontactcontactid.emailaddress1'  
        width='150' disableSorting='1' />  
  </row>  
</grid>";  
```  
  
 ユーザー定義アイコンとツールヒントのテキストを表示する JavaScript 関数には、次の 2 つの引数が表示されます: layoutxml で指定された行オブジェクト全体と呼び出し側ユーザーのロケール ID (LCID)。 LCID パラメーターでは、複数の言語でアイコンのツールヒントのテキストを指定できます。 サポートされている言語の詳細については、[追加言語の有効化](/dynamics365/customer-engagement/customize/enable-additional-languages)<!-- TODO need to update the link in the powerapps repo-->および[言語パックのインストールまたはアップグレード](https://technet.microsoft.com/library/hh699674.aspx)を参照してください。 コードで使用できるロケール ID (LCID) 値の一覧については、[Microsoft によって割り当てられるロケール ID](https://go.microsoft.com/fwlink/?linkid=829588) を参照してください。  
  
 事前定義された限定のオプション セットによるオプション セット型の属性でカスタム アイコンを追加する可能性が最も高いと想定される場合は、ラベルの代わりにオプションの整数値を使用して、ローカライズされたラベル文字列の変更によるコードの破損を回避することを確認します。 または、JavaScript関数で、属性の値のアイコンとして使用するイメージ Web リソースの名前を指定します。 イメージは、16 x 16 ピクセル サイズであるべきです; より大きな画像は、16 x 16 ピクセル サイズに自動的に縮小されます。  
  
 次のサンプル コードは、`opportunityratingcode (Rating)` 属性内の値 (1: 高、2: 中、3: 低) のいずれかに基づき、異なるアイコンおよびツールヒント テキストを表示します。 サンプル コードは、ローカライズしたツールヒントのテキストを表示する方法についても示します。 このサンプルが機能するには、それぞれ 16x16 イメージの 3 つのイメージ Web リソース (![高評価ボタン](media/dynamics365hotgridicon.png "高評価ボタン")、![中評価シンボル](media/dynamics365warmgridicon.png "中評価シンボル")、および![低評価ボタン](media/dynamics365coldgridicon.png "低評価ボタン")) をインスタンス内に`new_Hot`、`new_Warm`、および`new_Cold`という名前で作成します。  
  
```javascript 
function displayIconTooltip(rowData, userLCID) {      
    var str = JSON.parse(rowData);  
    var coldata = str.opportunityratingcode_Value;  
    var imgName = "";  
    var tooltip = "";  
    switch (coldata) {  
        case 1:  
            imgName = "new_Hot";  
            switch (userLCID) {  
                case 1036:  
                    tooltip = "French: Opportunity is Hot";  
                    break;  
                default:  
                    tooltip = "Opportunity is Hot";  
                    break;  
            }  
            break;  
        case 2:  
            imgName = "new_Warm";  
            switch (userLCID) {  
                case 1036:  
                    tooltip = "French: Opportunity is Warm";  
                    break;  
                default:  
                    tooltip = "Opportunity is Warm";  
                    break;  
            }  
            break;  
        case 3:  
            imgName = "new_Cold";  
            switch (userLCID) {  
                case 1036:  
                    tooltip = "French: Opportunity is Cold";  
                    break;  
                default:  
                    tooltip = "Opportunity is Cold";  
                    break;  
            }  
            break;  
        default:  
            imgName = "";  
            tooltip = "";  
            break;  
    }  
    var resultarray = [imgName, tooltip];  
    return resultarray;  
}  
```  
  
 この結果、値に基づいた適切なアイコンを含む [`Rating`] 列の値、およびカーソルを置いたときのアイコンのツールヒント テキストが表示されます。  
  
 ![ビューの列に表示するユーザー定義アイコン](media/customiconsinviews.png "ビューの列に表示するユーザー定義アイコン")  
  
<a name="BKMK_SetAsDefault"></a>   
## <a name="set-as-default"></a>既定として設定  
 既定のビューとして設定できるのは、アクティブな共有ビューが 1 つだけです。 ビューを既定のビューにするには、`IsDefault` プロパティを true に設定します。  
  
