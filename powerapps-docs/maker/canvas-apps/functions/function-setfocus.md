---
title: SetFocus 関数 |Microsoft Docs
description: 構文を含む PowerApps の SetFocus 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 08/23/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: cdf34c3c4909697b70a105e5145620ab5bd31ea9
ms.sourcegitcommit: 5899d37e38ed7111d5a9d9f3561449782702a5e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71038150"
---
# <a name="setfocus-function-in-powerapps"></a>PowerApps の SetFocus 関数
入力フォーカスを特定のコントロールに移動します。 

## <a name="description"></a>説明
**SetFocus**関数は、コントロールに入力フォーカスを与えます。  ユーザーのキーストロークがそのコントロールによって受信され、テキスト入力コントロールに入力するか、 *enter*キーを使用してボタンを選択できるようになります。  ユーザーは、 *Tab*キー、タッチ、マウス、またはその他のジェスチャを使用して入力フォーカスを移動することもできます。 *Tab*キーの動作は、 [ **TabIndex**プロパティ](../controls/properties-accessibility.md)によって管理されます。

にフォーカスを設定するには、 **SetFocus**関数を使用します (それぞれの例を以下に示します)。
- 新しく公開または有効化された入力コントロール。ユーザーに次のような情報を提供し、データ入力を高速化します。
- フォームが検証され、問題のある入力コントロールに焦点を合わせて表示し、すばやく解決することができます。
- 画面が表示され、[**画面**](../controls/control-screen.md)の**onvisible**プロパティを使用して最初の入力コントロールにフォーカスが移動します。

フォーカスが設定されたコントロールは、 [**FocusedBorderColor**](../controls/properties-color-border.md)プロパティと[**FocusedBorderThickness**](../controls/properties-color-border.md)プロパティに基づいて視覚的に異なる場合があります。

## <a name="limitations"></a>制限事項

**SetFocus**は、次の場合にのみ使用できます。
- [**ボタン**](../controls/control-button.md)コントロール
- [**アイコン**](../controls/control-shapes-icons.md)コントロール
- [**イメージ**](../controls/control-image.md)コントロール
- [**ラベル**](../controls/control-text-box.md) コントロール
- [**TextInput**](../controls/control-text-input.md)コントロール

[**ギャラリー**](../controls/control-gallery.md)コントロール、[**編集フォーム**](../controls/control-form-detail.md)コントロール、または[コンポーネント](../create-component.md)内のコントロールにフォーカスを設定することはできません。  **SetFocus**は、scrollbale 画面のコントロールで使用できます。

フォーカスを設定できるのは、 **SetFocus**呼び出しを含む数式と同じ画面上のコントロールだけです。

[**DisplayMode**](../controls/properties-core.md)プロパティが**Disabled**に設定されているコントロールにフォーカスを設定しようとしても、効果はありません。  フォーカスは、以前の状態のままになります。

Apple iOS では、直接ユーザー操作によって**SetFocus**が開始された場合にのみ、ソフトキーボードが自動的に表示されます。  たとえば、ボタンの**Onselect**プロパティからを呼び出すと、ソフトキーボードが表示されますが、画面の**onselect**からの呼び出しは表示されません。 

**SetFocus**は、[動作の数式](../working-with-formulas-in-depth.md)でのみ使用できます。

## <a name="syntax"></a>構文
**SetFocus**(*コントロール*)

* *Control* – 必須。  入力フォーカスを与えるコントロール。

## <a name="examples"></a>使用例

### <a name="focus-on-a-newly-exposed-or-enabled-input-control"></a>新しく公開された、または有効になっている入力コントロールにフォーカスを設定する

多くのショッピングカートでは、顧客は請求先住所を使用して、同じ情報を2回入力する必要性を軽減することができます。  別の請求先住所が必要な場合は、請求先住所のテキスト入力ボックスが有効になります。また、これらの新しく有効になったコントロールを顧客に案内して、データ入力を高速化することもできます。  

