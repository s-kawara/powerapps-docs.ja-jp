---
title: HTTP 要求の作成とエラーの処理 (アプリ用 Common Data Service) | Microsoft Docs
description: Web APIと対話するHTTPリクエストの一部を形成するHTTPメソッドおよびヘッダー、ならびに応答で返されるエラーを特定し、処理する方法について説明します
ms.custom: ''
ms.date: 11/05/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 64a39182-25de-4d31-951c-852025a75811
caps.latest.revision: 13
author: brandonsimons
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="compose-http-requests-and-handle-errors"></a>HTTP 要求の作成とエラーの処理

HTTP 要求を作成および送信することによって、Web API を操作します。 適切な HTTP ヘッダーの設定方法を理解し、応答にエラーが含まれている場合は、エラーを処理する必要があります。  

<a name="bkmk_url_versions"></a>

## <a name="web-api-url-and-versions"></a>Web API URL およびバージョン

Web API にアクセスするには、次の表にある部分を使用して URL を構成する必要があります。

|部分|説明|
|--|--|
|プロトコル| `https://`|
|環境名|環境に適用される一意の名前。 会社名が *Contoso* である場合、`contoso` となる可能性があります。|
|地域|環境は通常、地理的に近いデータ センターで利用できます。<br />北米: `crm`<br />南米: `crm2`<br />カナダ: `crm3`<br />ヨーロッパ、中東、およびアフリカ (EMEA): `crm4`<br />アジア太平洋地域 (APAC): `crm5`<br />オセアニア: `crm6`<br />日本: `crm7`<br />インド: `crm8`<br />北米 2: `crm9`<br />英国: `crm11`<br />新しいデータ センター領域が開かれるにつれて、より多くの値が追加されます。|
|基本 URL|`dynamics.com.`|
|Web API パス|Web API へのパスは `/api/data/` です。|
|[バージョン]|   バージョンは次のように表記されます: `v[Major_version].[Minor_version][PatchVersion]/`。 このリリースの有効なバージョンは `v9.0` です。|
|リソース |使用するエンティティの名前、機能、またはアクション。|


使用する URL は次のコンポーネントで構成されます: プロトコル + 環境名 + 地域 + 基本 URL + Web API パス + バージョン + リソース。

<a name="version_compatiblity"></a>

###   <a name="version-compatibility"></a>バージョン互換性

このリリースでは以前のバージョンでは使用できない機能を導入しています。 それ以降のマイナー バージョンには追加機能が提供されるかもしれませんが、以前のマイナー バージョンには遡って適用されない可能性があります。 v9.0 を対象として作成したコードは、使用する URL で v9.0 を参照すると 将来のバージョン でも引き続き機能します。

新しい機能が導入されると、以前のバージョンと競合する可能性があります。 このことは、サービスがより良いパフォーマンスをするために必要です。 通常は、機能はバージョン間で変わりませんが、変わらないのが当然だと考えるべきではありません。

> [!NOTE]
> v8.xの小さいリリースとは違い、将来のバージョンに追加される新しい機能またはそのほかの変更は以前のバージョンに適用されません。
> 使用しているバージョンを変更したら、コードを使用するおよびテストするサービスのバージョンに注意を払う必要があります。

<a name="bkmk_methods"></a>

## <a name="http-methods"></a>HTTP メソッド

 HTTP 要求では、さまざまなメソッドを適用できます。 Web API を使用する場合、次の表に記載されているメソッドのみを使用します。  
  
|メソッド|使用法|  
|------------|-----------|  
|GET|関数を呼び出すときを含め、データを取得するときに使用します。 取得の成功を表す期待されるステータス コードは、200 OK です。|  
|POST|エンティティを作成するとき、またはアクションを呼び出すときに使用します。|  
|PATCH|エンティティを更新するとき、または upsert 操作を実行するときに使用します。|  
|DELETE|エンティティまたはエンティティの個々のプロパティを削除するときに使用します。|  
|PUT|エンティティの個々のプロパティを更新するために、限られた状況で使用します。 このメソッドは、ほとんどのエンティティを更新するときにお勧めしません。 モデル エンティティを更新するときにこのメソッドを使用します。|  
  
<a name="bkmk_headers"></a>

## <a name="http-headers"></a>HTTP ヘッダー

OData プロトコルでは JSON と ATOM の両方の形式を使用できますが、Wb API では JSON のみがサポートされています。 したがって、次のヘッダーは適用可能です。  
  
