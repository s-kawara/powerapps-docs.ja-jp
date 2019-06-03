---
title: 'PDF ビューアー コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含む PDF ビューアー コントロールに関する情報
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/25/2016
ms.author: fikaradz
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 66813cf8c31fad82eeb25fd515acad4a5ea1f756
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61548802"
---
# <a name="pdf-viewer-control-experimental-in-powerapps"></a>PowerApps の PDF ビューアー コントロール (試験段階)
PDF ファイルの内容を表示する試験段階のコントロールです。

## <a name="description"></a>説明
PDF ファイルのテキスト、グラフィック、他の内容を表示するには、この種類のコントロールを追加し、その **Document** プロパティに、表示するファイルの URL を二重引用符で囲んで設定します。

## <a name="limitations"></a>制限事項
1. PowerApps のセキュリティ アーキテクチャには、HTTP ではなく HTTPS リンクのみをサポートする PDF ビューアーが必要です。  

2. **ドキュメント**プロパティは、PDF ファイルに直接リンクする必要があります。 サーバーのリダイレクトまたは文書の HTML ビューはサポートされていません。

3. ドキュメントをホストするサーバー認証を必要とする必要があります。

4. 制限の厳しいクロス オリジン リソース共有 (CORS) の設定をあるサーバーでドキュメントが存在する場合は、アプリで PDF ドキュメントを表示することはできません。 この問題を解決するには、PDF ドキュメントをホストするサーバーが powerapps.com からのクロス オリジン要求を許可する必要があります。

アプリ ユーザーは、コントロールがドキュメントを開くことができない場合の指示に従って外部のブラウザーで PDF ドキュメントを開くと、これらの制限を回避作業できます。 このオプションはすべての外部ドキュメントのコントロール メニューでも使用できます。

アプリの作成者は、アプリでメディア リソースとしての PDF ドキュメントを含めることによってこれらの制限を回避することができます。 これにより、PDF ビューアー コントロールでは、ドキュメントを表示するにします。

## <a name="key-properties"></a>主要なプロパティ
**Document** – 二重引用符で囲んだ、PDF ファイルの URL です。

## <a name="additional-properties"></a>その他のプロパティ
**ActualZoom** – コントロールの実際の拡大率です。**Zoom** プロパティで要求された拡大率と異なる場合があります。

**[BorderColor](properties-color-border.md)** – コントロールの境界線の色です。

**[BorderStyle](properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。

**[BorderThickness](properties-color-border.md)** – コントロールの境界線の太さです。

**CurrentFindText** – 使用されている現在の検索語です。

**CurrentPage** – 実際に表示されている PDF ファイルのページ番号です。

**[DisplayMode](properties-core.md)** – コントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**[DisabledBorderColor](properties-color-border.md)** – コントロールの **[DisplayMode](properties-core.md)** プロパティが **Disabled** に設定されている場合のコントロールの境界線の色です。

**[Fill](properties-color-border.md)** – コントロールの背景色です。

**FindNext** – ドキュメントで **FindText** の次のインスタンスを検索します。

**FindPrevious** – ドキュメントで **FindText** の前のインスタンスを検索します。

**FindText** – ドキュメント内で検索する検索語です。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**[HoverBorderColor](properties-color-border.md)** – コントロール上にユーザーがマウス ポインターを重ねているときのコントロールの境界線の色です。

**[OnSelect](properties-core.md)** – ユーザーがコントロールをタップまたはクリックした場合のアプリの反応を指定します。

**OnStateChange** – コントロールの状態が変化したときのアプリの反応を指定します。

**[PaddingBottom](properties-size-location.md)** – コントロール内のテキストとそのコントロールの下端間の距離です。

**[PaddingLeft](properties-size-location.md)** – コントロール内のテキストとそのコントロールの左端間の距離です。

**[PaddingRight](properties-size-location.md)** – コントロール内のテキストとそのコントロールの右端間の距離です。

**[PaddingTop](properties-size-location.md)** – コントロール内のテキストとそのコントロールの上端間の距離です。

**Page** – 表示するページ番号です。

**PageCount** – ドキュメントのページ数です。

**[PressedBorderColor](properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロールの境界線の色です。

**ShowControls** – オーディオ プレイヤーまたはビデオ プレイヤーに再生ボタンと音量スライダーなどを表示するかどうか、およびペン コントロールに描画、削除、クリアなどのアイコンを表示するかどうかを指定します。

**[Tooltip](properties-core.md)** – ユーザーがポインターをコントロールに合わせたときに表示される説明テキストです。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

**Zoom** – カメラからの画像、または PDF ビューアーでのファイルの表示を拡大する割合です。

## <a name="example"></a>例

**PDF ビューアー** コントロールを追加し、その **Document** プロパティを、この例のように二重引用符で囲んだ PDF の URL に設定します。

  **"https://blog.mozilla.org/security/files/2015/05/HTTPS-FAQ.pdf"**

    The control shows the PDF file.

    Don't know how to [add and configure a control](../add-configure-controls.md)?

## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン

**PDF ビューアー**はまだ実験段階にあるため、PDF ドキュメントのすべてのアクセシビリティ機能がサポートされているわけではありません。 そのため、ユーザーが外部アプリケーションでドキュメントを開くことができるように、**ShowControls** を **true**に設定する必要があります。

[WCAG 2.0](https://www.w3.org/TR/WCAG-TECHS/pdf.html) および [PDF/UA](https://www.pdfa.org/pdfua-the-iso-standard-for-universal-accessibility/) 標準を使用してアクセシビリティ対応の PDF ドキュメントを作成する方法を学びます。

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
* PDF ドキュメントにタイトルがない場合は、 **[ラベル](control-text-box.md)** を使用して見出しを追加することを検討してください。 見出しは **PDF ビューアー**の直前に配置することができます。
