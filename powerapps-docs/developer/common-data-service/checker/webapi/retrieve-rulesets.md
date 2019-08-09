---
title: ルールセットの一覧の取得 | Microsoft Docs
description: 使用できるルールセットの一覧を取得する PowerApps チェッカー Web API を使用して GET 要求の形成方法を読む。
ms.custom: ''
ms.date: 06/04/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 23c9391c-1697-47a3-a8f2-eedd5c862874
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

# <a name="retrieve-the-list-of-rulesets"></a>ルールセットの一覧の取得

[!INCLUDE [cc-beta-prerelease-disclaimer](../../../../includes/cc-beta-prerelease-disclaimer.md)]

ルールはルールセットを使用してグループ化されます。 ルールセットは制限なしで1つ以上のルールを持つことができます。 ルールには、ルールセットなしや複数のルールセットにすることはできません。 API、[Geographical URI]/api/ruleset を呼び出すことによって `GET` 要求を使用して、利用可能なすべてのルールセットの一覧を取得します。

> [!NOTE]
>  この API は OAuth トークンは必要ではありませんが、提供されれば一つを受け取ることができます。

<a name="bkmk_responses"></a>

## <a name="expected-responses"></a>予想回答率

|HTTP 状態コード|シナリオ|結果|
|---|---|---|
|200|1つまたは複数の結果が見つかりました|以下の例をご覧ください。 1つ以上の結果が返される場合があります。|
|204|結果が見つかりませんでした|結果回答本体は返されません。|

### <a name="expected-response-body"></a>想定される本文の反応

次の表は、それぞれの要求 (HTTP 200 要求のみ) に対する回答の構造を概説しています。

|プロパティ|型|予想値|必須?|
|---|---|---|---|
|id|Guid|ルールセットの識別子|あり|
|名前|文字列|ルールセットのフレンドリ名|あり|

<a name="bkmk_retrieve"></a>

## <a name="example-retrieve-all-rulesets"></a>例: すべてのルールセットの取得

この例では使用できるルールセットのすべてのデータを返します。

**要求**

```http
GET [Geographical URI]/api/ruleset?api-version=1.0
Accept: application/json
x-ms-correlation-id: 9E378E56-6F35-41E9-BF8B-C0CC88E2B832
Content-Type: application/json; charset=utf-8
```

**応答**

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "id": "083a2ef5-7e0e-4754-9d88-9455142dc08b",
        "name": "AppSource Certification"
    },
    {
        "id": "0ad12346-e108-40b8-a956-9a8f95ea18c9",
        "name": "Solution Checker"
    }
]
```

### <a name="see-also"></a>関連項目

[PowerApps チェッカー Web API の使用](overview.md)<br />
[ルールの一覧の取得](retrieve-rules.md)<br />
[ファイルのアップロード](upload-file.md)<br />
[分析の呼び出し](analyze.md)<br />
[分析状態の確認](check-status.md)<br />