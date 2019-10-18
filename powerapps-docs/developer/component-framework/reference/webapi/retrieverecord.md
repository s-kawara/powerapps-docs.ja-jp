---
title: RetrieveRecord |Microsoft Docs
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
ms.assetid: dddeecc9-5067-420d-8bd7-4c914218e969
ms.openlocfilehash: 9c77bf9975bd1f1f115df9385061c008975cc184
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72341704"
---
# <a name="retrieverecord"></a>retrieveRecord

[!INCLUDE [retrieverecord-description](includes/retrieverecord-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.webAPI.retrieveRecord(entityLogicalName, id, options).then(successCallback, errorCallback);`

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
<td>取得するレコードのエンティティ論理名。 例: &quot;account &quot;。</td>
</tr>
<tr>
<td>id</td>
<td>String</td>
<td>はい</td>
<td>取得するエンティティレコードの GUID。</td>
</tr>
<tr>
<td>オプション</td>
<td>String</td>
<td>いいえ</td>
<td><p>データを取得するための、OData システムクエリオプション、 <b>$select</b>および<b>$expand</b>。</p>
<ul><li>プロパティ名のコンマ区切りリストを含めることによって返されるプロパティを制限するには、 <b>$select</b>システムクエリオプションを使用します。 これは、パフォーマンスに関する重要なベストプラクティスです。 <b>$Select</b>を使用してプロパティが指定されていない場合は、すべてのプロパティが返されます。</li>
<li><b>$Expand</b>システムクエリオプションを使用して、関連エンティティから返されるデータを制御します。 ナビゲーションプロパティの名前だけを指定した場合は、関連レコードのすべてのプロパティを受け取ります。 関連レコードに対して返されるプロパティは、ナビゲーションプロパティ名の後にかっこで囲まれた<b>$select</b>システムクエリオプションを使用して制限できます。 これは、 <i>1 つの値</i>と<i>コレクション値</i>のナビゲーションプロパティの両方に使用します。</li>
</ul>
<p>@No__t_0 で始まるクエリオプションを指定します。 @No__t_0 を使用してクエリオプションを分離することにより、複数のクエリオプションを指定することもできます。 例:</p>
<code>?$select=name&amp;$expand=primarycontactid($select=contactid,fullname)</code>
<p>さまざまな取得シナリオで <code>options</code> パラメーターを定義する方法については、このトピックの後半の例を参照してください。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>いいえ</td>
<td><p>レコードが取得されるときに呼び出す関数。 取得したプロパティと値を持つ JSON オブジェクトが関数に渡されます。</p>
</td>
</tr>
<tr>
<td>errorCallback</td>
<td>関数</td>
<td>いいえ</td>
<td>操作が失敗したときに呼び出す関数。</td>
</tr>
</table>

## <a name="return-value"></a>戻り値

種類: [Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise) <[エンティティ](../entity.md)>



### <a name="related-topics"></a>関連トピック

[Web API](../webapi.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)