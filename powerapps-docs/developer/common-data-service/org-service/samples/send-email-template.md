---
title: 'サンプル: テンプレートを使用した電子メールの送信 (Common Data Service for Apps) | Microsoft Docs'
description: このサンプルは、テンプレートを使用した電子メール メッセージの送信方法を説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: samples
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-send-an-email-using-a-template"></a>サンプル: テンプレートを使用した電子メールの送信

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-send-email-template -->

このサンプルでは、[SendEmailFromTemplateRequest](https://docs.microsoft.com/en-us/dotnet/api/microsoft.crm.sdk.messages.sendemailfromtemplaterequest?view=dynamics-general-ce-9) メッセージを使用して、テンプレートを使用した電子メール メッセージを送信する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/SendEmailUsingTemp) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`SendEmailFromTemplateRequest` メッセージは、テンプレートを使用して電子メール メッセージを送信するために必要なデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. 電子メールを送信する取引先担当者レコードを作成します (To: フィールド)。

### <a name="demonstrate"></a>使用方法

1. `ActivityParty` は、電子メールの `From:` および `To:` 活動関係者を作成します。
2. 電子メール メッセージを作成します。
3. 種類が `Contact` の電子メール テンプレートの 1 つを取得する `QueryExpression` クエリ。
4. `SendEmailFromTemplateRequest` は、テンプレートを使用して電子メール メッセージを送信します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたサンプル データを削除するためのオプションを表示します。

    サンプルで作成されたエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除しても同じ結果を得られます。
