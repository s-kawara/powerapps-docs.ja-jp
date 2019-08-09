---
title: コードを使用してモデル駆動型アプリを作成、管理、公開する | Microsoft Docs
description: コードを使用して PowerApps 内のモデル駆動型アプリを作成、管理、および公開する方法について学習します。
keywords: ''
ms.date: 03/04/2019
ms.service: powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 4261c476-2eff-10e3-a334-d02e0cbbb9d5
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

# <a name="create-manage-and-publish-model-driven-apps-using-code"></a>コードを使用してモデル駆動型アプリを作成、管理、公開する

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/create-manage-custom-business-apps-using-code -->

PowerApps アプリ デザイナーを使用してモデル駆動型アプリを作成することに加えて、モデル駆動型アプリをプログラムで作成および管理できます。 

> [!IMPORTANT]
> 必要でない限り、モデル駆動型アプリを構築するコードを記述する必要はありません。 アプリ デザイナーには、タイル ベースの情報構造およびさらに単純なインターフェイスを提供することにより、コードを記述する必要なしにモデル駆動型アプリを構築するための非常に単純で直観的なエクスペリエンスが用意されています。 確認: [アプリ デザイナーを使用して、モデル駆動型アプリを設計](../../maker/model-driven-apps/design-custom-business-apps-using-app-designer.md)  
  
モデル駆動型アプリの作成には以下の手順が含まれます。
1. [AppModule エンティティ](../common-data-service/reference/entities/appmodule.md) インターフェイスを作成してアプリとそのプロパティを定義します。
2. <xref:Microsoft.Dynamics.CRM.AddAppComponents> および <xref:Microsoft.Dynamics.CRM.RemoveAppComponents> アクションを使用するカスタム アプリのエンティティ、サイトマップ、および他のコンポーネントなどの、コンポーネントをアプリに追加または削除します。
3. <xref:Microsoft.Dynamics.CRM.ValidateApp> 関数を使用することにより、欠落している必須コンポーネントのアプリを確認します。
4. アプリを公開します。
5. 適切なセキュリティ ロールをモデル駆動型アプリに関連付けて、ユーザーにアクセスを提供します。


## <a name="create-your-model-driven-app-and-define-its-properties"></a>モデル駆動型アプリを作成およびプロパティを定義する

アプリを作成するには、システム管理者またはシステム カスタマイザーのセキュリティ ロール、または同等のアクセス許可が必要です。 

アプリを作成するには、少なくとも以下のプロパティを指定する必要があります。
- **name**: アプリに対して一意
- **uniquename**: これはユーザーのアプリの名前とは異なる場合があり、英文字および数字のみで構成されます。 このアプリを作成するとき、ソリューション発行者の接頭辞 (たとえば 'new_') が名前に自動的に付きます。 
- **webresourceid**: アプリのイメージ アイコンとして設定する Web リソースの ID です。 システムにはデフォルトのWebリソース (ID: 953b9fac-1e5e-e611-80d6-00155ded156f)  が用意されており、アプリケーションのアイコンとして使用できます。

次の Web API 要求はアプリの統合インターフェイスの種類を作成します。

```http
POST [Organization URI]/api/data/v9.0/appmodules HTTP/1.1
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Accept: application/json

{
    "name": "SDKTestApp",
    "uniquename":"SDKTestApp",
    "webresourceid":"953b9fac-1e5e-e611-80d6-00155ded156f"    
}
```

応答 **OData-EntityId** ヘッダーには、作成したアプリの URI が含まれています。

```http
HTTP/1.1 204 No Content
OData-Version: 4.0
OData-EntityId: [Organization URI]/api/data/v9.0/appmodules(dd621d4a-d898-e711-80e7-00155db763be)
```  

## <a name="add-or-remove-components-from-your-model-driven-app"></a>モデル駆動型アプリからコンポーネントを追加または削除する

モデル駆動型アプリに含める、サイトマップ、エンティティ、ダッシュボード、ビジネス プロセス フロー、ビュー、およびフォームなどの、アプリ内のコンポーネントを追加または削除することができます。 モデル駆動型アプリに追加可能なコンポーネントの詳細については、[アプリ デザイナーでアプリ コンポーネントを追加または編集](../../maker/model-driven-apps/add-edit-app-components.md) を参照してください。

<xref:Microsoft.Dynamics.CRM.AddAppComponents> アクションまたは <xref:Microsoft.Crm.Sdk.Messages.AddAppComponentsRequest> メッセージを使用してコンポーネントをモデル駆動型アプリに追加します。 そのアクションでは以下の内容を指定する必要があります。
- **AppId**: コンポーネントを追加するアプリケーションの ID
- **コンポーネント**追加するコンポーネントのコレクションです。 追加するコンポーネントの ID およびエンティティの種類を指定する必要があります。 Common Data Service Web API におけるエンティティ種別のリストは、 <xref:Microsoft.Dynamics.CRM.EntityTypeIndex>を参照してください。

