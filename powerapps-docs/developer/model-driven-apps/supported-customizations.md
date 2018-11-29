---
title: コードを使用してモデル駆動型アプリケーションのカスタマイズを開始する | Microsoft Docs
description: 'PowerApps ポータルにあるツールまたは公式ドキュメントで説明されているツールを使用して、モデル駆動型アプリをカスタマイズできます。 '
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="get-started-with-model-driven-apps-customization-using-code"></a>コードを使用してモデル駆動型アプリケーションのカスタマイズを開始する

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/supported-extensions
Split to just include MDA issues
 -->

PowerApps ポータルにあるツールまたは公式ドキュメントで説明されているツールを使用して、モデル駆動型アプリをカスタマイズできます。 これらのカスタマイズはサポートされており、アップグレードが可能です。

ここに記述されている以外の方法を使用して行われたカスタマイズについてはサポートされず、更新時やモデル駆動型アプリへのアップグレード時に問題が生じる場合があります。 詳細については、このトピックの後方にある[サポートされていないカスタマイズ](#unsupported-customizations)を参照してください。

このサイトなどの Microsoft サイトに公開されている技術資料に記載のトピックは、サポートされていますがアップグレードされない可能性があります。


## <a name="customizations-using-powerapps-portal"></a>PowerApps ポータルを使用したカスタマイズ

モデル駆動型アプリには、カスタマイズに使用できるさまざまなツールが用意されています。 モデル駆動型アプリのツールおよび Web アプリケーションを使用したカスタマイズは完全にサポートされており、すべてアップグレード可能です。

次のカスタマイズ方法を使用すると、完全にサポートされるカスタマイズを実行できます。

- PowerApps ポータルまたはソリューション エクスプローラーのカスタマイズ。 詳細については、[モデル駆動型アプリの作成の概要](../../maker/model-driven-apps/model-driven-app-overview.md)を参照してください

- Web アプリケーションの設定。 詳細については、[モデル駆動型アプリの管理](/dynamics365/customer-engagement/admin/admin-guide)を参照してください。

- Reporting Services。 詳細については、[モデル駆動型アプリのレポートと分析ガイド](/dynamics365/customer-engagement/analytics/reporting-analytics-with-dynamics-365)を参照してください。

> [!NOTE]
> モデル駆動型アプリの動作は、関連する Common Data Service for Apps に適用されるカスタマイズによって異なります。 詳細: [Common Data Service for Apps のサポートされているカスタマイズ](../common-data-service/supported-customizations.md)
> *完全なサポート*とは、開発者サポートによってカスタマイズをサポートできること、およびアプリケーション サポートによってそれらの変更を行う顧客を支援できることを意味します。


## <a name="customizations-applied-using-code"></a>コードを使用して適用されたカスタマイズ

開発者受けのこのサイトのドキュメント、技術記事、このサイトのサンプル コードと、CDS for Apps 開発者サポート チームによってリリースされる情報は、コードを使用して適用されるカスタマイズの領域に含まれます。 具体的な操作とそのサポートおよびアップグレードのレベルは後ほどこのトピックで説明します。

### <a name="client-side-javascript"></a>クライアント側 JavaScript

以下の 3 つの領域のモデル駆動型アプリ内で JavaScript を使用できます。

- **フォーム スクリプト イベント ハンドラー**: フォーム イベント ハンドラーが JavaScript Web リソースで定義された関数を呼び出すように構成できます。

- **コマンドバー (リボン) コマンド**: JavaScript Web リソース内に定義された関数を呼び出すアクションを定義するために、`<CustomRule>` または `<JavaScriptFunction>` 要素を使用できます。

- **Web リソースと IFRAME**: HTML Web リソース内で JavaScript Web リソースを使用できます。 クロスサイト スクリプトまたはフォームに含まれる HTML Web リソース内のスクリプトを許可するように構成されたIFRAMEは、親参照を介してフォーム内でドキュメント化された`Xrm.Page`または`Xrm.Utility` メソッド対話することがあります。

アプリケーション ページとのすべての対話は、[モデル駆動型アプリのクライアント API 参照](clientapi/reference.md)に記載されているメソッドを使用したメソッドを通じてのみ実行する必要があります。  モデル駆動型アプリ ページのドキュメント オブジェクト モデル(DOM )に直接アクセスすることは、サポートされていません。 フォーム スクリプトおよびコマンドで jQuery を使用することはお勧めしません。 詳細: [JavaScript を使用したモデル駆動型アプリでのクライアント スクリプト作成](client-scripting.md)。

[URL を使用してフォーム、ビュー、ダイアログおよびレポートを開く](open-forms-views-dialogs-reports-url.md)に記載されている方法を使用して、モデル駆動型アプリ フォーム、ビュー、ダイアログ、およびレポートを開くことができます。

### <a name="ribbon-customization"></a>リボンのカスタマイズ

リボン要素の追加、削除、および非表示を行う `RibbonDiffXml` がサポートされています。 モデル駆動型アプリで定義されているリボン コマンドの再利用はサポートされますが、使用可能なコマンドは将来的に変更または削除される可能性があります。 リボン コマンドで定義された JavaScript 関数の再利用はサポートされていません。

## <a name="unsupported-customizations"></a>サポートされていないカスタマイズ

このドキュメントで説明されたメソッドまたは PowerApps ポータルのいずれのツールも使用しないで実行されたモデル駆動型アプリの変更はサポートされず、モデル駆動型アプリの更新時またはアップグレード時に保存されません。 このドキュメントおよびサポート ドキュメントに文書化されていないものはすべてサポートされません。 また、サポートされていない変更を加えると、修正プログラムや Service Pack によって更新する際、またはモデル駆動型アプリをアップグレードする際に問題が生じる可能性があります。

次は、よく質問されるサポートされていない操作の種類の一覧です: 

- モデル駆動型アプリケーション JavaScript コードの再利用。 このコードはアップグレード時に変更または上書きされる場合があります。
- ソリューション ファイルの編集による、リボン、フォーム、サイトマップ、または保存されたクエリ以外のソリューション コンポーネントの編集はサポートされていません。 詳細については、[カスタマイズを編集するタイミング](when-edit-customization-file.md)を参照してください。
    - ソリューション ファイルの定義による新しいソリューション コンポーネントの定義はサポートされていません。 
    - ソリューションと共にエクスポートされた Web リソース ファイルの編集はサポートされていません。 
    - [管理ソリューションの保守](../common-data-service/maintain-managed-solutions.md)に記載されている手順を除いて、マネージド ソリューションの内容の編集はサポートされていません。

- 別のエンティティ フォームに埋め込まれた IFrame 内のエンティティ フォームの表示はサポートされていません。

### <a name="see-also"></a>関連項目

[Common Data Service for Apps のサポートされているカスタマイズ](../common-data-service/supported-customizations.md)<br/>
[JavaScript を使用するモデル駆動型アプリでクライアント スクリプトを使用してビジネス ロジックを適用](client-scripting.md)<br/>
[コマンド、およびリボンをカスタマイズする](customize-commands-ribbon.md)<br/>
[モデル駆動型アプリの Web リソース](web-resources.md)
