---
title: ソリューション チェッカーを使用した PowerApps でのアプリの検証 | Microsoft Docs
description: ソリューションを検証するには、ソリューションのチェッカーを使用します。
author: Mattp123
manager: kvivek
ms.service: powerapps
ms.component: cds
ms.topic: article
ms.date: 12/04/2018
ms.author: matp
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="use-solution-checker-to-validate-your-model-driven-apps-in-powerapps"></a>ソリューション チェッカーを使用した PowerApps でのモバイル駆動型アプリの検証

複雑なビジネス要件を満たすため、モデル駆動型のアプリケーション メーカーは、アプリケーション プラットフォームの Common Data Service (CDS) をカスタマイズして拡張する非常に高度なソリューションで終わることがあります。 高度な実装により、パフォーマンス、安定性、信頼性の問題が生じるリスクが増加し、エンド ユーザーの作業に悪影響を与える可能性があります。 これらの問題を解決する方法を特定して理解することは、複雑で時間がかかることがあります。 ソリューション チェッカー機能を使用すると、一連のベスト プラクティス ルールに対してソリューションで機能豊富なスタティック分析チェックを実行し、これらの問題となるパターンを識別できます。 チェックが完了すると、特定された問題、影響を受けるコンポーネントとコード、各問題を解決する方法が説明されたするドキュメントへのリンクが一覧になった詳細なレポートを受け取ります。

ソリューション チェッカーは、これらのソリューション コンポーネントを分析します。 
- アプリ用 CDS プラグイン
- アプリ用 CDS のユーザー定義のワークフロー活動 
- アプリ用 CDS Web リソース (HTML と JavaScript)
- SDK メッセージ ステップなどのアプリ用 CDS 構成 

ソリューション チェッカーは、環境からエクスポートできるアンマネージド ソリューションを使用します。 ソリューション チェッカーは、次のソリューションでは機能しません。 
- システムの既定のソリューション (既定のソリューション、および Common Data Service の既定のソリューション)。
- ECMAScript 6 (2015) 以降のバージョンを使用した JavaScript を含むソリューション。 これらのバージョンのいずれかを使用した JavaScript が検出されると、Web リソースの JS001 構文は問題報告されます。

> [!NOTE]
> この機能は、現在プレビュー段階であり、北米地域でのみ使用できます。 
> [!INCLUDE [cc-preview-features-definition](../../includes/cc-preview-features-definition.md)]


## <a name="enable-the-solution-checker"></a>ソリューション チェッカーを有効にする
ソリューション チェッカーは、PowerApps チェッカー ソリューションをインストールした後 PowerApps のソリューションの領域で使用可能になります。 Microsoft AppSource を参照したり検索しても見つからないことに注意してください。 次の手順に従って、インストールを実行する必要があります。  

1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインし、ソリューション チェッカーを有効にする Common Data Service 環境を選択します。 
2. 左のナビゲーション ウィンドウで、**ソリューション** を選択します。
3. ツール バーで、**ソリューション チェッカー** を選択し、**インストール** を選択します。これにより、Microsoft AppSource ページが開きます。 ブラウザーでページがブロックされた場合、ポップアップを許可する必要があります。 

   ![ソリューション チェッカーのインストール](media/solution-checker-install.png)

