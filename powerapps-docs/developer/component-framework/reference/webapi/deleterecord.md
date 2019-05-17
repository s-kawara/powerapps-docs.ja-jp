---
title: deleteRecord | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5c9968bf-d535-425c-b1f1-0db6b7822de1
---

# <a name="deleterecord"></a>deleteRecord

[!INCLUDE [deleterecord-description](includes/deleterecord-description.md)]

## <a name="syntax"></a>構文

`deleteRecord(entityLogicalName, id).then(successCallback, errorCallback);`

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
<td>削除するレコードのエンティティの論理名。 たとえば、&quot;account&quot;。 </td>
</tr>
<tr>
<td>ID</td>
<td>String</td>
<td>はい</td>
<td>削除するエンティティ レコードの GUID。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>レコードを削除した場合に呼び出す関数。 次のプロパティを持つオブジェクトが渡され、削除されたレコードが識別されます:</p>
<ul>
<li><b>entityType</b>: 文字列。 レコードのエンティティの種類。</li>
<li><b>id</b>: 文字列。 レコードの GUID。</li>
<li><b>name</b>: 文字列。 レコードの名前。</li>
</ul></td>
</tr>
<tr>
<td>errorCallback</td>
<td>関数</td>
<td>No</td>
<td>処理が失敗したときに呼び出す関数。</td>
</tr>
</table>

## <a name="return-value"></a>戻り値

成功時に、**successCallback** パラメーターの説明で指定済みの属性を含む promise オブジェクトを戻します。


### <a name="related-topics"></a>関連トピック

[Web API](../webapi.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)