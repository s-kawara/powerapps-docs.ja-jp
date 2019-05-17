---
title: Common Data Service 開発者ガイド | Microsoft Docs
description: Common Data Service を使用して開発者が値を追加する方法を説明します。
author: JimDaly
manager: annbe
ms.service: powerapps
ms.topic: article
ms.date: 03/27/2019
ms.author: jdaly
ms.reviewer: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="common-data-service-developer-guide"></a>Common Data Service 開発者ガイド

PowerApps は、ユーザー、業務、独立系ソフトウェア ベンダー (ISV)、およびシステム インテグレーター (SI) に対して、業種アプリ構築用の強力なプラットフォームを提供します。 サーバー側のロジック (プラグインとワークフロー)、業務プロセス フロー、高度なセキュリティ モデル、そして開発者がアプリを構築する拡張可能なプラットフォームなど、**Common Data Service** は [Dynamics 365 for Customer Engagement プラットフォーム](/dynamics365/customer-engagement/developer/developer-guide) の中核機能を含む PowerApps の基盤となるデータ プラットフォームです。 

> [!NOTE]
> このはつまり Common Data Service が、たとえば Dynamics 365 for Sales、Dynamics 365 for Customer Service、Dynamics 365 for Marketing などの、Customer Engagement アプリの基盤となるプラットフォームでもあることを効果的に意味します。 既に Dynamics 365 for Customer Engagement アプリの経験があれば、その経験を Common Data Service のカスタマイズおよび拡張に生かしてアプリを構築することができます。 

Common Data Service を使用したアプリを作成するのに開発者がどのように貢献できるか多数の側面があります。 Common Data Service をデータソースとして使用したコードでアプリケーションを構築することは可能ですが、ほとんどのプロジェクトで [モデル駆動型アプリ](/powerapps/maker/model-driven-apps/model-driven-app-overview) や [キャンバス アプリ](/powerapps/maker/canvas-apps/getting-started) のいずれかを使用してユーザーが使用するエクスペリエンスを生成します。 

## <a name="working-with-model-driven-apps"></a>モデル駆動型アプリに関する作業

モデル駆動型アプリは Common Data Service 上に構築され、Common Data Service 環境にのみ接続できます。 モデル駆動型アプリを定義するすべてのデータは Common Data Service に格納されます。

モデル駆動型アプリは [ソリューション](introduction-solutions.md) を使用して、Common Data Service で使用されるカスタマイズと拡張機能を公開するメソッドを共有しています。

モデル駆動型アプリには開発者がコードを記述して拡張するための多くのポイントもあります。 開発者がモデル駆動型アプリでできることについては [モデル駆動型アプリ開発者ガイド](../model-driven-apps/overview.md) を参照してください。

## <a name="understand-when-to-write-code"></a>コードを記述する場合について

Common Data Service は、ユーザーがコードを記述することなく、カスタム ビジネス ロジックを構成できるように多くの機能を含んでいます。開発者が貢献する最も一般的なシナリオは、既存の機能が要件に合わせて必要な機能を提供していない場所にスペースを埋め込むことです。 しかし、Common Data Service は開発者がコードを使用して共通の機能を拡張するために、多くのポイントを提供します。

開発者がプロジェクトに貢献するためには、コードを記述せずに何ができるかを理解することが重要です。 これらの機能についてよく理解する必要があります。 詳細: [Common Data Service とは](../../maker/common-data-service/data-platform-intro.md) 

## <a name="content-for-on-premises-deployments"></a>設置型展開の内容

現時点では Common Data Service を設置型展開で使用できません。 このガイドの内容は、設置型またはインターネット経由の展開 (IFD) のオプションに関する情報は含まれていません。 これらのオプションに関連する詳細は [Dynamics 365 for Customer Engagement アプリの開発者ガイド](/dynamics365/customer-engagement/developer/developer-guide) を参照してください。

> [!div class="nextstepaction"]
> [はじめに](get-started-cds-developers.md)

### <a name="see-also"></a>関連項目

[開発者向け PowerApps の情報](/powerapps/#pivot=home&panel=developer)<br/>
[モデル駆動型アプリの開発者ガイド](../model-driven-apps/overview.md)
