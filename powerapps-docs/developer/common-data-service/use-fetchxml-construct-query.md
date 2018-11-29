---
title: FetchXML でデータをクエリする (アプリ用 Common Data Service) | Microsoft Docs
description: FetchXML は アプリ用 Common Data Service (CDS) で使用されている独自のクエリ言語です。 これは言語の機能を記述するスキーマを基に作成されています。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="use-fetchxml-to-construct-a-query"></a>FetchXML の使用によるクエリの作成

FetchXML は アプリ用 Common Data Service (CDS) で使用されている独自のクエリ言語です。 これは言語の機能を記述するスキーマを基に作成されています。 FetchXML 言語では、クエリ式と同様のクエリ機能がサポートされています。 さらに、この言語は主にクエリ式のシリアル化されたフォームとして使用され、[UserQuery エンティティ](reference/entities/userquery.md) 内のユーザー所有の保存済みビューとして、または [SavedQuery エンティティ](reference/entities/savedquery.md) 内の組織所有の保存済みビューとしてクエリを保存するために使用されます。  
  
FetchXML クエリを実行するには **Web API** または **組織サービス** のいずれかを使用します。

## <a name="create-the-fetchxml-query-string"></a>FetchXML クエリ文字列の作成
  
FetchXML クエリを実行するには、まず XML クエリ文字列をビルドしておく必要があります。 クエリ文字列を作成後、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*> メソッドを使用してクエリ文字列を実行します。 ログオンしているユーザーの特権は、返される一連のレコードに影響します。 ログオンしているユーザーが読み取りアクセス権を持っているレコードのみが返されます。  
  
 FetchXML クエリ文字列は、FetchXML 言語のスキーマ定義に従っている必要があります。 詳細については、「[Fetch XML スキーマ](fetchxml-schema.md)」を参照してください。  
  
 `SavedQuery` レコードを作成するとクエリを保存できます。 `link-entity` ノードの `visible` を `false` に設定し、**高度な検索**ユーザー インターフェイス内のリンクされたエンティティを非表示にします。 非表示にしてもクエリの実行には参加しており、適切な結果を返します。  
  
> [!WARNING]
>  パフォーマンスへの悪影響があるため、クエリの全属性を取得しないようにしてください。 これは、クエリが更新要求へのパラメーターとして使用される場合は特に true になります。 更新では、すべての属性が含まれている場合、これによりすべてのフィールド値が、変更されなくても設定されます。また、多くの場合子レコードへ更新の伝播が発生します。  
  

### <a name="example-fetchxml-query-strings"></a>FetchXML クエリ文字列の例

以下の例の **FetchXML** 文はすべての取引先企業を取得します。  
  
```xml  
  
<fetch mapping='logical'>   
   <entity name='account'>  
      <attribute name='accountid'/>   
      <attribute name='name'/>   
</entity>  
</fetch>  
  
```  
  
 以下の例では **FetchXML** 文は、所有ユーザーの姓が Cannon に等しくないすべての取引先企業を取得します。  
  
```xml  
  
<fetch mapping='logical'>  
   <entity name='account'>   
      <attribute name='accountid'/>   
      <attribute name='name'/>   
      <link-entity name='systemuser' to='owninguser'>   
         <filter type='and'>   
            <condition attribute='lastname' operator='ne' value='Cannon' />   
          </filter>   
      </link-entity>   
   </entity>   
</fetch>  
  
```  
  
 次の例では、**FetchXML** 文でカウントを使用してクエリから返されるレコードの最大数を設定します。 この場合、最初の 3 つの取引先企業がクエリで返され、  
  
```xml  
<fetch mapping='logical' count='3'>  
  <entity name='account'>  
   <attribute name='name' alias='name'/>  
  </entity></fetch>  
```  
  
この例は、EntityMapID が一致する EntityMap と AttributeMap 間での内部結合を示しています。  
  
```xml  
<fetch version='1.0' mapping='logical' distinct='false'>  
   <entity name='entitymap'>  
      <attribute name='sourceentityname'/>  
      <attribute name='targetentityname'/>  
      <link-entity name='attributemap' alias='attributemap' to='entitymapid' from='entitymapid' link-type='inner'>  
         <attribute name='sourceattributename'/>  
         <attribute name='targetattributename'/>  
      </link-entity>  
   </entity>  
 </fetch>  
```  
  
## <a name="execute-the-fetchxml-query"></a>FetchXML クエリの実行

FetchXML クエリを実行するには **Web API** または **組織サービス** のいずれかを使用します。

### <a name="using-web-api"></a>Web API の使用
URL エンコード FetchXml 文字列は `fetchXml` クエリ文字列パラメーターを使用して適切なエンティティセットに渡すことができます。 詳細については、[ユーザー定義の FetchXML を使用する](webapi/retrieve-and-execute-predefined-queries.md#use-custom-fetchxml)を参照してください。

### <a name="using-organization-service"></a>組織サービスの使用

<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*> <xref:Microsoft.Xrm.Sdk.Query.FetchExpression.Query> プロパティに FetchXml クエリが含まれる <xref:Microsoft.Xrm.Sdk.Query.FetchExpression> を渡すメソッド。

以下のコードは組織サービスを使用した **FetchXML** クエリの実行方法を示しています:  
  
```csharp  
  
// Retrieve all accounts owned by the user with read access rights to the accounts and   
// where the last name of the user is not Cannon.   
string fetch2 = @"  
   <fetch mapping='logical'>  
     <entity name='account'>   
        <attribute name='accountid'/>   
        <attribute name='name'/>   
        <link-entity name='systemuser' to='owninguser'>   
           <filter type='and'>   
              <condition attribute='lastname' operator='ne' value='Cannon' />   
           </filter>   
        </link-entity>   
     </entity>   
   </fetch> ";   
  
EntityCollection result = _serviceProxy.RetrieveMultiple(new FetchExpression(fetch2));
foreach (var c in result.Entities)
{
   System.Console.WriteLine(c.Attributes["name"]);
}  
```  
> [!NOTE]
> FetchXML クエリは <xref:Microsoft.Crm.Sdk.Messages.FetchXmlToQueryExpressionRequest> メッセージを使用してクエリ式に変換することができます。 

  
## <a name="fetchxml-query-results"></a>FetchXML クエリ結果  
 <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy>.<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy.RetrieveMultiple(Microsoft.Xrm.Sdk.Query.QueryBase)> メソッドを使用して FetchXML クエリを実行すると、ユーザーが認証されます。 メソッド、戻り値はクエリの結果を格納している <xref:Microsoft.Xrm.Sdk.EntityCollection> です。 これで、エンティティ コレクション内を反復できます。 前述の例では、`foreach` ループを使用して、FetchXML クエリの結果コレクション内を反復しています。  
  
