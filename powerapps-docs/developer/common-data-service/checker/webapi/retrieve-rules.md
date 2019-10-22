---
title: ルールの一覧の取得 | Microsoft Docs
description: 使用できるルールの一覧を取得するために PowerApps チェッカー Web API を使用して GET 要求の形成方法を説明します。
ms.custom: ''
ms.date: 06/04/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: a8dc3019-c49e-48e4-a646-8a3a3fecd3a6
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

# <a name="retrieve-the-list-of-rules"></a>ルールの一覧の取得

[!INCLUDE [cc-beta-prerelease-disclaimer](../../../../includes/cc-beta-prerelease-disclaimer.md)]

ルールはルールセットを使用してグループ化されます。 ルールには、ルールセットなしや複数のルールセットにすることはできません。 API `[Geographical URI]/api/rule` を呼び出すことによって利用可能なルールセット (複数可) の一覧を取得するために `GET` 要求を使用します。 この API を呼び出すためにいくつかの種類がありますが、最も一般的な用法は、特定のルールセットのルールの一覧を取得することです。

> [!NOTE]
>  この API は OAuth トークンは必要ではありませんが、提供されれば一つを受け取ることができます。

<a name="bkmk_headers"></a>

## <a name="headers"></a>ヘッダー

|Name|型|予想値|必須?|
|---|---|---|---|
|言語の承諾|文字列|言語コード (たとえば、 en-US)。 既定値は en-US です。|いいえ

<a name="bkmk_params"></a>

## <a name="parameters"></a>パラメーター

|Name|型|予想値|必須?|
|---|---|---|---|
|ルールセット|文字列|ルールセットの名前や ID、ルールセットの一覧、あるいはコンマやセミコロンで区切られた名前 (「ソリューション チェッカー」など)。|いいえ|
|includeMessageFormats|bool|`true` に設定すると、可能なメッセージの種類の一覧がある場合は言語要求の結果に含まれます。 これは、翻訳を複数の言語にするために役立ちます。 必要のない場合は、このパラメーターを与えたり、値として `false` を提供したりしないでください。このパラメーターは回答のサイズを増大し、処理時間を長くしてしまいます。|いいえ|

<a name="bkmk_responses"></a>

## <a name="expected-responses"></a>予想回答

|HTTP 状態コード|シナリオ|結果|
|---|---|---|
|200|1つまたは複数の結果が見つかりました|以下の例を参照してください。 1つ以上の結果が返される場合があります。|
|204|結果が見つかりませんでした|回答の本体に結果が見つかりませんでした。|

### <a name="expected-response-body"></a>想定される本文の反応

次の表は、それぞれの要求 (HTTP 200 要求のみ) に対する回答の構造を概説しています。

|プロパティ|型|予想値|必須?|
|---|---|---|---|
|コード|文字列|ルールの識別子、ルール ID として参照されることもあります。|あり|
|概要|文字列|ルールの概要。|あり|
|説明|文字列|ルールに関する詳細な説明。|あり|
|guidanceUrl|URI|公表されたガイダンスを見つけるために公開する URL。 専用サポート ガイダンス記事のないケースが一部ある場合があります。|あり|
|include|boolean|分析にルールを含めるサービスに対するシグナル。 これがこの APIに対する `true` になります。|なし|
|messageTemplates|配列|このプロパティ値は、 `includeMessageFormats` が `true` の場合のみ含まれます。|なし|
|messageTemplates.ruleId|文字列| `code` プロパティとして同じ ID 値を返します。|あり|
|messageTemplates.messageTemplateId|文字列| ルールのためのさまざまな問題メッセージを通知するために、スタティック分析結果の相互交換フォーマット (SARIF) レポートで使用される識別子。|あり|
|messageTemplates.messageTemplate|文字列|ルールを報告する問題のシナリオ向けのさまざまなメッセージのテキスト。 これはる詳細なメッセージを構成するために使用できる SARIF レポートで提供されている因数のトークンを含めることができるフォーマット文字列です。|あり|

<a name="bkmk_retrieveForRuleset"></a>

## <a name="example-retrieve-rules-for-a-ruleset-in-another-language"></a>例: 別の言語でルールセットのルールを取得します。

この例では、フランス語の *ソリューションのチェッカー* ルールセットのルールのすべてのデータを返します。 希望言語が英語の場合は、Accept-Language ヘッダーを削除します。

**要求**

```http
GET [Geographical URI]/api/rule?ruleset=083A2EF5-7E0E-4754-9D88-9455142DC08B&api-version=1.0
x-ms-correlation-id: 9E378E56-6F35-41E9-BF8B-C0CC88E2B832
Accept: application/json
Content-Type: application/json; charset=utf-8
Accept-Language: fr
```

