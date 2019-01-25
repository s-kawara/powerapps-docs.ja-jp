---
title: 開発者:Common Data Service for Apps 用のプラグインとワークフロー開発に関するベスト プラクティスとガイダンス | Microsoft Docs
description: PowerApps における Common Data Service for Apps の開発者向けのプラグインとワークフロー開発に関するベスト プラクティスとガイダンスです。
services: ''
suite: powerapps
documentationcenter: na
author: jowells
manager: austinj
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 1/15/2019
ms.author: jowells
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 87e7337a4bf62a10647edfd9b6c17bce0a0903bf
ms.sourcegitcommit: 72c97378e96fb54e5d92ec087a59dd0fb1444f99
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54334019"
---
# <a name="best-practices-and-guidance-regarding-plug-in-and-workflow-development-for-the-common-data-service-for-apps"></a>Common Data Service for Apps 用のプラグインとワークフロー開発に関するベスト プラクティスとガイダンス

以下の一覧には、Common Data Service for Apps 内のプラグインとワークフロー開発に関するガイダンスとベスト プラクティスがすべて含まれています。

|ベスト プラクティス  |説明  |
|---------|---------|
|[プラグインとワークフローのアクティビティでバッチ要求の種類の使用を避ける](avoid-batch-requests-plugin.md)     |プラグインまたはワークフロー アクティビティのコンテキスト内で ExecuteMultipleRequest または ExecuteTransactionRequest メッセージの要求クラスを使用しないでください。         |
|[IPlugin 実装をステートレスとして開発する](develop-iplugin-implementations-stateless.md)     |IPlugin を実装するクラスのメンバーは、データの不整合やパフォーマンスの問題を引き起こす可能性があるスレッド セーフの問題にさらされます。         |
|[プラグイン手順の登録を重複させないでください](do-not-duplicate-plugin-step-registration.md)     |重複したプラグイン手順の登録は、同じメッセージ/イベントでプラグインを複数回発生させる原因となります。         |
|[プラグインの登録でフィルター属性を含める](include-filtering-attributes-plugin-registration.md)     |プラグインの登録手順でフィルター属性を設定しない場合、そのイベントに対して更新メッセージが発生するたびにプラグインによって実行されます。         |
|[Retrieve メッセージと RetrieveMultiple メッセージのプラグインの登録を制限する](limit-registration-plugins-retrieve-retrievemultiple.md)     |Retrieve と RetrieveMultiple のメッセージ イベントに非同期プラグイン ロジックを追加すると、パフォーマンスが低下することがあります。         |
|[カスタム アセンブリの開発を最適化する](optimize-assembly-development.md)     |アセンブリ サイズがサンドボックスのアセンブリ サイズの制限に近い場合、個別のプラグイン/カスタム ワークフロー アクティビティを単一のカスタム アセンブリにマージして、パフォーマンスや保守容易性を改善し、プラグイン/カスタム ワークフロー アクティビティを複数のカスタム アセンブリに移動することを検討してください。         |
|[プラグインで外部ホストとやりとりするときに KeepAlive を false に設定する](set-keepalive-false-interacting-external-hosts-plugin.md)     |KeepAlive プロパティが HTTP 要求ヘッダーで true に設定されるか、明示的に false として定義されていない場合、プラグインの実行回数を増加させることがあります。         |
|[プラグインとワークフローのアクティビティで InvalidPluginExecutionException を使用する](use-invalidpluginexecutionexception-plugin-workflow-activities.md)     |プラグインまたはワークフロー アクティビティのコンテキスト内でエラーが発生している場合、InvalidPluginExecutionException を使用します。         |

# <a name="see-also"></a>関連項目
[コードを使用したビジネス ロジックの適用](../../apply-business-logic-with-code.md)<br />
[ビジネス プロセスを拡張するためのプラグインの使用](../../plug-ins.md)<br />
[ワークフローの拡張機能](../../workflow/workflow-extensions.md)<br />