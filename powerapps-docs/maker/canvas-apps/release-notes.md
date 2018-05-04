---
title: PowerApps の新機能 | Microsoft Docs
description: PowerApps の更新内容 (リリースの日付順)
documentationcenter: na
author: skjerland
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 04/23/2018
ms.author: sharik
ms.openlocfilehash: 00b80bd5b9e0953366dd58d6e3b3266ffe7956bd
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="whats-new-in-powerapps"></a>PowerApps の新機能
既知の制限については、「[Common issues and resolutions (お問い合わせの多い問題と解決方法)](common-issues-and-resolutions.md)」を参照してください。


> [!NOTE]
> リリースは、数日間にわたってロールアウトします。 新機能や更新された機能は、すぐには表示されない場合があります。

## <a name="announcing-the-business-applications-spring-18-release-notes"></a>ビジネス アプリケーション 18 年春のリリース ノートのお知らせ

Microsoft のビジネス アプリケーションの最新情報や、プラットフォームに独自のアプリケーションと拡張機能を構築するための新しい機能のホストについて説明します。 Dynamics 365、PowerApps、Microsoft Flow、Power BI について説明した [18 年春のリリース ノートの PDF をダウンロード](https://aka.ms/businessappsreleasenotes)してください。

**近日公開予定:** 機能の出荷に応じてリリース ノートの PDF は常に更新しており、同じものを Web ページでも公開しています。

## <a name="apr-23"></a>4 月 23 日
* Internet Explorer の SharePoint カスタム リスト フォーム内で[添付ファイル](controls/control-attachments.md)をダウンロードします。

## <a name="apr-9"></a>4 月 9 日
* 切り取り (Ctrl + X)、コピー (Ctrl + C)、および貼り付け (CTRL + V) のコントロール&mdash;コントロールのスタイル、書式、プロパティを含む&mdash;が、Web ブラウザーのアプリ全体に適用されます。

## <a name="mar-21"></a>3 月 21 日
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

## <a name="mar-5"></a>3 月 5 日
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

## <a name="dec-8"></a>12 月 8 日
1. ルール用の[条件テンプレート](working-with-rules.md)により、コントロール共通のプロパティを推定します (**テキスト**または**値**など)。
2. ルールのアクションを定義する際の、[**アクションの定義**の確認ダイアログ ボックス](working-with-rules.md)が表示されないようにしました。

## <a name="nov-13"></a>11 月 13 日
1. SharePoint リストで、同じフィールドに複数の値を選択できます。
2. SharePoint リストで、[添付ファイルの表示とダウンロード](controls/control-attachments.md)を行うことができます。
3. PowerApps を使用して [SharePoint リスト フォームをカスタマイズ](customize-list-form.md)できます。

## <a name="nov-10"></a>11 月 10 日
* アプリの[ルール名を変更](working-with-rules.md)し、選択したコントロールがルールの条件にある場合に、ルールを表示します。
