---
title: updateRecord | Microsoft Docs
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
ms.assetid: 179ced61-ff0f-45ef-aa14-835ce99532cf
---

# <a name="updaterecord"></a>updateRecord

[!INCLUDE [updaterecord-description](includes/updaterecord-description.md)]

## <a name="syntax"></a>構文

`updateRecord(entityLogicalName, id, data).then(successCallback, errorCallback);`

## <a name="parameters"></a>パラメーター

<table style="width:100%">
<tr>
<th>Name</th>
<th>型</th>
<th>必須出席者</th>
<th>説明</th>
</tr>
<tr>
<td>entityLogicalName</td>
<td>String</td>
<td>あり</td>
<td>更新するレコードのエンティティの論理名。 たとえば、&quot;account&quot;。</td>
</tr>
<tr>
<td>ID</td>
<td>String</td>
<td>はい</td>
<td>更新するエンティティ レコードの GUID。</td>
</tr>
<tr>
<td>data</td>
<td>オブジェクト</td>
<td>あり</td>
<td><p><code>key</code> がエンティティのプロパティである、 <code>key: value</code> ペアを含む JSON オブジェクト <code>value</code> が更新すべきプロパティの値です。</p>
<p>さまざまな更新のシナリオ向けに <code>data</code> オブジェクトを定義する方法については、このトピックの以降の例を参照してください。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>レコードを更新した場合に呼び出す関数。 次のプロパティを持つオブジェクトが渡され、更新されたレコードが識別されます:</p>
<ul>
<li><b>entityType</b>: 文字列。 更新されたレコードのエンティティの種類。</li>
<li><b>id</b>: 文字列。 更新されたレコードの GUID。</li>
</ul></td>
</tr>
<tr>
<td>errorCallback</td>
<td>関数</td>
<td>No</td>
<td>処理が失敗したときに呼び出す関数。 次のプロパティを持つオブジェクトが渡されます。
<ul>
<li><b>errorCode</b>: 数値。 エラー コード。</li>
<li><b>message</b>: 文字列。 問題を示すエラー メッセージが表示されます。</li>
</ul></td>
</tr>
</table>

## <a name="return-value"></a>戻り値

成功時に、**successCallback** パラメーターの説明で指定済みの属性を含む promise オブジェクトを戻します。


### <a name="related-topics"></a>関連トピック

[Web API](../webapi.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)