次の Web API 要求は、ビュー (savedquery) およびフォーム (systemform) をアプリに追加します。

```http
POST [Organization URI]/api/data/v9.0/AddAppComponents HTTP/1.1
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Accept: application/json

{
    "AppId":"dd621d4a-d898-e711-80e7-00155db763be",
    "Components":[
        {
            "savedqueryid":"00000000-0000-0000-00aa-000000666000",
            "@odata.type":"Microsoft.Dynamics.CRM.savedquery"
        },
        {
            "formid":"c9e7ec2d-efca-4e4c-b3e3-f63c4bba5e4b",
            "@odata.type":"Microsoft.Dynamics.CRM.systemform"
        }
    ]
}
```

アプリからコンポーネントを削除するには、<xref:Microsoft.Dynamics.CRM.RemoveAppComponents> アクションまたは <xref:Microsoft.Crm.Sdk.Messages.RemoveAppComponentsRequest> メッセージを使用します。 このアクションは、**AddAppComponents** アクションと同じパラメーターのセットを使用します。

次の Web API 要求はビュー (savedquery) をアプリから削除します。 

```http
POST [Organization URI]/api/data/v9.0/RemoveAppComponents HTTP/1.1
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Accept: application/json

{
    "AppId":"dd621d4a-d898-e711-80e7-00155db763be",
    "Components":[
        {
            "savedqueryid":"00000000-0000-0000-00aa-000000666000",
            "@odata.type":"Microsoft.Dynamics.CRM.savedquery"
        }
    ]
}
```

## <a name="validate-your-model-driven-app"></a>モデル駆動型アプリを検証する

アプリの検証には、アプリが適切に動作することを確認するための、モデル駆動型アプリ内に追加済みのコンポーネントの依存関係のチェックが含まれます。 これはアプリ デザイナー で**検証**をクリックすることと同じです。 詳細: [アプリケーションを検証する](../../maker/model-driven-apps/validate-app.md)

<xref:Microsoft.Dynamics.CRM.ValidateApp> 関数または <xref:Microsoft.Crm.Sdk.Messages.ValidateAppRequest> メッセージを使用してアプリを検証します。 以下のWeb API要求は、次に示すIDを使用してモデル駆動型アプリケーションを検証する方法を説明しています: dd621d4a-d898-e711-80e7-00155db763be

`GET [Organization URI]/api/data/v9.0/ValidateApp(AppModuleId=dd621d4a-d898-e711-80e7-00155db763be)`

検証エラーが発生しなければ、応答は次のいずれかになります。

```http
HTTP/1.1 200 OK
OData-Version: 4.0

{
    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.ValidateAppResponse",
    "AppValidationResponse": {
        "ValidationSuccess": true,
        "ValidationIssueList": []
    }
}
```

アプリに検証の問題がある場合、応答により **ValidationIssueList** コレクション内にエラー/警告が表示されます。

```http
HTTP/1.1 200 OK
OData-Version: 4.0

{
    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.ValidateAppResponse",
    "AppValidationResponse": {
        "ValidationSuccess": false,
        "ValidationIssueList": [
            {
                "ErrorType": "Error",
                "Message": "App does not contain Site Map",
                "DisplayName": null,
                "ComponentId": "00000000-0000-0000-0000-000000000000",
                "ComponentType": 0,
                "ComponentSubType": 0,
                "ParentEntityId": "00000000-0000-0000-0000-000000000000",
                "ParentEntityName": null,
                "CRMErrorCode": -2147155684,
                "RequiredComponents": []
            },
            {
                "ErrorType": "Warning",
                "Message": "Account doesn’t reference a form or view. App users will see all forms and views.",
                "DisplayName": null,
                "ComponentId": "00000000-0000-0000-0000-000000000000",
                "ComponentType": 0,
                "ComponentSubType": 0,
                "ParentEntityId": "00000000-0000-0000-0000-000000000000",
                "ParentEntityName": null,
                "CRMErrorCode": -2147155691,
                "RequiredComponents": []
            }
        ]
    }
}
```

## <a name="publish-your-model-driven-app"></a>モデル駆動型アプリを公開する

必須コンポーネントをモデル駆動型アプリに追加して検証したら、ユーザーが使用可能にするために公開する必要があります。

<xref:Microsoft.Dynamics.CRM.PublishXml> アクションまたは <xref:Microsoft.Crm.Sdk.Messages.PublishXmlRequest> メッセージを使用してモデル駆動型アプリを公開します。 以下のWeb API要求は、次に示すIDを使用してモデル駆動型アプリケーションを公開する方法を説明しています: dd621d4a-d898-e711-80e7-00155db763be

```http
POST [Organization URI]/api/data/v9.0/PublishXml HTTP/1.1
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Accept: application/json

{  
  "ParameterXml":"<importexportxml><appmodules><appmodule>dd621d4a-d898-e711-80e7-00155db763be</appmodule></appmodules></importexportxml>"
}
```

