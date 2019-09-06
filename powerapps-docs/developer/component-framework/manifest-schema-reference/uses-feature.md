---
title: uses-feature要素 | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 87f5e921-4114-4710-a362-db741426a69b
---

# <a name="uses-feature-element"></a>uses-feature要素

コンポーネントが使用する機能を示します。

## <a name="parent-element"></a>親要素

|Element|説明|
|--|--|
|feature-usage|feature-usage 要素は uses-feature 要素のラッパーとして機能し、開発者はこの要素を使用して、コンポーネントが使用する機能を宣言できます。 uses-feature の要素が定義されていない場合は、この要素は必要ありません。|

## <a name="child-elements"></a>下位要素

|Element|説明|
|--|--|
|名前|コンポーネントで宣言されている機能の名称です|
|必須|コンポーネントがその機能を必要とするかどうかを示します|


### <a name="example"></a>例 

```XML
<feature-usage>
    <uses-feature name="WebAPI" required="true" />
</feature-usage>
```

以下の表は、これらの設定と実行時にコード内で行われる処理との関係を示しています。 マニフェストで定義されたuses-feature 設定に基づいた、機能関数の呼び出しへの対応を表しています。

|マニフェスト|ホストがサポートしている場合|ホストがサポートしていない場合|
|----|----|-----|
|`uses-feature name="device.captureImage" required=”true"`|`Context.device.captureImage != null`、チェックは不要です。|設計時に警告を表示します。 実行時にコンポーネントのロードが失敗します。|
|`uses-feature name="device.captureImage" required=”false"`|`Context.device.captureImage != null`|`Context.device.captureImage == null`コンポーネントは実行時にこれを適応的にチェックすることができます。 |
|(なし)|`Context.device.captureImage == null` |`Context.device.captureImage == null` |

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)