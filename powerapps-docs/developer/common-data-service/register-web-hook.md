---
title: webhook の登録 (Common Data Service for Apps) | Microsoft Docs
description: このトピックでは、プラグイン登録ツールを使用して webhook を登録する方法について説明します
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="register-a-webhook"></a>webhook の登録

プラグイン登録ツールを使用して webhook を登録します。 プラグイン登録ツールを取得するには、「[NuGet からツールをダウンロード](download-tools-nuget.md)」を参照してください。 

プラグイン登録ツールには、新しい **webhook の登録**オプションがあります。

![新しい webhook を登録するためのメニュー オプションが表示されます。 Ctrl + W のショートカット キーが使用できます。](media/register-new-web-hook.PNG)

webhook の登録時に、2 つの情報アイテムを提供する必要があります。


|アイテム  |内容  |
|---------|---------|
|**名前**|webhook を示す一意の名前。|
|**エンドポイント URL**|実行コンテキスト情報のポスト先となる URL。|
|**認証**|3 つの認証オプションのうちの 1 つ。 どの認証タイプでも、要求が正当であることを示すキーを提供する必要があります。|

## <a name="authentication-options"></a>認証オプション

どの webhook 登録認証オプションと値を使用するのが正しいかは、エンドポイントが何を期待するかによって異なります。  エンドポイントの所有者が何を使用するか伝える必要があります。 CDS for Apps で webhook を使用するには、エンドポイントは以下の 3 つの認証オプションのいずれかを使用する必要があります。


|種類​​  |内容  |
|---------|---------|
|**HttpHeader**|http 要求のヘッダーに 1 つ以上のキー値ペアが含まれます。<br />例:  <br />`Key1: Value1`<br />`Key2: Value2`|
|**WebhookKey**|`code` をキーとして使用してするクエリ文字列、およびエンドポイントに必要な値が含まれています。 プラグイン登録ツールを使用して webhook を登録するときは、値のみを入力します。<br />例:  <br />`?code=00000000-0000-0000-0000-000000000001`|
|**HttpQueryString**|クエリ文字列パラメーターとして 1 つ以上のキー値ペアが含まれます。<br />例:  <br />`?Key1=Value1&Key2=Value2`|

