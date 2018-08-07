---
title: Common Data Model を使用した開発 | Microsoft Docs
description: Common Data Model を使用して、アプリやソリューションを開発する方法について説明します。
author: RobertBruckner
ms.service: powerapps
ms.topic: article
ms.date: 07/24/2018
ms.author: robruc
ms.openlocfilehash: 6e99fbe13d9b6e3acdd0cfdd08662676a321471c
ms.sourcegitcommit: abe4d4728db7f56088f618af5b820af78e7099c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2018
ms.locfileid: "39332094"
---
# <a name="how-to-use-the-common-data-model"></a>Common Data Model を使用する方法

**Common Data Model (CDM)** を使用すると、一般的に使用される概念とアクティビティを表す形式、および幅広く使用され理解されている形式にデータを変換することができます。これにより、そのデータに対してクエリを実行したり、データを再利用したり、その形式を使用している他のビジネスやアプリケーションと相互運用したりすることができます。 すべてのリモコンで使用できるように、単三電池のサイズと形状を知ることと同様に、CDM では、(たとえば) *連絡先*のサイズとシェイプを定義して、アプリケーション開発者とビジネス パートナーがそのデータを使って、機敏性と信頼性のあるアプリをビルド (または相互運用) する方法を理解できるようにしています。 また、CDM は標準エンティティのオープン ソース定義であるため、関心がある開発者のコミュニティで理解が得られやすく、スキーマの定義に参加してもらいやすくなります。

現在 CDM は、Dynamics と PowerApps をサポートする Common Data Service (CDS) for Apps 内と、Azure Data Lake でスキーマ化されたファイルを作成するための Power BI のデータ準備機能で使用されています。

![Common Data Model と CDS for Apps](media/cdm-with-cds.png)

CDM と CDS for Apps は、次の方法で使用できます。

-   **CDM 形式でデータを安全に格納し、管理する**: CDS for Apps を使用して、標準化された CDM 形式のデータを安全に格納して管理することができます。 こうすることで、Microsoft のアプリやサービス (Dynamics、PowerApps、Flow、Power BI など)、または独自のカスタム アプリケーションでそのデータにアクセスして使用することができます。

-   **カスタムの CDM エンティティを作成する**: CDM は拡張可能なため、自分の組織に固有の、まだ CDM にない任意のエンティティを作成したり、**Power Query** を使用してこれらのエンティティに既存のデータを入力したりすることができます。 これにより、CDM を活用するだけでなく、ビジネスに合わせて調整することもできます。

-   **独自のデータのリポジトリを作成する**: **Common Data Model (CDM)** スキーマに準拠したデータのリポジトリをビルドし、Microsoft のデータ コネクタを使用してこれらのデータ ソースに接続できます。 これにより、元のデータがある場所やデータが格納されている場所に関係なく、CDM データを使用または共有するカスタムの基幹業務アプリケーションをビルドすることができます。

-   **Power BI を使用して分析情報をすばやく派生させて配布する**: Power BI で高度なデータの準備サービスを使用できます。このサービスは、CDM データ ストア (CDS for Apps に入力したデータなど) にアクセスしてレポートやダッシュボードを作成してから、CDM データを組織内の個人やグループ用にカスタマイズした分析情報に自動的にプルするレポート生成アプリを作成します。

-   **Power BI で組織全体のカスタマイズされたレポートを生成する**: カスタマイズされたレポートを自動的に生成するアプリを使用できます。このレポートは、組織内のユーザーおよびそれ以外の Power BI ワークスペースに配置することができます。

Microsoft は、多くのパートナーと各分野の専門家と協力して、CDM の拡張を続けているため、医療業界などの新しい業界でも CDM とそれをサポートするプラットフォームを利用できるようになります。

## <a name="data-integration-and-power-query-online"></a>データ統合および Power Query Online

現在 CDM をサポートしているどちらのプラットフォームでも、Power Query Online を通じてデータ統合エクスペリエンスを提供しています。Power Query Online を使用すると、ユーザーはさまざまなソースからデータを取り込んで、必要に応じて変換し、標準の CDM エンティティにマップしたり、カスタム エンティティを作成したりすることができます。 Power Query Online では、Excel および Power BI Desktop の Power Query と同じビジュアル、セルフ サービスのデータ準備エクスペリエンスを利用しているため、既存のユーザーはすぐに使用できるようになります。

![データを CDM 内のエンティティにマップする](media/cdm-map-entities.png)

## <a name="common-data-service-for-apps"></a>Common Data Service for Apps

CDS for Apps を使用すると、ビジネス ロジック、セキュリティ、および統合が組み込まれた CDM を使用して、アプリをすぐに開始することができます。 このプラットフォームでは、次のことができます。

-   **パッケージ化されたビジネス アプリケーションを利用する**: 多くの Microsoft Dynamics ソリューションおよび多くのサード パーティ製アプリケーションが、CDS for Apps 上にビルドされています (または少なくとも CDS for Apps を利用しています)。 データが CDM 内にある場合は、これらのパッケージ化されたアプリケーションを利用できます。

-   **カスタマイズされたソリューションへのアクセスを得る**: CDM 形式のデータを理解して使用する開発者によって作成された、拡張機能と完全なアプリケーションのエコシステムが存在します。 詳細については、「[ソリューションの概要](https://docs.microsoft.com/powerapps/developer/common-data-service/introduction-solutions)」を参照してください。

ユーザーの意図が何であれ、ユーザーがデータをより簡単に使用、共有および分析できるように、CDM によりデータが共通の形式に変換されます。

**CDS for Apps のリソース**

-   [Common Data Service for Apps とは](https://docs.microsoft.com/powerapps/maker/common-data-service/data-platform-intro)

-   [Power Query を使用して Common Data Service for Apps のエンティティにデータを追加する](https://docs.microsoft.com/powerapps/maker/common-data-service/data-platform-cds-newentity-pq)

-   [ソリューションの概要](https://docs.microsoft.com/powerapps/developer/common-data-service/introduction-solutions)

-   [モデル駆動型アプリのビルド](https://docs.microsoft.com/powerapps/maker/model-driven-apps/model-driven-app-overview)

-   [キャンバス アプリのビルド](https://docs.microsoft.com/powerapps/maker/canvas-apps/getting-started)

-   [Common Data Service を使用するフローの作成](https://docs.microsoft.com/flow/common-data-model-intro)

