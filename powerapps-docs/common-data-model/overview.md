---
title: Common Data Model の概要 | Microsoft Docs
description: Common Data Model で Common Data Service for Apps と Common Data Service for Analytics を接続する方法について説明します。
author: RobertBruckner
ms.service: powerapps
ms.topic: article
ms.date: 03/14/2018
ms.author: jdaly
ms.openlocfilehash: 4e9b929558de0b2451bb2df4add4b300d7115848
ms.sourcegitcommit: 91a102426f1bc37504142cc756884f3670da5110
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2018
ms.locfileid: "34803244"
---
# <a name="common-data-model-overview"></a>Common Data Model の概要

**Common Data Model** (CDM) は、さまざまなビジネスおよびアプリケーション ドメインでよく使用される概念とアクティビティを表す、標準エンティティのオープン ソース定義です。 Common Data Model は、アクティビティおよびサービス レベル アグリーメントなど、ベンダー、ワーカー、および顧客間の対話や関係だけでなく、アカウント、部署、ケース、連絡先、潜在顧客、ビジネス チャンス、製品など、*適切に定義されたモジュール形式の拡張可能な*ビジネス エンティティを提供します。 

Microsoft の [Common Data Service for Apps](../maker/common-data-service/data-platform-intro.md) と Common Data Service for Analytics <!-- TODO add link when available  -->は、Common Data Model を実装します。 これらのサービスは、Common Data Model 定義に準拠するデータを保持します。 これらのサービスをベースにビルドすることで、パッケージ化されたアプリケーションと分析ソリューションでは、データの元の場所やデータが最初に管理されていた場所に関係なく、適切に定義されたエンティティ シェイプを操作してデータを共有することができます。 カスタムの基幹業務アプリと分析ソリューションではデータ共有のために同じエンティティを利用できるため、特定のニーズやビジネス要件をサポートできます。 

Microsoft およびパートナー企業は、Common Data Service をベースとしてアプリケーションをビルドし、CDM 形式でビジネス データを格納できるよう努めています。 *データが CDM 形式で格納されている場合に効率的に連動する大規模な拡大し続けるソリューションのコレクション*が用意されています。つまり、新しいビジネス プロセスをすばやく実装し、煩雑さや複雑さに悩まされることなく、事業運営を洞察することができます。 次の図には、Common Data Services をベースにしたアプリケーションでの Common Data Model エンティティの利用の様子が示されています。

![Common Data Services をベースにしたアプリケーションでの Common Data Model エンティティの利用](media/cdm-overview.png)

Common Data Model は、*アプリケーションおよび展開において構造とセマンティクスに一貫性がある*既知の形式でデータを統合することで、データ管理の課題を単純化します。 ビジネス プロセス、デジタル インタラクション、製品利用統計情報、ユーザー操作などを通じて収集されるデータを統合して、*データのあいまいさを解消する*のに役立ちます。 

両方のサービスを使用する顧客のために、Common Data Service for Apps に格納されているデータを Common Data Service for Analytics に*簡単かつ自動的に統合*できます。 まず、既に所有しているエンタープライズおよびトランザクション データ (潜在顧客、キャンペーン情報、以前の顧客の購入など) を統合し、他のソースからのデータ (Web ログや製品利用統計情報など) と結合して、全体を把握することができます。

また、Common Data Model は*拡張可能*です。つまり、CDM に付属しているカスタム可能なエンティティのいずれかにフィールドを追加したり、独自のカスタム エンティティを作成したりすることができます。 CDM 標準では、販売、サービス、マーケティング、運営、財務、人材およびコマースにおけるあらゆるビジネス プロセスをカバーし、会社のビジネス プロセスの中核となる顧客、ユーザーおよび製品エンティティを対象とした、ビジネス エンティティの共通言語が定義されます。 Common Data Model は、複数のチャネル、サービスの実装、ベンダーにまたがるデータの相互運用を容易にします。

Common Data Model および Common Data Service では、次の機能を通じて、豊富な生産性の高い開発プラットフォームが提供されます。

