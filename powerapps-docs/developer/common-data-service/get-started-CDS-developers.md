---
title: '開発者向け: Common Data Service を使う | Microsoft Docs'
description: PowerAppsで Common Data Service を使ってどのように値を追加するか、開発者向けの手順を説明します。
suite: powerapps
author: JimDaly
manager: ryjones
ms.service: powerapps
ms.date: 08/05/2019
ms.author: jdaly
ms.reviewer: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="developers-get-started-with-common-data-service"></a>開発者向け: Common Data Service を使う

どこから開始するかは、解決しようとしている問題により異なります。 このガイドは広範囲に及ぶ機能の情報を含みますが、すべての機能を使用することはほとんどありません。 次のセクションは開始するいくつか重要な分野を含みます。

## <a name="work-with-data-using-web-services"></a>Web サービスを使用したデータの操作

データの操作に使用できる Web サービスはふたつあります: **Web API** と **組織サービス**。 

どれを使用するかは作業中のプロジェクトの種類によって異なります。 詳細: [コードを使用したデータの操作](work-with-data-cds.md)

## <a name="applying-business-logic"></a>ビジネスロジックの適用

コードを使用して作成した最も一般的な拡張機能は、ビジネスで使用されるプロセスの自動化を含みます。 その利用可能なオプションの概要は [コードによるビジネスロジックの適用](apply-business-logic-with-code.md) にあります。 これらのそれぞれの方法は、通常サーバーで発生するイベントに基づいて呼び出します。[イベントフレームワーク](event-framework.md) を理解することは重要です。

## <a name="integrate-with-external-data"></a>外部データと統合

Common Data Service のデータ管理機能を使用すると、 Common Data Service 内のデータを処理できるだけでなく、ビジネスに不可欠な外部データと効果的なやりとりをすることができます。 詳細: 

- [データのインポート](/powerapps/developer/common-data-service/import-data)
- [データの同期](/powerapps/developer/common-data-service/data-synchronization)
- [仮想エンティティ](/powerapps/developer/common-data-service/virtual-entities/get-started-ve)
- [Azure 統合](/powerapps/developer/common-data-service/azure-integration)
- [Webhooks](/powerapps/developer/common-data-service/use-webhooks
)

## <a name="common-data-service-entities"></a>Common Data Service エンティティ

エンティティはユーザーが操作するビジネスデータを保存します。 それらが何であるか、またどのように操作するかを理解することが重要です。
詳細:

- [Common Data Service エンティティ](entities.md)
- [エンティティの参照について](reference/about-entity-reference.md)

## <a name="work-with-metadata"></a>メタデータに関する作業

システムのメタデータを十分に理解することで、 Common Data Service プラットフォームの働きを容易に把握することができます。 メタデータを定義するエンティティ スキーマを追加、更新、または削除するためにデザイナを使用しますが、Web API と組織サービスの Web サービスには、エンティティ スキーマに対して CRUD 操作を実行する機能が用意されています。 詳細: [コードを使用したメタデータに関する作業](metadata-services.md) 

## <a name="use-solutions-to-package-and-distribute-extensions"></a>拡張子をパッケージ化して配布するためにソリューションを使用します

拡張機能やそれらが依存するカスタマイズを配布する場合は、ソリューションを理解する必要があります。 個人が作成したソリューションは操作が比較的簡単で開発者のスキルを必要としません。 ただし、開発者チームがソリューションで生産的に作業し、効果的なアプリケーションであるライフサイクル管理の原則を使用するためには、より高度な方法が必要です。 詳細:

 - [ソリューションの概要](introduction-solutions.md)
 - [SolutionPackager ツール](compress-extract-solution-file-solutionpackager.md)
 - [Package Deployer ツール](./package-deployer/create-packages-package-deployer.md)
 - [AppSourceでアプリを公開する](publish-app-appsource.md)

## <a name="create-client-applications-and-authentication"></a>クライアント アプリケーションと認証を作成します

サーバ上でビジネス ロジックが適用する拡張機能を作成するときは、認証するコードを含める必要はありません。 認証する必要があるのは [クライアント アプリケーションを作成する](/powerapps/developer/common-data-service/connect-cds) ときだけです。 簡単なコンソール クライアント アプリケーションは、 Common Data Service APIに対する理解を深めるには最適です。 データに接続する方法を有効化することは、重要な最初のステップです。 用意されているほとんどのコードサンプルは認証方法を含みます。 Xrm.Tooling コネクタ 認証を容易にする機能を提供します。 詳細:

- [認証](authentication.md)
- [サーバー間 (S2S) の認証を使用して Web アプリケーションを作成する](/powerapps/developer/common-data-service/build-web-applications-server-server-s2s-authentication)
- [XRM ツールを使用して Windows のクライアント アプリケーションを作成する](/powerapps/developer/common-data-service/xrm-tooling/build-windows-client-applications-xrm-tools)
