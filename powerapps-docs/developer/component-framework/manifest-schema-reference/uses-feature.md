---
title: 使用-機能 |Microsoft Docs
description: ''
keywords: ''
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 87f5e921-4114-4710-a362-db741426a69b
ms.openlocfilehash: fe4d384c8dd53fc0f9efcf5558252984a4be74a3
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72345890"
---
# <a name="uses-feature-element"></a>使用-機能要素

コンポーネントが使用する機能を示します。

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリ

## <a name="parent-element"></a>親要素

|要素|Description|
|--|--|
|機能-使用法|機能使用量要素は、使用する機能要素のラッパーとして機能します。これにより、開発者は、コンポーネントが使用する機能を宣言できます。 使用する機能の要素が定義されていない場合、機能の使用に関する要素は必要ありません。|

## <a name="child-elements"></a>子要素

|要素|Description|種類|必須|
|--|--|---|----|
|指定|コンポーネントで宣言されている機能の名前|`string`|はい|
|必須|コンポーネントがその機能を必要とするかどうかを示します|`boolean`|はい|

### <a name="example"></a>例 

```XML
<feature-usage>
    <uses-feature name="WebAPI" required="true" />
</feature-usage>
```

次の表は、マニフェストで定義されている使用機能の設定に基づいて機能関数を呼び出すことができるかどうかに関係なく、実行時にコードで行われる処理に対するこれらの設定の関係を示しています。

|マニフェスト|ホストがサポートする場合|ホストがサポートしていない場合|
|----|----|-----|
|`uses-feature name="device.captureImage" required=”true"`|`Context.device.captureImage != null`、チェックは必要ありません。|デザイン時に警告が出てきます。 コンポーネントの読み込みは実行時に失敗します。|
|`uses-feature name="device.captureImage" required=”false"`|`Context.device.captureImage != null`|`Context.device.captureImage == null`、コンポーネントは実行時にこれをアダプティブに確認できます。 |
|存在|`Context.device.captureImage == null` |`Context.device.captureImage == null` |

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)