---
title: コードを使用したビジネス ロジックの適用 | Microsoft Docs
description: 開発者がコードを使用して Common Data Service for Apps でビジネス ロジックを適用する方法について説明します。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: faisalmo
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/26/2018
ms.author: jdaly
ms.openlocfilehash: 12925c57103b1ecc00dc19205af5f32d165bdc63
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="apply-business-logic-with-code"></a>コードを使用したビジネス ロジックの適用

ビジネス ロジックの定義に要件がある場合は、可能な限り、宣言によるプロセス オプションのいずれかの適用を最初に検討することをお勧めします。 [Dynamics 365 Customer Engagement の「カスタマイズ ガイド」の「プロセスを通じてカスタム ビジネス ロジックを作成する」](/dynamics365/customer-engagement/customize/guide-staff-through-common-tasks-processes)を参照してください

宣言によるプロセスが要件を満たさない場合、開発者であればいくつかのオプションがあります。 このトピックでは、コードを記述するための一般的なオプションについて説明します。

## <a name="create-a-workflow-extension"></a>ワークフロー拡張機能の作成

プロセス デザイナー内に新しいオプションを提供する .NET アセンブリを作成できます。 この方法では、ワークフロー デザイナーを使用するユーザーに、条件を適用したり、新しいアクションを実行したりする新しいオプションを提供できます。 開発者ではないユーザーがワークフロー拡張機能を再利用して、コードにロジックを適用することができます。

詳細情報: [Dynamics 365 Customer Engagement 開発者ドキュメント: ユーザー定義ワークフロー活動 (ワークフロー アセンブリ)](/dynamics365/customer-engagement/developer/custom-workflow-activities-workflow-assemblies)

## <a name="create-a-plug-in"></a>プラグインの作成

データ トランザクション フローに接続する .NET アセンブリを作成して、サーバー上にビジネス ロジックを適用できます。 Common Data Service for Apps プラットフォームには、特定のイベントを登録して、アセンブリのクラス内で定義されたコードを実行できるフレームワークがあります。 このクラスは [Execute メソッド](/dotnet/api/microsoft.xrm.sdk.iplugin.execute)を公開する特定のインターフェイスを継承します。 登録されたイベントが発生すると、クラスに対して `Execute` メソッドが呼び出され、イベントに関するコンテキスト データが渡されます。

*Plug-in Registration Tool* を使用してアセンブリを登録します。

`Execute` メソッド内では、SDK アセンブリ内で定義されているオブジェクト モデルを使用し、コンテキスト イベント データを評価し、以下の処理に適切なアクションを実行できます。
- エラーをスローして操作を取り消すかどうかを決定する
- Execute メソッドに渡されるコンテキスト データを変更する
- 追加の操作を実行して、組織のサービスを使用してプロセスを自動化する

### <a name="synchronous-and-asynchronous-plug-ins"></a>同期プラグインと非同期プラグイン
トランザクション内で同期して実行されるプラグイン、またはサーバーに与える影響が小さくなる時間にロジックが適用されるように遅延させてキューに送信するプラグインを登録できます。 この理由から、非同期プラグインが推奨されます。

イベントに対して同期的に実行するようにプラグインを登録すると、コードを実行するタイミングについていくつかのオプションがあります。 3 つの段階があります。

|イベント  |説明  |
|---------|---------|
|検証前|データベース トランザクションが開始される前に発生します。 トランザクションのロールバックによるパフォーマンスの低下を防ぐために、トランザクションが始まる前に操作を取り消すかどうかを判断するビジネス ロジックを適用する場合に適しています。|
|操作前|データベース トランザクションが開始された後に発生します。 この段階で操作を取り消すと、トランザクションをロールバックする必要があります|
|操作後|主要なデータ操作が完了した後にデータベース トランザクション内で発生します。 以前のイベントで適用された可能性があるすべての変更が含まれますが、操作を取り消すとパフォーマンスの低下がさらに大きくなります。|

> [!NOTE]
> 同期プラグインには、使用できるシステム リソースの量に制約があります。 プラグインがしきい値を超えるか応答しなくなると、操作が取り消され、例外がスローされます。

詳細情報: [Dynamics 365 Customer Engagement 開発者ドキュメント: ビジネス プロセスを拡張するためのプラグインを記述する](/dynamics365/customer-engagement/developer/write-plugin-extend-business-processes)

### <a name="see-also"></a>関連項目

[Common Data Service for Apps Developer の概要](overview.md)
