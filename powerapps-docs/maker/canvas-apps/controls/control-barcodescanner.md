---
title: 'Web バーコード スキャナー コントロール: リファレンス |Microsoft Docs'
description: プロパティや例については、バーコード スキャナー コントロールに関するなどの情報
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.date: 10/25/2016
ms.author: fikaradz
ms.reviewer: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 787fa34bdfcabf6103fefd82f66e976b680544e2
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61544593"
---
# <a name="web-barcode-scanner-control-experimental-in-powerapps"></a>PowerApps で (試験段階) の web バーコード スキャナー コントロール

レガシ バーコードのスキャンをコントロールは廃止されていますが、web ブラウザーでコードをスキャンするために便利です。

## <a name="description"></a>説明

コントロールは、ユーザーがすべてのデバイスでのバーコードをスキャンするため、アプリでカメラのフィードを示しています。 コントロールが古いため、パフォーマンスの低下、およびモバイル**[バーコード スキャナー](control-new-barcode-scanner.md)** コントロールには、このコントロールが置き換えられます。

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

1. 追加、**ラベル**を制御して、その出力をバーコード スキャナーに設定**テキスト**プロパティ。

1. 設定の種類のバーコードをスキャン**BarcodeType**プロパティ。

    ラベルには、スキャンされたバーコードが表示されます。

## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン

### <a name="video-alternatives"></a>ビデオの代替手段

* **[Text](properties-core.md)** をバーコード スキャナーの **Text** に設定した **[ラベル](control-text-box.md)** を追加することを検討してください。 バーコード スキャナーは識別されたバーコード値を表示しないので、上記のようにすると、視覚障碍を持つユーザーだけでなく、誰でもスキャナーにアクセスできるようになります。

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート

* **[AccessibleLabel](properties-accessibility.md)** が存在する必要があります。

    > [!NOTE]
  > 新しいバーコードが検出されたときに、スクリーン リーダーが通知されます。 値は発表はありません。 スクリーン リーダー、バーコードがビューに表示、限りは、ユーザーが同じバーコードがまだ識別されているを 5 秒ごとに通知されます。
