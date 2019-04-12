---
title: 'サンプル: テンプレートを使用した電子メールの作成 (Common Data Service) | Microsoft Docs'
description: このサンプルは、電子メール レコードをインスタンス化する方法を示します
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
# <a name="sample-create-an-email-using-a-template"></a>サンプル: テンプレートを使用した電子メールの作成

このサンプルは、[InstantiateTemplateRequest](https://docs.microsoft.com/dotnet/api/microsoft.crm.sdk.messages.instantiatetemplaterequest?view=dynamics-general-ce-9) メッセージを使用して、電子メール レコードのインスタンスの作成方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/EmailTemplate) からダウンロードできます。 

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`InstantiateTemplateRequest` メッセージは、電子メール レコードをインスタンス化するシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. 取引先企業レコードを作成します。 
2. **XML** 形式で電子メール テンプレートの本文と件名を定義します。
3. 電子メール テンプレートを作成します。

### <a name="demonstrate"></a>使用方法

1. `InstantiateTemplateRequest` メッセージは、テンプレートを使用して電子メール メッセージを作成するために使用します。 
2. **XML** に電子メール メッセージをシリアル化し、ファイルに保存します。


### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。
    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。
