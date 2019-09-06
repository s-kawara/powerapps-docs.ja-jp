---
title: retrieveMultipleRecords | Microsoft Docs
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
ms.assetid: 824a53f9-c743-435a-9de2-8128846f3191
---

# <a name="retrievemultiplerecords"></a>retrieveMultipleRecords

[!INCLUDE [retrievemultiplerecords-description](includes/retrievemultiplerecords-description.md)]

## <a name="syntax"></a>構文

`retrieveMultipleRecords(entityLogicalName, options, maxPageSize).then(successCallback, errorCallback);`

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
<td>オプション</td>
<td>String</td>
<td>いいえ</td>
<td><p>データを取得する OData システム クエリ オプションまたは FetchXML クエリ。 </p> 
<ul>
<li>システム クエリ オプション <b>$select</b>、<b>$top</b>、<b>$filter</b>、<b>$expand</b>、および <b>$orderby</b> はサポートされます。</li>
<li>FetchXML クエリを指定するには、クエリを指定する <code>fetchXml</code> 属性を使用します。</li>
</ul>
<p>メモ:  <b>$select</b> システム クエリ オプションを使用し、プロパティ名のコンマ区切りリストを含めて、エンティティ レコードに対して返されるプロパティを制限する必要があります。 これは重要なパフォーマンスのベスト プラクティスです。 プロパティが <b></b> を使用して指定されない場合は、すべてのプロパティが返されます。</li>
<p><code>?</code> で始まるクエリ オプションを指定します。 クエリ オプションを <code>&amp;</code> で区切って、複数のシステム クエリ オプションを指定することもできます。
<p>複数取得のさまざまなシナリオ向けに <code>options</code> パラメーターを定義する方法については、このトピックの以降の例を参照してください。</td>
</tr>
<tr>
<td>maxPageSize</td>
<td>数値</td>
<td>No</td>
<td><p>ページごとに返されるエンティティ レコードの数を表す正の数を指定します。 このパラメーターを指定しない場合、既定の 5000 が渡されます。</p>
<p>取得されるレコード数が、指定された <code>maxPageSize</code> 値より多い場合は、返された Promise オブジェクト内の <code>nextLink</code> 属性に、エンティティの次のセットを取得するためのリンクが含まれます。 </td>
</tr>
<tr>
<td>successCallback</td>
<td>機能</td>
<td>なし</td>
<td><p>エンティティ レコードを取得した場合に呼び出す関数。 次の属性のオブジェクトは関数に渡されます。</p>
<ul>
<li><b>entities</b>: JSON オブジェクトの配列。各オブジェクトは、属性と値のペア <code>key: value</code> を含む、取得したエンティティ レコードを表します。 既定では、エンティティ レコードの ID が取得されます。</li>
<li><b>nextLink</b>: 文字列。 取得されるレコードの件数が、要求内の <code>maxPageSize</code> パラメーターで指定された値より多い場合、この属性はレコードの次のセットを返す URL を返します。</li>
</ul>
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

成功すると、要求内でページング (`maxPageSize`) が指定され、返されるレコード数がページング値を超える場合にレコードの次のセットを指す URL とともに、取得したエンティティ レコードおよび **nextLink** 属性 (オプション) を含む JSON オブジェクト (**エンティティ**) の配列を含む promise を返します。


### <a name="related-topics"></a>関連トピック

[Web API](../webapi.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)