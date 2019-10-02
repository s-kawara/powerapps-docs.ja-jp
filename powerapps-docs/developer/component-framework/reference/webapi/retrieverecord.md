---
title: RetrieveRecord | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dddeecc9-5067-420d-8bd7-4c914218e969
---

# <a name="retrieverecord"></a>retrieveRecord

[!INCLUDE [retrieverecord-description](includes/retrieverecord-description.md)]

## <a name="syntax"></a>構文

`retrieveRecord(entityLogicalName, id, options).then(successCallback, errorCallback);`

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
<td>取得するレコードのエンティティの論理名。 たとえば、&quot;account&quot;。</td>
</tr>
<tr>
<td>ID</td>
<td>String</td>
<td>はい</td>
<td>取得するエンティティ レコードの GUID。</td>
</tr>
<tr>
<td>オプション</td>
<td>String</td>
<td>No</td>
<td><p>データを取得する OData システム クエリ オプション、<b>$select</b> および <b>$expand</b>。</p>
<ul><li>プロパティ名のコンマ区切りリストを含めることにより返されるプロパティを制限するためには <b>$select</b> システム クエリ オプションを使用します。 これは重要なパフォーマンスのベスト プラクティスです。 プロパティが <b></b> を使用して指定されない場合は、すべてのプロパティが返されます。</li>
<li><b>$expand</b> システム クエリ オプションを使用して、関連エンティティからどのデータが返されるかをコントロールします。 単にナビゲーション プロパティ名を含めた場合は、関連レコードのすべてのプロパティが表示されます。 ナビゲーション プロパティ名の後にかっこで示される <b>$select</b> システム クエリ オプションを使用して、関連レコードに対して返されるプロパティを制限できます。 これは、<i>単一値</i>と<i>コレクション値</i>のナビゲーション プロパティの両方で使用します。</li>
</ul>
<p><code>?</code> で始まるクエリ オプションを指定します。 クエリ オプションを <code>&amp;</code> で区切って複数のクエリ オプションを指定することもできます。 たとえば、次のようになります。</p>
<code>?$select=name&amp;$expand=primarycontactid($select=contactid,fullname)</code>
<p>さまざまな取得のシナリオ向けに <code>options</code> パラメーターを定義する方法については、このトピックの以降の例を参照してください。</td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>No</td>
<td><p>レコードを取得した場合に呼び出す関数。 取得したプロパティと値を持つ JSON オブジェクトが関数に渡されます。</p>
</td>
</tr>
<tr>
<td>errorCallback</td>
<td>関数</td>
<td>No</td>
<td>処理が失敗したときに呼び出す関数。</td>
</tr>
</table>

## <a name="return-value"></a>戻り値

成功すると、取得した属性とその値を持つ JSON オブジェクトを含む Promise が返されます。


### <a name="related-topics"></a>関連トピック

[Web API](../webapi.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)