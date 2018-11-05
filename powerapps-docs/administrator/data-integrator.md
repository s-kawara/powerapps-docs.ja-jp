---
title: Common Data Service for Apps にデータを統合する
description: Common Data Service for Apps に複数のソースからのデータを統合する
author: sabinn-msft
ms.service: powerapps
ms.topic: how-to
ms.component: cds
ms.date: 09/19/2018
ms.author: sabinn
search.audienceType:
- admin
search.app:
- D365CE
- PowerApps
- Powerplatform
ms.openlocfilehash: b8cebc6f9db8a1a7c1a060aad461f4f32fcee05b
ms.sourcegitcommit: 2bcf40aeaa35420dc43f5803f4e57ff0f6afb57b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2018
ms.locfileid: "46469756"
---
# <a name="integrate-data-into-common-data-service-for-apps"></a>Common Data Service for Apps にデータを統合する

<!--note from editor: the style guide says not to use "the" in front of Common Data Service for Apps, so I'm removing that.-->

Data Integrator (管理者向け) は、Common Data Service for Apps にデータを統合するために使用されるポイント ツー ポイント統合サービスです。 複数のソース (たとえば、Dynamics 365 for Finance and Operations、Dynamics 365 for Sales、Dynamics 365 for Sales and SalesForce (プレビュー)、SQL (プレビュー)) からのデータの Common Data Service for Apps への統合がサポートされます。 また、Dynamics 365 for Finance and Operations および Dynamics 365 for Sales へのデータの統合もサポートされます。 このサービスは 2017 年 7 月から一般公開されています。  

Dynamics 365 for Finance and Operations および Dynamics 365 for Sales などのファーストパーティ アプリから始めました。 Power Query または M ベースのコネクタを利用することで、SalesForce (プレビュー) や SQL (プレビュー) などの追加ソースをサポートできるようになりました。近い将来、これを 20 を超えるソースに拡張する予定です。 

> [!div class="mx-imgBorder"]
> ![データのソースからターゲットへ](media/data-integrator/DataIntegratorP2P-new.PNG "データのソースからターゲットへ")

## <a name="how-can-you-use-the-data-integrator-for-your-business"></a>ビジネスで Data Integrator をどのように使用できるのか

Data Integrator (管理者向け) では、Dynamics 365 for Finance and Operations と Dynamics 365 for Sales の間の直接同期を提供する見込顧客の現金化などのプロセスベースの統合シナリオもサポートされます。 データ統合機能で使用できる見込顧客の現金化テンプレートは、Finance and Operations と Sales の間の取引先企業、連絡先、製品、販売見積、販売注文、売上請求書に関するデータの流れを可能にします。 データは Finance and Operations と Sales との間を流れていますが、Sales では販売とマーケティング活動を行うことができ、Finance and Operations では在庫管理を使用して注文の履行を処理することができます。 

> [!div class="mx-imgBorder"]
> ![見込顧客の現金化](media/data-integrator/ProspectToCash631.png "見込顧客の現金化")

見込顧客の現金化統合により、販売者は Dynamics 365 for Sales の長所を活かして販売プロセスを処理および監視できるようになり、履行と請求のすべての部分で Finance and Operations の豊富な機能が利用されます。 Microsoft Dynamics 365 の見込顧客の現金化統合では、両方のシステムの力を組み合わせて利用できます。 

