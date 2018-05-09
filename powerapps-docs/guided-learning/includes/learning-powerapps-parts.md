ガイド学習の最初のトピックでは、PowerApps の主要なパーツについて説明しました。 ここでは、各パーツをより詳細に説明します。 PowerApps は連動するソフトウェア サービスとアプリのセットです。また、この優れたエコシステムをサポートする関連テクノロジがあります。 PowerApps コンポーネントは次のとおりです。

* **web.powerapps.com** - 構築したアプリを管理および共有します
* **PowerApps Studio** - 使いやすいビジュアル ツールを使用して強力なアプリを構築します
* **PowerApps Mobile** - Windows、iOS、および Android デバイスでアプリを実行します
* **PowerApps 管理センター** - PowerApps 環境とその他のコンポーネントを管理します
* **Common Data Service for Apps** - 共通データ モデルを使用してビジネス データを統合します

PowerApps が*何であるか*を学習するためだけに多くの時間を費やす必要はありませんが、少し詳しく知っておくことをお勧めします。

## <a name="webpowerappscom"></a>web.powerapps.com
アプリを構築する場合は、ほとんどの時間をここで費やすことになります。 ここでは、入手できる**サンプル アプリとテンプレート**を学習して、作成したすべてのアプリを確認します。 アプリは **PowerApps Studio** で作成し、個人や組織とそのアプリを共有します。 データ (**接続**、**ゲートウェイ**、**エンティティ**) を管理します (これらはすべて後ほど説明します)。**flows.microsoft.com** で作成したすべての**フロー**を確認します。フローはアプリと統合することができます。

![web.powerapps.com サイト](./media/learning-powerapps-parts/powerapps-web-site.png)

## <a name="powerapps-studio"></a>PowerApps Studio
**PowerApps Studio** は、最新の任意のブラウザーで使用できる Web アプリケーションとして利用できます。 PowerApps Studio は 3 つのウィンドウとリボンで構成されるため、アプリの作成が **Powerpoint でスライド デッキを構築するのと**似たように感じられます。

1. **左側のナビゲーション バー**。アプリの各画面のサムネイルを表示したり、各画面上のすべてのコントロールの階層を表示したりできます
2. **中央のウィンドウ**。作業中の画面が表示されます
3. **右側のウィンドウ**。レイアウトやデータ ソースなどのオプションを設定します
4. **プロパティ** ドロップダウン リスト。数式を適用するプロパティを選択します
5. **数式バー**。アプリの動作を定義する数式を (Excel のように) 追加します
6. **リボン**。コントロールを追加し、デザイン要素をカスタマイズします

![PowerApps Studio](./media/learning-powerapps-parts/powerapps-studio.png)

## <a name="powerapps-mobile"></a>PowerApps Mobile
**Windows、iOS、および Android 用 PowerApps Mobile** は、アプリを見つけて使用できる環境を提供します。 個別のアプリ ストアを使わなくても、PowerApps 内に留まって、作成したすべてのアプリと、他のユーザーと共有しているすべてのアプリにアクセスできます。 PowerApps Mobile でアプリを使用すると、カメラのコントロール、GPS の位置情報など、デバイスの機能を最大限に活用できます。

![PowerApps Mobile](./media/learning-powerapps-parts/powerapps-mobile.png)

## <a name="admin-center"></a>管理センター
**PowerApps 管理センター**は、組織で PowerApps を管理するための、一元管理された場所です。 ここで、アプリ、データ接続、およびその他の要素を格納するさまざまな**環境**を定義します。 管理センターは、Common Data Service データベースを作成して、アクセス許可とデータ ポリシーを管理する場所でもあります。

![PowerApps 管理センター](./media/learning-powerapps-parts/powerapps-admin-center.png)

### <a name="microsoft-common-data-service-for-apps"></a>Microsoft Common Data Service for Apps
**Common Data Service for Apps** を使用すると、複数のソースのビジネス データを簡単に統合できます。 このサービスの特徴は、アプリやビジネス プロセスに共通する多くの**エンティティ**を含む**共通データ モデル**です。 スケーラブルで信頼性の高い方法でデータが格納され、複数のアプリケーションでデータを利用できます。 アプリケーションは、PowerApps で構築したアプリ、Dynamics 365 などの Microsoft アプリケーション、サード パーティ アプリケーションの場合があります。 下図に web.powerapps.com のエンティティの一部を示します。

![PowerApps の Contact (連絡先) エンティティ](./media/learning-powerapps-parts/powerapps-contact.png)

次のトピックでは、アプリ開発用の優れたエコシステムを構築するために PowerApps が連動する一連の関連テクノロジについて説明します。

