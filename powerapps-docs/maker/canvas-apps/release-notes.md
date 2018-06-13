---
title: 新機能 | Microsoft Docs
description: PowerApps の更新内容 (リリースの日付順)
documentationcenter: na
author: AFTOwen
ms.service: powerapps
ms.topic: conceptual
ms.component: canvas
ms.date: 05/21/2018
ms.author: anneta
ms.openlocfilehash: ef4360dda5d4003ff91389af78958052bbb1e052
ms.sourcegitcommit: 68e2c696397f3002dd14e72a4c2054a603a5e2d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2018
ms.locfileid: "34851709"
---
# <a name="whats-new-in-powerapps"></a>PowerApps の新機能
> [!IMPORTANT]
> **リリース ノートのお知らせ**<br>
> PowerApps の今後リリースされる機能と最近リリースされた機能については、<br>
[リリース ノートを参照してください](https://docs.microsoft.com/en-us/business-applications-release-notes/april18/powerapps/overview)。 計画に利用できるあらゆる詳細情報を網羅しています。

既知の制限については、「[Common issues and resolutions (お問い合わせの多い問題と解決方法)](common-issues-and-resolutions.md)」を参照してください。

> [!NOTE]
> リリースは、数日間にわたってロールアウトします。 新機能や更新された機能は、すぐには表示されない場合があります。

## <a name="may-30"></a>5 月 30 日
1. [リッチテキスト エディター コントロール](controls/control-richtexteditor.md) (実験的機能) - エンド ユーザーが WYSIWYG 編集領域内でテキストの書式を設定できます。 

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
    - **追加のデータ型**は、より複雑なエンティティ定義をサポートし、豊富なエクスペリエンスを提供します  (キャンバスとモデル駆動型アプリに適用されます)。
    - PowerApps サイトから直接 CDS for Apps で[エンティティを作成してカスタマイズ](../common-data-service/data-platform-create-entity.md)します。 **更新されたエクスペリエンス**には、パフォーマンスの向上、ユーザーにわかりやすい UI、オプション セットのインライン作成のような便利な機能が含まれます  (キャンバスとモデル駆動型アプリに適用されます)。
    - CDS for Apps に入力されたデータを検証するための**サーバー側ビジネス ルール**を作成します  (キャンバスとモデル駆動型アプリに適用されます)。
    - PowerApps サイトから直接 CDS for Apps で**計算フィールドとロールアップ フィールド**を作成します  (キャンバスとモデル駆動型アプリに適用されます)。  
    - 開発者は、CDS for Apps の**ソフトウェア開発キット** (SDK) を使って、CDS for Apps のコードに基づくカスタマイズを作成します。
    - 上級ユーザーは、新しい **OData Web API** を使って CDS for Apps に格納されているデータにアクセスできます。
    - **Power Query** を使って CDS for Apps に[データをインポートします](../common-data-service/data-platform-cds-newentity-pq.md)。 Web で Power Query を使って、複数のソースから CDS for Apps にデータを直接インポートします

## <a name="march-5"></a>3 月 5 日
1. [添付ファイル](controls/control-attachments.md) が SharePoint リストとの間で追加 (および削除) されます。
2. 外部の [PDF](controls/control-pdf-viewer.md) ファイルが Web ブラウザーで開きます。 (実験的な機能)

## <a name="feb-12"></a>2 月 12 日
* 埋め込まれた[ビデオ](controls/control-audio-video.md)および[オーディオ](controls/control-audio-video.md)の再生用ボリューム コントロールがインラインになりました。 再生をミュートにするには、ユーザーはボタンをクリックまたはタップする代わりに、ボリューム コントロールを使用してボリュームを下げる必要があります。

## <a name="feb-7"></a>2 月 7 日
1. [カメラ](controls/control-camera.md)および[バーコード スキャナー](controls/control-barcodescanner.md)のコントロールから、ズーム、明るさおよびコントラストのプロパティを削除しました。
2. [テキスト入力](controls/control-text-input.md)コントロールのクリア ボタンがユーザー入力に割り当てられた領域を制限する問題を解決しました。 この修正によって、テキスト入力コントロールの[クリア](controls/control-text-input.md#additional-properties) プロパティは、Microsoft Edge (最新バージョン) および Internet Explorer 11 Web ブラウザーでのみサポートされます。
3. アクセシビリティの機能強化が[マルチメディア](add-images-pictures-audio-video.md) コントロールに追加されました。

## <a name="jan-31"></a>1 月 31 日
1. [ビデオ](controls/control-audio-video.md)コントロールにクローズド キャプションが追加されました。
2. [PDF ビューアー](controls/control-pdf-viewer.md)コントロールのエラー処理が向上しました。

## <a name="jan-18"></a>1 月 18 日
1. PowerApps for iOS と PowerApps for Android での Microsoft Authenticator との統合がサポートされました。
2. フォームの [SharePoint lookup コントロール](sharepoint-lookup-fields.md)が[コンボ ボックス](controls/control-combo-box.md)に置き換えられ、PowerApps Studio の単一選択 lookup フィールドに、新しい[データ カード](working-with-cards.md) テンプレートが既定で選択されます。
3. 拡張された読み取りモードを使用すると、[コンボ ボックス](controls/control-combo-box.md)内の候補リストにすべての項目が表示されます。
4. [委任不可のクエリ](delegation-overview.md#non-delegable-limits)におけるローカル レコードの保存上限サイズを、最大 2000 レコードまでに制御できます。 (実験的な機能)

## <a name="jan-5"></a>1 月 5 日
* Power BI レポートからコンテキスト データを取得する [PowerApps カスタム ビジュアル (プレビュー リリース)](https://powerapps.microsoft.com/blog/powerbi-powerapps-visual/) を統合したことで、Power BI レポートやダッシュボードのデータに基づいて行動できます。
