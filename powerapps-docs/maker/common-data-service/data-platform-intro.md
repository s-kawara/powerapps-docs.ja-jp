---
title: Common Data Service とは何ですか。 | Microsoft Docs
description: Common Data Service、エンティティ、およびサーバー側ロジックの概要。
author: clwesene
manager: kfile
ms.service: powerapps
ms.topic: overview
ms.component: cds
ms.date: 05/01/2018
ms.author: matp
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="what-is-common-data-service"></a>Common Data Service とは何ですか。
Common Data Service によってビジネス アプリケーションで使用されるデータを安全に保存および管理できます。 Common Data Service 内のデータは、一連のエンティティ内に格納されます。 *エンティティ*はデータベース内にデータを格納する方法と同様に、データの格納に使用される一連のレコードです。 Common Data Service は標準的なシナリオをカバーする標準エンティティの基本セットを含んでいますが、組織に固有のカスタム エンティティを作成し、Power Query を使用してデータを入力することもできます。 アプリ作成者はこのデータを使用して機能豊富なアプリケーションを作成するために PowerApps を使用できます。

![ビジネス アプリケーション プラットフォームの概要を示すスクリーンショット。](./media/data-platform-cds-intro/platform.png "プラットフォームの概要")

Common Data Service 使用計画の購入に関する情報については、[価格設定情報](../../administrator/pricing-billing-skus.md) を参照してください。

## <a name="why-use-common-data-service"></a>Common Data Service を使用する理由。
Common Data Service の標準エンティティおよびユーザー定義エンティティは、データに安全なクラウド ベースのストレージ オプションを提供します。 エンティティを使用すると、アプリ内で使用するための組織のデータのビジネス重視の定義を作成できます。 エンティティが最善の選択肢であるかどうか分からない場合は、次の点を考慮してください。

* **簡単に管理できます** &ndash; メタデータとデータの両方がクラウドに格納されます。 それらがどのように格納されているかの詳細について気にする必要はありません。
* **セキュリティ保護を簡単にできます** &ndash; データが安全に保存されるため、ユーザーはアクセスを許可した場合にのみデータを見ることができます。 ロール ベースのセキュリティでは、組織内のさまざまなユーザーのエンティティへのアクセスを制御できます。
* **Dynamics 365 データにアクセスする** &ndash; Dynamics 365 アプリケーションのデータは、Common Data Service にも格納されており PowerApps を使用して Dynamics 365 データを活用してアプリケーションを迅速に構築し、アプリケーションを拡張できます。
* **豊富なメタデータ** &ndash; データの種類と関連付けは、PowerApps 内で直接利用されます。
* **ロジックおよび検証** &ndash; 計算フィールド、業務ルール、ワークフロー、およびビジネス プロセス フローを定義して、データ品質を保証し、業務プロセスを推進します。
* **生産性向上ツール** &ndash; エンティティは、Microsoft Excel のアドイン内で使用でき、生産性を向上させ、データへのアクセスを保証します。

## <a name="dynamics-365-and-the-common-data-service"></a>Dynamics 365 と Common Data Service

Dynamics 365 for Sales、Service、Talent などの Dynamics 365 アプリケーションは、アプリケーションで使用されるデータを格納および保護するために Common Data Service も使用します。 これにより、統合を必要とせずに Dynamics 365 ですでに使用されている主なビジネス データに対して、PowerApps と Common Data Service を直接使用してアプリケーションを構築できます。

* **Dynamics 365 データに対するアプリケーションの構築** &ndash; PowerApps 内のビジネス データに対して、または Pro Developer SDK を使用して、アプリケーションを迅速に構築します。
* **再利用可能なビジネス ロジックとルールを管理する** &ndash; Dynamics 365 エンティティで既に定義されている業務ルールとロジックは、ユーザーがデータにアクセスする方法やアプリケーションに関係なく、データの一貫性を保証するために PowerApps に適用されます。
* **Dynamics 365 と PowerApps で再利用可能なスキル** &ndash; 以前に PowerApps または Dynamics 365 のスキルを持つユーザーは、新しい Common Data Service プラットフォーム全体でこれらのスキルを活用できるようになりました。 エンティティ、フォーム、チャートなどの作成は、アプリケーション全体で共通になりました。

    > [!NOTE]
    > Dynamics 365 for Finance and Operations のビジネス データを Common Data Service で利用できるように、Data Integrator の設定を現在必要としています。

## <a name="integrating-data-into-the-common-data-service"></a>Common Data Service にデータの統合

アプリケーションの構築には、通常、複数のソースからのデータが含まれますが、これはアプリケーション レベルで行われることもあります。このデータを共通のストアに統合することで、アプリケーション構築の経験が簡単になり、データを維持して操作するための単一のロジック セットが可能になる場合もあります。 Common Data Service は複数のソースから単一のストアにデータを統合し、Dynamics 365 アプリケーションから既に利用可能なデータとともに、PowerApps、Flow および Power BI で使用することができます。

