---
title: createRecord |Microsoft Docs
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
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
ms.assetid: 9179f03b-9d26-4253-9535-13ab544d58ac
ms.openlocfilehash: f3a2b860f17d7efaaf8efebcf2418aef04478947
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72340830"
---
# <a name="createrecord"></a>createRecord

[!INCLUDE [createrecord-description](includes/createrecord-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.webAPI.createRecord(entityLogicalName, data).then(successCallback, errorCallback);`

## <a name="parameters"></a>パラメーター

<table style="width:100%">
<tr>
<th>名前</th>
<th>種類</th>
<th>必須</th>
<th>Description</th>
</tr>
<tr>
<td>entityLogicalName</td>
<td>String</td>
<td>はい</td>
<td>作成するエンティティの論理名。 例: &quot;account &quot;。</td>
</tr>
<tr>
<td>データ</td>
<td>素材</td>
<td>はい</td>
<td><p>新しいエンティティレコードの属性と値を定義する JSON オブジェクト。</p>
<p>さまざまな作成シナリオで <code>data</code> オブジェクトを定義する方法については、このトピックの後半の例を参照してください。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>いいえ</td>
<td><p>レコードが作成されるときに呼び出す関数。 新しいレコードを識別するために、次のプロパティを持つオブジェクトが渡されます。</p>
<ul>
<li><b>entityType</b>: String。 新しいレコードのエンティティ論理名。</li>
<li><b>id</b>: 文字列。 新しいレコードの GUID。</li>
</ul></td>
</tr>
<tr>
<td>errorCallback</td>
<td>関数</td>
<td>いいえ</td>
<td>操作が失敗したときに呼び出す関数。 次のプロパティを持つオブジェクトが渡されます。
<ul>
<li><b>errorCode</b>: 数値。 エラーコード。</li>
<li><b>message</b>: 文字列。 問題を説明するエラーメッセージ。</li>
</ul></td>
</tr>
</table>

## <a name="return-value"></a>戻り値

型: [Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise) <[Entityreference](../entityreference.md) >

説明: 成功した場合、 **successCallback**パラメーターの説明で指定された属性を含む promise オブジェクトを返します。

### <a name="related-topics"></a>関連トピック

[Web API](../webapi.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)