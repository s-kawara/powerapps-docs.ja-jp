---
title: 新機能 | Microsoft Docs
description: PowerApps の更新内容 (リリースの日付順)
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 05/21/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 07308a4e611938436df69a0e0a77d928e8269b3c
ms.sourcegitcommit: 5c31cfdb568f9604756d77667784530b3171650a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2018
ms.locfileid: "43178874"
---
# <a name="whats-new-in-powerapps"></a>PowerApps の新機能

> [!IMPORTANT]
>
> **リリース ノートのお知らせ**
>
> PowerApps の今後リリースされる機能と最近リリースされた機能については、
>[リリース ノートを参照してください](https://docs.microsoft.com/business-applications-release-notes/april18/powerapps/overview)。 計画に利用できるあらゆる詳細情報を網羅しています。

既知の制限については、「[Common issues and resolutions (お問い合わせの多い問題と解決方法)](common-issues-and-resolutions.md)」を参照してください。

> [!NOTE]
> リリースは、数日間にわたってロールアウトします。 新機能や更新された機能は、すぐには表示されない場合があります。

## <a name="august-20"></a>8 月 20 日
* キャンバス アプリでは、[GUID 関数](functions/function-guid.md)を使用し、GUID 値を作成するか、文字列を GUID 値に変換します。

## <a name="july-30"></a>7 月 30 日

* キャンバス アプリの数式バーで自動的に[コードの書式を設定](https://powerapps.microsoft.com/en-us/blog/automatically-format-your-formula/) (ブログ) します。

## <a name="july-16"></a>7 月 16 日

1. [Common Data Service for Apps のセキュリティ](share-app.md##manage-entity-permissions)の構成が簡単になりました。
2. PowerApps Studio のキャンバス アプリ用の[ツリー ビュー](https://powerapps.microsoft.com/blog/tree-view-now-even-better-with-expand-all-collapse-all-and-more/) (ブログ) が改善されました。

## <a name="july-9"></a>7 月 9 日

1. [AppChecker](https://powerapps.microsoft.com/blog/new-app-checker-helps-you-fix-errors-and-make-accessible-apps/) でキャンバス アプリの誤りと[アクセシビリティの問題](accessibility-checker.md) (ブログ) を特定します。
2. [**Concurrent** 関数](functions/function-concurrent.md)でキャンバス アプリの起動を速くします。

## <a name="june-18"></a>6 月 18 日

* キャンバス アプリで[コントロールの選択、編集、移動、テストが簡単に](https://powerapps.microsoft.com/blog/say-goodbye-to-miss-clicks-on-the-canvas/)なりました (ブログ)。

## <a name="june-11"></a>6 月 11 日

1. [Common Data Services for Apps との間でデータをインポートまたはエクスポートし、そのデータを Excel で開きます](https://powerapps.microsoft.com/blog/cds-for-apps-excel-importexport/) (ブログ)。
1. [**Notify** 関数](functions/function-showerror.md)によって、キャンバス アプリにバナー メッセージが表示されます。

## <a name="june-4"></a>6 月 4 日

1. [SharePoint Web パーツとしてアプリを埋め込みます](https://powerapps.microsoft.com/blog/embedding-powerapps-in-office-and-beyond/) (ブログ)。
1. [タブレット キャンバス アプリのカスタム サイズを指定します](https://powerapps.microsoft.com/blog/embedding-powerapps-in-office-and-beyond/) (ブログ)。
1. キャンバス アプリで[数式にコメント](https://powerapps.microsoft.com/blog/comment-your-powerapps-code/) (ブログ) を追加します。
1. [管理者向け PowerShell コマンドレット](https://docs.microsoft.com/powerapps/administrator/powerapps-powershell)。
1. [リッチテキスト エディター コントロール](controls/control-richtexteditor.md) (実験的機能) - エンド ユーザーがキャンバス アプリの WYSIWYG 編集領域内でテキストの書式を設定できます。

## <a name="may-21"></a>5 月 21 日

1. アップグレードされた Common Data Service (CDS) for Apps 環境で使用できるようになった **Excel ファイルからのデータ取得**と**データのエクスポート**の機能を使用すると、アプリのユーザーはローカルに保存された Excel または CSV ファイルにデータをインポートしたり、データをエクスポートしたりすることができるようになりました。 
1. PowerApps 向け Excel アドインを使用して、アプリのユーザーが [Excel のエンティティを開き](../common-data-service/data-platform-excel-addin.md)、CDS for Apps 内でのデータの作成、更新、削除ができるようになりました。 
1. CDS for Apps に接続された Power BI Desktop を使用して、[Power BI レポートの作成と公開](../common-data-service/data-platform-powerbi-connector.md)ができるようになりました。

## <a name="april-23"></a>4 月 23 日

* Internet Explorer の SharePoint カスタム リスト フォーム内で[添付ファイル](controls/control-attachments.md)をダウンロードします。

## <a name="april-9"></a>4 月 9 日

* 切り取り (Ctrl + X)、コピー (Ctrl + C)、および貼り付け (CTRL + V) のコントロール&mdash;コントロールのスタイル、書式、プロパティを含む&mdash;が、Web ブラウザーのアプリ全体に適用されます。

## <a name="march-21"></a>3 月 21 日

1. [モデル駆動型アプリ](../model-driven-apps/model-driven-app-overview.md)の作成は、データ モデルから始まり、Common Data Service for Apps のコア ビジネス データとプロセスの形状を基に構築して、フォーム、ビューなどのコンポーネントをモデル化します。 モデル駆動型アプリでは、デバイス間の応答性が高い優れた UI を自動的に生成できます。
2. 環境の最新バージョンの CDS for Apps で[データベースを作成します](../../administrator/create-database.md)。
3. CDS for Apps に以下が含まれるようになりました。

    * **追加のデータ型**は、より複雑なエンティティ定義をサポートし、豊富なエクスペリエンスを提供します  (キャンバスとモデル駆動型アプリに適用されます。)\

    * PowerApps サイトから直接 CDS for Apps で[エンティティを作成してカスタマイズ](../common-data-service/data-platform-create-entity.md)します。 **更新されたエクスペリエンス**には、パフォーマンスの向上、ユーザーにわかりやすい UI、オプション セットのインライン作成のような便利な機能が含まれます  (キャンバスとモデル駆動型アプリに適用されます)。
    * CDS for Apps に入力されたデータを検証するための**サーバー側ビジネス ルール**を作成します  (キャンバスとモデル駆動型アプリに適用されます)。
    * PowerApps サイトから直接 CDS for Apps で**計算フィールドとロールアップ フィールド**を作成します  (キャンバスとモデル駆動型アプリに適用されます)。  
    * 開発者は、CDS for Apps の**ソフトウェア開発キット** (SDK) を使って、CDS for Apps のコードに基づくカスタマイズを作成します。
    * 上級ユーザーは、新しい **OData Web API** を使って CDS for Apps に格納されているデータにアクセスできます。
    * **Power Query** を使って CDS for Apps に[データをインポートします](../common-data-service/data-platform-cds-newentity-pq.md)。 Web で Power Query を使って、複数のソースから CDS for Apps にデータを直接インポートします

## <a name="march-5"></a>3 月 5 日

1. [添付ファイル](controls/control-attachments.md) が SharePoint リストとの間で追加 (および削除) されます。
2. 外部の [PDF](controls/control-pdf-viewer.md) ファイルが Web ブラウザーで開きます。 (実験的な機能)