すべての要求には、Acceptヘッダー値として `application/json` を含める必要があります。予期される応答がない場合でも、含める必要があります。 応答でエラーが返される場合、エラーは JSON として返されます。 このヘッダーが含まれていなくてもコードは動作しますが、ベスト プラクティスとして、このヘッダーを含めることをお勧めします  
  
現在の  OData バージョンの 4.0 ですが、今後のバージョンで新機能が使用できるようになる可能性があります。 将来のその特定の時点でコードに適用される  OData バージョンについてのあいまいさをなくすため、現在の  OData バージョンとコードに適用する最大バージョンを表す明示的なステートメントを必ず含める必要があります。 値として 4.0 が設定された OData-Version  および  OData-MaxVersion ヘッダーの両方を使用します。  
 
コレクション値ナビゲーション プロパティを展開するクエリは、最新の変更を反映しないそれらのプロパティのキャッシュされたデータを返す場合があります。 Web API要求のブラウザのキャッシュを上書きするためには、要求の本体に `If-None-Match: null` ヘッダーを含めます。 詳細については、[HTTP/1.1 ハイパーテキスト トランスファー プロトコル (HTTP/1.1) : 条件要求 3.2: If-None-Match](https://tools.ietf.org/html/rfc7232#section-3.2)を参照してください。
 
すべての HTTP ヘッダーに、少なくとも次のヘッダーを含める必要があります。  
  
```
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0
If-None-Match: null
```  
  
要求の本文に  JSON データが含まれるすべての要求に、`application/json` を値に持つ Content-Type ヘッダーを含める必要があります。  
  
```  
Content-Type: application/json  
```  
  
追加のヘッダーを使用して特定の機能を有効にすることができます。  
  
-   エンティティに対して作成 (POST) または更新 (PATCH) 操作でデータを返すには、`return=representation` 基本設定を含めます。 この基本設定を POST リクエストに適用する場合、正常な応答として、201 (Created) というステータスが表示されます。 PATCH リクエストの場合は、正常な応答として、200 (OK) というステータスが表示されます。 この基本設定を適用しない場合、既定では応答の本文メッセージにはデータが返されないことを反映して、両方の操作に対して、204 (No Content) というステータスが返されます。  
  
-   クエリに書式設定された値を返すには、[設定](https://tools.ietf.org/html/rfc7240)ヘッダーを使用してMicrosoft.Dynamics.CRM.formattedvalueに設定されているodata.include-annotations 基本設定を含めます。 詳細: [書式設定値を含める](query-data-web-api.md#bkmk_includeFormattedValues)  
  
-   また、 Prefer ヘッダーと odata.maxpagesize オプションを使用して、返されるページ数を指定することもできます。 詳細: [ページに戻すエンティティ数の指定](query-data-web-api.md#bkmk_specifyNumber)  
  
-   別のユーザーを偽装するには (呼び出し元がこれを行う権限を持っている場合)、MSCRMCallerID ヘッダーと、偽装する対象となるユーザーの systemuserid 値を追加します。 詳細情報: [Web API を使用して別のユーザーを偽装する](impersonate-another-user-web-api.md)。  
  
-   オプティミスティック同時実行を適用するには、[If-Match ヘッダー](https://tools.ietf.org/html/rfc7232#section-3.1)と Etag 値 を適用できます。 詳細: [オプティミスティック同時実行の適用](perform-conditional-operations-using-web-api.md#bkmk_Applyoptimisticconcurrency)。  
  
-   upsert 操作でエンティティを実際に作成または更新するかどうかを制御するために、If-Match および [If-None-Match](https://tools.ietf.org/html/rfc7232#section-3.2) ヘッダーを使用することもできます。 詳細: [エンティティの Upsert](update-delete-entities-using-web-api.md#bkmk_upsert)。  
  
-   バッチ操作を実行する場合、要求では本文で送信される部分ごとに多数の異なるヘッダーを適用する必要があります。 詳細: [Web API を使用してバッチ操作を実行する](execute-batch-operations-using-web-api.md)。  
  
<a name="bkmk_statusCodes"></a>

## <a name="identify-status-codes"></a>ステータス コードの確認

 http 要求が成功したか失敗したかにかかわらず、応答にはステータス コードが含まれます。 アプリ用 Common Data Service Web API で返されるステータス コードには、次が含まれます。  
  
|Code|説明|型|  
|----------|-----------------|----------|  
|200 OK|操作で応答本文にデータが返されるときに発生します。|成功|  
|201 Created|エンティティの POST 操作が成功し、要求に `return=representation` 基本設定を指定した場合は、これが発生します。|成功|  
|204 コンテンツがありません|操作は成功したものの応答本文にデータが返されないときに発生します。|成功|  
|304  更新されていません|エンティティが最後に取得されてから以降に変更されたかどうかをテストするときに発生します。 詳細: [条件付き検索](perform-conditional-operations-using-web-api.md#bkmk_DetectIfChanged)|リダイレクト|  
|403 無効です|次のような種類のエラーの場合に発生します。<br /><br /> -   AccessDenied<br />-   AttributePermissionReadIsMissing<br />-   AttributePermissionUpdateIsMissingDuringUpdate<br />-   AttributePrivilegeCreateIsMissing<br />-   CannotActOnBehalfOfAnotherUser<br />-   CannotAddOrActonBehalfAnotherUserPrivilege<br />-   CrmSecurityError<br />-   InvalidAccessRights<br />-   PrincipalPrivilegeDenied<br />-   PrivilegeCreateIsDisabledForOrganization<br />-   PrivilegeDenied<br />-   unManagedinvalidprincipal<br />-   unManagedinvalidprivilegeedepth|クライアント エラー|  
|401 承認されていません|次のような種類のエラーの場合に発生します。<br /><br /> -   BadAuthTicket<br />-   ExpiredAuthTicket<br />-   InsufficientAuthTicket<br />-   InvalidAuthTicket<br />-   InvalidUserAuth<br />-   MissingCrmAuthenticationToken<br />-   MissingCrmAuthenticationTokenOrganizationName<br />-   RequestIsNotAuthenticated<br />-   TamperedAuthTicket<br />-   UnauthorizedAccess<br />-   UnManagedInvalidSecurityPrincipal|クライアント エラー|  
|413 ペイロードが大きすぎます|要求の長さが大きすぎるときに発生します。|クライアント エラー|  
|400 不正なリクエスト|引数が無効である場合に発生します。|クライアント エラー|  
|404 見つかりません|リソースが存在しない場合に発生します。|クライアント エラー|  
|405 許可されていないメソッド|このエラーは、メソッドとリソースの組み合わせが正しくない場合に発生します。 たとえば、DELETE または PATCH をエンティティのコレクションに対して使用することはできません。<br /><br /> 次のような種類のエラーの場合に発生します。<br /><br /> -   CannotDeleteDueToAssociation<br />-   InvalidOperation<br />-   NotSupported|クライアント エラー|  
|412 前提条件失敗|次のような種類のエラーの場合に発生します。<br /><br /> -   ConcurrencyVersionMismatch<br />-   DuplicateRecord|クライアント エラー|
|429 リクエストが多すぎます|API 制限を超えた場合に発生します。 詳細: [API の制限](../api-limits.md)|クライアント エラー|  
|501 実装されていません|要求した何らかの操作が実装されていない場合に発生します。|サーバー エラー|  
|503 サービスは利用できません|Web API サービスを使用できない場合に発生します。|サーバー エラー|  
  
<a name="bkmk_parseErrors"></a>

## <a name="parse-errors-from-the-response"></a>応答からのエラーの解析

 エラーに関する詳細が応答に JSON として含まれています。 エラーはこの形式になります。  
  
```json  
{  
 "error":{  
  "code": "<This code is not related to the http status code and is frequently empty>",  
  "message": "<A message describing the error>",  
  "innererror": {  
   "message": "<A message describing the error, this is frequently the same as the outer message>",  
   "type": "Microsoft.Crm.CrmHttpException",  
   "stacktrace": "<Details from the server about where the error occurred>"  
  }  
 }  
}  
```  
  
### <a name="see-also"></a>関連項目  

[Web API を使用して演算を実行する](perform-operations-web-api.md)<br />
[Web API を使用したクエリ データ](query-data-web-api.md)<br />
[Web API を使用してエンティティを作成する](create-entity-web-api.md)<br />
[Web API を使用してエンティティを取得する](retrieve-entity-using-web-api.md)<br />
[Web API を使用したエンティティの更新と削除](update-delete-entities-using-web-api.md)<br />
[Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)<br />
[Web API 関数の使用](use-web-api-functions.md)<br />
[Web API アクションの使用](use-web-api-actions.md)<br />
[Web API を使用してバッチ操作を実行する](execute-batch-operations-using-web-api.md)<br />
[Web API を使用して別のユーザーを偽装する](impersonate-another-user-web-api.md)<br />
[Web API を使用する条件付き演算を実行する](perform-conditional-operations-using-web-api.md)
