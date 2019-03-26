---
title: 外部 Web サービスにアクセスする (アプリ用 Common Data Service) | Microsoft Docs
description: カスタム プラグインもしくはワークフロー活動から Web サービスにアクセスする方法について説明します。
ms.custom: ''
ms.date: 2/6/2019
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: pehecke
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# 外部 Web サービスにアクセスする

サンドボックスで実行されているプラグインとカスタム ワークフロー活動は、HTTP および HTTPS プロトコルを介してネットワークにアクセスできます。 この機能によって、ソーシャル サイト、ニュース フィード、Web サービスなどの一般的な Web サービスにアクセスできます。 このサンドボックスの機能には、次の Web アクセス制限が適用されます。  
  
- 許可されるプロトコルは HTTP および HTTPS だけです。
- localhost (ループバック) へのアクセスは許可されません。
- IP アドレスは使用できません。 DNS による名前解決を必要とする名前付き Web アドレスを使用する必要があります。
- 匿名認証がサポートされ、その使用が推奨されます。 ログオン ユーザーの資格情報を入力または保存する必要はありません。

Webhook および [!INCLUDE [pn_azure_service_bus](../../includes/pn_azure_service_bus.md)] の使用を含む Web サービスにアクセスする別の方法。 これらのトピックの詳細については以下で提供されるリンクを参照してください。

## 関連項目

[[プラグイン](plug-ins.md)](plug-ins.md)<br />
[[ワークフローの拡張機能](workflow/workflow-extensions.md)](workflow/workflow-extensions.md)<br />
[[Azure統合](azure-integration.md)](azure-integration.md)<br />
[[Webhook の使用](use-webhooks.md)](use-webhooks.md)<br />
[[サンプル: 隔離されたプラグインからの Web アクセス](org-service/samples/web-access-plugin.md)](org-service/samples/web-access-plugin.md)
