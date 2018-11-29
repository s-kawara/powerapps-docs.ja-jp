---
title: 'サンプル: 電子メール メッセージの登録 (アプリ用 Common Data Service) | Microsoft Docs'
description: <Description>
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
# <a name="sample-promote-an-email-message"></a>サンプル: 電子メール メッセージの登録

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-promote-email-message -->

このサンプルは、[DeliverPromoteEmailRequest](https://docs.microsoft.com/en-us/dotnet/api/microsoft.crm.sdk.messages.deliverpromoteemailrequest?view=dynamics-general-ce-9) メッセージを使用して、アプリ用 Common Data Service で指定された電子メール メッセージから電子メール活動インスタンスを作成する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/PromoteEmail) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`DeliverPromoteEmailRequest` メッセージは、指定された電子メール メッセージから電子メール活動レコードを作成する必要があるデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。

### <a name="demonstrate"></a>使用方法

1. 取引先担当者に送信する電子メール メッセージを作成します (To: フィールド)。
2. `WhoAmIRequest` は、電子メールを送信するシステム ユーザーを取得します (From: フィールド)。
3. `DeliverPromoteEmailRequest` メッセージによって要求が作成され、実行されます。
4. 電子メール ステータスの値として指定できる値の匿名型を定義することにより、成功したことを確認します。 
5. 配布された電子メールを照会し、ステータス コードが`sent`であることを確認します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。
