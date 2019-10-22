---
title: 解析ステータスを確認する | Microsoft Docs
description: PowerApps チェッカーの Web APIを使用して GETリクエストを作成し、解析リクエスト ジョブのステータスの確認方法を説明します。
ms.custom: ''
ms.date: 06/04/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 6e2abe2d-2205-4d15-9e0f-5975ccc0484e
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

# <a name="check-for-analysis-status"></a>解析ステータスを確認する

[!INCLUDE [cc-beta-prerelease-disclaimer](../../../../includes/cc-beta-prerelease-disclaimer.md)]

URLは `analyze` APIへのリクエストに応じて `Location` ヘッダーの一部として返されます。 これはHTTP `GET` を介して解析ジョブのステータスを照会するために使用されます。 分析ジョブが終了すると、レスポンスの本文には結果出力をダウンロードできるURL、またはURLのリストが含まれています。 HTTPステータスコードの200が返されるまで、このURIを呼び出しが継続されます。 ジョブが継続している間は、 `analyze` から返されたURIと同じURIを含む `Location` のヘッダを含むHTTPステータスコードの202が返されます。 コード200の応答が返されると、 `resultFileUris` のプロパティにはzipファイルが作成され、ダウンロードが可能な単一または複数の出力の場所が含まれています。 [Static Analysis Results Interchange Format (SARIF)](https://sarifweb.azurewebsites.net) V2 形式のファイルは、このダウンロードされたzipファイルに含まれており、分析の結果を含む `JSON` 形式のファイルとなります。 応答の本体部分には、検出された問題数の要約を含む `IssueSummary` オブジェクトが含まれています。

> [!NOTE]
>  状態チェックの間隔は 15～60 秒空けることをお勧めします。 分析の実行には通常 1～5 分かかります。<br />
>  このAPIには、OAuth トークンが必要となりますが、これは分析ジョブを開始したのと同じクライアント アプリケーションのトークンである必要があります。

<a name="bkmk_headers"></a>

## <a name="headers"></a>ヘッダー

|Name|型|予測値|必須?|
|---|---|---|---|
|認証|文字列|AADのアプリケーションIDを要求する OAuth 1 ベアラトークン。|はい|
|x-ms-tenant-id|GUID|アプリケーションのテナントの ID。|はい|
|x-ms-correlation-id|GUID|解析実行の識別子 処理の全体 (アップロード、解析、状態) で同じIDを指定する必要があります|はい|

<a name="bkmk_responses"></a>

## <a name="expected-responses"></a>想定される反応

|HTTP 状態コード|シナリオ|結果|
|---|---|---|
|200|1つまたは複数の結果が見つかりました|以下の例を参照してください。 1件の結果が見つかりました。|
|202|処理中|以下の例を参照してください。 1件の結果が見つかりました。|
|403|許可されていません|要求元が分析要求の依頼者と同じではありません。|
|404|見つかりません|URLに指定された参照を持つ分析要求が見つかりません。|

### <a name="expected-response-headers"></a>予想回答ヘッダー

|Name|型|予測値|必須?|
|---|---|---|---|
|Location|URI|現在の状態を照会して結果の取得に使用するURI|はい|

### <a name="expected-response-body"></a>想定される本文の反応

次の表に、各要求に対する応答の構造概要を示します(HTTP200または202応答のみ)。

|プロパティ|型|予測値|必須?|
|---|---|---|---|
|privacyPolicy|文字列|プライバシーポリシーのURI。|あり|
|進捗状況|int|0 から 100 パーセントの範囲で処理完了までの進捗の値を表します。10 と表示された場合は処理が約10%完了したことを示します。|あり|
|runCorrelationId|GUID|それぞれの処理要求に含まれる要求の識別子。 必要に応じて、これを使用して要求に関連付けることができます。|あり|
|状態|文字列|ジョブの処理が継続されている場合、`InProgress` が返されます。 `Failed` は、サーバ上でのジョブの処理で重大な問題が発生した場合に返されます。 エラー プロパティには、詳細情報が含まれています。 `Finished` は、ジョブが問題なく正常に完了した場合に返されます。 `FinishedWithErrors` は、ジョブは正常に完了したが、1つまたは複数のエラーが発生した場合に返されます。 これは、レポートが完了していない可能性があることを通知します。 Microsoftはバックエンドにおけるこれらの問題を認識し、問題の診断と解決に取り組んでいきます。|あり|
|resultFileUris|文字列の配列|アウトプットを直接ダウンロードできるURIのリスト。 元の解析APのI呼び出しに含まれていたファイルごとに1つずつ存在する必要があります。|番号 これは処理が完了した場合にのみ含まれます。|
|issueSummary|IssueSummary|以下がプロパティのリストです|番号 これは処理が完了した場合にのみ含まれます。|
|issueSummary.criticalIssueCount|int|結果にて重大な深刻性を示した問題の数|あり|
|issueSummary.highIssueCount|int|結果にて高い深刻性を示した問題の数|あり|
|issueSummary.mediumIssueCount|int|結果にて中程度の深刻性を示した問題の数|あり|
|issueSummary.lowIssueCount|int|結果にて低い深刻性を示した問題の数|あり|
|issueSummary.informationalIssueCount|int|結果にて深刻性を示した問題の数|あり|

<a name="bkmk_checkStatusDone"></a>

## <a name="example-status-check-when-done"></a>例: 完了時のステータスチェック

この例では、ステータス チェック呼び出しを行い、結果を完了に更新します。

**要求**

```http
GET [Geographical URI]/api/status/9E378E56-6F35-41E9-BF8B-C0CC88E2B832&api-version=1.0
Accept: application/json
Content-Type: application/json; charset=utf-8
x-ms-correlation-id: 9E378E56-6F35-41E9-BF8B-C0CC88E2B832
x-ms-tenant-id: F2E60E49-CB87-4C24-8D4F-908813B22506
```

**応答**

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
    "privacyPolicy":"https://go.microsoft.com/fwlink/?LinkID=310140",
    "progress":100,
    "resultFileUris":["https://fakeblob.blob.core.windows.net/report-files/mySolution.zip?sv=2017-11-09&sr=b&sig=xyz&se=2019-06-11T20%3A27%3A59Z&sp=rd"],"runCorrelationId":"9E378E56-6F35-41E9-BF8B-C0CC88E2B832","status":"Finished","issueSummary":
    {
        "informationalIssueCount":0,
        "lowIssueCount":0,
        "mediumIssueCount":302,
        "highIssueCount":30,
        "criticalIssueCount":0
    }
}
```


### <a name="see-also"></a>関連項目

[PowerApps チェッカー Web API の使用](overview.md)<br />
[ルールセットの一覧の取得](retrieve-rulesets.md)<br />
[ルールの一覧の取得](retrieve-rules.md)<br />
[ファイルのアップロード](upload-file.md)<br />
[分析を呼び出す](analyze.md)<br />
