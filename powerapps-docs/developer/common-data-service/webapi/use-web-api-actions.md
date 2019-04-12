---
title: Web API アクションの使用 (Common Data Service) | Microsoft Docs
descriptions: Actions are reusable operations that can be performed using the Web API. These are used with a POST request to modify data on Common Data Service
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 53eafd67-385a-485b-9022-5127df08ea2f
caps.latest.revision: 14
author: brandonsimons
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-web-api-actions"></a>Web API アクションの使用

アクションと関数は、Web API を使って実行できる再利用可能な操作を表します。 POST 要求と「<xref:Microsoft.Dynamics.CRM.ActionIndex>」に示されているアクションを使用して、副作用がある操作を実行します。 カスタム アクションを定義して使用することもできます。

<a name="bkmk_unboundActions"></a>

## <a name="unbound-actions"></a>バインドされていないアクション

アクションは、「[CSDL メタデータ ドキュメント](web-api-types-operations.md#bkmk_csdl)」で定義されています。 例として、メタデータ ドキュメントで表された <xref href="Microsoft.Dynamics.CRM.WinOpportunity?text=WinOpportunity Action" /> の定義を次に示します。

```xml
<Action Name="WinOpportunity">
  <Parameter Name="OpportunityClose" Type="mscrm.opportunityclose" Nullable="false" />
  <Parameter Name="Status" Type="Edm.Int32" Nullable="false" />
</Action>
```

<xref href="Microsoft.Dynamics.CRM.WinOpportunity?text=WinOpportunity Action" /> は、組織サービスを使用した <xref:Microsoft.Crm.Sdk.Messages.WinOpportunityRequest> に対応します。 このアクションを使用して、営業案件の状態を "受注" に設定し、<xref href="Microsoft.Dynamics.CRM.opportunityclose?text=opportunityclose EntityType" /> を作成してイベントを記録します。 このアクションに戻り値はありません。 成功すると、操作が完了します。

`OpportunityClose` パラメーターには、操作を作成するために opportunityclose エンティティの JSON 表現が必要です。 このエンティティは、単一値のナビゲーション プロパティである opportunityid を発行する営業案件に関連している必要があります。 JSON では、これは `@odata.bind` 注釈を使って設定されます (「[作成時にエンティティを関連付ける](create-entity-web-api.md#bkmk_associateOnCreate)」を参照)。

`Status` パラメーターは、クローズ時の opportunity の状態に設定する必要があります。 この既定値は、<xref href="Microsoft.Dynamics.CRM.opportunity?text=opportunity EntityType" /> statuscode プロパティで確認できます。 **受注**オプションの値は 3 です。 **受注**を表すステータス オプションが 1 つしか存在しないのに、この値をなぜ設定する必要があるか疑問に思うかもしれません。 理由は、受注を表すカスタム状態オプション ("**大型受注**" や "**小型受注**" など) をユーザーは定義でき、その場合、値は 3 とは異なる可能性があるためです。

次の例は、営業案件の `WinOpportunity` アクションを呼び出す HTTP 要求と応答です。opportunityid 値は `b3828ac8-917a-e511-80d2-00155d2a68d2` です。

 **要求**

```http
POST [Organization URI]/api/data/v9.0/WinOpportunity HTTP/1.1
Accept: application/json
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0

{
 "Status": 3,
 "OpportunityClose": {
  "subject": "Won Opportunity",
  "opportunityid@odata.bind": "[Organization URI]/api/data/v9.0/opportunities(b3828ac8-917a-e511-80d2-00155d2a68d2)"
 }
}

```

 **応答**

```http
HTTP/1.1 204 No Content
OData-Version: 4.0
```

<a name="bkmk_boundActions"></a>

## <a name="bound-actions"></a>バインドされたアクション

[CSDL メタデータ ドキュメント](web-api-types-operations.md#bkmk_csdl) では、`Action` 要素がバインドされたアクションを表す場合、その要素には、`true` の値を持つ `IsBound` 属性が指定されています。 アクション内に定義された最初の `Parameter` 要素は、操作がバインドされているエンティティを表します。 パラメーターの `Type` 属性がコレクションである場合、操作はエンティティのコレクションにバインドされています。 例として、CSDL で表された <xref href="Microsoft.Dynamics.CRM.AddToQueue?text=AddToQueue Action" />の定義を次に示します。

```xml
 <ComplexType Name="AddToQueueResponse">
 <Property Name="QueueItemId" Type="Edm.Guid" Nullable="false" />
 </ComplexType>
 <Action Name="AddToQueue" IsBound="true">
  <Parameter Name="entity" Type="mscrm.queue" Nullable="false" />
  <Parameter Name="Target" Type="mscrm.crmbaseentity" Nullable="false" />
  <Parameter Name="SourceQueue" Type="mscrm.queue" />
  <Parameter Name="QueueItemProperties" Type="mscrm.queueitem" />
  <ReturnType Type="mscrm.AddToQueueResponse" Nullable="false" />
</Action>
```

このバインドされたアクションは、組織サービスで使用される <xref:Microsoft.Crm.Sdk.Messages.AddToQueueRequest> と同等です。 Web API でこのアクションは <xref:Microsoft.Crm.Sdk.Messages.AddToQueueRequest>.<xref:Microsoft.Crm.Sdk.Messages.AddToQueueRequest.DestinationQueueId> プロパティを表す <xref href="Microsoft.Dynamics.CRM.queue?text=queue EntityType" />)  にバインドされます。 このアクションは複数の追加のパラメーターを受け取り、組織サービスによって返される <xref:Microsoft.Crm.Sdk.Messages.AddToQueueResponse> に対応する <xref href="Microsoft.Dynamics.CRM.AddToQueueResponse?text=AddToQueueResponse ComplexType" /> を返します。 アクションが複合型を返す場合、複合型の定義は、CSDL でアクションのすぐ上に表示されます。

バインドされたアクションは、最初のパラメーター値を設定するために URI を使って呼び出す必要があります。 名前付きパラメーターの値として設定することはできません。

バインドされた関数を呼び出すときは、`Microsoft.Dynamics.CRM` 名前空間を含めた関数の完全な名前を使用する必要があります。 完全な名前を使用しないと、次のエラーが発生します。状態コード:400 要求メッセージに未解決のパラメーターがあります。

次の例は、<xref href="Microsoft.Dynamics.CRM.AddToQueue?text=AddToQueue Action" /> を使用してレターをキューに追加する方法を示しています。 `Target` パラメーターの種類が固有 (`mscrm.crmbaseentity`) ではないため、オブジェクトの種類を明示的に宣言する必要があります。この宣言には、`@odata.type` プロパティの値として、`Microsoft.Dynamics.CRM` 名前空間を含むエンティティの完全名を使用します。 この例の場合は、`Microsoft.Dynamics.CRM.letter` になります。 詳細:[エンティティのパラメータの種類を指定する](#bkmk_specifyentityparametertype)

 **要求**

```http
POST [Organization URI]/api/data/v9.0/queues(56ae8258-4878-e511-80d4-00155d2a68d1)/Microsoft.Dynamics.CRM.AddToQueue HTTP/1.1
Accept: application/json
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0

{
 "Target": {
  "activityid": "59ae8258-4878-e511-80d4-00155d2a68d1",
  "@odata.type": "Microsoft.Dynamics.CRM.letter"
 }
}
```

 **応答**

```http

HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal
OData-Version: 4.0

{
 "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.AddToQueueResponse",
 "QueueItemId": "5aae8258-4878-e511-80d4-00155d2a68d1"
}
```

<a name="bkmk_customActions"></a>

## <a name="use-a-custom-action"></a>カスタム アクションの使用

<!-- TODO: 
If you define custom actions for your organization or solution these will also be included in the [CSDL metadata document](web-api-types-operations.md#bkmk_csdl). For information about creating actions using the customization tools in the application, see the TechNet topic [Actions](/dynamics365/customer-engagement/customize/actions). For information about creating and using your own custom actions, see [Create your own actions](../create-own-actions.md). -->

カスタム アクションに含まれる操作に副作用があるかどうかにかかわらず、それらの操作はデータを変更する可能性があり、したがって関数ではなくアクションと見なされます。 カスタム関数を作成する方法はありません。

### <a name="custom-action-example-add-a-note-to-a-contact"></a>カスタム アクションの例: 取引先担当者にメモを追加

 特定の取引先担当者に新しいメモを追加するカスタム アクションを作成することを考えてみましょう。 次のプロパティを持つ取引先担当者エンティティにバインドされているカスタム アクションを作成できます。

|UI ラベル|値|
|--------------|-----------|
|**プロセス名**|AddNoteToContact|
|**一意の名前**|new_AddNoteToContact|
|**エンティティ**|取引先​​担当者|
|**カテゴリ**|アクション|

 **プロセスの引数**

|名前|種類​​|必須項目|方向|
|----------|----------|--------------|---------------|
|NoteTitle|文字列|必須項目|Input|
|NoteText|文字列|必須項目|Input|
|NoteReference|エンティティ参照|必須項目|Output|

 **ステップ**

|名前|ステップの種類|内容|
|----------|---------------|-----------------|
|メモの作成|レコードの作成|Title = {NoteTitle(Arguments)}<br /> Note Body = {NoteText(Arguments)}<br /> Regarding = {Contact{Contact}}|
|メモへの参照を返す|値の割り当て|NoteReference Value = {Note(Create the note (Note))}|

 カスタム アクションを公開してアクティブ化した後、CSDL をダウンロードするときに、この新しいアクションが定義されていることがわかります。

```xml

<Action Name="new_AddNoteToContact" IsBound="true">
  <Parameter Name="entity" Type="mscrm.contact" Nullable="false" />
  <Parameter Name="NoteTitle" Type="Edm.String" Nullable="false" Unicode="false" />
  <Parameter Name="NoteText" Type="Edm.String" Nullable="false" Unicode="false" />
  <ReturnType Type="mscrm.annotation" Nullable="false" />
</Action>

```

次の HTTP 要求と応答は、カスタム アクションを呼び出す方法と、成功した場合に返される応答を示しています。  

 **要求**

```http
POST [Organization URI]/api/data/v9.0/contacts(94d8c461-a27a-e511-80d2-00155d2a68d2)/Microsoft.Dynamics.CRM.new_AddNoteToContact HTTP/1.1
Accept: application/json
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0

{
 "NoteTitle": "New Note Title",
 "NoteText": "This is the text of the note"
}
```


 **応答**

```http

HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal
OData-Version: 4.0

{
 "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#annotations/$entity",
 "annotationid": "9ad8c461-a27a-e511-80d2-00155d2a68d2"
}
```

<a name="bkmk_specifyentityparametertype"></a>

## <a name="specify-entity-parameter-type"></a>エンティティのパラメーターの種類を指定する

操作がパラメータとしてのエンティティを必要し、エンティティの種類が曖昧である場合は、`@odata.type` プロパティを使用して、エンティティの種類を指定する必要があります。 このプロパティの値は、エンティティの完全修飾名であり、このパターンに従います: `Microsoft.Dynamics.CRM.`+*\<エンティティの論理名*。

上記の「[バインドされたアクション](#bkmk_boundActions)」セクションに示したように、<xref href="Microsoft.Dynamics.CRM.AddToQueue?text=AddToQueue Action" /> に対する `Target` パラメーターは活動です。 ただし、すべての活動は <xref href="Microsoft.Dynamics.CRM.activitypointer?text=activitypointer EntityType" /> から継承するため、次のプロパティをエンティティ JSON に含め、エンティティの種類が文字であることを指定する必要があります: `"@odata.type": "Microsoft.Dynamics.CRM.letter"`。

`Members` パラメーターが <xref href="Microsoft.Dynamics.CRM.principal?text=principal EntityType" /> から `ownerid` プライマリー キーを継承する <xref href="Microsoft.Dynamics.CRM.systemuser?text=systemuser EntityType" /> のコレクションであるため、他の 2 つの例は <xref href="Microsoft.Dynamics.CRM.AddMembersTeam?text=AddMembersTeam Action" /> と <xref href="Microsoft.Dynamics.CRM.RemoveMembersTeam?text=RemoveMembersTeam Action" /> です。 次の JSON を渡し、単一の systemuser をコレクションで表示する場合、エンティティが systemuser であり、主体 entitytype からも継承される <xref href="Microsoft.Dynamics.CRM.team?text=team EntityType" /> ではないことが明確です。

```json
{
 "Members": [{
  "@odata.type": "Microsoft.Dynamics.CRM.systemuser",
  "ownerid": "5dbf5efc-4507-e611-80de-5065f38a7b01"
 }]
}
```

この状況においてエンティティの種類を指定しない場合、次のエラーが発生する可能性があります: `"EdmEntityObject passed should have the key property value set."`。

### <a name="see-also"></a>関連項目

[Web API 機能およびアクションのサンプル (C#)](samples/functions-actions-csharp.md)<br />
[Web API 機能およびアクションのサンプル (クライアント側 JavaScript)](samples/functions-actions-client-side-javascript.md)<br />
[Web API を使用して演算を実行する](perform-operations-web-api.md)<br />
[HTTP 要求の作成とエラーの処理](compose-http-requests-handle-errors.md)<br />
[Web API を使用したクエリ データ](query-data-web-api.md)<br />
[Web API を使用してエンティティを作成する](create-entity-web-api.md)<br />
[Web API を使用してエンティティを取得する](retrieve-entity-using-web-api.md)<br />
[Web API を使用したエンティティの更新と削除](update-delete-entities-using-web-api.md)<br />
[Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)<br />
[Web API 関数の使用](use-web-api-functions.md)<br />
[Web API を使用してバッチ操作を実行する](execute-batch-operations-using-web-api.md)<br />
[Web API を使用して別のユーザーを偽装する](impersonate-another-user-web-api.md)<br />
[Web API を使用する条件付き演算を実行する](perform-conditional-operations-using-web-api.md)<br />