> [!NOTE]
> **WebhookKey** オプションは、認証クエリ文字列に `code` というキー名が想定されるため、[Azure Functions](https://azure.microsoft.com/services/functions/)で使用すると便利です。

構成されたエンドポイントへの要求は、要求で渡された認証オプションが一致しない場合は失敗します。 これはエンドポイントの責任です。

<a name="query-webhook-registrations"></a>

## <a name="query-webhook-registrations"></a>webhook 登録のクエリ

webhook 登録は [ServiceEndpoint Entity](reference/entities/serviceendpoint.md) に格納され、[Contract](reference/entities/serviceendpoint.md#BKMK_Contract) 値は `8` です。

**ServiceEndpoint** エンティティをクエリすることで登録された webhook の詳細を参照できます。

**Web API:**

`GET [organization URI]/api/data/v9.0/serviceendpoints?$filter=contract eq 8&$select= serviceendpointid,name,authtype,url`

詳細: [Web API を使用するクエリ データ](webapi/query-data-web-api.md)

**FetchXml:**

```xml
<fetch>
  <entity name="serviceendpoint" >
    <attribute name="serviceendpointid" />
    <attribute name="name" />
    <attribute name="authtype" />
    <attribute name="url" />
    <filter>
      <condition attribute="contract" operator="eq" value="8" />
    </filter>
  </entity>
</fetch> 
```

詳細: [FetchXML と FetchExpression の使用](org-service/entity-operations-query-data.md#use-fetchxml-with-fetchexpression)

設定された認証の値の詳細は [AuthValue](reference/entities/serviceendpoint.md#BKMK_AuthValue) プロパティにあり、取得できません。

## <a name="register-a-step-for-a-webhook"></a>webhook のステップの登録

webhook のステップの登録は、プラグインの手順の登録に似ています。 主な相違点は、構成情報を指定できないことです。 

プラグインのようにメッセージを指定し、適切な場合はエンティティのメッセージを指定します。 また、webhook を実行するイベント パイプラインの場所、実行モード、操作が成功した場合に **AsyncOperation** を削除するかどうかを指定します。 

![新しい webhook のステップを登録するプラグイン登録ダイアログ](media/Plugin-registration-register-webhook-step.PNG)

**ステップ名**と**説明**の情報は、選択したオプションに基づいて自動挿入されますが、それらは変更可能です。 それらをサポートするメッセージの**フィルタ属性**を設定しない場合、パフォーマンスのベスト プラクティスとして設定するよう求められます。

### <a name="execution-mode-and-debugging-your-web-hook-registration"></a>実行モードと webhook 登録のデバッグ

webhook の登録の選択は、不具合が生じた場合のデバッグのエクスペリエンスを左右します。

#### <a name="asynchronous-mode"></a>非同期モード
非同期実行モードを使用すると、asyncoperation ジョブが作成され、操作の成功または失敗を取得します。 成功した場合に asyncoperation を削除するよう選択すると、データベースのスペースを節約できます。 

発生したエラーはシステム ジョブに記録されます。 Web アプリケーションで、**設定 > システム > システム ジョブ**にアクセスして、任意の webhook のステータスを確認できます。 **ステータス**の値は**失敗**になります。 ジョブが失敗した理由の説明を表示するには、失敗したシステム ジョブ エンティティを開きます。

<a name="query-failed-asynchronous-jobs-for-a-given-step"></a>

#### <a name="query-failed-asynchronous-jobs-for-a-given-step"></a>特定のステップで失敗した非同期ジョブをクエリする

特定のステップの **sdkmessageprocessingstepid** を知っている場合、任意のエラーの [AsynchronousOperations エンティティ](reference/entities/asyncoperation.md) をクエリできます。 [OwningExtensionId](reference/entities/asyncoperation.md#BKMK_OwningExtensionId) 値を使用して、特定の登録されたステップに結果をフィルターできます。 次の例は *&lt;stepid&gt;* をステップの **sdkmessageprocessingstepid** として使用します。

> [!TIP]
> 特定のステップの **sdkmessageprocessingstepid** を取得するには、以下の[webhook に登録されたステップをクエリする](#query-steps-registered-for-a-webhook)を参照してください。

**Web API:**

`GET [organization URI]/api/data/v9.0/asyncoperations?$orderby=completedon desc&$filter=statuscode eq 31 and _owningextensionid_value eq @stepid&$select=name,friendlymessage,errorcode,message,completedon?@stepid=<stepid>`

詳細: [Web API を使用するクエリ データ](webapi/query-data-web-api.md)

**FetchXML:**

```xml
<fetch>
  <entity name="asyncoperation" >
    <attribute name="name" />
        <attribute name="friendlymessage" />
    <attribute name="errorcode" />
    <attribute name="message" />
    <attribute name="completedon" />     
    <filter>
      <condition attribute="owningextensionid" operator="eq" value="<stepid>" />
    </filter>
    <order attribute="completedon" descending="true" />
  </entity>
</fetch>
```

詳細: [FetchXML と FetchExpression の使用](org-service/entity-operations-query-data.md#use-fetchxml-with-fetchexpression)

#### <a name="synchronous-mode"></a>同期モード

[!INCLUDE [synchronous-webhook-error](includes/synchronous-webhook-error.md)]

> [!NOTE]
> 同期モードは、webhook によってトリガーされる操作をすぐに実行することが重要である場合、または webhook のペイロードをサービスが受け取らないとトランザクション全体が失敗するようにする場合に使用します。 簡単な webhook ステップの登録では、失敗を管理するための限定的なオプションが提供されていますが、詳細な制御が必要な場合はプラグイン ワークフロー活動を使用してwebhook を呼び出すこともできます。 詳細: [プラグインまたはワークフロー活動から webhook を呼び出す](use-webhooks.md#invoke-a-webhook-from-a-plugin-or-workflow-activity)。

## <a name="query-steps-registered-for-a-webhook"></a>webhook に登録されたステップをクエリする

登録された webhook のデータは [SdkMessageProcessingStep エンティティ](reference/entities/sdkmessageprocessingstep.md)にあります。

webhook の serviceendpointid を知っている場合に特定の webhook に登録されているステップをクエリできます。 登録されている webhook の ID を取得するクエリについては、「[webhook 登録のクエリ](#query-webhook-registrations)」を参照してください。

**Web API:**

この Web API クエリを使用でき、*&lt;id&gt;* は webhook の [ServiceEndpointId](reference/entities/serviceendpoint.md#BKMK_ServiceEndpointId) です。

```http
GET [organization URI]/api/data/v9.0/serviceendpoints(@id)/serviceendpoint_sdkmessageprocessingstep?$select=sdkmessageprocessingstepid,name,description,asyncautodelete,filteringattributes,mode,stage?@id=<id>
```

登録されたステップに関する詳細については、この Web API クエリを使用でき、*&lt;stepid&gt;* はステップの [SdkMessageProcessingStepId](reference/entities/sdkmessageprocessingstep.md#BKMK_SdkMessageProcessingStepId) です。

```http
GET [organization URI]/api/data/v9.0/sdkmessageprocessingsteps(@id)?$select=name,description,filteringattributes,asyncautodelete,mode,stage&$expand=plugintypeid($select=friendlyname),eventhandler_serviceendpoint($select=name),sdkmessagefilterid($select=primaryobjecttypecode),sdkmessageid($select=name)?@id=<stepid>
```

**FetchXML:**

この FetchXML を使用して 1 つのクエリで同じ情報を取得でき、*&lt;serviceendpointid&gt;* は webhook の ID です。

```xml
<fetch>
  <entity name="sdkmessageprocessingstep" >
    <attribute name="name" />
    <attribute name="filteringattributes" />
    <attribute name="stage" />
    <attribute name="asyncautodeletename" />
    <attribute name="description" />
    <attribute name="mode" />
    <link-entity name="serviceendpoint" from="serviceendpointid" to="eventhandler" link-type="inner" alias="endpnt" >
      <attribute name="name" />
      <filter>
        <condition attribute="serviceendpointid" operator="eq" value="<serviceendpointid>" />
      </filter>
    </link-entity>
    <link-entity name="sdkmessagefilter" from="sdkmessagefilterid" to="sdkmessagefilterid" link-type="inner" alias="fltr" >
      <attribute name="primaryobjecttypecode" />
    </link-entity>
    <link-entity name="sdkmessage" from="sdkmessageid" to="sdkmessageid" link-type="inner" alias="msg" >
      <attribute name="name" />
    </link-entity>
  </entity>
</fetch>
```

## <a name="next-steps"></a>次のステップ

[要求ログ サイトで webhook 登録をテストする](test-webhook-registration.md)<br />
[ｗebhook を使用してサーバー イベント用に外部ハンドラーを作成する](use-webhooks.md)