![カスタム請求先住所の使用を選択するアニメーション。その結果、フォーカスが課金名の入力コントロールに移動され、輸送アドレスとの自動同期がオフになります。](media/function-setfocus/shipping-billing.gif)

ここでは多くの数式が再生されますが、フォーカスを移動する式は、**チェックボックス**コントロールの**onuncheck**プロパティにあります。

```powerappa-dot
SetFocus( BillingName ) 
```

*Tab*キーを使用して、あるフィールドから別のフィールドにフォーカスをすばやく移動することもできます。  わかりやすく説明するために、このアニメーションでは*Tab*キーを使用しませんでした。

この例を作成するには、次のようにします。
1. 新しいアプリを作成します。
1. "出荷先住所"、"名前:"、"アドレス:"、"請求先住所"、"名前:"、および "Address:" というテキストが付いた[**ラベル**コントロール](../controls/control-text-box.md)を追加し、アニメーションに示されているように配置します。
1. [**テキスト入力**コントロール](../controls/control-text-input.md)を追加し、その名前を**ShippingName**に変更します。
1. [**テキスト入力**コントロール](../controls/control-text-input.md)を追加し、その名前を**ShippingAddress**に変更します。
1. [**チェックボックス**コントロール](../controls/control-check-box.md)を追加し、 **syncaddresses**の名前を変更します。
1. このコントロールの**Text**プロパティを数式`"Use Shipping address as Billing address"`に設定します。
1. [**テキスト入力**コントロール](../controls/control-text-input.md)を追加し、**名前**を変更します。
1. このコントロールの**既定**のプロパティを数式`ShippingName`に設定します。
1. このコントロールの**DisplayMode**プロパティを数式`If( SyncAddresses.Value, DisplayMode.View, DisplayMode.Edit )`に設定します。  これにより、チェックボックスコントロールの状態に基づいて、このコントロールが自動的に有効または無効になります。
1. [**テキスト入力**コントロール](../controls/control-text-input.md)を追加し、その名前を「**住所**」に変更します。
1. このコントロールの**既定**のプロパティを数式`ShippingAddress`に設定します。
1. このコントロールの**DisplayMode**プロパティを数式`If( SyncAddresses.Value, DisplayMode.View, DisplayMode.Edit )`に設定します。  これにより、チェックボックスコントロールの状態に基づいて、このコントロールが自動的に有効または無効になります。
1. チェックボックスの **[既定]** プロパティを数式`true`に設定します。  これにより、出荷先住所と同じ値を使用する請求先住所が既定で使用されます。
1. チェックボックスの**oncheck**プロパティを数式`Reset( BillingName ); Reset( BillingAddress )`に設定します。  ユーザーが配送先住所と請求先住所の同期を選択した場合、請求先住所フィールドのすべてのユーザー入力がクリアされ、それぞれの**既定**のプロパティで対応する出荷先住所フィールドから値を取得できるようになります。
1. チェックボックスの**Onuncheck**プロパティを数式`SetFocus( BillingName )`に設定します。  ユーザーが別の請求先住所を選択した場合は、請求先住所の最初のコントロールにフォーカスが移動されます。  これらのコントロールは、 **DisplayMode**プロパティによって既に有効になっています。

### <a name="focus-on-validation-issues"></a>検証の問題に焦点を当てる

> [!NOTE]
> この例は**編集フォーム**コントロールであるように見えますが、残念ながら、このコントロールではまだ**SetFocus**はサポートされていません。  代わりに、この例では、スクロール可能な画面を使用して入力コントロールをホストしています。

フォームを検証する際には、問題が発生した場合にのみメッセージを表示し、問題が発生したフィールドにユーザーを移動すると便利な場合があります。  問題のフィールドが画面の外にスクロールされ、表示されない場合は、特に便利です。

![データ入力フォームを検証し、メッセージが表示されるだけでなく、入力フォーカスを、画面の外にスクロールした場合でも、問題のある入力コントロールに設定するアニメーション。](media/function-setfocus/scrollable-screen.gif)