**応答**

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "description": "Ne pas implémenter d’activités de workflow Microsoft Dynamics CRM 4.0",
        "guidanceUrl": "http://go.microsoft.com/fwlink/?LinkID=398563&error=il-avoid-crm4-wf&client=PAChecker",
        "include": true,
        "code": "il-avoid-crm4-wf",
        "summary": "Ne pas implémenter d’activités de workflow Microsoft Dynamics CRM 4.0",
        "howToFix": {
            "summary": ""
        }
    },
    {
        "description": "Utiliser InvalidPluginExecutionException dans des plug-ins et activités de workflow",
        "guidanceUrl": "http://go.microsoft.com/fwlink/?LinkID=398563&error=il-use-standard-exception&client=PAChecker",
        "include": true,
        "code": "il-use-standard-exception",
        "summary": "Utiliser InvalidPluginExecutionException dans des plug-ins et activités de workflow",
        "howToFix": {
            "summary": ""
        }
    },
...
]
```

<a name="bkmk_retrieveAll"></a>

## <a name="example-retrieve-all"></a>例: すべてを取得

この例では使用できるルールのすべてのデータを返します。

**要求**

```http
GET [Geographical URI]/api/rule?api-version=1.0
Accept: application/json
Content-Type: application/json; charset=utf-8
```

**応答**

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "description": "Retrieve specific columns for an entity via query APIs",
        "guidanceUrl": "http://go.microsoft.com/fwlink/?LinkID=398563&error=il-specify-column&client=PAChecker",
        "include": true,
        "code": "il-specify-column",
        "summary": "Retrieve specific columns for an entity via query APIs",
        "howToFix": {
            "summary": ""
        }
    },
    {
        "description": "Do not duplicate plug-in step registration",
        "guidanceUrl": "http://go.microsoft.com/fwlink/?LinkID=398563&error=meta-remove-dup-reg&client=PAChecker",
        "include": true,
        "code": "meta-remove-dup-reg",
        "summary": "Do not duplicate plug-in step registration",
        "howToFix": {
            "summary": ""
        }
    },
...
]
```

<a name="bkmk_retrieveForRuleset"></a>

## <a name="example-retrieve-for-a-ruleset-with-message-formats"></a>例: メッセージ フォーマットを持つルールセットを取得します。

この例では、フランス語の *ソリューションのチェッカー* ルールセットのルールのすべてのデータを返します。 希望言語が英語の場合は、Accept-Language ヘッダーを削除します。

**要求**

```http
GET [Geographical URI]/api/rule?ruleset=083A2EF5-7E0E-4754-9D88-9455142DC08B&includeMessageFormats=true&api-version=1.0
Accept: application/json
Content-Type: application/json; charset=utf-8
```

**応答**

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "description": "Do not implement Microsoft Dynamics CRM 4.0 workflow activities",
        "guidanceUrl": "http://go.microsoft.com/fwlink/?LinkID=398563&error=il-avoid-crm4-wf&client=PAChecker",
        "include": true,
        "code": "il-avoid-crm4-wf",
        "summary": "Do not implement Microsoft Dynamics CRM 4.0 workflow activities",
        "howToFix": {
            "summary": ""
        },
        "messageTemplates": [
            {
                "ruleId": "il-avoid-crm4-wf",
                "messageTemplateId": "message1",
                "messageTemplate": "Update the {0} class to derive from System.Workflow.Activities.CodeActivity, refactor Execute method implementation, and remove Microsoft.Crm.Workflow.CrmWorkflowActivityAttribute from type"
            },
            {
                "ruleId": "il-avoid-crm4-wf",
                "messageTemplateId": "message2",
                "messageTemplate": "Change the {0} property's type from {1} to {2} Argument &lt;T&gt; type"
            },
            {
                "ruleId": "il-avoid-crm4-wf",
                "messageTemplateId": "message3",
                "messageTemplate": "Replace the Microsoft.Crm.Workflow.Crm{0}Attribute with Microsoft.Xrm.Sdk.Workflow.{0}Attribute"
            },
            {
                "ruleId": "il-avoid-crm4-wf",
                "messageTemplateId": "message4",
                "messageTemplate": "Remove the {0} System.Workflow.ComponentModel.DependencyProperty type field"
            }
        ]
    },
    {
        "description": "Use InvalidPluginExecutionException in plug-ins and workflow activities",
        "guidanceUrl": "http://go.microsoft.com/fwlink/?LinkID=398563&error=il-use-standard-exception&client=PAChecker",
        "include": true,
        "code": "il-use-standard-exception",
        "summary": "Use InvalidPluginExecutionException in plug-ins and workflow activities",
        "howToFix": {
            "summary": ""
        },
        "messageTemplates": [
            {
                "ruleId": "il-use-standard-exception",
                "messageTemplateId": "message1",
                "messageTemplate": "An unguarded throw of type {0} was detected. Refactor this code to either throw an exception of type InvalidPluginExecutionException or guard against thrown exceptions of other types."
            },
            {
                "ruleId": "il-use-standard-exception",
                "messageTemplateId": "message2",
                "messageTemplate": "An unguarded rethrow of type {0} was detected. Refactor this code to either throw an exception of type InvalidPluginExecutionException or guard against thrown exceptions of other types."
            }
        ]
    },
...
]
```

### <a name="see-also"></a>関連項目

[PowerApps チェッカー Web API の使用](overview.md)<br />
[ルールセットの一覧の取得](retrieve-rulesets.md)<br />
[ファイルのアップロード](upload-file.md)<br />
[分析の呼び出し](analyze.md)<br />
[分析状態の確認](check-status.md)<br />