* **他のシステムとのスケジュールされた統合** &ndash; 別のアプリケーションに保存されているデータは、Common Data Service と定期的に同期して PowerApps の他のアプリケーション データを活用できます。
* **PowerQuery を使用したデータの変換とインポート** &ndash; Common Data Service にインポートする際にデータを変換するには、Excel と Power BI で共通のツールである多くのオンライン データ ソースから PowerQuery を使用できます。
* **1 回限りのデータ インポート** &ndash; Excel および CSV ファイルの簡単なインポートとエクスポートは、Common Data Service への 1 回限りまた頻度が低いデータのインポートに使用されます。

Common Data Service へのデータの統合に関する詳細は、 [Power Query を使用して Common Data Service のエンティティにデータを追加する](data-platform-cds-newentity-pq.md) を参照してください。

## <a name="interacting-with-entities"></a>エンティティとのやりとり
アプリケーションを開発する場合は、標準エンティティ、ユーザー定義エンティティ、または両方を使用できます。 Common Data Service は既定で標準エンティティを提供します。 組織内の最も一般的な概念やシナリオを取得するよう、推奨事項に従って設計されています。

![エンティティのリストを表示するスクリーンショット。](./media/data-platform-cds-intro/entitylist.png "エンティティ リスト")

エンティティのリストの全一覧については、[エンティティ参照](https://docs.microsoft.com/powerapps/developer/common-data-service/reference/about-entity-reference) を参照してください。

組織に固有の情報を格納する 1 つ以上のカスタム エンティティを作成して、標準エンティティの機能を拡張できます。 詳細については、[カスタム エンティティの作成方法](create-custom-entity.md) を参照してください。

## <a name="logic-and-validation"></a>ロジックおよび検証
Common Data Service 内のエンティティは、豊富なサーバー側のロジックと検証を活用して、データ品質を保証し、エンティティ内のデータを作成して使用する各アプリケーションの反復コードを削減できます。

* **業務ルール**は、複数のフィールドとエンティティ間でデータを検証し、データの作成に使用されたアプリケーションに関係なく、警告メッセージとエラー メッセージを表示します。 詳細については、[業務ルールの作成](./data-platform-create-business-rule.md) を参照してください。
* **業務プロセス フロー**は、ユーザーがデータを統一して入力し、毎回同じ手順に従うようにします。 業務プロセス フローでは、現在モデル駆動型アプリでのみサポートされています。 詳細については、[業務プロセス フローの概要](/dynamics365/customer-engagement/customize/business-process-flows-overview) を参照してください。
* **ワークフロー**は、ユーザー対話を使用しないビジネス プロセスを可能にします。 詳細については、[ワークフローの概要](/dynamics365/customer-engagement/customize/workflow-processes)の説明を参照してください。
* **コードによるビジネス ロジック**は、高度な開発者シナリオをサポートし、アプリケーションをコードを通じて直接拡張します。 詳細については、[コードによるビジネスロジックの適用](../../developer/common-data-service/apply-business-logic-with-code.md) を参照してください。

## <a name="developer-capabilities"></a>開発者機能
[PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) ポータルで利用可能な機能に加えて、Common Data Service には開発者がメタデータとデータにプログラムでアクセスして、エンティティやビジネス ロジックを作成しデータとやりとりする機能も含まれます。 詳細については、[Common Data Service の開発者の概要](../../developer/common-data-service/overview.md) を参照してください。

## <a name="next-steps"></a>次のステップ
Common Data Service を使い始めるには:
* [Common Data Service データベースを使用してアプリを作成](../canvas-apps/data-platform-create-app-scratch.md)。
* [ユーザー定義エンティティの作成](create-custom-entity.md) および、その [エンティティを使用するアプリを作成する](../canvas-apps/data-platform-create-app.md)。
* [Power Query を使用](./data-platform-cds-newentity-pq.md) してオンラインまたはオンプレミスのデータ ソースに接続し、そのデータを Common Data Service に直接インポートします。

## <a name="privacy-notice"></a>プライバシーに関する声明
Microsoft PowerApps 共通データ モデルでは、Microsoft はユーザー定義エンティティおよびフィールド名を収集し、診断システムに保存します。 この情報を使って、お客様の共通データ モデルを改善します。 アプリ作成者が作成するエンティティ名およびフィールド名は、Microsoft が PowerApps コミュニティに共通するシナリオを理解し、組織に関連するスキーマなど、サービスの標準エンティティ範囲のすきまを確認するのに役立ちます。 これらのエンティティに関連付けられたデータベース テーブル内のデータは、Microsoft によりアクセスまたは使用されず、データベースがプロビジョニングされた地域の外部にレプリケーションされません。 しかし、カスタム エンティティおよびフィールド名は、地域間でレプリケーションされ、データ保持ポリシーに基づいて削除される可能性がある点に注意してください。 マイクロソフトは、[セキュリティ センター](https://www.microsoft.com/trustcenter/Privacy/default.aspx) で詳しく説明されているとおりにプライバシー保護に努めています。