このアニメーションでは、すべてのフィールドが適切に入力されるまで、[検証] ボタンが繰り返し押されます。  マウスポインターが画面の上部から下に移動しないことに注意してください。   代わりに、 **SetFocus**関数は、次の数式で注意が必要なコントロールに入力フォーカスを移動しました。

```powerapps-dot
If( IsBlank( Name ), 
        Notify( "Name requires a value", Error ); SetFocus( Name ),
    IsBlank( Street1 ), 
        Notify( "Street Address 1 requires a value", Error ); SetFocus( Street1 ),
    IsBlank( Street2 ), 
        Notify( "Street Address 2 requires a value", Error ); SetFocus( Street2 ),
    IsBlank( City ), 
        Notify( "City requires a value", Error ); SetFocus( City ),
    IsBlank( County ), 
        Notify( "County requires a value", Error ); SetFocus( County ),
    IsBlank( StateProvince ), 
        Notify( "State or Province requires a value", Error ); SetFocus( StateProvince ),
    IsBlank( PostalCode ), 
        Notify( "Postal Code requires a value", Error ); SetFocus( PostalCode ),
    IsBlank( Phone ), 
        Notify( "Contact Phone requires a value", Error ); SetFocus( Phone ),
    Notify( "Form is Complete", Success )
)
```

この例を作成するには、次のようにします。
1. 新しい空の電話アプリを作成します。
1. **[挿入]** メニューの **[新しい画面]** をクリックし、 **[スクロール]** 可能 を選択します。
1. 画面の中央のセクションで、**テキスト入力**コントロールを追加**し、名前、** **Street1**、 **Street2**、**市区町村**、**郡**、**州**、**郵便**番号、**電話番号**を入力します。 各フィールドの上に**ラベル**コントロールを追加します。  すべてのコントロールを収めるのに十分な長さでない場合は、セクションのサイズを変更することが必要になる場合があります。
1. スクロール可能なセクションの上にあるチェックマーク[**アイコン**コントロール](../controls/control-shapes-icons.md)を画面の上部に追加します。  
1. Icon コントロールの**onselect**プロパティを、上記の数式`If( IsBlank( ...`に設定します。

### <a name="focus-when-displaying-a-screen"></a>画面を表示するときにフォーカスを移動する

> [!NOTE]
> この例は**編集フォーム**コントロールであるように見えますが、unforutnatley **SetFocus**はそのコントロールではまだサポートされていません。  代わりに、この例では、スクロール可能な画面を使用して入力コントロールをホストしています。

入力コントロールを公開する場合と同様に、データ入力画面を表示するときは、データ入力の速度を上げるために最初の入力コントロールに集中すると便利です。

![データ入力画面を表示するときに、SetFocus を使用するか、または使用しないことのサイドバイサイド比較を示すアニメーション](media/function-setfocus/visible-setfocus.gif)

このアニメーションでは、左側のデータ入力画面では**SetFocus**が使用されていません。  表示時には、フォーカスのある入力コントロールはありません。ユーザーは tab、タッチ、マウスを使用するか、別の方法で**名前**フィールドにフォーカスを設定してから、値を入力する必要があります。

右側には、次の数式に設定されたデータ入力画面の**Onvisible**プロパティとまったく同じアプリがあります。

```powerapps-dot
SetFocus( Name )
```

これにより、 **[名前]** フィールドに自動的にフォーカスが設定されます。  ユーザーは、前の操作を必要とせずに、すぐにフィールド間の入力とタブ移動を開始できます。

この例を作成するには、次のようにします。
1. 上記の「検証の問題に焦点を当てる」アプリを作成します。
1. この画面で、 **Onvisible**プロパティを数式`SetFocus( Name )`に設定します。
1. 2番目の画面を追加します。
1. [**ボタン**コントロール](../controls/control-button.md)を追加します。
1. このコントロールの**Onselect**プロパティを数式`Navigate( Screen1 )`に設定します。
1. この画面からアプリをプレビューします。  ボタンを押します。  **Onvisible**式が評価され、 **[名前]** フィールドが自動的にフォーカスされます。
