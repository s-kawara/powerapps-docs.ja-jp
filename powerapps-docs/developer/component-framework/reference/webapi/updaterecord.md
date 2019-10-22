---
title: updateRecord |Microsoft Docs
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
ms.assetid: 179ced61-ff0f-45ef-aa14-835ce99532cf
ms.openlocfilehash: 96037bcd8ca43448e928abef714ae031222d8e98
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72340692"
---
# <a name="updaterecord"></a>updateRecord

[!INCLUDE [updaterecord-description](includes/updaterecord-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.webAPI.updateRecord(entityLogicalName, id, data).then(successCallback, errorCallback);`

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
<td>更新するレコードのエンティティ論理名。 例: &quot;account &quot;。</td>
</tr>
<tr>
<td>id</td>
<td>String</td>
<td>はい</td>
<td>更新するエンティティレコードの GUID。</td>
</tr>
<tr>
<td>データ</td>
<td>素材</td>
<td>はい</td>
<td><p>@No__t_0 のペアを含む JSON オブジェクト。 <code>key</code> はエンティティのプロパティであり、 <code>value</code> 更新するプロパティの値を指定します。</p>
<p>さまざまな更新シナリオで <code>data</code> オブジェクトを定義する方法については、このトピックの後半の例を参照してください。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>いいえ</td>
<td><p>レコードが更新されたときに呼び出す関数。 更新されたレコードを識別するために、次のプロパティを持つオブジェクトが渡されます。</p>
<ul>
<li><b>entityType</b>: String。 更新されたレコードのエンティティ型。</li>
<li><b>id</b>: 文字列。 更新されたレコードの GUID。</li>
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

種類: [Promise] ((datestrings info. md) <[Entityreference](../entityreference.md) >

説明: 成功した場合、 **successCallback**パラメーターの説明で指定された属性を含む promise オブジェクトを返します。


### <a name="related-topics"></a>関連トピック

[Web API](../webapi.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)