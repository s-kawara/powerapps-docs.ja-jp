---
title: getOutputs | MicrosoftDocs
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.topic: reference
applies_to: ''
ms.assetid: c83c3a09-f04e-4dc6-8ddf-ccd0b4cc080e
ms.author: nabuthuk
author: Nkrb
---
# <a name="getoutputs"></a>getOutputs

[!INCLUDE[./includes/getoutputs-description.md](./includes/getoutputs-description.md)]

## <a name="syntax"></a>構文

`getOutputs()`

## <a name="remarks"></a>備考

出力はマニフェストで `input-output` や `bound` にマークされた各プロパティの値を含みます。
たとえば、マニフェストが `input-output` であるプロパティ `value` を持っていて、それをローカル変数 `myvalue` に設定したい場合、以下を返す必要があります:

```javascript
{
    value: myvalue
}
```

## <a name="example"></a>例

```javascript
MyControl.prototype.getOutputs = function () {
    var result = {
        value: this._value
    };
    return result;
};
```


### <a name="related-topics"></a>関連トピック

[[コントロール]](../control.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)