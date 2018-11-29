---
title: モデル駆動型アプリの getFormContext (クライアント API 参照) | MicrosoftDocs
description: 呼び出された場所に基づいてフォームへの参照またはフォーム上のアイテムを返す getFormContext メソッドについて説明します。
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9f3b2fed-fde5-46e4-8c59-43aa51aa82df
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getformcontext-client-api-reference"></a>getFormContext (クライアント API 参照)



呼び出された場所によってフォーム上のフォームまたはアイテムへの参照を返します。

## <a name="syntax"></a>構文

`ExecutionContextObj.getFormContext()`

## <a name="return-value"></a>戻り値

**種類**: オブジェクト

**説明**: メソッドが呼び出された場所に基づいて、編集可能グリッドなどの、フォームへの参照またはフォーム上のアイテムを返します。 このメソッドによって、呼び出される場所によってフォーム上のフォームまたはアイテム上のいずれかに操作ができるイベント ハンドラーの作成が可能となります。

## <a name="example"></a>例

次のコード例は、スクリプトの登録場所 ( [フィールド OnChange](../events/attribute-onchange.md) イベントまたは編集可能グリッド [OnChange](../events/grid-onchange.md) イベント) によって、フォーム フィールドまた編集可能グリッド セル上で通知の設定を行うメソッドの作成方法を説明します。

```JavaScript
function commonEventHandler(executionContext) {
    var formContext = executionContext.getFormContext();    
    var telephoneAttr = formContext.data.entity.attributes.getByName('telephone1');
    var isNumberWithCountryCode = telephoneAttr.getValue().substring(0,1) === '+';

    // telephoneField will be a form control if invoked from a form OnChange event;
    // telephoneField will be a editable grid GridCell object if invoked from editable grid OnChange event.
    var telephoneField = telephoneAttr.controls.getByIndex(0);

    if (!isNumberWithCountryCode) {
        telephoneField.setNotification('Please include the country code beginning with ‘+’.', 'countryCodeNotification');
    }
    else {
        telephoneField.clearNotification('countryCodeNotification');
    }
}
```


### <a name="related-topics"></a>関連トピック
[実行コンテキスト](../execution-context.md)

[フォーム コンテキスト](../../clientapi-form-context.md)





