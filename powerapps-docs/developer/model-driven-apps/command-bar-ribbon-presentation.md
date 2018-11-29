---
title: コマンド バーまたはリボンの表示 (モデル駆動型アプリ) | MicrosoftDocs
description: アプリ用 Common Data Service のコマンドを定義するデータは、クライアントによってさまざまな方法で表現でき、エンティティの処理方法に違いがあります。 リボン コマンドを変更したり、新しいフィルターを定義する際に、次の要因を検討する必要があります。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 5b1d7633-ab0d-94ec-166f-f5bc1af2a657
author: JimDaly
ms.author: jdaly
manager: shilpas
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="command-bar-or-ribbon-presentation"></a>バーまたはリボンの表示

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/command-bar-ribbon-presentation -->

アプリ用 Common Data Service のコマンドを定義するデータは、クライアントによってさまざまな方法で表現でき、エンティティの処理方法に違いがあります。 リボン コマンドを変更したり、新しいフィルターを定義する際に、次の要因を検討する必要があります。
  
<a name="BKMK_DifferentPresentations"></a>   
## <a name="different-presentations-of-commands"></a>コマンドのさまざまな表示  
 コマンド データを表示する方法には、3 通りあります。  
  
### <a name="updated-user-experience"></a>更新済みのユーザー エクスペリエンス  
 これは、アプリケーション全体のコマンド バーと、ユーザー エクスペリエンスを更新したエンティティのフォームの表示です。  
  
 ![取引先企業のコマンド バー](media/customization-account-grid-command-bar.PNG "Dynamics 365 の取引先企業のコマンド バー")
  
 このエクスペリエンスでは、最初の 7 つのコマンドのみが表示され、そのほかのコマンドはポップアップ メニューに表示されます。  
  
 ルールを有効にすると使用しないコマンドが非表示になります。  
  
 サブグリッドのコントロールの数には制限があります。 レコードを追加する、レコードを削除する、グリッド ビューを開くことが可能なコントロールのみを使用できます。 しかし、これらのコマンドは、リボン データで定義されており、カスタマイズできます。  
  
 ![取引先担当者のサブグリッド](media/customization-contract-subgrid.PNG "Dynamics 365 の取引先担当者のサブグリッド")  
  
 サブグリッドに表示されるレコードの一覧で、そのほかの操作を実行するには、グリッド ビューを開くオプションを選択します。  
  
 サブグリッド コントロールの動作に関する詳細およびカスタマイズ方法については、[サブグリッドリボン](/dynamics365/customer-engagement/developer/customize-dev/ribbons-available-microsoft-dynamics-365#BKMK_SubGridRibbons)を参照してください。  
  
### <a name="classic-user-experience"></a>従来のユーザー エクスペリエンス  
 これはリボンを使用した表示です。 また、Outlook クライアント内の一覧と、更新されたユーザー エクスペリエンスを使用しないエンティティ フォームで使用されます。  
  
 ![記事リボン](media/customization-article-ribbon.PNG "Dynamics 365 の記事リボン")  
  
 このエクスペリエンスでは、タブを使用でき、タブの使用できるコマンドを画面の幅の変更に合わせてすべて表示できるようグループでスケーリングを定義できます。  
  
 ルールを有効にすると、コマンドを表示したままコマンドを無効にできます。  
  
 サブグリッドが選択されている場合、サブグリッド コマンドがページの上部リスト ツールのコンテキスト タブに表示されます。  
  
 ![記事コメントのサブグリッド リボン](media/customization-article-comments-subgrid-ribbon.PNG "Dynamics 365 の記事コメントのサブグリッド リボン")  
  
<a name="BKMK_CRMForTablets"></a>   
### <a name="dynamics-365-for-tablets"></a>Dynamics 365 for tablets  
 Dynamics 365 for tablets は、タッチ操作に最適になるようにコマンドが表示されます。 コマンドは、画面の右下のコマンド バーに右から左の順で表示されます。  
  
 ![タブレット用の Dynamics 365 のアカウント フォーム コマンド](media/customization-nobile-app-account-form-command.PNG "タブレット用の Dynamics 365 のアカウント フォーム コマンド")  
  
> [!NOTE]
>  コマンド用に構成済みのアイコンは表示されず、長すぎるラベルは途中で切り捨てられます。  
> 
> Dynamics 365 for tablets は実行時に `<FlyoutAnchor>` または `<SplitButton>` 要素への動的要素の追加をサポートしていません。  
  
 サブグリッド コマンドは、サブグリッド コントロールをタップしたり押したりすると表示されます。 これらのコマンドは、画面の左下に右から左の順で表示されます。  
  
 ![Dynamics 365 for tablets の活動のサブグリッド コマンド](media/customization-mobile-app-activity-subgrid.PNG "Dynamics 365 for tablets の活動のサブグリッド コマンド")  
  
<a name="BKMK_CommandData"></a>   
## <a name="command-data"></a>コマンド データ  
 これらの非常に異なる表示に関わらず、エンティティのコマンドを定義するデータはコマンドの表示方法に関わらず一定です。 これには、タブおよびグループがスケーリングとともに定義されていますが、コントロールのこれらのコンテナーの表示部分は、従来のユーザー インターフェイスにのみ表示されます。  
  
 更新されたユーザー エクスペリエンスおよびタブレット、タブ、グループ用の Dynamics 365 は両方とも、コントロールのコンテナーとして機能しますが、これらのコンテナーの表示はなく、スケーリングは適用されません。  
  
<a name="BKMK_FilteringCommands"></a>   
## <a name="filtering-commands-based-on-presentation-and-client"></a>表示およびクライアントに基づいたコマンドのフィルター  
  
> [!IMPORTANT]
>  コマンドをすべてのクライアントや表示で使用可能にする場合以外は、コマンドの表示をフィルターするための特定の種類のルールを含める必要があります。  
  
 このリリースでは、表示に使用できる新しい要素はなく、ルールを表示するコマンドに適用することができます。  
  
 `<CommandClientTypeRule>` は、表示に基づいて評価される `Type` の属性が含まれます。 次で有効なオプションは、次の表示方法に対応します。  
  
- `Refresh`: 更新されたユーザー エクスペリエンス  
  
- `Legacy`: 従来のユーザー エクスペリエンス  
  
- `Modern`: タブレット PC 用 Dynamics 365  
  
  表示方法別に表示するかどうかを制御するコマンドを定義するには、この要素を使用します。  
  
  また既存の `<CrmClientTypeRule>` 要素が含まれていますが、その要素の `Type` 属性は `Web` と `Outlook` クライアントの間でのみ識別できます。 このルールは、Web クライアントとしてタブレット クライアント用 Dynamics 365 を評価します。  
  
### <a name="see-also"></a>関連項目  
 [コマンド、およびリボンをカスタマイズする](customize-commands-ribbon.md)   
 [利用できるリボン](/dynamics365/customer-engagement/developer/customize-dev/ribbons-available-microsoft-dynamics-365)   
 [リボン定義のエクスポート](export-ribbon-definitions.md)   
 [カスタマイズの開発者ガイド](/dynamics365/customer-engagement/developer/customize-dev/customize-applications)
