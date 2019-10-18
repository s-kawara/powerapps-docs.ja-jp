---
title: deleteRecord |Microsoft Docs
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
ms.assetid: 5c9968bf-d535-425c-b1f1-0db6b7822de1
ms.openlocfilehash: f6c8dd6ea7d156e28ab3ae54d7fe37dad6c4546a
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72340761"
---
# <a name="deleterecord"></a>deleteRecord

[!INCLUDE [deleterecord-description](includes/deleterecord-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.webAPI.deleteRecord(entityLogicalName, id).then(successCallback, errorCallback);`

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
<td>削除するレコードのエンティティ論理名。 例: &quot;account &quot;。 </td>
</tr>
<tr>
<td>id</td>
<td>String</td>
<td>はい</td>
<td>削除するエンティティレコードの GUID。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>いいえ</td>
<td><p>レコードが削除されたときに呼び出す関数。 削除されたレコードを識別するために、次のプロパティを持つオブジェクトが渡されます。</p>
<ul>
<li><b>entityType</b>: String。 レコードのエンティティ型。</li>
<li><b>id</b>: 文字列。 レコードの GUID。</li>
<li><b>name</b>: String。 レコードの名前。</li>
</ul></td>
</tr>
<tr>
<td>errorCallback</td>
<td>関数</td>
<td>いいえ</td>
<td>操作が失敗したときに呼び出す関数。</td>
</tr>
</table>

## <a name="return-value"></a>戻り値

型: [Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise) <[Entityreference](../entityreference.md) >

### <a name="related-topics"></a>関連トピック

[Web API](../webapi.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)