4. AppSource ページで **無料試用版** を選択します。 
5. 同意した場合、契約条件に同意し、PowerApps チェッカー ソリューションをインストールする環境を選択します。 
6.  インストールが完了したら、ソリューション チェッカーが使用可能であることを確認するために、PowerApps サイトで **ソリューション** を更新します。  
7. ソリューションを確認するには、[ソリューション チェッカーを実行します](#run-the-solution-checker)。


<!-- ### Components created with the PowerApps checker
When you install the PowerApps checker these solution specific components are created. 
- Entities: The entities that are created are required to store the results of solution analysis and the status of analysis jobs in your environment.
   - Analysis Component
   - Analysis Job
   - Analysis Result
- System job: A system job is created so admins can remove solution analysis data from the environment. The job contains a configuration value, currently set to remove the solution analysis data after 60 days, which an administrator can override. 
- Security Roles: Two security roles, **Export Customizations**, and **Solution Checker** are created. These roles are required to export the solution for analysis, and storing the analysis results to the entities in your environment.
- User principle: The **PowerApps Advisor** user is created that allows the checker to authenticate with your CDS for Apps environment and assign the two security roles, Export Customizations and Solution Checker. The PowerApps Advisor is an application user and does not consume a license.  -->

## <a name="run-the-solution-checker"></a>ソリューション チェッカーを実行する
環境に PowerApps チェッカーをインストールしたら、PowerApps の **ソリューション** 領域でアンマネージド ソリューションを選択すると **ソリューション チェッカー** メニュー項目が利用可能になります。 

1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。 
2. 左側のウィンドウで、**ソリューション** を選択します。 
3. 分析するアンマネージド ソリューションの横で、**...** を選択し、**ソリューション チェッカー** をポイントして **実行** を選択します。 

   ![ソリューション チェッカー コマンドを実行する](media/solution-checker-run.png)

4.  **ソリューション** ページの右上にあるステータス ウィンドウに、**ソリューション チェッカーの実行** が表示されます。 

    ![ソリューション チェッカーのステータス](media/solution-checker-status.png)
   
     以下に注意します。
       - ソリューション チェッカーが分析を完了するまで、数分間かかる場合があります。 
    
       - この間、**実行…**  状態と、**ソリューション** リストの **ソリューション チェック** 列に表示されます。 
    
       - チェックが完了したら、電子メール通知を受け取り、PowerApps サイトの **通知** 領域に通知が表示されます。  

5.  チェックが完了したら、[レポートを表示します](#reviewing-the-solution-checker-report)。

## <a name="cancel-a-check"></a>チェックを取り消す

環境でソリューション チェックを送信すると、**ソリューション** ページの右上領域の状態ウィンドウでチェックを取り消すことができます。 

チェックを取り消すと、ソリューション チェックが実行を停止し、ソリューション チェック状態が以前の状態に戻ります。 

## <a name="solution-checker-states"></a>ソリューション チェッカーの状態
環境にソリューション チェッカーをインストールすると、**ソリューション チェック** 列が **ソリューション** リストで使用可能になります。 この列には、ソリューションのソリューション分析状態が表示されます。 

|都道府県  |説明  |
|---------|---------|
|実行されていない    | ソリューションはまったく分析されていません。        |
|実行中     | ソリューションが分析されています。       |
|完了できなかった     |  ソリューションの分析が要求されましたが、分析が正常に完了しませんでした。       |
|*日時* 現在の結果   | ソリューションの分析が完了し、結果をダウンロードできます。      |
| 完了できなかった。 *日時* 現在の結果     | 最新の分析要求が正常に完了しませんでした。 最後の正常な結果をダウンロードできます。         |
|Microsoft がチェック     | これは、Microsoft の管理ソリューションです。 ソリューションの分析は、これらのソリューションで使用できません。         |
|発行元がチェック     |  これは、サードパーティの管理ソリューションです。 現在、ソリューション分析は、これらのソリューションで利用できません。        |


## <a name="review-the-solution-checker-report"></a>ソリューション チェッカー レポートを確認
ソリューション チェックが完了すると、分析レポートは、Web ブラウザーからダウンロードできるようになります。 レポートは、[!INCLUDE [pn-excel-short](../../includes/pn-excel-short.md)] 形式であり、ソリューションで検出された各問題の影響、種類、場所を識別するのに役立ついくつかのビジュアル化と列が含まれています。 問題の解決方法に関する詳細なガイダンスへのリンクも提供されます。 

1. 左側のウィンドウで、**ソリューション** を選択します。
2. ソリューション チェッカー レポートをダウンロードするアンマネージド ソリューションの横で、**...** を選択し、**ソリューション チェッカー** をポイントして **最新の結果をダウンロード** を選択します。  
3. ソリューション チェッカーの ZIP ファイルは、Web ブラウザーによって指定されたフォルダーにダウンロードされます。

レポート内の各列の概要を以下に示します。

|レポート フィールド |説明  |コンポーネントに適用   |
|---------|---------|---------|
|問題     |   ソリューションで識別される問題のタイトル。      | すべて        |
|カテゴリ     | 問題の分類が識別されます。**パフォーマンス**、**使用状況**、または **サポート可能性** などです。      |  すべて       |
|重要度     | 検出された問題の潜在的な影響を表します。 使用可能な影響の種類は、**高**、**中**、**下**、**情報** です。         |  すべて       |
|ガイダンス     |  問題、影響、推奨される解決先の詳細が記載された記事へのリンク。 アクション。       |  すべて       |
|コンポーネント     |  問題が特定されたソリューション コンポーネントです。        |   すべて      |
|Location     |  アセンブリや JavaScript ファイル名など、特定された問題が発生したコンポーネントの場所やソース ファイルです。        |  すべて       |
|行番号     |  影響を受ける Web リソース コンポーネントの問題の行番号参照。       |  Web リソース       |
|モジュール     | アセンブリで特定された問題が検出されたモジュール名。     |   プラグインまたはユーザー定義ワークフロー活動      |
|型     | アセンブリで識別された問題の種類。        | プラグインまたはユーザー定義ワークフロー活動        |
|メンバー     |  アセンブリで識別された問題のメンバー。      | プラグインまたはユーザー定義ワークフロー活動        |
|ステートメント     | 問題が発生したコード ステートメントまたは構成。        |  すべて       |
|コメント     | 高レベルな解決手順が含まれる問題に関する詳細。         |  すべて       |



## <a name="best-practice-rules-used-by-solution-checker"></a>ソリューション チェッカーにより使用される推奨事項ルール


|ソリューション コンポーネント   |ルール名  |ルールの説明  |
|---------|---------|---------|
|プラグインまたはワークフロー活動   | [il-specify-column](http://go.microsoft.com/fwlink/?LinkID=398563&error=il-specify-column&client=PAChecker&source=featuredocs)  | Dynamics 365 for Customer Engagement クエリ API を使用してすべての列を選択しないでください。     |
|プラグインまたはワークフロー活動   | [meta-remove-dup-reg](http://go.microsoft.com/fwlink/?LinkID=398563&error=meta-remove-dup-reg&client=PAChecker&source=featuredocs)     | 重複する Dynamics 365 for Customer Engagement プラグイン登録を避けてください。     |
|プラグインまたはワークフロー活動   | [il-turn-off-keepalive](http://go.microsoft.com/fwlink/?LinkID=398563&error=il-turn-off-keepalive&client=PAChecker&source=featuredocs)   | Dynamics 365 for Customer Engagement プラグインで外部ホストを操作するときは、キープアライブを false に設定します。     |
|プラグインまたはワークフロー活動   | [il-avoid-unpub-metadata](http://go.microsoft.com/fwlink/?LinkID=398563&error=il-avoid-unpub-metadata&client=PAChecker&source=featuredocs)   | 非公開 Dynamics 365 for Customer Engagement メタデータを取得しないでください。     |
|プラグインまたはワークフロー活動   | [il-avoid-batch-plugin](http://go.microsoft.com/fwlink/?LinkID=398563&error=il-avoid-batch-plugin&client=PAChecker&source=featuredocs)   | Dynamics 365 Customer Engagement プラグインとワークフロー活動でバッチ要求の種類を使用しないでください。    |
|プラグインまたはワークフロー活動   | [meta-avoid-reg-no-attribute](http://go.microsoft.com/fwlink/?LinkID=398563&error=meta-avoid-reg-no-attribute&client=PAChecker&source=featuredocs)  | Dynamics 365 for Customer Engagement プラグイン登録にフィルター属性を含めます。    |
|プラグインまたはワークフロー活動   | [meta-avoid-reg-retrieve](http://go.microsoft.com/fwlink/?LinkID=398563&error=meta-avoid-reg-retrieve&client=PAChecker&source=featuredocs)  | Retrieve および RetrieveMultiple メッセージに登録された Dynamics 365 for Customer Engagement プラグインは注意して使用してください。    |
|プラグインまたはワークフロー活動   | [meta-remove-inactive](http://go.microsoft.com/fwlink/?LinkID=398563&error=meta-remove-inactive&client=PAChecker&source=featuredocs)    | Dynamics 365 for Customer Engagement で非アクティブな構成を削除します。    |
|プラグインまたはワークフロー活動   | [window.top を使用しないでください](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-avoid-window-top&client=PAChecker&source=featuredocs)   | window.top を使用しないでください。    |
|プラグインまたはワークフロー活動   | [il-meta-avoid-crm2011-depr-message](http://go.microsoft.com/fwlink/?LinkID=398563&error=il-avoid-crm2011-depr-message&client=PAChecker&source=featuredocs)  | Microsoft Dynamics CRM 2011 の削除されたメッセージを使用しないでください。     |
|プラグインまたはワークフロー活動   | [meta-avoid-crm4-event](http://go.microsoft.com/fwlink/?LinkID=398563&error=meta-avoid-crm4-event&client=PAChecker&source=featuredocs) | Microsoft Dynamics CRM 4.0 プラグイン登録ステージを使用しないでください。    |
|プラグインまたはワークフロー活動   | [il-avoid-specialized-update-ops](http://go.microsoft.com/fwlink/?LinkID=398563&error=il-avoid-specialized-update-ops&client=PAChecker&source=featuredocs)  | Dynamics 365 for Customer Engagement で特殊な更新操作要求を使用しないでください。        |
|Web リソース  | [web-use-async](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-use-async&client=PAChecker&source=featuredocs)  |  HTTP および HTTPS リソースを非同期に操作します。   |
|Web リソース  | [meta-remove-invalid-form-handler](http://go.microsoft.com/fwlink/?LinkID=398563&error=meta-remove-invalid-form-handler&client=PAChecker&source=featuredocs)  | 無効な Dynamics 365 for Customer Engagement フォーム イベント登録を修正するか、削除してください。   |
|Web リソース  | [meta-remove-orphaned-form-element](http://go.microsoft.com/fwlink/?LinkID=398563&error=meta-remove-orphaned-form-element&client=PAChecker&source=featuredocs)  | 孤立した Dynamics 365 for Customer Engagement フォーム イベント登録を修正するか、削除してください。   |
|Web リソース  | [web-avoid-modals](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-avoid-modals&client=PAChecker&source=featuredocs)  | モーダル ダイアログを使用しないでください。   |
|Web リソース  | [web-avoid-crm2011-service-odata](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-avoid-crm2011-service-odata&client=PAChecker&source=featuredocs)   | Microsoft Dynamics CRM 2011 OData 2.0 エンドポイントをターゲットにしないでください。     |
|Web リソース  | [web-avoid-crm2011-service-soap](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-avoid-crm2011-service-soap&client=PAChecker&source=featuredocs)  | Microsoft Dynamics CRM 2011 SOAP サービスをターゲットにしないでください。   |
|Web リソース  | [web-avoid-browser-specific-api](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-avoid-browser-specific-api&client=PAChecker&source=featuredocs) | Internet Explorer レガシー API やブラウザーのプラグインを使用しないでください。   |
|Web リソース  | [web-avoid-2011-api](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-avoid-2011-api&client=PAChecker&source=featuredocs)  | 廃止された Microsoft Dynamics CRM 2011 オブジェクト モデルを使用しないでください。  |
|Web リソース  | [web-use-relative-uri](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-use-relative-uri&client=PAChecker&source=featuredocs)   | アプリ用 CDS エンドポイント絶対 URL を使用しないでください。    |
|Web リソース  | [web-use-client-context](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-use-client-context&client=PAChecker&source=featuredocs)  | クライアント コンテキストを使用してください。   |
|Web リソース  | [web-use-dialog-api-param](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-use-dialog-api-param&client=PAChecker&source=featuredocs)   | ダイアログ API パラメーターを使用します。   |
|Web リソース  | [web-use-org-setting](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-use-org-setting&client=PAChecker&source=featuredocs)   | 組織設定を使用します。   |
|Web リソース  | [web-use-grid-api](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-use-grid-api&client=PAChecker&source=featuredocs)   | グリッド API を使用します。    |
|Web リソース  | [web-avoid-isActivityType](http://go.microsoft.com/fwlink/?LinkID=398563&error=web-avoid-isActivityType&client=PAChecker&source=featuredocs)   | Xrm.Utility.isActivityType メソッドを新しい Xrm.Utility.getEntityMetadata に置き換えます。リボン ルールは使用しないでください。    |
|Web リソース  | [meta-avoid-silverlight](http://go.microsoft.com/fwlink/?LinkID=398563&error=meta-avoid-silverlight&client=PAChecker&source=featuredocs)   | Silverlight Web リソースの使用は廃止されました。   |


## <a name="see-also"></a>関連項目
[PowerApps での実験とプレビュー機能について](../canvas-apps/working-with-experimental.md) <br/>
[PowerApps ソリューションを構築するためのガイドおよび推奨事項](https://docs.microsoft.com/dynamics365/customer-engagement/guidance/)
