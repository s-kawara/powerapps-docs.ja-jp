---
title: '開発者: アプリ用 Common Data Service に関する入門情報 | Microsoft Docs'
description: PowerApps アプリ用 Common Data Service を使用して開発者が値を追加する方法を学習します。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: kvivek
editor: ''
tags: ''
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

# <a name="developers-get-started-with-common-data-service-for-apps"></a>開発者: アプリ用 Common Data Service に関する入門情報

アプリ用 Common Data Service (CDS) を使用したアプリを作成するのに開発者がどのように貢献できるか多数の側面があります。 データ用ソースとしてアプリ用 CDS を使用したコードでアプリを構築することは可能ですが、多くのプロジェクトはモデル駆動型アプリまたはキャンバス アプリを使用してユーザーが各自使用する体験を生成します。 

## <a name="working-with-model-driven-apps"></a>モデル駆動型アプリに関する作業

モデル駆動型アプリはアプリ用 CDS の上に構築されます。 モデル駆動型アプリはアプリ環境用 CDS にのみ接続でき、モデル駆動型アプリを定義するすべてのデータはアプリ用 CDS に格納されます。

モデル駆動型アプリはアプリ用 CDS に使用されるカスタマイズと拡張の配布方法を共有します：ソリューション。 ソリューションの詳細については [ソリューションの概要](introduction-solutions.md) を参照してください。

モデル駆動型アプリには開発者がコードを記述して拡張するための多くのポイントもあります。 開発者がモデル駆動型アプリでできることについては [モデル駆動型アプリ開発者用概要](../model-driven-apps/overview.md) を参照してください。

## <a name="understand-when-to-write-code"></a>コードを記述する場合について

アプリ用 CDS は、ユーザーがコードを記述することなく、カスタム ビジネス ロジックを構成できるように多くの機能を含んでいます。開発者が貢献する最も一般的なシナリオは、既存の機能が要件に合わせて必要な機能を提供していない場所にスペースを埋め込むことです。 しかし、アプリ用 CDS は、開発者がコードを使用して共通の機能を拡張するために、多くのポイントを提供します。

開発者がプロジェクトに貢献するためには、コードを記述せずに何ができるかを理解することが重要です。 これらの機能についてよく理解する必要があります。 詳細: [アプリ用 Common Data Service とは](../../maker/common-data-service/data-platform-intro.md)

## <a name="where-to-begin"></a>どこから開始するか

どこから開始するかは、解決しようとしている問題によって異なります。 このガイドは広範囲に及ぶ機能の内容を含みますが、すべての機能を使用することはほとんどありません。 開始するための重要な領域として次のいくつかのものが含まれます。

> [Web サービスを使用したデータとの連携](#work-with-data-using-web-services)<br/>
> [ビジネス ロジックの適用](#applying-business-logic)<br/>
> [アプリ用 CDS エンティティ](#cds-for-apps-entities)<br/>
> [メタデータに関する作業](#work-with-metadata)<br/>
> [拡張子をパッケージ化して配布するためのソリューションの使用](#use-solutions-to-package-and-distribute-extensions)<br/>
> [クライアントアプリケーションと認証の作成](#create-client-applications-and-authentication)<br/>
> [設置型展開の内容](#content-for-on-premises-deployments)<br/>

### <a name="work-with-data-using-web-services"></a>Web サービスを使用したデータの操作

データを操作するために 2 つの異なった Web サービスが使用できます。 どれを使用するかは作業中のプロジェクトの種類によって異なります。 詳細: [コードを使用したデータの操作](work-with-data-cds.md)

### <a name="applying-business-logic"></a>ビジネスロジックの適用

コードを使用して作成した最も一般的な拡張機能は、ビジネスで使用されるプロセスの自動化を含みます。 その利用可能なオプションの概要は [コードによるビジネスロジックの適用](apply-business-logic-with-code.md) にあります。 これらのそれぞれの方法は、通常サーバーで発生するイベントに基づいて呼び出します。[イベントフレームワーク](event-framework.md) を理解することは重要です。

### <a name="cds-for-apps-entities"></a>アプリ用 CDS エンティティ

エンティティはユーザーが操作するビジネスデータを保存します。 それらが何であるか、またどのように操作するかを理解することが重要です。
詳細:

- [アプリ用 Common Data Service のエンティティ](entities.md)
- [エンティティの参照について](reference/about-entity-reference.md)

### <a name="work-with-metadata"></a>メタデータに関する作業

システム内のメタデータを正しく理解することで、アプリ用 CDS プラットフォームの動作を理解できます。 メタデータを定義するエンティティ スキーマを追加、更新、または削除するためにデザイナを使用しますが、Web API と組織サービスの Web サービスには、エンティティ スキーマに対して CRUD 操作を実行する機能が用意されています。 詳細: [コードを使用したメタデータに関する作業](metadata-services.md) 

### <a name="use-solutions-to-package-and-distribute-extensions"></a>拡張子をパッケージ化して配布するためにソリューションを使用します

拡張機能やそれらが依存するカスタマイズを配布する場合は、ソリューションを理解する必要があります。 個人が作成したソリューションは操作が比較的簡単で開発者のスキルを必要としません。 ただし、開発者チームがソリューションで生産的に作業し、効果的なアプリケーションであるライフサイクル管理の原則を使用するためには、より高度な方法が必要です。 詳細:

 - [ソリューションの概要](introduction-solutions.md)
 - [SolutionPackager toolSolutionPackager ツール](compress-extract-solution-file-solutionpackager.md)
 - [Package Deployer ツール](./package-deployer/create-packages-package-deployer.md)
 - [AppSource 上にアプリを公開する](publish-app-appsource.md)

### <a name="create-client-applications-and-authentication"></a>クライアント アプリケーションと認証を作成します

サーバ上でビジネス ロジックが適用する拡張機能を作成するときは、認証するコードを含める必要はありません。 認証する必要があるのは、クライアント アプリケーションを作成するときだけです。 簡単なコンソール クライアント アプリケーションは、アプリ用 API の CDS についてよく理解するための 1 つの方法です。 データに接続する方法を有効化することは、重要な最初のステップです。 用意されているほとんどのコードサンプルは認証方法を含みます。 Xrm.Tooling コネクタ 認証を容易にする機能を提供します。 詳細:

- [認証](authentication.md)
- [クライアント アプリケーション作成](connect-cds.md)
- [クイック スタート: 組織サービスを使用してコンソール アプリケーションを作成する](org-service/quick-start-org-service-console-app.md)
- [クイック スタート: Web API のサンプル (C#)](webapi/quick-start-console-app-csharp.md)
- [サンプル: XRM ツール API のクイック スタート](xrm-tooling/sample-quick-start-xrm-tooling-api.md)

## <a name="content-for-on-premises-deployments"></a>設置型展開の内容

アプリ用 CDS はこの時点では設置型展開に利用できません。 このガイドの内容は、設置型またはインターネット経由の展開 (IFD) のオプションに関する情報は含まれていません。 オプションに関連する詳細は、[Microsoft Dynamics 365 (online) および Dynamics 365 (on-premises) 向けソフトウェア開発キット](https://msdn.microsoft.com/library/hh547453.aspx) を参照してください。