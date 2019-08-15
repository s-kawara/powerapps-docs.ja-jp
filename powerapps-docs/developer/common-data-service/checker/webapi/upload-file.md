---
title: 分析用のファイルをアップロードします| Microsoft Docs
description: 分析するファイルを回復してアップロードするために PowerApps チェッカー Web API を使用して POST 要求の形成方法を読みます。
ms.custom: ''
ms.date: 06/04/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 08d7d73b-1377-4d3f-b8ef-5c89b19dd735
caps.latest.revision: 21
author: mhuguet
ms.author: mhuguet
ms.reviewer: pehecke
manager: maustinjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="upload-a-file-for-analysis"></a>分析用のファイルをアップロードします。

[!INCLUDE [cc-beta-prerelease-disclaimer](../../../../includes/cc-beta-prerelease-disclaimer.md)]

分析ジョブの開始には、URL にアクセス可能になるために Azure BLOB へのパスが必要です。 アップロード サービスを使用して、指定場所の Azure Blob Storage にファイルをアップロードできる機能が付与されます。 分析を実行するためにアップロード済みの API を使用することは必須ではありません。 次のことに対する `POST` 要求を使用してアップロードできます。`[Geographical URI]/api/upload?api-version=1.0` 30 MB までのサイズのファイルをアップロードすることをサポートしています。 より大規模なものには、自分で外部アクセス可能な Azure Storage および SAS URIを供給する必要があります。

> [!NOTE]
>  この API には OAuth トークンが必要です。

<a name="bkmk_headers"></a>

## <a name="headers"></a>ヘッダー

|Name|型|予想値|必須?|
|---|---|---|---|
|認証|文字列|Azure Active Directory (AAD) アプリケーション ID クレームを含む OAuth 1 ベアラー トークン。|はい|
|x-ms-tenant-id|GUID|アプリケーションのテナントの ID。|はい|
|x-ms-correlation-id|GUID|分析実行の識別子。 実行全体 (アップロード、分析、状態) に同じ ID を指定する必要があります。|はい|
|コンテンツ タイプ|object|multipart/form-data|はい|
|Content-Disposition|object|名前およびファイル名パラメーターを含みます。 (例<br />`form-data; name="solution1.zip"; filename="solution1.zip"`|はい|

<a name="bkmk_responses"></a>

## <a name="expected-responses"></a>予想回答

|HTTP 状態コード|シナリオ|結果|
|---|---|---|
|200|アップロードに成功しました|本体に結果が見つかりませんでした|
|400|zip 以外のファイルが送信されたか、パラメータが正しくないか、ファイルにウイルスが含まれていました|本体に結果が見つかりませんでした|
|413|ファイルが大きすぎます|本体に結果が見つかりませんでした|

<a name="bkmk_upload"></a>

## <a name="example-upload-a-file"></a>例: ファイルのアップロード

ここでは、分析するファイルをアップグレードする例を示しています。

**要求**

```http
POST [Geographical URI]/api/upload
Accept: application/json
x-ms-correlation-id: 9E378E56-6F35-41E9-BF8B-C0CC88E2B832
x-ms-tenant-id: F2E60E49-CB87-4C24-8D4F-908813B22506
Content-Type: multipart/form-data
Content-Disposition: form-data; name=mySolution.zip; filename=mySolution.zip
```

**応答**

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

["https://mystorage.blob.core.windows.net/solution-files/0a4cd700-d1d0-4ef8-8318-e4844cc1636c/mySolution.zip?sv=2017-11-09&sr=b&sig=xyz&se=2019-06-11T19%3A05%3A20Z&sp=rd"]
```

### <a name="see-also"></a>関連項目

[PowerApps チェッカー Web API の使用](overview.md)<br />
[ルールセットの一覧の取得](retrieve-rulesets.md)<br />
[ルールの一覧の取得](retrieve-rules.md)<br />
[分析の呼び出し](analyze.md)<br />
[分析状態の確認](check-status.md)<br />