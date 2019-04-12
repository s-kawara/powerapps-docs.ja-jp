---
title: コードを使用するビジネス ロジックの適用 (Common Data Service)| Microsoft Docs
description: 開発者が Common Data Service でビジネス ロジックを適用するコードの使用方法を学習します。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: kvivek
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/31/2018
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="apply-business-logic-using-code"></a>コードを使用してビジネス ロジックの適用

可能な限り、ビジネスロジックを定義または適用するいくつかの宣言型プロセス オプションの 1 つを適用することを最初に検討する必要があります。 詳細: [Common Data Service でビジネス ロジックの適用](../../maker/common-data-service/cds-processes.md)

宣言型プロセスが要件を満たさない場合、開発者にはいくつかのオプションがあります。 このトピックではコードを記述する共通オプションを紹介します。

## <a name="create-a-plug-in"></a>プラグインの作成

サーバーでビジネスロジックを適用するため、データ トランザクションへのプラグインに .NET アセンブリを記述できます。 Common Data Service には、アセンブリのクラス内で定義されるコードを実行するよう特定のイベントを登録するのに使用するフレームワークがあります。 

詳細: [ビジネス プロセスを拡張するためのプラグインの作成](plug-ins.md)

## <a name="create-a-workflow-extension"></a>ワークフロー拡張の作成

プロセス デザイナー内で新しいオプションを提供する .NET アセンブリを記述できます。 このメソッドは、ユーザーがワークフロー デザイナを使用して条件を適用したり、新しいアクションを実行するための新しいオプションを提供します。 ワークフロー拡張は、開発者ではないユーザーがコード内にロジックを適用するために再利用できます。

詳細: [ワークフロー拡張](workflow/workflow-extensions.md)

### <a name="see-also"></a>関連項目

[Common Data Service 開発者向けの概要](overview.md)
