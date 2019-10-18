---
title: init |MicrosoftDocs
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.topic: reference
applies_to: ''
ms.assetid: 4485b7d4-c68f-4298-8676-1820eb33c1ad
ms.author: nabuthuk
author: Nkrb
ms.openlocfilehash: 57a5ce0d4e930184bf42502f1dc16b6a648f1292
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72345499"
---
# <a name="init"></a>init

[!INCLUDE[./includes/init-description.md](./includes/init-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="syntax"></a>構文

`init(context,notifyOutputChanged,state,container)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|関連|[コンテキスト](../context.md)|はい|パラメーター、コンポーネントメタデータ、およびインターフェイス関数を含む*入力プロパティ*。|
|notifyOutputChanged|`function`|いいえ|新しい出力があることをフレームワークに通知するメソッド|
|状態|`Dictionary`|いいえ|最後のセッションで*Setcontrolstate*から保存されるコンポーネントの状態|
|コンテナー|[ある htmldivelement](https://developer.mozilla.org/docs/Web/API/HTMLDivElement)|いいえ|表示する div 要素|

## <a name="example"></a>例

```JavaScript
MyNameSpace.JSHelloWorldControl.prototype.init = function (context, notifyOutputChanged, state, container) {
    this._labelElement = document.createElement("label");
    this._labelElement.setAttribute("class", "JS_HelloWorldColor");
    container.appendChild(this._labelElement);
};
```

### <a name="related-topics"></a>関連トピック

[コントロール](../control.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
