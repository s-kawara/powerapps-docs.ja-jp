---
title: 'サンプル: 永続キュー リスナー (Common Data Service) | Microsoft Docs'
description: このサンプルは、Azure Service Bus リスナー アプリケーションを永続キュー エンドポイント契約に対して記述する方法を示します。
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
# <a name="sample-persistent-queue-listener"></a>サンプル: 永続キュー リスナー

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-persistent-queue-listener -->

このサンプルは、Azure Service Bus リスナー アプリケーションを永続キュー エンドポイント契約に対して記述する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/PersistentQueueListener) からダウンロードできます。

このリスナーは、メッセージがサービス バスにポストされて、エンドポイント キューで使用可能になるまで待機します。 メッセージがキューに入ると、リスナーはメッセージを読み取り、メッセージに含まれる実行コンテキストをコンソールに出力し、キューからメッセージを削除します。