## <a name="manage-access-to-model-driven-app-using-security-roles"></a>セキュリティ ロールを使用してモデル駆動型アプリへのアクセスを管理する

ユーザーがDynamics 365 ホーム ページの**設定** > **マイ アプリ**領域からアクセスすることができるように、アプリへのアクセス権限をユーザーに提供するため、セキュリティ ロールをモデル駆動型アプリに関連付けることができます。 関連するセキュリティ役割が付与され、 Common Data Service にてモデル駆動型アプリケーションの表示および使用ができるユーザー。 

[AppModule エンティティ](../common-data-service/reference/entities/appmodule.md) エンティティの **appmoduleroles_association** ナビゲーション プロパティを使用して、モデル駆動型アプリをセキュリティ ロールに関連付けます。 次の要求はモデル駆動型アプリをセキュリティ ロールと関連付ける方法を示しています。

```http
POST [Organization URI]/api/data/v9.0/appmodules(dd621d4a-d898-e711-80e7-00155db763be)appmoduleroles_association/$ref HTTP/1.1
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Accept: application/json

{  
  "@odata.id":"[Organization URI]/api/data/v9.0/roles(<roleId>)"
}
```

モデル駆動型アプリからセキュリティ ロールの関連付けを解除するには、同じナビゲーション プロパティで DELETE 要求を使用します。 たとえば、次のようになります。

```
DELETE  [Organization URI]/api/data/v9.0/appmodules(dd621d4a-d898-e711-80e7-00155db763be)/appmoduleroles_association/$ref?$id=[Organization URI]/api/data/v9.0/roles(<roleId)
```

## <a name="manage-your-model-driven-apps-and-its-components"></a>モデル駆動型アプリとそのコンポーネントの管理

このセクションでは、アプリの取得、アプリのプロパティの更新、アプリのコンポーネントの取得、およびアプリの削除に関する情報を提供します。

### <a name="retrieve-published-apps"></a>公開済みアプリの取得
公開済みアプリを取得するには、以下の要求を使用します。

`GET [Organization URI]/api/data/v9.0/appmodules?$select=name,clienttype`

### <a name="retrieve-unpublished-apps"></a>未公開のアプリの取得
未公開アプリを取得するには、<xref:Microsoft.Dynamics.CRM.RetrieveUnpublishedMultiple> 関数を使用します。 たとえば、次のようになります。

`GET [Organization URI]/api/data/v9.0/appmodules/Microsoft.Dynamics.CRM.RetrieveUnpublishedMultiple()?$select=name,clienttype`

### <a name="retrieve-components-in-a-published-model-driven-app"></a>公開済みモデル駆動型アプリ内のコンポーネントの取得
モデル駆動型アプリのアプリ コンポーネントを取得するには、<xref:Microsoft.Dynamics.CRM.RetrieveAppComponents> 関数または <xref:Microsoft.Crm.Sdk.Messages.RetrieveAppComponentsRequest> メッセージを使用します。 たとえば、次のようになります。

`GET [Organization URI]/api/data/v9.0/RetrieveAppComponents(AppModuleId=dd621d4a-d898-e711-80e7-00155db763be)`

### <a name="retrieve-security-roles-associated-with-published-model-driven-app"></a>公開済みモデル駆動型アプリに関連付けられたセキュリティ ロールの取得

ユーザーのモデル駆動型アプリに関連付けられたセキュリティ ロールを取得するには、`$expand` システム クエリ オプションを **appmoduleroles_association** ナビゲーション プロパティと共に使用します。 たとえば、ID: dd621d4a-d898-e711-80e7-00155db763be のモデル駆動型アプリケーションに関連付けられたすべてのセキュリティ役割を取得する要求は次のとおりです。

`GET [Organization URI]/api/data/v9.0/appmodules(dd621d4a-d898-e711-80e7-00155db763be)?$expand=appmoduleroles_association&$select=name,appmoduleroles_association`

### <a name="delete-model-driven-apps"></a>モデル駆動型アプリを削除する

DELETE 要求を使用してモデル駆動型アプリを削除します。 たとえば、次のようになります。

`DELETE [Organization URI]/api/data/v9.0/appmodules(dd621d4a-d898-e711-80e7-00155db763be)`

## <a name="client-api-support-for-model-driven-apps"></a>モデル駆動型アプリのクライアント API サポート

以下のクライアント API を使用してモデル駆動型アプリの作業をすることができます。

- [getCurrentAppName](clientapi/reference/xrm-utility/getglobalcontext/getcurrentappname.md)
- [getCurrentAppProperties](clientapi/reference/xrm-utility/getglobalcontext/getCurrentAppProperties.md)
- [getCurrentAppUrl](clientapi/reference/xrm-utility/getglobalcontext/getCurrentAppUrl.md) 
  
### <a name="see-also"></a>関連項目  
[アプリ デザイナーを使用してモデル駆動型アプリを設計する](../../maker/model-driven-apps/design-custom-business-apps-using-app-designer.md)
 
