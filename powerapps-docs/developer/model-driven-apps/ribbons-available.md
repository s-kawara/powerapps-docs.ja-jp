---
title: モデル駆動型アプリで使用可能なリボン | MicrosoftDocs
description: このトピックでは、リボンを定義および変更する場所について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="ribbons-available"></a>利用できるリボン

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/ribbons-available-microsoft-dynamics-365 -->

このトピックでは、モデル駆動型アプリでリボンを定義および変更する場所について説明します。

<a name="ribbon_defs"></a>   
## <a name="ribbon-definitions"></a>リボン定義  
 モデル駆動型アプリには、アプリケーションのすべてのリボンについて既定の `<RibbonDiffXml>` 定義が含まれています。 組織のリボンを定義している現在の XML をエクスポートおよび表示することはできますが、XML を直接更新することはできません。 リボンをカスタマイズするには、リボンをどのように変更するかを定義します。 指定した変更定義は、リボンがアプリケーションに表示される際に適用されます。 すべての変更は、`<CustomAction>` 要素または `<HideCustomAction>` に含めます。 これらの要素は、モデル駆動型アプリが提供する既定のリボン定義よりも優先して適用されます。  

 変更定義を記述する場合は、既定のリボンの定義を頻繁に参照する必要があります。 たとえば、特定のリボン要素を非表示にする場合は、その要素の一意の ID を知る必要があります。 新しいリボン要素を既存のリボン要素の中または横に配置する場合は、それらの要素の ID 値と、要素の相対位置を制御するシーケンス順序を知る必要があります。  

 このように、既存のリボン要素の定義を参照する必要があるため、組織の現在のリボン定義を理解することは非常に重要です。 リボンの現在の状態を表す XML ファイルのエクスポートに使用できるメッセージは 2 つあります。 これらの定義には、既にシステムに適用されているすべてのカスタマイズが含まれているので、以前適用されたすべてのユーザー定義リボンをカスタマイズできます。 詳細については、「[リボン定義のエクスポート](export-ribbon-definitions.md)」を参照してください。  

 簡単に開始するために、[Microsoft ダウンロード: ExportedRibbonXml.zip](http://download.microsoft.com/download/C/2/A/C2A79C47-DD2D-4938-A595-092CAFF32D6B/ExportedRibbonXml.zip) から MDA の既定のリボン定義をダウンロードできます。 ExportedRibbonXml.zip ファイルには、リボンがカスタマイズされていない組織のための出力ファイルが含まれています。 このデータをエクスポートするために、サンプル アプリケーションを実行する必要はありません。 リボンがカスタマイズされている場合は、サンプル アプリケーションを実行して、このフォルダーのファイルをこれまで組織に適用されたすべてのカスタマイズで更新する必要があります。  

 エクスポートされたリボン XML ファイルの中で、applicationRibbon.xml ファイルには、特定のエンティティに対して定義されていないすべてのリボンが含まれます。 これらのリボンは、**アプリケーション リボン**ソリューション コンポーネントに対応しています。 エンティティごとに、*エンティティ名*ribbon.xml ファイルがあります。 このファイルは、各エンティティに含まれる `RibbonDiffXml` に対応しています。 特定のエンティティのリボンを編集する場合は、そのエンティティのリボン XML ファイルを見つける必要があります。  

<a name="entity_ribbons"></a>   
## <a name="entity-ribbons"></a>エンティティ リボン  
 すべてのエンティティで、*エンティティ リボン テンプレート*と呼ばれる共通のリボン定義が使用されます。 エンティティ リボン テンプレート定義は、applicationribbon.xml ファイル内にあります。 ユーザー定義エンティティを作成した場合、表示されるリボンは、エンティティ リボン テンプレートによって定義された既定のリボンです。 各システム エンティティには、エンティティ リボン テンプレート定義に基づいて作成された個々の `<RibbonDiffXml>` 定義があります。  

 applicationribbon.xml ファイル内には、すべてのエンティティに適用される以下のタブがあります。  

- `Mscrm.Form.{!EntityLogicalName}.MainTab`  

   エンティティの表示名をラベルに表示するタブ。  

- `Mscrm.Form.{!EntityLogicalName}.Related`  

   **追加**というラベルを持つタブ。  

- `Mscrm.Form.{!EntityLogicalName}.Developer`  

   **カスタマイズ**というラベルを持つタブ。  

- `Mscrm.HomepageGrid.{!EntityLogicalName}.MainTab`  

   エンティティの複数形での表示名をラベルに表示するタブ。  

- `Mscrm.HomepageGrid.{!EntityLogicalName}.View`  

   **表示**というラベルを持つタブ。  

- `Mscrm.HomepageGrid.{!EntityLogicalName}.Related`  

   **追加**というラベルを持つタブ。  

- `Mscrm.HomepageGrid.{!EntityLogicalName}.Developer`  

   **カスタマイズ**というラベルを持つタブ。  

- `Mscrm.SubGrid.{!EntityLogicalName}.ContextualTabs`  

   フォームまたはグラフのサブ グリッドにフォーカスがある場合は、**リスト ツール**というラベルを持つ状況依存のタブが表示されます。  

  -   `Mscrm.SubGrid.{!EntityLogicalName}.MainTab`  

       エンティティの複数形での表示名を表示するタブ。  

  特定のエンティティのリボン定義を表示すると、通常は、エンティティの名前が `{!EntityLogicalName}`トークンに置き換わることがわかります。 特定のエンティティのリボン定義で、`{!EntityLogicalName}` トークンを表示すると、それは、そのエンティティに対する特定の定義はなく、単にエンティティ リボン テンプレートの定義を使用することを意味します。 特定のエンティティにリボンを定義した場合は、常に実際のエンティティ名が使用されます。 特定のエンティティのリボンの変更は、`//ImportExportXml/Entities/Entity/RibbonDiffXml` ノードで定義する必要があります。  

  RibbonDiffXml ノードでエンティティの論理名の代わりにトークン `{!EntityLogicalName}` を代用するアプリケーション リボンへの変更を定義することで、すべてのエンティティに適用する変更を行うことができます。 すべてのエンティティに対して定義されているアプリケーション リボンへの変更は、`ImportExportXml/RibbonDiffXml` ノードで定義する必要があります。 特定のエンティティの RibbonDiffXml ノードで定義することはできません。  

### <a name="grid-ribbons"></a>グリッド リボン  
 エンティティ グリッド リボンは、`Mscrm.HomepageGrid.<entity logical name>` で始まる ID 属性値を持つタブのコレクションです。 たとえば、取引先企業エンティティ グリッドに「Accounts」というテキストを持つタブは `Mscrm.HomepageGrid.account.MainTab` です。 取引先企業エンティティ グリッドに表示されるすべてのタブは、`Mscrm.HomepageGrid.account` で始まる ID 値を持ちます。  

<a name="BKMK_SubGridRibbons"></a>   
### <a name="subgrid-ribbons"></a>サブグリッド リボン  
 エンティティ サブグリッド リボンは、`Mscrm.SubGrid.<entity logical name>` で始まる ID 属性値を持つタブのコレクションで構成される状況依存グループです。 たとえば、取引先企業エンティティ サブグリッドに「Accounts」というテキストを持つタブは `Mscrm.SubGrid.account.MainTab` です。  

 エンティティのレコードのリストが別のエンティティのフォームまたはグラフのサブグリッド内に表示される場合、サブグリッドの上部または内で直接使用できるコントロールは 3 種類のみです。 これらのコントロールの動作は、関連付けられているコマンドの変更で、変更できます。  

- **追加** ![[追加] ボタン](media/customization-subgrid-add.PNG "[追加] ボタン")のアイコンを含むコマンドの既定動作は、 サブグリッドのレコードが現在のレコードに関連しているかどうかによって異なります。  

     レコードが現在のレコードに関連する場合、既定動作では既存レコードを探します。 既存のレコードを検索できない場合、またはユーザーが新しいレコードを作成するときには、**新規追加**をクリックできます。  

     レコードが現在のレコードに関連していない場合、既定動作では新しいレコードを追加します。 エンティティに簡易作成フォームがある場合、これが表示されますが、他の場合には、新しい完全なフォームが表示されます。  

     活動は、このパターンに対する例外です。 追加コマンドでは常に、活動のタイプが最初にプロンプトされます。

     > [!NOTE]
     >  Dynamics 365 のオフライン モードはユーザー定義エンティティの多対多関連付けをサポートしていません。 このため、Dynamics 365 のオフライン モードではサブグリッドの**新規追加**ボタンは表示されません。

- **リストの表示** ![[ビューを開く] ボタン](media/customization-open-view.PNG "[ビューを開く] ボタン")のアイコンを含むコマンドにより、使用できるすべてコマンドが使用できる一覧が開かれます。  

     サブグリッドが現在のレコードに関連付けられている場合、このコマンドの既定動作は、関連ビューをオープンすることです。  

     サブグリッドが現在のレコードに関連付けられていない場合、このコマンドの既定動作は、メインリストビューのビューをオープンすることです。  

- **削除** ![サブリストの削除アイコン](media/customization-subgrid-delete.PNG "サブリストの削除アイコン")が、 一覧内のレコードにカーソルを置くと、行の右側に表示されます。  

     1:N の関連付けのレコードまたは関連付けがないレコードの場合、既定動作はレコードを削除することです。 関係構成のために許可されていない場合、削除はブロックされている可能性があります。 オープンしている活動および請求書は、関連構成のために削除されない可能性があるレコードで共通の例です。  

     N:N の関連付けを示す関連付けの場合、既定動作は、レコード自体ではなく、レコードをつなぐ関連付けを削除することです。  

  `<CommandDefinition>`を使用してコマンドに関連付けられたアクションを変更することで、既定動作を変更できますが、コマンドの名前を変更することはできません。 たとえば、削除動作は、レコードを削除するのではなくレコードを非アクティブ化するように変更することはできます。  

  これらのコマンドに対して表示されるアイコンを変更することはできません。 
  `<HideCustomAction>`を使用して、これらのコマンドを非表示にすることができます。  

### <a name="form-ribbons"></a>フォーム リボン  
 エンティティごとに複数のフォームを持つことができます。 エンティティ レベルでの定義を追加することにより、そのエンティティのすべてのフォームに対するフォーム リボンへの変更を定義できます (`//ImportExportXml/Entities/Entity/RibbonDiffXml`)。  

 エンティティ フォームごとに固有のリボン定義を持つことができます。 エクスポートした customizations.xml ファイル内の `//ImportExportXml/Entities/Entity/FormXml/forms/systemform/form/RibbonDiffXml` の場所に、変更した `<RibbonDiffXml>` を追加する必要があります。  

 エンティティ フォーム リボンは、`Mscrm.Form.<entity logical name>` で始まる ID 属性値を持つタブのコレクションです。 たとえば、取引先企業エンティティ フォームに**Account**というラベルを持つタブは `Mscrm.Form.account.MainTab` です。 取引先企業エンティティ フォームに表示されるすべてのタブは、`Mscrm.Form.account` で始まる ID 値を持ちます。  

<a name="BKMK_BasicHomeTab"></a>   
## <a name="basic-home-tab"></a>基本ホーム タブ  
 基本ホーム タブは、特定のページにタブを表示しないエンティティ コンテキストまたは表示規則によって代替タブが定義されていない場合、常にメインのアプリケーション リボンに表示されます。 たとえば、MDA **ヘルプ**を表示すると、このタブが表示されます。 基本ホーム タブの ID は、`Mscrm.BasicHomeTab` です。  

<!-- [!NOTE]-->
<!-- >  The Jewel that was shown in [!INCLUDE[pn_crm2011_and_online](../../includes/pn-crm2011-and-online.md)] is no longer displayed. Changes to the Jewel will not appear in [!INCLUDE[pn_dynamics_crm_online](../../includes/pn-dynamics-crm-online.md)]  -->

<!--<a name="outlook_ribbons"></a>   
## [!INCLUDE[pn_dynamics_crm](../../includes/pn-dynamics-crm.md)] for Microsoft Office Outlook ribbons  
 [!INCLUDE[pn_MS_Outlook_Full](../../includes/pn-ms-outlook-full.md)] 2007 do not display a ribbon. [!INCLUDE[ribbon_enum_Version_2010](../../includes/ribbon-enum-version-2010.md)] uses the ribbon. You can use [!INCLUDE[pn_dynamics_crm](../../includes/pn-dynamics-crm.md)] ribbon definitions to add controls to all of them.  -->

<!--### Microsoft Office Outlook 2007  
 The [!INCLUDE[pn_crm_for_outlook_full](../../includes/pn-crm-for-outlook-full.md)] controls to support older versions of [!INCLUDE[pn_MS_Outlook_Full](../../includes/pn-ms-outlook-full.md)] toolbars and menus are defined as tabs with the Id values of `Mscrm.LegacyOfficeToolbar` and `Mscrm.LegacyOfficeMenubar`, respectively.  -->

<!--### Microsoft Office Outlook 2010  
 The [!INCLUDE[pn_crm_for_outlook_full](../../includes/pn-crm-for-outlook-full.md)] controls to support [!INCLUDE[ribbon_enum_Version_2010](../../includes/ribbon-enum-version-2010.md)] toolbars and menus are defined as tabs with the Id values of `Mscrm.Outlook14GlobalToolbar` and `Mscrm.Outlook14GlobalMenubar`, respectively.  -->

<a name="other_ribbons"></a> ## 他のリボン: 特別な目的のリボン タブが複数と状況依存グループが 1 つ、MDA によって定義されています。
各タブは、いつ表示されるかを制御する固有の `<TabDisplayRule>` と関連付けられています。 使用できるタブを次の表に示します。  


|                 タブ                  |             ルート ID              |                                                              説明                                                              |
|--------------------------------------|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|     Web リソース編集ページ タブ      |    `Mscrm.WebResourceEditTab`    |                                        ソリューション内で Web リソースを編集するときに表示されます。                                         |
|           フォーム エディター タブ            |      `Mscrm.FormEditorTab`       |                               エンティティ フォームに [保存]、[編集]、[選択]、および [表示] 操作グループを提供します。                               |
|        フォーム エディター挿入タブ        |   `Mscrm.FormEditorInsertTab`    |                               エンティティ フォームにセクション、タブ、コントロールを挿入するためのボタンを提供します。                                |
|        ダッシュボード ホームページ タブ        |       `Mscrm.DashboardTab`       |                                                    [ワークプレース] 領域に表示されます。                                                    |
| ビジュアル化ツール状況依存グループ |    `Mscrm.VisualizationTools`    |             エンティティ グリッド リボンに表示される**グラフ**タブの**新規グラフ**ボタンをクリックすると表示されます。              |
|       AptbookTab ホームページ タブ        |        `Mscrm.AptbookTab`        |                                    [サービス] 領域にサービス カレンダーを表示すると表示されます。                                    |
|          高度な検索タブ           |       `Mscrm.AdvancedFind`       |                                               **高度な検索**ウィンドウに表示されます。                                               |
|         ダッシュボード エディター タブ         |    `Mscrm.DashboardEditorTab`    |                                                  ダッシュボードを編集するときに表示されます。                                                   |
|            ドキュメント タブ             |       `Mscrm.DocumentsTab`       | 組織に対して SharePoint 統合が有効になっている場合、表示されます。 |
|           グラフ エディター タブ           | `Mscrm.VisualizationDesignerTab` |                                       ソリューション ウィンドウからグラフを編集するときに表示されます。                                        |
|    検索ツール状況依存グループ     |      `Mscrm.ArticleSearch`       |                                             `KBarticle` エンティティを表示すると表示されます。                                             |

<a name="BKMK_RibbonsForCustomPages"></a>

## <a name="ribbons-for-custom-pages"></a>カスタム ページのリボン

サイトマップを使用して、アプリケーション ナビゲーション内にカスタム ページを表示できます。 これらのページには、常に[基本ホーム タブ](ribbons-available.md#BKMK_BasicHomeTab) (`Mscrm.BasicHomeTab`) が表示されます。 

`<PageRule>` を使用して、カスタム ページ上のカスタム リボン コンポーネントを有効化または表示することはできません。  

### <a name="see-also"></a>関連項目  
 [リボンのカスタマイズ](customize-commands-ribbon.md)   
 [バーまたはリボンの表示](command-bar-ribbon-presentation.md)
