PowerApps のすべてのパーツと、アプリを作成するための各種オプションに慣れたところで、実際にアプリを構築してみましょう。 このトピックでは、SharePoint Online リストから電話アプリを生成しますが、他にも Excel やクラウド サービス (Salesforce など)、オンプレミスのソース (SQL Server など) といった多くのソースのデータを使用することができます。

## <a name="connect-to-a-data-source"></a>データ ソースへの接続
web.powerapps.com で、左端近くにある **[アプリ]** をクリックまたはタップします。次に、バナーの **[アプリの作成]** をクリックまたはタップします。

PowerApps では、データやテンプレートからアプリを作成できます。また、最初から作成することもできます。 SharePoint リストの電話アプリを構築するので、**[SharePoint]** の下の **[Phone layout]** (電話レイアウト) をクリックまたはタップします。

![SharePoint リストの電話アプリ](./media/learning-create-first-app-powerapps/generate-sharepoint-phone.png)

生成されたアプリは常に、1 つのリストまたはテーブルをベースにしています (後でアプリにデータをさらに追加できます)。 次の 3 つの画面に、SharePoint Online の **[Flooring Estimates]** (床材見積もり) リストに接続する過程を示します。

![SharePoint Online リストに接続する](./media/learning-create-first-app-powerapps/generate-connect-list.png)

**[Connect]** (接続) をクリックすると、PowerApps がアプリの生成を開始します。 PowerApps は、データに関するあらゆる推論を行うため、開始点として便利なアプリが生成されます。

## <a name="explore-the-generated-app"></a>生成されたアプリの詳細
成功です。 新しい 3 画面アプリが PowerApps Studio で開きます。 データから生成されたすべてのアプリには、同じ画面セットが含まれています。

* **ブラウズ**画面: リストから取得したデータを参照、並べ替え、フィルター処理、更新し、(+) アイコンをクリックして項目を追加する画面。
* **詳細**画面: 項目の詳細を表示し、項目の削除または編集ができる画面。
* **編集/作成**画面: 既存の項目を編集したり、新規に作成する画面。

左側のナビゲーション バーで、右上のアイコンをクリックまたはタップしてサムネイル表示に切り替えます。 

![表示の切り替え](./media/learning-create-first-app-powerapps/toggle-view.png)

各サムネイルをクリックまたはタップすると、その画面上のコントロールが表示されます。

![生成されたアプリ](./media/learning-create-first-app-powerapps/generate-finished-app.png)

右上にある ![アプリのプレビューを開始する矢印を](./media/learning-create-first-app-powerapps/f5-arrow-sm.png) クリックまたはタップしてアプリを実行します。 アプリ全体を見ると、アプリにリストのすべてのデータが含まれていて、アプリが既定で良いエクスペリエンスを提供していることが分かります。

とても簡単ですね。 ほんの数分で、データ ソースに接続して、アプリを生成し、PowerApps Studio と 3 つのアプリ画面を確認する方法を学習しました。 以降のセクションでは、生成されたアプリをカスタマイズする方法を確認します。 次のトピックでは、コースのこのセクションを確認し、以降のレッスンの準備をします。

