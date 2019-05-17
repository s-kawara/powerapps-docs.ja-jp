---
title: init | MicrosoftDocs
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.topic: reference
applies_to: ''
ms.assetid: 4485b7d4-c68f-4298-8676-1820eb33c1ad
ms.author: nabuthuk
---
# <a name="init"></a>init

[!INCLUDE[./includes/init-description.md](./includes/init-description.md)]

## <a name="syntax"></a>構文

`init(context,notifyOutputChanged,state,container)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|コンテキスト|[コンテキスト](../context.md)|はい|パラメーター、コンポーネントのメタデータ、インタフェース関数を含む *入力プロパティ*。|
|notifyOutputChanged|`function`|いいえ|新しい出力があることをフレームワークに通知するメソッド|
|状態|`Dictionary`|いいえ|最後のセッションで *setControlState* から保存されたコンポーネントの状態|
|コンテナ|[HTMLDivElement](https://developer.mozilla.org/docs/Web/API/HTMLDivElement)|いいえ|表示する div 要素|

## <a name="example"></a>例

```JavaScript
MyNameSpace.JSHelloWorldControl.prototype.init = function (context, notifyOutputChanged, state, container) {
    this._labelElement = document.createElement("label");
    this._labelElement.setAttribute("class", "JS_HelloWorldColor");
    container.appendChild(this._labelElement);
};
```

### <a name="related-topics"></a>関連トピック

[[コントロール]](../control.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
