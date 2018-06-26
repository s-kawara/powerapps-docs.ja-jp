---
title: 'リッチ テキスト エディター コントロール: リファレンス | Microsoft Docs'
description: プロパティとサンプルを含むリッチ テキスト エディター コントロールに関する情報
services: ''
suite: powerapps
documentationcenter: na
author: fikaradz
manager: anneta
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2018
ms.author: fikaradz
ms.openlocfilehash: 36fa317a4611c72ab4d2f6ce09e176b14b688a55
ms.sourcegitcommit: 91a102426f1bc37504142cc756884f3670da5110
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2018
ms.locfileid: "34585091"
---
# <a name="rich-text-editor-control-experimental-in-powerapps"></a>PowerApps のリッチ テキスト エディター コントロール (試験段階)
エンド ユーザーが WYSIWYG 編集領域内でテキストを書式設定できるようにする試験段階のコントロール。  出力形式は、HTML です。

## <a name="description"></a>説明
**リッチ テキスト エディター** コントロールにより、アプリのユーザーにテキストの書式設定のための WYSIWYG 編集領域が提供されます。  コントロールの入出力形式は HTML です。

コントロールにより、(Web ブラウザーまたは Word から) コピーしたリッチ テキストを コントロールに貼り付けることができます。  

コントロールの目的はテキストの書式設定であるため、入力 HTML の整合性の保持は保証されません。  すべてのスクリプト、スタイル、オブジェクト、その他の影響を受ける可能性のあるタグがエディターによって削除されます。  これは、リッチ テキストが PowerApps の外部で作成された場合、元々作成された製品と同じように表示されない可能性があることを意味します。

現在サポートされている機能は次のとおりです。
- 太字、斜体、下線
- テキストの色、色の強調表示
- テキスト サイズ
- 番号付きリスト、箇条書きリスト
- ハイパーリンク
- 書式のクリア

フォーム内のコントロールを使用するには、"複数行テキストの編集" カードを選択し、RTE コントロールを挿入してカスタマイズします。

## <a name="limitations"></a>制限
現在のバージョンのコントロールは以下の一時的な制限があるため、試験段階です。
- コントロールのテキストの書式設定の機能が制限されている。  

- コントロールが主に、大画面のブラウザーでの使用を目的としている。  携帯電話でこのコントロールを使用すると、操作性に不備がある場合があります。

- Windows Studio または Edge ブラウザーを使用した場合、作成機能に既知の問題がある。  現在、Chrome で WebStudio を使用することを推奨しています。


## <a name="key-properties"></a>主要なプロパティ
**[Default](properties-core.md)** – エディターに表示される最初のテキスト値の入力プロパティ。

**HtmlText** – HTML 形式で作成されたリッチ テキストの出力プロパティ。



## <a name="additional-properties"></a>その他のプロパティ
**[AccessibleLabel](properties-accessibility.md)** – スクリーン リーダー用のラベルです。 添付ファイルの目的を説明する必要があります。

**[DisplayMode](properties-core.md)** – コントロールで、ファイルの追加と削除を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**[TabIndex](properties-accessibility.md)** – 他のコントロールに関連するキーボード ナビゲーションの順序です。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかです。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。
