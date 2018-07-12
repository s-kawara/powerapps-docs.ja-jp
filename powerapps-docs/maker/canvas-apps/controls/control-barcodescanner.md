---
title: 'バーコード スキャナー コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含むバーコード スキャナー コントロールに関する情報
author: fikaradz
ms.service: powerapps
ms.topic: reference
ms.component: canvas
ms.date: 10/25/2016
ms.author: fikaradz
ms.openlocfilehash: b8b25f5bfa3ddbce7b1c541afb7a935a2fe4aa36
ms.sourcegitcommit: 79b8842fb0f766a0476dae9a537a342c8d81d3b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2018
ms.locfileid: "37898170"
---
# <a name="barcode-scanner-control-experimental-in-powerapps"></a>PowerApps のバーコード スキャナー コントロール (試験段階)
デバイスのバーコード スキャナーを使って写真を撮影できる試験段階のコントロールです。

## <a name="description"></a>説明
このコントロールを追加した場合、ユーザーは、アプリを実行している任意の場所から 1 枚以上の写真でデータ ソースを更新できます。

## <a name="key-properties"></a>主要なプロパティ
**barcode scanner** – 複数のバーコード スキャナーを備えるデバイスで、アプリが使うバーコード スキャナーの数値 ID です。

## <a name="additional-properties"></a>その他のプロパティ
**[AccessibleLabel](properties-accessibility.md)** – スクリーン リーダー用のラベルです。

**[BorderColor](properties-color-border.md)** – コントロールの境界線の色です。

**[BorderStyle](properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。

**[BorderThickness](properties-color-border.md)** – コントロールの境界線の太さです。

**[DisplayMode](properties-core.md)** – コントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**ShowLiveBarcodeDetection** – バーコード検出の状態を示す視覚的な手がかりが表示されるかどうかを示します。 黄色の四角形は、検査されている領域を表します。 四角形内の緑色の線は、バーコードの識別に成功したことを示します。

**Stream** – **StreamRate** プロパティに基づいて自動的に更新された画像です。

**StreamRate** – **Stream** プロパティの画像を更新する頻度です (ミリ秒単位)。  この値の範囲は、100 (0.1 秒) から 3,600,000 (1 時間) です。

**Text** – スキャナーによって最後に識別されたバーコードの値。

**[Tooltip](properties-core.md)** – ポインターをコントロールに合わせたときに表示される説明テキストです。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

## <a name="related-functions"></a>関連する関数
[**Patch**( *DataSource*, *BaseRecord*, *ChangeRecord* )](../functions/function-patch.md)

## <a name="example"></a>例
### <a name="add-photos-to-an-image-gallery-control"></a>イメージ ギャラリー コントロールに写真を追加する
1. **バーコード スキャナー** コントロールを追加し、名前を **Mybarcode scanner** に設定します

    [コントロールの追加、命名、構成についてはこちらをご覧ください](../add-configure-controls.md)。
2. **ラベル** コントロールを追加し、その出力をバーコードの **Text** に設定します。  
3. BarcodeType プロパティで設定されている種類のバーコードをスキャンします。
4. スキャンされたバーコードがラベルに表示されます。


## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン
### <a name="video-alternatives"></a>ビデオの代替手段
* **[Text](properties-core.md)** をバーコード スキャナーの **Text** に設定した**[ラベル](control-text-box.md)** を追加することを検討してください。 バーコード スキャナーは識別されたバーコード値を表示しないので、上記のようにすると、視覚障碍を持つユーザーだけでなく、誰でもスキャナーにアクセスできるようになります。

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
* **[AccessibleLabel](properties-accessibility.md)** が存在する必要があります。

    > [!NOTE]
  > 新しいバーコードが検出されると、スクリーン リーダーから通知されます。 値は通知されません。 バーコードが表示されている限り、スクリーン リーダーから同じバーコードがまだ識別中であることが 5 秒ごとに通知されます。
