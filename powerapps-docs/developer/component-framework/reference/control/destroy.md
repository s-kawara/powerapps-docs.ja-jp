---
title: 破棄 | MicrosoftDocs
ms.topic: reference
applies_to: ''
ms.assetid: ba66b513-2a7b-4ba6-b2d5-446ea2b42fdb
author: nkrb
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
---
# <a name="destroy"></a>破棄

[!INCLUDE[./includes/destroy-description.md](./includes/destroy-description.md)]

## <a name="syntax"></a>構文

`destroy()`

## <a name="example"></a>例

```javascript
MyControl.prototype.destroy = function () {
 this.button.removeEventListener("click", this.onButtonClick);
};
```

### <a name="related-topics"></a>関連トピック

[[コントロール]](../control.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)