[見込顧客の現金化統合](https://www.youtube.com/watch?v=AVV9x5x-XCg)に関するビデオをご覧ください。

見込顧客の現金化統合の詳細については、[見込顧客を現金化するソリューション](https://docs.microsoft.com/en-us/dynamics365/unified-operations/supply-chain/sales-marketing/prospect-to-cash)に関するドキュメントを参照してください。

Microsoft では、Dynamics 365 for Finance and Operations への[フィールド サービス統合](https://docs.microsoft.com/dynamics365/unified-operations/supply-chain/sales-marketing/field-service-work-order)および [PSA (Project Service Automation) 統合](https://docs.microsoft.com/dynamics365/unified-operations/financials/project-management/psa-integration?toc=/fin-and-ops/toc.json)もサポートしています。

## <a name="data-integrator-platform"></a>Data Integrator プラットフォーム

Data Integrator (管理者向け) は、Data Integrator プラットフォーム、(Dynamics 365 for Finance and Operations や Dynamics 365 for Sales などの) アプリケーション チームによって提供されるすぐに使えるテンプレートおよびお客様とパートナーによって作成されるカスタム テンプレートで構成されています。 さまざまなソース間でスケーリング可能なアプリケーションに依存しないプラットフォームが構築されています。 そのまさに中心に、(統合エンドポイントへの) 接続を作成し、(さらにカスタマイズ可能な) マッピングが事前に定義されているカスタマイズ可能なテンプレートのいずれかを選択し、データ統合プロジェクトを作成して実行します。  

統合テンプレートは、ソースからターゲットへのデータの流れを可能にするための、エンティティとフィールド マッピングが事前に定義されたブループリントとして機能します。 また、データをインポートする前に転送する機能も提供されます。 多くの場合、ソース アプリとターゲット アプリの間のスキーマは大きく異なることがあり、エンティティとフィールド マッピングが事前に定義されたテンプレートは、統合プロジェクトの最適な開始点として機能します。  

> [!div class="mx-imgBorder"]
> ![データ統合プラットフォーム](media/data-integrator/DIPlatform.PNG "データ統合プラットフォーム")

## <a name="how-to-set-up-a-data-integration-project"></a>データ統合プロジェクトを設定する方法

次の 3 つの主な手順があります。

1. 接続を作成する (データ ソースに資格情報を提供する)。

2. 接続セットを作成する (前の手順で作成した接続用の環境を識別する)。

3. テンプレートを使用してデータ統合プロジェクトを作成する (1 つ以上のエンティティに対して定義済みのマッピングを作成または使用する)。

統合プロジェクトを作成したら、プロジェクトを手動で実行することができ、また、今後のスケジュール ベースの更新を設定することもできます。 この記事の残りの部分では、これら 3 つの手順について詳しく説明します。

### <a name="how-to-create-a-connection"></a>接続を作成する方法

データ統合プロジェクトを作成する前に、Microsoft PowerApps ポータルで使用する各システムの接続をプロビジョニングする必要があります。 これらの接続を統合点として考えてください。

**接続を作成するには**

1. [PowerApps 管理センター](https://admin.powerapps.com)に移動します。

2. [データ] で、**[接続]**、**[新しい接続]** の順に選択します。

3. 接続の一覧から接続を選択するか、接続を検索できます。

    > [!div class="mx-imgBorder"] 
    > ![接続を作成する](media/data-integrator/CreateConnection780.png "接続を作成する")

4. 接続を選択したら、**[作成]** を選びます。 その後、資格情報を求めるメッセージが表示されます。

5. 資格情報を指定すると、接続内容が自分の接続の下に一覧表示されます。

    > [!div class="mx-imgBorder"] 
    > ![接続の一覧](media/data-integrator/CreateConnection1780.png "接続の一覧")

### <a name="how-to-create-a-connection-set"></a>接続セットを作成する方法

接続セットは、2 つの接続、接続用の環境、組織のマッピング情報、および複数のプロジェクト間で再利用できる統合キーのコレクションです。 まず、開発向けの接続セットを使用し、その後、運用向けの別の接続セットに切り替えることができます。 接続セットに格納される 1 つの重要な情報は組織単位のマッピングです。たとえば、Finance and Operations の法人 (または会社) と Dynamics 365 for Sales の組織または部署の間のマッピングです。 接続セットには複数の組織のマッピングを格納できます。

**接続セットを作成するには**

1. [PowerApps 管理センター](https://admin.powerapps.com)に移動します。

2. 左側のナビゲーション ウィンドウで、**[データ統合]** タブを選択します。

3. **[接続セット]** タブを選択し、**[新しい接続セット]** を選びます。

4. 接続セットの名前を指定します。
  
    > [!div class="mx-imgBorder"] 
    > ![接続セットを作成する](media/data-integrator/CreateConnectionSet1780.png "接続セットを作成する")
  
5. 先ほど作成した接続を選択し、適切な環境を選びます。

6. 次の接続を選択して、手順を繰り返します (これらを順不同のソースとターゲットとして考えてください)。

7. 組織から部署へのマッピングを指定します (Finance and Operations および Sales システムの間で統合を行う場合)。
  
    > [!NOTE]
    > 接続セットごとに複数のマッピングを指定することができます。
  
8. すべてのフィールドに入力したら、**[作成]** を選択します。

9. [接続セット] の一覧ページに先ほど作成した新しい接続セットが表示されます。
    
    > [!div class="mx-imgBorder"] 
    > ![接続セットの一覧](media/data-integrator/CreateConnectionSet2780.png "接続セットの一覧")

接続セットをさまざまな統合プロジェクト全体で使用する準備ができました。

### <a name="how-to-create-a-data-integration-project"></a>データ統合プロジェクトを作成する方法

プロジェクトでは、システム間のデータ フローを有効にします。 プロジェクトには、1 つ以上のエンティティのマッピングが含まれています。 マッピングは、どのフィールドが他のどのフィールドにマップされるかを示します。

**データ統合プロジェクトを作成するには**

1. [PowerApps 管理センター](https://admin.powerapps.com)に移動します。

2. 左側のナビゲーション ウィンドウで、**[データ統合]** タブを選択します。

3. 一方、**[プロジェクト]** タブでは、右上隅にある **[新しいプロジェクト]** を選択します。

    > [!div class="mx-imgBorder"] 
    > ![プロジェクトを作成する](media/data-integrator/CreateNewProject780.png "プロジェクトを作成する")

4. 統合プロジェクトの名前を指定します。

5. 利用可能なテンプレートのいずれかを選択します (または[独自のテンプレートを作成します](#how-to-customize-or-create-your-own-template))。 この場合、Products エンティティを Finance and Operations から Sales に移動します。

    > [!div class="mx-imgBorder"] 
    > ![テンプレートを選択して新しいプロジェクトを作成する](media/data-integrator/CreateNewProjectSelectTemplate780.png "テンプレートを選択して新しいプロジェクトを作成する")

6. **[次へ]** を選択し、先ほど作成した接続セットを選びます (または[新しい接続セットを作成します](#how-to-create-a-connection-set))。

7. 接続と環境の名前を確認し、適切なものを選択したことを確認します。

    > [!div class="mx-imgBorder"] 
    > ![新しい接続セットを作成する](media/data-integrator/CreateNewProjectSelectConnectionSet780.png "新しい接続セットを作成する")

8. **[次へ]** を選択し、法人から部署へのマッピングを選びます。

    > [!div class="mx-imgBorder"] 
    > ![新しい法人マッピングを作成する](media/data-integrator/CreateNewProjectLegalEntityMapping780.png "新しい法人マッピングを作成する")

9. 次の画面でプライバシーに関する声明と同意を確認した上で受け入れます。

10. 続けてプロジェクトを作成し、プロジェクトを実行します。これにより、プロジェクトが実行されます。

    > [!div class="mx-imgBorder"] 
    > ![プロジェクトを実行する](media/data-integrator/RunProject780.png "プロジェクトを実行する")

    この画面に **[スケジュール]** や **[実行履歴]** などのタブがいくつかあり、**[タスクの追加]**、**[エンティティの更新]**、および **[詳細クエリ]** などのボタン (この記事の後半で説明します) がいくつか示されていることがわかります。

### <a name="execution-history"></a>実行履歴

<!--note from editor: Do you think most people reading this will know what "upsert" means?-->

[実行履歴] にはすべてのプロジェクトの実行の履歴が表示されます。これには、プロジェクト名、プロジェクトが実行されたときのタイムスタンプ、実行の状態、upsert やエラーの数が含まれます。

-   プロジェクトの実行履歴の例。

    > [!div class="mx-imgBorder"] 
    > ![プロジェクトの実行履歴](media/data-integrator/ExecutionHistorySuccessFailures4780.png "プロジェクトの実行履歴")

-   \# 回の upsert で完了したことを示す、成功した実行の例  (Update Insert は、既に存在するレコードを更新するか、新しいレコードを挿入する場合のロジックです)。

    > [!div class="mx-imgBorder"] 
    > ![実行の成功](media/data-integrator/ExecutionHistorySuccess2780.png "実行の成功")

-   実行の失敗については、ドリルダウンして根本原因を確認することができます。

    プロジェクトの検証エラーによる失敗の例を以下に示します。 この場合、プロジェクトの検証エラーの原因は、エンティティ マッピングにソース フィールドがないことです。

    > [!div class="mx-imgBorder"] 
    > ![失敗に関する実行履歴](media/data-integrator/ExecutionHistoryFailures3780.png "失敗に関する実行履歴")

-   プロジェクトの実行状態が "エラー" の場合、次にスケジュールされている実行で再試行されます。

-   プロジェクトの実行の状態が "警告" の場合、ソースに関する問題を修正する必要があります。 次にスケジュールされている実行で再試行されます。

    いずれの場合も、手動で "実行を再実行する" こともできます。

### <a name="how-to-set-up-a-schedule-based-refresh"></a>スケジュール ベースの更新を設定する方法

現在、次のような 2 種類の実行/書き込みがサポートされています。

-   手動による書き込み (手動でプロジェクトを実行および更新する)

-   スケジュール ベースの書き込み (自動更新)

統合プロジェクトを作成した後、手動で実行するか、(プロジェクトの自動更新を設定できる) スケジュール ベースの書き込みを構成することができます。

**スケジュール ベースの書き込みを設定するには**

1. [PowerApps 管理センター](https://admin.powerapps.com)に移動します。

2. 2 つの方法でプロジェクトをスケジュールすることができます。<br>

    プロジェクトを選択して **[スケジュール]** タブを選ぶか、プロジェクトの一覧ページから、プロジェクト名の横にある省略記号をクリックしてスケジューラを起動します。

    > [!div class="mx-imgBorder"] 
    > ![スケジュール ベースの書き込み](media/data-integrator/Schedulebasedwrites780.png "スケジュール ベースの書き込み")

3. **[繰り返しの間隔]** を選択し、すべてのフィールドへの入力が完了したら、**[スケジュールの保存]** を選びます。

    > [!div class="mx-imgBorder"] 
    > ![スケジュール ベースの書き込み](media/data-integrator/Schedulebasedwrites1780.png "スケジュール ベースの書き込み")

頻度を 1 分程度に設定するか、特定数の時間、日、週、または月に繰り返すように指定できます。 前のプロジェクト タスクの実行が完了するまで、次の更新が開始されないことに注意してください。

また、[通知] で、(警告で完了したか、エラーのために失敗したか、あるいはその両方で終了したジョブの実行について知らせる) 電子メール ベースのアラート通知を選択できることに注意してください。 コンマで区切られたグループを含む、複数の受信者を指定できます。

> [!div class="mx-imgBorder"] 
> ![電子メール通知](media/data-integrator/EmailNotification780.png "電子メール通知")

## <a name="customizing-projects-templates-and-mappings"></a>プロジェクト、テンプレート、およびマッピングのカスタマイズ 

テンプレートを使用して、データ統合プロジェクトを作成します。 テンプレートでは、データの移動が共用化されるため、ビジネス ユーザーや管理者がソースからデータをターゲットにすばやく統合するのに役立ち、全体的な負担とコストが削減されます。 ビジネス ユーザーや管理者は、Microsoft によって公開されている、すぐに使えるテンプレートをベースにし、さらにカスタマイズしてからプロジェクトを作成できます。 その後、テンプレートとしてプロジェクトを保存し、組織で共有したり、新しいプロジェクトを作成したりすることができます。 

テンプレートでは、ソース、ターゲット、データ フローの方向が示されます。 独自のテンプレートをカスタマイズしたり、作成したりする際には、このことに注意する必要があります。  

プロジェクトとテンプレートは次のようにカスタマイズできます。

-   フィールド マッピングをカスタマイズする。

-   任意のエンティティを追加して、テンプレートをカスタマイズする。

### <a name="how-to-customize-field-mappings"></a>フィールド マッピングをカスタマイズする方法

**接続セットを作成するには**

1. [PowerApps 管理センター](https://admin.powerapps.com)に移動します。

2. フィールド マッピングをカスタマイズするプロジェクトを選択し、ソース フィールドとターゲット フィールドの間の矢印を選びます。

    > [!div class="mx-imgBorder"] 
    > ![フィールド マッピング](media/data-integrator/FieldMapping780.png "フィールド マッピング")

3. これでマッピング画面が表示され、そこで右上隅にある **[マッピングの追加]** を選択して、新しいマッピングを追加できます。また、ドロップダウン リストの**既存のマッピングをカスタマイズする**こともできます。

    > [!div class="mx-imgBorder"] 
    > ![フィールド マッピングのカスタマイズ](media/data-integrator/FieldMappingCustomize780.png "フィールド マッピングのカスタマイズ")

4. フィールド マッピングをカスタマイズしたら、**[保存]** を選択します。

### <a name="how-to-customize-or-create-your-own-template"></a>独自のテンプレートを作成またはカスタマイズする方法 

**独自のテンプレートを作成するには**

1. [PowerApps 管理センター](https://admin.powerapps.com)に移動します。

2. 新しいテンプレートのソース、ターゲット、フローの方向を特定します。

3. 任意のソース、ターゲット、フローの方向と一致する既存のテンプレートを選んでプロジェクトを作成します。

<!--note from editor: Didn't we create the project in step 3? Step 4 tells us to create the project.-->

4. 適切な接続を選択した後、プロジェクトを作成します。

5. プロジェクトを保存したり、実行したりする前に、右上隅にある **[タスクの追加]** を選択します。

    > [!div class="mx-imgBorder"] 
    > ![テンプレートをカスタマイズする](media/data-integrator/CustomizeTemplate780.png "テンプレートをカスタマイズする")

    これで、**[タスクの追加]** ダイアログが起動します。

6. わかりやすいタスク名を指定し、任意のソースとターゲットのエンティティを追加します。

    > [!div class="mx-imgBorder"] 
    > ![テンプレートのカスタマイズの [タスクの追加]](media/data-integrator/CustomizeTemplateAddtask75.png "テンプレートのカスタマイズの [タスクの追加]")

7. ドロップダウン リストには、ソースとターゲットのエンティティがすべて示されます。

    > [!div class="mx-imgBorder"] 
    > ![テンプレートのカスタマイズの [タスクの追加]](media/data-integrator/CustomizeTemplateAddtask175.png "テンプレートのカスタマイズの [タスクの追加]")

    この場合、SalesForce の User エンティティを Common Data Service for Apps の Users エンティティに同期するための新しいタスクが作成されています。

    > [!div class="mx-imgBorder"] 
    > ![テンプレートのカスタマイズの [タスクの追加]](media/data-integrator/CustomizeTemplateAddtask275.png "テンプレートのカスタマイズの [タスクの追加]")

8. タスクを作成したら、新しいタスクが一覧表示され、元のタスクを削除できます。

    > [!div class="mx-imgBorder"] 
    > ![テンプレートのカスタマイズの [タスクの追加]](media/data-integrator/CustomizeTemplateAddtask3780.png "テンプレートのカスタマイズの [タスクの追加]")

9. これで新しいテンプレート (この場合、User エンティティを SalesForce から Common Data Service にプルするためのテンプレート) が作成されました。 **[保存]** を選択して、カスタマイズ内容を保存します。

10. この新しいテンプレート用にフィールド マッピングをカスタマイズする手順に従います。 このプロジェクトを実行したり、**[プロジェクトのリスト]** ページからテンプレートとしてプロジェクトを保存したりすることができます。

    > [!div class="mx-imgBorder"] 
    > ![テンプレートのカスタマイズの [テンプレートとして保存]](media/data-integrator/CustomizeTemplateSaveAsTemplate780.png "テンプレートのカスタマイズの [テンプレートとして保存]")

11. 名前と説明を入力したり、組織内の他の人と共有したりすることができます。

    > [!div class="mx-imgBorder"] 
    > ![テンプレートのカスタマイズの [テンプレートとして保存]](media/data-integrator/CustomizeTemplateSaveAsTemplate175.png "テンプレートのカスタマイズの [テンプレートとして保存]")

## <a name="advanced-data-transformation-and-filtering"></a>高度なデータ変換とフィルター処理 

Power Query のサポートにより、ソース データの高度なフィルター処理とデータ変換が提供されるようになりました。 Power Query では、使いやすく、魅力的な、コード不要のユーザー エクスペリエンスにより、ユーザーはニーズに合わせてデータを再形成することができます。 プロジェクトごとにこれを有効にすることができます。 

### <a name="how-to-enable-advanced-query-and-filtering"></a>高度なクエリとフィルター処理を有効にする方法

**高度なフィルター処理とデータ変換を設定するには**

1. [PowerApps 管理センター](https://admin.powerapps.com)に移動します。

2. 高度なクエリを有効にするプロジェクトを選択し、**[詳細クエリ]** を選びます。

    > [!div class="mx-imgBorder"] 
    > ![[詳細クエリ] を選択する](media/data-integrator/EnablePQ1780.png "[詳細クエリ] を選択する")

3. 高度なクエリを有効にすることは一方向の操作であり、元に戻せないことを示す警告が表示されます。 **[OK]** を選択して続行し、ソースとターゲットのマッピング矢印を選びます。

    > [!div class="mx-imgBorder"] 
    > ![警告](media/data-integrator/EnablePQ275.png "警告")

4. これで、高度なクエリとフィルター処理を起動するためのリンクと共に、使い慣れたエンティティ マッピング ページが表示されます。

    > [!div class="mx-imgBorder"] 
    > ![高度なクエリとフィルター処理](media/data-integrator/EnablePQ3780.png "高度なクエリとフィルター処理")

5. **リンク**を選択して高度なクエリとフィルター処理ユーザー インターフェイスを起動すると、Microsoft Excel タイプの列にソース フィールドのデータが示されます。

    > [!div class="mx-imgBorder"] 
    > ![高度なクエリとフィルター処理](media/data-integrator/EnablePQ4780.png "高度なクエリとフィルター処理")

6. 上部のメニューから、**[条件列の追加]**、**[重複する列]**、**[抽出]** など、データを変換するためのいくつかのオプションから選ぶことができます。

    > [!div class="mx-imgBorder"] 
    > ![列の追加](media/data-integrator/EnablePQAddColumn75.png "列の追加")

7. 任意の列を右クリックして、**[列の削除]**、**[重複部分の削除]**、**[列の分割]** などの他のオプションを表示することもできます。

    > [!div class="mx-imgBorder"] 
    > ![列を右クリックする](media/data-integrator/EnablePQAddColumn180.png "列を右クリックする")

8. また、各列をクリックし、Excel タイプのフィルターを使用してフィルター処理することもできます。

    > [!div class="mx-imgBorder"] 
    > ![フィルター処理を有効にする](media/data-integrator/EnablePQFiltering80.png "フィルター処理を有効にする")

<!--note from editor: I don't see an "otherwise" in the screenshot. I see "else".-->

9. 既定値の変換は、条件付きの列を使用して行うことができます。 そのためには、**[列の追加]** ドロップダウン リストから **[条件列の追加]** を選択し、新しい列の名前を入力します。 **Then** と **Otherwise** (既定値が示される) の両方を入力します。その場合、任意のフィールドと **If** および **equal to** の値を使用します。

    > [!div class="mx-imgBorder"] 
    > ![条件列の追加](media/data-integrator/EnablePQDefaultValueTransforms2780.png "条件列の追加")

10. 上部にある、*fx* エディターの **each** 句に注目してください。

    > [!div class="mx-imgBorder"] 
    > ![fx エディター](media/data-integrator/EnablePQDefaultValueTransforms2780.png "fx エディター")

11. *fx* エディターで **each** 句を修正して、**[OK]** を選択します。

    > [!div class="mx-imgBorder"] 
    > ![each 句を修正する](media/data-integrator/EnablePQDefaultValueTransforms5780.png "each 句を修正する")

<!--note from editor: The sentence that starts with "Additionally" is confusing - not sure where the "same steps" fit in.-->

12. 変更を加えるたびに、手順を適用します。 右側のウィンドウで適用された手順を確認できます (最新の手順を確認するには、一番下までスクロールします)。 編集する必要がある場合は、手順を元に戻すことができます。 また、左側のウィンドウの一番上にある **[QrySourceData]** を右クリックし、[詳細エディター] に移動して、同じ手順で、背後で実行される M 言語を表示することができます。

    > [!div class="mx-imgBorder"] 
    > ![詳細エディター](media/data-integrator/EnablePQDefaultValueTransforms4780.png "詳細エディター")

13. **[OK]** を選択して高度なクエリとフィルター処理インターフェイスを閉じてから、マッピング タスク ページで、新しく作成された列をソースとして選択し、適宜マッピングを作成します。

    > [!div class="mx-imgBorder"] 
    > ![新しい列を選択する](media/data-integrator/EnablePQDefaultValueTransforms6780.png "新しい列を選択する")

Power Query の詳細については、[Power Query のドキュメント](https://docs.microsoft.com/power-query/)を参照してください。
