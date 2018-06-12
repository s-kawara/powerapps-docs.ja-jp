---
title: Common Data Service for Apps とは | Microsoft Docs
description: Common Data Service (CDS) for Apps、エンティティ、サーバー側ロジックの概要について説明します。
author: clwesene
manager: kfile
ms.service: powerapps
ms.topic: overview
ms.component: cds
ms.date: 05/01/2018
ms.author: matp
ms.openlocfilehash: 586750edf476a9145e2822522cc0b4b5ad729539
ms.sourcegitcommit: 7296649d03ebc33dc5ddb9e7c551869dc781f154
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2018
ms.locfileid: "35250825"
---
# <a name="what-is-common-data-service-for-apps"></a>Common Data Service for Apps とは
Common Data Service (CDS) for Apps を使用すると、ビジネス アプリケーションで使用されるデータを安全に格納し、管理することができます。 CDS for Apps 内のデータは、エンティティ セットに格納されます。 *エンティティ*は、データを格納するために使用されるレコード セットであり、データベース内のテーブルにデータを格納する方法に似ています。 CDS for Apps には、一般的なシナリオを網羅した標準的なエンティティの基本セットが含まれていますが、組織に固有のカスタム エンティティを作成し、Power Query によってそのエンティティにデータを読み込むこともできます。 次にアプリ作成者は、PowerApps を使用して、このデータを利用するリッチ アプリケーションをビルドすることができます。

![ビジネス アプリケーション プラットフォームの概要を示すスクリーンショット。](./media/data-platform-cds-intro/platform.png "プラットフォームの概要")

CDS for Apps を使用するプランの購入については、[価格情報](../../administrator/pricing-billing-skus.md)に関するページをご覧ください。

## <a name="why-use-common-data-service-for-apps"></a>Common Data Service for Apps を使用する理由
CDS for Apps 内の標準エンティティおよびカスタム エンティティではデータに対して、セキュリティ保護されたクラウド ベースのストレージ オプションを提供します。 エンティティを使用すると、アプリ内で使用するために組織のデータのビジネスに焦点を合わせた定義を作成できます。 エンティティが最善の選択かどうかわからない場合は、次のようなメリットが得られることを考慮してみてください。

* **管理が容易** &ndash; メタデータとデータはどちらもクラウド上に保存されます。 保存方法の詳細を気にする必要がありません。
* **セキュリティ保護が容易** &ndash; データが安全に保存されるため、アクセスが許可されたユーザー以外はデータを表示できません。 ロール ベースのセキュリティにより、組織内のユーザー別にエンティティへのアクセスを制御できます。
* **Dynamics 365 のデータへのアクセス**&ndash; Dynamics 365 アプリケーションのデータも Common Data Service for Apps 内に保存されるため、Dynamics 365 データを活用するアプリを迅速にビルドしたり、PowerApps を使用してアプリを拡張したりできるようになります。
* **豊富なメタデータ** &ndash; データの型とリレーションシップは PowerApps 内で直接活用されます。
* **ロジックと検証** &ndash; 計算フィールド、ビジネス ルール、ワークフロー、および業務プロセス フローを定義して、データの品質を保証し、ビジネス プロセスを推進します。
* **生産性向上ツール** &ndash; エンティティは、Microsoft Excel のアドイン内で利用可能で、生産性を向上させ、データ アクセスを保証します。

## <a name="dynamics-365-and-the-common-data-service-for-apps"></a>Dynamics 365 と Common Data Service for Apps

Dynamics 365 for Sales/Service/Talent のような Dynamics 365 アプリケーションも、Common Data Service for Apps を使用してアプリケーションで使用されたデータの保存とセキュリティ保護を行います。 これにより、Dynamics 365 内で既に使用されているコア ビジネス データに対して統合することなく直接、PowerApps と Common Data Service for Apps を使用してアプリのビルドができるようになります。

* **Dynamics 365 データに対してアプリをビルド**&ndash; PowerApps 内で、または Pro Developer SDK を使用して、ビジネス データに対して迅速にアプリをビルドします。
* **再利用可能なビジネス ロジックとルールを管理**&ndash; Dynamics 365 エンティティで既に定義されているビジネス ルールとロジックが PowerApps に適用されることで、ユーザーがどのアプリからデータにアクセスしているかに関係なくデータの一貫性が確保されます。
* **Dynamics 365 と PowerApps でスキルが再利用可能**&ndash; 既に PowerApps または Dynamics 365 のスキルを持っているユーザーはそのスキルを新しい Common Data Service for Apps プラットフォームで活かすことができます。 エンティティ、フォーム、チャートなどの作成がアプリケーション間で共通になりました。

    > [!NOTE]
    > Dynamics 365 for Finance and Operations では現在、Common Data Service for Apps 内でファイナンスとオペレーションのビジネス データを使用できるようにするために、データ インテグレーターの構成が必要です。

## <a name="integrating-data-into-the-common-data-service"></a>Common Data Service へのデータの統合

アプリのビルドには通常、複数のソースからのデータを伴います。ビルドはアプリケーション レベルで行われることもありますが、このデータを共通ストアに統合することでアプリのビルドが容易になったり、1 つのロジックでデータを維持し、運用できるようになるケースもあります。 Common Data Service for Apps では、複数のソースから統合されたデータを 1 つのストアに統合して、PowerApps、Flow、Power BI で Dynamics 365 アプリケーションで既に使用できるデータと共に使用することができます。

