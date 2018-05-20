---
title: アクセシビリティ対応の色 | Microsoft Docs
description: PowerApps の色コントラストのガイドライン
author: tahoon
ms.service: powerapps
ms.topic: article
ms.date: 04/23/2018
ms.author: tahoon
ms.openlocfilehash: 56a11edcd1c43313e9b380ca8ac1c8a68d85772d
ms.sourcegitcommit: 45fac73f04aa03b5796ae6833d777f4757e67945
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="accessible-colors-in-powerapps"></a>PowerApps でのアクセシビリティ対応の色
アプリで使用する色は、色覚や視力に障碍のあるユーザーでも認識できるものにする必要があります。 PowerApps のすべてのテーマは、既定でアクセシビリティ対応になっています。 アプリで使う色を変更するときは、この記事のガイドラインに従って、アクセシビリティを維持するようにしてください。

## <a name="minimum-contrast-for-text"></a>テキストの最低限のコントラスト
* テキストとその背景のコントラスト比を、4.5:1 以上にする必要があります
* 大きなテキストは、コントラスト比を 3:1 以上にする必要があります
* 無効になっているテキストについては、コントラストの要件はありません

実際には、すべての対話型コントロールで次のものの間が適切な色コントラストになっている必要があります。
* **[Color](controls/properties-color-border.md)** と **[Fill](controls/properties-color-border.md)**
* **[PressedColor](controls/properties-color-border.md)** と **[PressedFill](controls/properties-color-border.md)**
* **[HoverColor](controls/properties-color-border.md)** と **[HoverFill](controls/properties-color-border.md)**

## <a name="minimum-contrast-for-non-text"></a>テキスト以外の最低限のコントラスト

> [!NOTE]
> [WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) 標準では、コントラストの要件はテキストのみに適用されます。 アクセシビリティをよりよくするため、アイコン ボタンのような基本的なユーザー インターフェイス コンポーネントについては、今後の [WCAG 2.1 コントラスト ガイドライン](https://www.w3.org/TR/WCAG21/#non-text-contrast)を検討してください。 これらのコンポーネントの場合は、3:1 以上の比率にすることをお勧めします。 このセクションで説明されているガイドラインは、WCAG 2.0 へのコンプライアンスに関しては**オプション**です。

### <a name="user-interface-components"></a>ユーザー インターフェイスのコンポーネント
すべての対話型コントロールで次のものの間が適切な色コントラストになっている必要があります。
* **[FocusedBorderColor](controls/properties-color-border.md)** とコントロールの外側の色

領域全体が対話型または情報提供型であるコントロールについては、追加の色コントラスト チェックが適用されます。 たとえば、**[ボタン](controls/control-button.md)** や、ボタンとして使われている**[アイコン](controls/control-shapes-icons.md)** などです。 これにより、コントロールの境界が明確になり、ユーザーはどこをクリックまたはタップすればよいかがわかります。

そのようなコントロールの境界がある場合は、次のものの間の色コントラストを適切にする必要があります。
* **[BorderColor](controls/properties-color-border.md)** とコントロールの外側の色
* **[PressedBorderColor](controls/properties-color-border.md)** とコントロールの外側の色
* **[HoverBorderColor](controls/properties-color-border.md)** とコントロールの外側の色

境界がない場合は、次のものの間の色コントラストを適切にする必要があります。
* **[Fill](controls/properties-color-border.md)** とコントロールの外側の色
* **[PressedFill](controls/properties-color-border.md)** とコントロールの外側の色
* **[HoverFill](controls/properties-color-border.md)** とコントロールの外側の色

### <a name="graphical-objects"></a>グラフィック オブジェクト
画像が重要な情報を伝達する場合は、画像についてコントラストの問題を確認することを検討します。 これは、**[オーディオ](controls/control-audio-video.md)**、**[イメージ](controls/control-image.md)**、**[マイク](controls/control-microphone.md)**、**[ビデオ](controls/control-audio-video.md)** など、画像を表示できるコントロールに当てはまります。

ビデオ コンテンツの場合、コントラストの問題を確認することを検討します。 その代わりに、またはそれに加えて、ビデオについて説明する[クローズド キャプション](controls/control-audio-video.md)を提供します。

## <a name="provide-other-visual-cues"></a>他の視覚的な手掛かりを提供する
アプリが色だけで情報を伝達していないことを確認します。 たとえば、赤緑の色覚に障碍があるユーザーは、赤のエラー メッセージと緑の成功メッセージを区別できません。

**[アイコン](controls/control-shapes-icons.md)** または**[斜体](controls/properties-text.md)** や**[下線](controls/properties-text.md)** などのテキスト スタイルといった追加の手掛かりは、意味を伝えるのに役立ちます。

## <a name="next-steps"></a>次の手順
PowerApps のコントロールの[アクセシビリティ プロパティ](controls/properties-accessibility.md)について詳しく学習してください。