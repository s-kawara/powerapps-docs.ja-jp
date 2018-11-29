---
title: モデル駆動型アプリにおける isLoaded (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1870151d-6029-4733-ac35-6ee4d43f9553
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="isloaded-client-api-reference"></a>isLoaded (クライアント API 参照)



[!INCLUDE[./includes/isLoaded-description.md](./includes/isLoaded-description.md)]

## <a name="syntax"></a>構文

`quickViewControl.isLoaded();`

## <a name="return-value"></a>戻り値

**種類**: ブール値。

**説明**: 構成コントロールでデータ バインドが完了した場合には True、それ以外の場合は False です。 

## <a name="remarks"></a>備考

簡易表示コントロールの構成コントロールのデータ バインドは、 メイン フォーム **OnLoad** イベントでは完了していない場合があります。コントロールがバインドされている簡易表示フォームが完全には読み込まれていないためです。 その結果、[getAttribute](../controls/getattribute.md) または構成コントロールのデータ関連メソッドは動作しません。 簡易表示コントロールの **isLoaded** メソッドは、簡易表示コントロールの構成コントロールのバインド状況を特定するのに役立ちます。

## <a name="example"></a>例

次のコード サンプルは、**isLoaded** メソッドを使用して、バインド状況を確認し簡易表示コントロールの構成コントロールがバインドされている属性の値を取得する方法を示します。

```JavaScript
function getAttributeValue(executionContext) {
    var formContext = executionContext.getFormContext();
    var quickViewControl = formContext.ui.quickForms.get("<QuickViewControlName>");
    if (quickViewControl != undefined) {
        if (quickViewControl.isLoaded()) {
            // Access the value of the attribute bound to the constituent control
            var myValue = quickViewControl.getControl(0).getAttribute().getValue();
            console.log(myValue);
            return;
        }
        else {
            // Wait for some time and check again
            setTimeout(getAttributeValue, 10);
        }
    }
    else {
        console.log("No data to display in the quick view control.");
        return;
    }
}
```

### <a name="related-topics"></a>関連トピック

[formContext.ui.quickForms](../formContext-ui-quickForms.md)