* **他のシステムとの統合をスケジュール** &ndash; 別のアプリケーション内に保存されているデータを Common Data Service for Apps と定期的に同期できるため、PowerApps の他のアプリケーション データを活用できます。
* **PowerQuery を使用したデータの変換とインポート** &ndash; Common Data Service へのインポート中に、Excel と Power BI で共通のツールである PowerQuery を使用して、多くのオンライン データ ソースのデータを変換することができます。
* **データの 1 回限りのインポート** &ndash; Excel と CSV ファイルの 1 回のインポートとエクスポートを、Common Data Service for Apps に対する 1 回限りのインポートにも、不定期のインポートにも使用することができます。


## <a name="interacting-with-entities"></a>エンティティの操作
アプリを開発する際に、標準エンティティとカスタム エンティティのいずれか、または両方を使用できます。 標準エンティティは、CDS for Apps に既定で用意されているエンティティです。 これらは、ベスト プラクティスに従って、組織で最も一般的な概念およびシナリオを取り込むように設計されています。

![エンティティの一覧を示すスクリーン ショット。](./media/data-platform-cds-intro/entitylist.png "エンティティの一覧")

エンティティの完全な一覧については、[エンティティ参照](https://docs.microsoft.com/powerapps/developer/common-data-service/reference/about-entity-reference)に関するページを参照してください。

1 つ以上のカスタム エンティティを作成して標準エンティティの機能を拡張することで、組織に固有の情報を格納できます。 詳細については、[カスタム エンティティの作成方法](create-custom-entity.md)に関するページをご覧ください。

## <a name="logic-and-validation"></a>ロジックと検証
CDS for Apps 内のエンティティは、豊富なサーバー側ロジックと検証を利用して、データの品質を保証し、各アプリでエンティティ内のデータを作成および使用するコードの反復を減らすことができます。

* **ビジネス ルール**は、データの作成に使われているアプリに関係なく、複数のフィールドとエンティティにまたがってデータを検証し、警告やエラー メッセージを表示します。 詳しくは、[ビジネス ルールの作成](./data-platform-create-business-rule.md)に関するページをご覧ください。
* **業務プロセス フロー**は、データが一貫して入力され、毎回同じ手順が使われるように、ユーザーを確実に誘導します。 現在、業務プロセス フローはモデル駆動型アプリに対してのみサポートされています。 詳しくは、「[業務プロセス フローの概要](/dynamics365/customer-engagement/customize/business-process-flows-overview)」をご覧ください。
* **ワークフロー**を使用すると、ユーザーによる操作なしで業務プロセスを自動化できます。 詳しくは、[ワークフローの概要](/dynamics365/customer-engagement/customize/workflow-processes)に関するページをご覧ください。
* **コードを使用したビジネス ロジック**では、高度な開発者シナリオをサポートしているため、コードを使ってアプリケーションを直接拡張できます。 詳しくは、「[Apply business logic with code](../../developer/common-data-service/apply-business-logic-with-code.md)」(コードを使用したビジネス ロジックの適用) をご覧ください。

## <a name="developer-capabilities"></a>開発者用の機能
[PowerApps](https://web.powerapps.com) ポータルで使用できる機能に加えて、CDS for Apps には、プログラムでメタデータとデータにアクセスしてエンティティやビジネス ロジックを作成したり、データを操作したりする、開発者向けの機能も含まれます。 詳しくは、「[Common Data Service for Apps Developer Overview](../../developer/common-data-service/overview.md)」(Common Data Service for Apps Developer の概要) をご覧ください。

## <a name="next-steps"></a>次の手順
CDS for Apps を使用して開始するには:
* [Common Data Service データベースを使用してアプリを生成する](../canvas-apps/data-platform-create-app-scratch.md)。
* [カスタム エンティティを作成](create-custom-entity.md)してから、[そのエンティティを使用するアプリを作成](../canvas-apps/data-platform-create-app.md)します。
* [Power Query を使用](./data-platform-cds-newentity-pq.md)してオンラインまたはオンプレミスのデータ ソースに接続し、CDS for Apps にデータを直接インポートします。

## <a name="privacy-notice"></a>プライバシーに関する声明
Microsoft では、Microsoft PowerApps の Common Data Service を使用して、Microsoft の診断システムにカスタム エンティティとフィールド名を収集して格納します。 収集した情報は、お客様向けの Common Data Service の改善に使用します。 アプリ作成者が作成するエンティティとフィールド名は、Microsoft PowerApps コミュニティ全体で共通するシナリオを理解したり、組織に関するスキーマなどの、サービスの標準エンティティの対象範囲のギャップを確認したりする場合に役立ちます。 このエンティティに関連するデータベース テーブルのデータに、Microsoft がアクセスまたは使用することはありません。また、データベースがプロビジョニングされているリージョン外にデータがレプリケートされることもありません。 ただし、カスタム エンティティとフィールド名はリージョン間でレプリケートされ、Microsoft のデータ保持ポリシーに基づいて削除される場合があります。 Microsoft はお客様のプライバシーを尊重いたします。詳細については、[Trust Center](https://www.microsoft.com/trustcenter/Privacy/default.aspx) を参照してください。
