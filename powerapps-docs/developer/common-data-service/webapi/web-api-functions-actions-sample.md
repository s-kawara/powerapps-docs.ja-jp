---
title: Web API 機能およびアクションのサンプル (Common Data Service) | Microsoft Docs
description: 'このサンプル グループは、Common Data Service Web API を使用して、バインドされた関数とバインドされていない関数およびカスタム アクションを含むアクションを実行する方法を示します。 これらは、クライアント側の JavaScript と C# を使用して実装されます'
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 953c3137-6171-4e6e-b249-6a96221c6e96
caps.latest.revision: 16
author: brandonsimons
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-functions-and-actions-sample"></a>Web API 機能およびアクションのサンプル

このサンプル グループは、Common Data Service Web API を使用して、バインドされた関数とバインドされていない関数およびカスタム アクションを含むアクションを実行する方法を示します。 このサンプルは次の言語に対する別個のプロジェクトとして実装されます。  
  
-   [機能およびアクションのサンプル (C#)](samples/functions-actions-csharp.md)  
  
このトピックは、より高度でニュートラル言語レベルの構造と内容を説明します。 このトピックに説明されている操作を実行する方法に関する言語固有の実装の詳細については、上記にリンクされたサンプル トピックを確認してください。  
  
<a name="bkmk_demonstrates"></a>  
 
## <a name="demonstrates"></a>説明  

このサンプルは次の主要なセクションに分かれています。それには関連する概念的なトピックでより詳しく説明される Web API 関数とアクションの処理が含まれます。  
  
|トピック セクション|関連するトピック|  
|-------------------|---------------------------|  
|[サンプル データ](#bkmk_sampleData)||  
|[パラメーターなしでバインドされていない関数を使用する](#bkmk_unboundFunctionNoParams)|[バインドされていない関数](use-web-api-functions.md#bkmk_unboundFunctions)<br /><br /> <xref href="Microsoft.Dynamics.CRM.WhoAmI?text=WhoAmI Function" /><br /><br /> <xref href="Microsoft.Dynamics.CRM.systemuser?text=systemuser EntityType" />|  
|[パラメーターを使用するバインドされていない関数を使用する](#bkmk_unboundFunctionWithParams)|[バインドされていない関数](use-web-api-functions.md#bkmk_unboundFunctions)<br /><br /> <xref href="Microsoft.Dynamics.CRM.GetTimeZoneCodeByLocalizedName?text=GetTimeZoneCodeByLocalizedName Function" />|  
|[パラメーターなしでバインドされた関数を使用する](#bkmk_boundFunctionWithParams)|[バインドされた関数](use-web-api-functions.md#bkmk_boundFunctions)<br /><br /> <xref href="Microsoft.Dynamics.CRM.CalculateTotalTimeIncident?text=CalculateTotalTimeIncident Function" />|  
|[パラメーターを使用するバインドされていないアクションを使用する](#bkmk_unboundActionWithParams)|[バインドされていないアクション](use-web-api-actions.md#bkmk_unboundActions)<br /><br /> <xref href="Microsoft.Dynamics.CRM.WinOpportunity?text=WinOpportunity Action" /><br /><br /> <xref href="Microsoft.Dynamics.CRM.opportunity?text=opportunity EntityType" />|  
|[パラメーターを使用するバインドされているアクションを使用する](#bkmk_boundActionWithParams)|[バインドされたアクション](use-web-api-actions.md#bkmk_boundActions)<br /><br /> <xref href="Microsoft.Dynamics.CRM.AddToQueue?text=AddToQueue Action" /><br /><br /> <xref href="Microsoft.Dynamics.CRM.WhoAmI?text=WhoAmI Function" /><br /><br /> <xref href="Microsoft.Dynamics.CRM.systemuser?text=systemuser EntityType" /><br /><br /> <xref href="Microsoft.Dynamics.CRM.letter?text=letter EntityType" />|  
|[パラメーターを使用するバインドされているユーザー定義アクションを使用](#bkmk_boundCustomActionWithParams)|[カスタム アクションの使用](use-web-api-actions.md#bkmk_customActions)<br /><br /> [バインドされたアクション](use-web-api-actions.md#bkmk_boundActions)<br /><br /> <xref href="Microsoft.Dynamics.CRM.contact?text=contact EntityType" />|  
|[パラメーターを使用するバインドされていないカスタム アクションを使用する](#bkmk_unboundCustomActionWithParams)|[カスタム アクションの使用](use-web-api-actions.md#bkmk_customActions)<br /><br /> [バインドされていないアクション](use-web-api-actions.md#bkmk_unboundActions)<br /><br /> <xref href="Microsoft.Dynamics.CRM.account?text=account EntityType" />|  
|[ユーザー定義アクション例外の処理](#bkmk_boundCustomActionErrorHandling)|[カスタム アクションの使用](use-web-api-actions.md#bkmk_customActions)<br /><br /> [バインドされていないアクション](use-web-api-actions.md#bkmk_unboundActions)<br /><br /> <xref href="Microsoft.Dynamics.CRM.contact?text=contact EntityType" />|  
  
次のセクションには、Common Data Service Web API 操作の実行に関する簡単な説明が、対応する HTTP メッセージおよび関連するコンソール出力と共に示されています。  
  
<a name="bkmk_sampleData"></a>
   
## <a name="sample-data"></a>サンプル データ  

このサンプルでの操作が確実に実行されるために、まず Common Data Service サーバーにサンプル データを作成します。 これらのサンプル データは、ユーザーがレポートの削除をしないという選択をしない限りサーバーから削除されます。 このサンプルのデータは、次のように個別に作成されます。  
  
- 取引先企業 (例: `Fourth Coffee`) を作成し、30 分のタスクが 3 回 (合計 90 分) あるインシデントと関連付けます。 タスクを作成された後、それらは完了としてマークされます。 この操作は、これらの 3 つのタスクを完了するために必要とした合計時間を計算します。  
  
    ```json  
    {  
      title: "Sample Case",  
      "customerid_account@odata.bind": accountUri,  
      Incident_Tasks: [  
       {  
        subject: "Task 1",  
        actualdurationminutes: 30  
       },  
       {  
        subject: "Task 2",  
        actualdurationminutes: 30  
       },  
       {  
        subject: "Task 3",  
        actualdurationminutes: 30  
       }  
      ]  
     };  
    ```  
  
- 取引先企業を作成し、営業案件と関連付けます。 この営業案件は、サンプル操作内で受注案件としてマークされます。  
  
    ```json  
    {  
     name: "Sample Account for WebAPIFunctionsAndActions sample",  
     opportunity_customer_accounts: [{  
      name: "Opportunity to win"  
     }]  
    };  
    ```  
  
- レター活動を作成します。 レターは、サンプル操作内で、現在のユーザーのキューに追加されます。  
  
    ```json  
    {  
      description: "Example letter"  
    }  
    ```  
  
- サンプル操作内の `sample_AddNoteToContact` カスタム アクションと共に使用する、取引先担当者を作成します。  
  
    ```json  
    {  
      firstname: "Jon",  
      lastname: "Fogg"  
    }  
    ```  
  
<a name="bkmk_sampleOperations"></a>
   
## <a name="sample-operations"></a>サンプルの操作  

このトピックのサンプル操作は次の方法で組織されます。  
  
- 関数の操作: これらの操作はパラメーターを受け入れるか受け入れないかに関係なく、バインドされた関数とバインドされていない関数を示します。  
- アクションの操作: これらの操作はパラメーターを受け入れるか受け入れないかに関係なく、バインドされたアクションとバインドされていないアクションを示します。  
- ユーザー定義アクション: これらの操作は、バインドされたアクションとバインドされていないアクションを示し、ユーザー定義のエラーの例外を処理する方法を示します。  
  
<a name="bkmk_workingWithFunctions"></a> 
  
## <a name="working-with-functions"></a>関数に関する作業  

[機能](web-api-types-operations.md#bkmk_functions) は副作用がない操作です。 関数には、エンティティ インスタンスまたはエンティティ コレクションにバインドされている場合があります。 クエリ関数はバインドされることはありません。 詳細については、[Web API 機能を使用](use-web-api-functions.md) を参照してください。 このセクションは、バインドされた関数とバインドされていない関数が使用される方法、およびパラメーターが受け渡される方法を示します。  
  
<a name="bkmk_unboundFunctionNoParams"></a>  
 
### <a name="using-unbound-function-with-no-parameters"></a>パラメーターなしでバインドされていない関数を使用する 
 
<xref href="Microsoft.Dynamics.CRM.WhoAmI?text=WhoAmI Function" /> を使用している現在のユーザーのフル ネームを取得するために、バインドされていない関数を使用します。 この操作はパラメーターを受け取らないバインドされていない関数を呼び出す方法を示します。 この操作は、現在のユーザーのフル ネームを返します。  
  
<xref href="Microsoft.Dynamics.CRM.WhoAmI?text=WhoAmI Function" /> に対する要求と応答を取得します。  
  
 **要求**  
  
```http  
GET http://[Organization URI]/api/data/v9.0/WhoAmI HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8   
```  
  
 **応答**  
  
```http  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Content-Length: 273  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.WhoAmIResponse",  
   "BusinessUnitId":"0d6cc84a-d3f6-e511-80d0-00155da84802",  
   "UserId":"b08dc84a-d3f6-e511-80d0-00155da84802",  
   "OrganizationId":"0f47eae2-a906-4ae4-9215-f09875979f6a"  
}  
```  
  
<a name="bkmk_unboundFunctionWithParams"></a>
   
### <a name="using-unbound-function-with-parameters"></a>パラメーターを使用するバインドされていない関数を使用する  

バインドされていない関数を使用してタイム ゾーン コードを取得します。 この操作はパラメーターを受け取るバインドされていない関数を呼び出す方法を示します。 この操作は指定されたタイム ゾーンの現在のタイム ゾーン コードを返します。 詳細情報: [関数にパラメーターを渡す](use-web-api-functions.md#bkmk_passParametersToFunctions)  
  
 **要求**  
  
```http  
GET http://[Organization URI]/api/data/v9.0/GetTimeZoneCodeByLocalizedName(LocalizedStandardName=@p1,LocaleId=@p2)?@p1='Pacific%20Standard%20Time'&@p2=1033 HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8 
```  
  
 **応答**  
  
```http  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Content-Length: 154  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.GetTimeZoneCodeByLocalizedNameResponse",  
   "TimeZoneCode":4  
}  
```  
  
 **コンソール出力**  
  
```  
Unbound function: GetTimeZoneCodeByLocalizedName  
    Function returned time zone Pacific Standard Time, with code '4'.  
```  
  
<a name="bkmk_boundFunctionWithParams"></a>
   
### <a name="using-bound-function-with-no-parameters"></a>パラメーターなしでバインドされた関数を使用する  

バインドされた関数を使用して、インシデントのタスクすべてを完了するために必要とされた合計時間を取得します。 この操作はパラメーターを受け取らないバインドされた関数を呼び出す方法を示します。 この操作は、インシデントがすべてのタスクを終了するために必要とされた合計時間 (分) を返します。 この関数は、このサンプル プログラム用に作成されたインシデント データも使用します。 詳細は: [バインドされた関数](use-web-api-functions.md#bkmk_boundFunctions)  
  
 **要求**  
  
```http  
GET http://[Organization URI]/api/data/v9.0/incidents(3d920da5-fb4a-e611-80d5-00155da84802)/Microsoft.Dynamics.CRM.CalculateTotalTimeIncident() HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
  
```  
  
 **応答**  
  
```http  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Content-Length: 148  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.CalculateTotalTimeIncidentResponse",  
   "TotalTime":90  
}  
```  
  
 **コンソール出力**  
  
```  
Bound function: CalculateTotalTimeIncident  
    Function returned 90 minutes - total duration of tasks associated with the incident.  
```  
  
<a name="bkmk_workingWithActions"></a> 
  
## <a name="working-with-actions"></a>アクションに関する作業  

[アクション](web-api-types-operations.md#bkmk_actions) は副作用を許可する操作です。 アクションはバインドされているか、またはバインドされていません。 詳細については、[Web API アクションを使用](use-web-api-actions.md) を参照してください。 このセクションは、バインドされたアクションとバインドされていないアクションが使用される方法、およびパラメーターが受け渡される方法を示します。 また、ユーザー定義のアクションが使用される方法と、これらのユーザー定義のアクションでの例外を処理する方法も示します。  
  
<a name="bkmk_unboundActionWithParams"></a>
   
### <a name="using-unbound-action-with-parameters"></a>パラメーターを使用するバインドされていないアクションを使用する 
 
一連のパラメーターを受け取るバインドされていないアクションを使用します。 この操作は、営業案件をクローズし、<xref href="Microsoft.Dynamics.CRM.WinOpportunity?text=WinOpportunity Action" /> の呼び出しにより受注したとマークします。 先ほどこのプログラムで、<xref href="Microsoft.Dynamics.CRM.opportunity?text=opportunity EntityType" /> がサンプル データとして作成されました。 詳細: [バインドされていないアクション](use-web-api-actions.md#bkmk_unboundActions)  
  
 **要求**  
  
```http  
POST http://[Organization URI]/api/data/v9.0/WinOpportunity HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
  
{  
   "Status":3,  
   "OpportunityClose":{  
      "subject":"Won Opportunity",  
      "opportunityid@odata.bind":"http://[Organization URI]/api/data/v9.0/opportunities(47920da5-fb4a-e611-80d5-00155da84802)"  
   }  
}  
```  
  
 **応答**  
  
```http  
HTTP/1.1 204 No Content  
OData-Version: 4.0   
```  
  
 **コンソール出力**  
  
```  
Unbound Action: WinOpportunity  
    Opportunity won.  
```  
  
<a name="bkmk_boundActionWithParams"></a>
   
### <a name="using-bound-action-with-parameters"></a>パラメーターを使用するバインドされているアクションを使用する
  
パラメーターを受け取るバインドされているアクションを使用します。 この操作は、現在のユーザーのキューにレターを追加します。 これを達成するには、<xref href="Microsoft.Dynamics.CRM.WhoAmI?text=WhoAmI Function" /> および<xref href="Microsoft.Dynamics.CRM.systemuser?text=systemuser EntityType" /> を、現在のユーザーのキューへの参照を取得するために使用します。  また <xref href="Microsoft.Dynamics.CRM.letter?text=letter EntityType" /> への参照が必要です。 先ほどこのプログラムで、この手紙がサンプル データとして作成されました。 次に、バインドされた <xref href="Microsoft.Dynamics.CRM.AddToQueue?text=AddToQueue Action" /> が呼び出されて、現在のユーザーのキューにレターが追加されます。 詳細: [バインドされたアクション](use-web-api-actions.md#bkmk_boundActions)  
  
 **要求**  
  
```http  
POST http://[Organization URI]/api/data/v9.0/queues(1f7bcc50-d3f6-e511-80d0-00155da84802)/Microsoft.Dynamics.CRM.AddToQueue HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Content-Length: 110  
  
{  
   "Target":{  
      "activityid":"4c920da5-fb4a-e611-80d5-00155da84802",  
      "@odata.type":"Microsoft.Dynamics.CRM.letter"  
   }  
}  
```  
  
 **応答**  
  
```http  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Content-Length: 170  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.AddToQueueResponse",  
   "QueueItemId":"67bdfabd-fc4a-e611-80d5-00155da84802"  
}  
```  
  
 **コンソール出力**  
  
```  
Bound Action: AddToQueue  
    QueueItemId returned from AddToQueue Action: 67bdfabd-fc4a-e611-80d5-00155da84802  
```  
  
<a name="bkmk_customActions"></a> 
  
## <a name="working-with-custom-actions"></a>ユーザー定義アクションの操作  

ソリューションのユーザー定義アクションを定義する場合、Common Data Service Web API を使用して呼び出します。 カスタム アクションに含まれる操作に副作用があるかどうかにかかわらず、それらの操作はデータを変更する可能性があり、したがって関数ではなくアクションと見なされます。 カスタム関数を作成する方法はありません。 詳細: [ユーザー定義アクションの使用](use-web-api-actions.md#bkmk_customActions)。  
  
このサンプルでは、2 つのカスタム アクションが用意されています。 両方にパラメーターが必要ですが、1 つはバインドされていて、もう 1 つはバインドされていません。  
  
- `sample_AddNoteToContact`: 2 つのパラメーターを受け取るバインドされたユーザー定義アクション。 1 つは `NoteTitle` で、もう 1 つは `NoteText` です。 このユーザー定義アクションは、<xref href="Microsoft.Dynamics.CRM.contact?text=contact EntityType" /> にメモを追加します。 以下は、このユーザー定義アクションの **情報** ページのスクリーン ショットです。  
  
 <!-- TODO:
 ![Custom Action &#45; AddNoteToContact information](../media/custom-action-add-note-contact.PNG "Custom Action - AddNoteToContact information")   -->
  
- `sample_CreateCustomer`: 作成されている顧客の種類に応じて異なるパラメーターが必要な、バインドされていないユーザー定義アクション。 たとえば、`AccountType` が ”取引先企業" の場合、`AccountName` パラメーターのみが必要です。 `AccountType` が、"取引先担当者" の場合、`ContactFirstName` および `ContactLastName` パラメーターが必要です。 以下は、このユーザー定義アクションの **情報** ページのスクリーン ショットです。  
<!-- TODO:  
 ![Custom Action &#45; CreateCustomer information](../media/custom-action-create-customer.PNG "Custom Action - CreateCustomer information")  
   -->
<a name="bkmk_boundCustomActionWithParams"></a>
   
### <a name="using-bound-custom-action-with-parameters"></a>パラメーターを使用するバインドされているカスタム アクションを使用する 
 
この例では、`sample_AddNoteToContact` ユーザー定義アクションが呼び出され、必要なパラメーターを使用する取引先担当者エンティティにバインドされます。 このユーザー定義アクションは、既存の取引先担当者にメモを追加します。 このアクションは、`annotationid` プロパティを持つエンティティを返します。 メモが追加されていることを示すために、`annotationid` が使用されてメモの情報を要求します。  
  
アクションの要求と応答。  
  
 **要求**  
  
```http  
POST http://[Organization URI]/api/data/v9.0/contacts(4d920da5-fb4a-e611-80d5-00155da84802)/Microsoft.Dynamics.CRM.sample_AddNoteToContact HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Content-Length: 80  
  
{  
   "NoteTitle":"The Title of the Note",  
   "NoteText":"The text content of the note."  
}  
```  
  
 **応答**  
  
```http  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Content-Length: 149  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#annotations/$entity",  
   "annotationid":"ba146d0b-fd4a-e611-80d5-00155da84802"  
}  
```  
  
 コメントの要求と応答。  
  
 **要求**  
  
```http  
GET http://[Organization URI]/api/data/v9.0/annotations(ba146d0b-fd4a-e611-80d5-00155da84802)?$select=subject,notetext&$expand=objectid_contact($select=fullname) HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
  
```  
  
 **応答**  
  
```http  
HTTP/1.1 200 OK  
OData-Version: 4.0  
Content-Length: 450  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#annotations(subject,notetext,objectid_contact,objectid_contact(fullname))/$entity",  
   "@odata.etag":"W/\"622978\"",  
   "subject":"The Title of the Note",  
   "notetext":"The text content of the note.",  
   "annotationid":"ba146d0b-fd4a-e611-80d5-00155da84802",  
   "objectid_contact":{  
      "@odata.etag":"W/\"622968\"",  
      "fullname":"Jon Fogg",  
      "contactid":"4d920da5-fb4a-e611-80d5-00155da84802"  
   }  
}  
```  
  
 **コンソール出力**  
  
```http  
Custom action: sample_AddNoteToContact  
    A note with the title 'The Title of the Note' and the content 'The text content of the note.' was created and associated with the contact Jon Fogg.  
```  
  
<a name="bkmk_unboundCustomActionWithParams"></a> 
  
### <a name="using-unbound-custom-action-with-parameters"></a>パラメーターを使用するバインドされていないカスタム アクションを使用する  

この操作は `sample_CreateCustomer` ユーザー定義アクションを呼び出して、”取引先企業” 顧客を作成します。 必須パラメーターは `account` の `CustomerType` に渡されます。  
  
 **要求**  
  
```http  
POST http://[Organization URI]/api/data/v9.0/sample_CreateCustomer HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Content-Length: 103  
  
{  
   "CustomerType":"account",  
   "AccountName":"Account Customer Created in WebAPIFunctionsAndActions sample"  
}  
```  
  
 **応答**  
  
```http  
HTTP/1.1 204 No Content  
OData-Version: 4.0  
  
```  
  
<a name="bkmk_boundCustomActionErrorHandling"></a> 
  
### <a name="handling-custom-action-exceptions"></a>ユーザー定義アクション例外の処理  

この例は、ユーザー定義アクションがユーザー定義のエラー メッセージを返せることを示します。 ユーザー定義の例外を、標準の例外と同じ方法で処理します。 `sample_CreateCustomer` ユーザー定義アクションからユーザー定義エラー メッセージを取得するには、この例では "取引先担当者" 顧客を作成します。 ただし、この `CustomerType` パラメーターに関しては、意図的に間違ったパラメーターを渡しています。 この操作は次に、例外をキャッチし、エラー メッセージを表示し、次に同じプログラムを続行します。  
  
 **要求**  
  
```http  
POST http://[Organization URI]/api/data/v9.0/sample_CreateCustomer HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Content-Length: 103  
  
{  
   "CustomerType":"contact",  
   "AccountName":"Account Customer Created in WebAPIFunctionsAndActions sample"  
}  
```  
  
 **応答**  
  
```http  
HTTP/1.1 500 Internal Server Error  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Content-Length: 2760  
  
{  
   "error":{  
      "code":"",  
      "message":"ContactFirstName and ContactLastName are required when CustomerType is contact.",  
      "innererror":{  
         "message":"ContactFirstName and ContactLastName are required when CustomerType is contact.",  
         ...[truncated]  
      }  
   }  
}  
```  
  
 **コンソール出力**  
  
```  
Expected custom error: ContactFirstName and ContactLastName are required when CustomerType is contact.  
```  
  
### <a name="see-also"></a>関連項目  

[Common Data Service Web API の使用](overview.md)<br />
[Web API 関数の使用](use-web-api-functions.md)<br />
[Web API アクションの使用](use-web-api-actions.md)<br />
[Web API 機能およびアクションのサンプル (C#)](samples/functions-actions-csharp.md)<br />