- **標準エンティティの定義** - Common Data Model では、ビジネスおよび生産性アプリケーション全体で最もよく使用されるエンティティを表すエンティティの定義が提供されます。 パブリック CDM GitHub リポジトリ [(https://github.com/Microsoft/CDM)](https://github.com/Microsoft/CDM) は、ビジネス プロセス環境全体にまたがるコア エンティティ、追加の垂直産業データ モデル、およびアンケート、検索エンジン、製品利用統計情報などの異種混在ソースによって継続的に強化されています。
- **データ統合** - 組み込みの Web エクスペリエンスとして Power Query を使用して、既存のシステムからデータをインポートして視覚的に変換します。また、オンラインおよびオンプレミスのソースからのデータをノーコードまたはローコードと結合します。 Excel と Power BI のデータ変換スキルをシームレスに活かすことができます。 「[Power Query を使用して Common Data Service のエンティティにデータを追加する](../maker/common-data-service/data-platform-cds-newentity-pq.md)」を参照してください。
    
    Common Data Service にデータをインポートする場合、データを標準の Common Data Model エンティティにマップできます。また、新しいエンティティを作成して、そのエンティティにマップすることもできます。 既存のデータ統合およびマッピング テンプレートは、Salesforce などの共通データ ソースへの接続を簡略化します。 これらのマッピング テンプレートは完全にカスタマイズ可能であり、拡張可能です。 次のスクリーンショットには、外部データをインポートし、それを Power Query で標準エンティティにマップする様子が示されています。 
    
    ![外部データをインポートして、Power Query で標準エンティティにマップする ](media/cdm-mapping-entities.png)<br />

- **拡張性** – 他のアプリとのデータの共有を妨げることなく、エンティティを拡張することができます。
- **信頼性** – 共通エンティティに頼ることができるため、エンティティにバインドされている再利用可能なコンポーネントをビルドすることができます。 Common Data Model では、開発投資を保護するバージョン管理と拡張性がサポートされます。
- **展開におけるエンティティの整合性** - ソリューションでは、生産性プラットフォームからの情報を、ビジネス アプリケーションからのデータに接続することができます。 たとえば、カレンダーの予定または Microsoft Outlook のタスクを販売機会に接続することができます。 

[Common Data Service for Apps](../maker/common-data-service/data-platform-intro.md) は Common Data Model を実装します。これにより、ビジネス アプリケーションの開発で次のことが可能になります。

- **パッケージ化されたビジネス アプリケーションを利用する** - サード パーティ製のアプリケーションだけでなく、Dynamics 365 for Marketing、Sales、Service、Talent、Finance、Operations アプリケーションを利用します。これらは、Common Data Service for Apps をベースにビルドされています。
- **ニーズに合わせてアプリケーションをカスタマイズし、ネイティブ拡張機能をビルドする** - カスタマイザーと開発者は、適切に定義されたアプリケーションのライフ サイクルでアプリケーション ソリューションを配布します。 ソリューションは、アプリケーションと拡張機能を配布するための方法です。 「[ソリューションの概要](../developer/common-data-service/introduction-solutions.md)」を参照してください。
- **PowerApps を使用して、ノーコード/ローコード、モデル駆動型および WYSIWYG キャンバス アプリをビルドする** - パッケージ化されたアプリケーション、または他のサード パーティ製アプリケーションで作成/使用されたものと同じ共有エンティティを使用して、追加のスタンドアロン アプリを作成します。 以下を参照してください。 
    - [モデル駆動型アプリのビルド](../maker/model-driven-apps/model-driven-app-overview.md)
    - [キャンバス アプリのビルド](../maker/canvas-apps/getting-started.md) 
- **フローを使用してビジネス プロセスを自動化する** - ビジネス プロセス フローを使用して、期待どおりの結果が得られるように一連のステージと手順を定義します。 「[Common Data Service を使用するフローの作成](/flow/common-data-model-intro)」を参照してください。
 
**Common Data Service for Analytics** <!-- TODO add link when available  --> の今後のパブリック プレビューでも Common Data Model を実装します。これにより、以下を含む、標準化された形式でのビジネス データのデータ分析がサポートされます。

- **標準データ エンティティに基づくパッケージ化およびカスタマイズされた分析ソリューション** - 過去の販売実績を追跡する、Sales Insights などの分析アプリケーションでは、データが最初に管理されていた場所に関係なく、一貫した洞察が得られます。これは、データ統合エクスペリエンスで他のソース (Salesforce.com など) のデータが Common Data Model エンティティ シェイプにマップされるためです。 これにより、分析ソリューションが簡略化され、潜在顧客やビジネス チャンスなどの適切に定義されたエンティティのデータ セマンティクスに重点を置くことができます。
- **ノーコード/ローコードの Power Query データ統合** - 組み込みのエクスペリエンスを使用して、エンティティを作成、設定、変換、強化します。 
- **独自の Azure ストレージの使用** - Azure データ スタックを利用して、Common Data Service for Analytics でデータを使用できるようにします。 エンティティは同じ共通モデル形式で格納され、分析ソリューションで認識されます。

