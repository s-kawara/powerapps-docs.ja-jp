---
title: 'サンプル: 双方向リスナー (アプリ用 Common Data Service) | Microsoft Docs'
description: このサンプルは双方向エンドポイント コントラクトに対して Azure Service Bus リスナーを記述する方法を示します。
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
# <a name="sample-two-way-listener"></a>サンプル: 二方向リスナー

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-two-way-listener -->

このサンプルでは、 `Azure Service Bus` リスナーを二方向エンドポイント契約に対して記述する方法を示します。 サンプルを [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/TwoWayListener) からダウンロードできます。

このサンプルは `Azure Service Bus` の双方向エンドポイントへメッセージが送信されるとき、常に実行されるリモート サービス プラグインを登録します。 このプラグインは実行されるときにメッセージに含まれる実行コンテキストの内容をコンソールへ出力します。
