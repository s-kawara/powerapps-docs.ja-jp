---
title: 'Attachments コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含む Attachments コントロールに関する情報
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
ms.date: 09/29/2017
ms.author: fikaradz
ms.openlocfilehash: 6b46cfd778dcb29553dce252988b8b6a049ba12d
ms.sourcegitcommit: d7ed5144f96d1ecc17084c30ed0e2ba3c6b03c26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2018
---
# <a name="attachments-control-in-powerapps"></a>PowerApps の Attachments コントロール
ユーザーが自分のデバイスへのファイルのダウンロードや、SharePoint リストからのファイルのアップロードや削除ができるようになるコントロール。

## <a name="limitations"></a>制限
Attachments コントロールには次の一時的な制限があります。
1. 添付ファイルのダウンロードは、Internet Explorer ではサポートされていません。

1. 添付ファイルのアップロードは、SharePoint リストのデータ ソースでのみ機能します。  他のデータ ソースのサポートは、CDS から徐々に導入されます。

1. アップロードと削除の機能は、フォームの内部でのみ機能します。  Attachments コントロールは、編集モードでフォーム内にない場合、無効と表示されます。   ファイルの追加と削除をバックエンドに保存するには、エンド ユーザーがフォームを保存する必要があります。

1. アップロードできるファイルのサイズは最大で 10 MB です。  

1. 現在、iOS デバイスはドキュメントまたはクラウド ストレージ アカウントからファイルをアップロードすることだけができます。 写真/動画を添付するには、iOS デバイス上の Web ブラウザーを使用してアプリを実行してください。

## <a name="description"></a>説明
**Attachments** コントロールにより、データ ソースに保存されたファイルを開いたり、SharePoint リストの間でファイルを追加したり削除したりできるようになります。

## <a name="key-properties"></a>主要なプロパティ
**[Items](properties-core.md)** – ダウンロードできるファイルを記述するソースです。

**MaxAttachments** - コントロールが受け入れるファイルの最大数です。

**MaxAttachmentSize** – 新しい添付ファイルごとに許容される最大ファイル サイズ (MB) です。  現在、10 MB の制限があります。

**OnAttach** – ユーザーが新しい添付ファイルを追加したときのアプリの応答です。

**OnRemove** – ユーザーが既存の添付ファイルを削除したときのアプリの応答です。

**[OnSelect](properties-core.md)** – ユーザーが添付ファイルをクリックしたときのアプリの応答です。

## <a name="additional-properties"></a>その他のプロパティ
**[AccessibleLabel](properties-accessibility.md)** – スクリーン リーダー用のラベルです。 添付ファイルの目的を説明する必要があります。

**AddAttachmentText** – 新しい添付ファイルを追加するために使用するリンクのラベル テキストです。

**[BorderColor](properties-color-border.md)** – コントロールの境界線の色です。

**[BorderStyle](properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。

**[BorderThickness](properties-color-border.md)** – コントロールの境界線の太さです。

**[DisplayMode](properties-core.md)** – コントロールで、ファイルの追加と削除を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**[FocusedBorderColor](properties-color-border.md)** – コントロールにフォーカスがあるときのコントロールの境界線の色です。

**[FocusedBorderThickness](properties-color-border.md)** – コントロールにフォーカスがあるときのコントロールの境界線の太さです。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**MaxAttachmentsText** – コントロールに許容される最大数のファイルが含まれている場合に "ファイルの添付" リンクと置き換えられるテキストです。

**NoAttachmentsText** – 添付されているファイルが存在しないときにユーザーに表示する情報テキストです。

**[TabIndex](properties-accessibility.md)** – 他のコントロールに関連するキーボード ナビゲーションの順序です。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかです。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。


## <a name="example"></a>例
1. データ ソースとして SharePoint リストを使用してデータからアプリを作成します。  または、アプリにフォームを追加し、そのデータ ソースとして SharePoint リストを設定します。

2. 左側にあるツリー ビュー内の **Form** コントロールを選択します。

3. 右側の [オプション] パネルの [プロパティ] タブで **[データ]** をクリックします。

4. **[フィールド]** の下で、**[添付ファイル]** フィールドを有効にします。

    SharePoint リストに関連付けられている添付ファイル フィールドが、フォームに表示されます。

[コントロールを追加して構成する方法について学習してください。](../add-configure-controls.md)


## <a name="accessibility-guidelines"></a>アクセシビリティ ガイドライン
### <a name="color-contrast"></a>色のコントラスト
以下の間には適切な色のコントラストが必要です。
* **ItemColor** と **ItemFill**
* **ItemHoverColor** と **ItemHoverFill**
* **ItemPressedColor** と **ItemPressedFill**
* **AddedItemColor** と **AddedItemFill**
* **RemovedItemColor** と **RemovedItemFill**
* **ItemErrorColor** と **ItemErrorFill**
* **AddAttachmentColor** と **Fill**
* **MaxAttachmentsColor** と **Fill**
* **NoAttachmentsColor** と **Fill**

これは、標準の色のコントラスト要件に追加されるものです。

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
次のプロパティが存在する必要があります。
* **[AccessibleLabel](properties-accessibility.md)**
* **AddAttachmentsText**
* **MaxAttachmentsText**
* **NoAttachmentsText**

### <a name="keyboard-support"></a>キーボードのサポート
* **[TabIndex](properties-accessibility.md)** を 0 以上にして、キーボード ユーザーがそこに移動できるようにする必要があります。
* フォーカス インジケーターは明確に表示する必要があります。 これを実現するには **[FocusedBorderColor](properties-color-border.md)** と **[FocusedBorderThickness](properties-color-border.md)** を使用します。
