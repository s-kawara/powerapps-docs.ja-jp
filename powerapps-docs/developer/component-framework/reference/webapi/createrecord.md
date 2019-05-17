---
title: 'createRecord | Microsoft '
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
ms.assetid: 9179f03b-9d26-4253-9535-13ab544d58ac
---

# <a name="createrecord"></a>createRecord

[!INCLUDE [createrecord-description](includes/createrecord-description.md)]

## <a name="syntax"></a>構文

`createRecord(entityLogicalName, data).then(successCallback, errorCallback);`

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
<td>はい</td>
<td>作成するエンティティの論理名。 たとえば、&quot;account&quot;。</td>
</tr>
<tr>
<td>data</td>
<td>オブジェクト</td>
<td>はい</td>
<td><p>新しいエンティティ レコードの属性および値を定義する JSON オブジェクト。</p>
<p>さまざまな作成のシナリオ向けに <code>data</code> オブジェクトを定義する方法については、このトピックの以降の例を参照してください。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>レコードを作成した場合に呼び出す関数。 次のプロパティを持つオブジェクトが渡され、新しいレコードが識別されます:</p>
<ul>
<li><b>entityType</b>: 文字列。 新しいレコードのエンティティ論理名。</li>
<li><b>id</b>: 文字列。 新しいレコードの GUID。</li>
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