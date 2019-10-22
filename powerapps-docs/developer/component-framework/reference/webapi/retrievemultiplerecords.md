---
title: retrieveMultipleRecords |Microsoft Docs
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
ms.assetid: 824a53f9-c743-435a-9de2-8128846f3191
ms.openlocfilehash: d708596e9b8e12ead8f84d31d3b35fb5b27843f8
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72340807"
---
# <a name="retrievemultiplerecords"></a>retrieveMultipleRecords

[!INCLUDE [retrievemultiplerecords-description](includes/retrievemultiplerecords-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.webAPI.retrieveMultipleRecords(entityLogicalName, options, maxPageSize).then(successCallback, errorCallback);`

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
<td>オプション</td>
<td>String</td>
<td>いいえ</td>
<td><p>データを取得する OData システムクエリオプションまたは FetchXML クエリ。 </p> 
<ul>
<li>次のシステムクエリオプションがサポートされています: <b>$select</b>、 <b>$top</b>、 <b>$filter</b>、 <b>$expand</b>、および<b>$orderby</b>。</li>
<li>FetchXML クエリを指定するには、<code>fetchXml</code> 属性を使用してクエリを指定します。</li>
</ul>
<p>注: プロパティ名のコンマ区切りのリストを含めることによって、エンティティレコードに対して返されるプロパティを制限するには、常に<b>$select</b>システムクエリオプションを使用する必要があります。 これは、パフォーマンスに関する重要なベストプラクティスです。 <b>$Select</b>を使用してプロパティが指定されていない場合は、すべてのプロパティが返されます。</li>
<p>@No__t_0 で始まるクエリオプションを指定します。 複数のシステムクエリオプションを指定する場合は、<code>&amp;</code> を使用してクエリオプションを分離することもできます。
<p>このトピックの後半の例を参照して、さまざまな取得のシナリオで <code>options</code> パラメーターを定義する方法を確認してください。</td>
</tr>
<tr>
<td>maxPageSize</td>
<td>Number</td>
<td>いいえ</td>
<td><p>1ページあたりに返されるエンティティレコードの数を示す正の数値を指定します。 このパラメーターを指定しない場合、既定値は5000として渡されます。</p>
<p>取得するレコードの数が指定された <code>maxPageSize</code> 値を超えている場合、返される promise オブジェクトの <code>nextLink</code> 属性には、次のエンティティのセットを取得するためのリンクが含まれます。 </td>
</tr>
<tr>
<td>successCallback</td>
<td>関数</td>
<td>いいえ</td>
<td><p>エンティティレコードを取得するときに呼び出す関数。 次の属性を持つオブジェクトが関数に渡されます。</p>
<ul>
<li><b>エンティティ</b>: JSON オブジェクトの配列。各オブジェクトは、属性とその値を含む取得されたエンティティレコードを <code>key: value</code> のペアとして表します。 エンティティレコードの Id は、既定で取得されます。</li>
<li><b>Nextlink</b>: 文字列。 取得されるレコードの数が要求の <code>maxPageSize</code> パラメーターで指定された値を超える場合、この属性は、次のレコードのセットを返す URL を返します。</li>
</ul>
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

型: [Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise) <RetrieveMultipleResponse>

説明: `RetrieveMultipleResponse` は、取得されたエンティティレコードを含む JSON オブジェクトの配列を含む promise を返し、要求でページング (`maxPageSize`) が指定されている場合、次のレコードセットを指す URL を使用して**Nextlink**属性を返します。返されたレコード数がページング値を超えています。 次のパラメーターがあります。

|引き|戻り値|Description|
|----|------|-------|
|事業|`Entity[]`|JSON オブジェクトの配列。各オブジェクトは、属性とその値を含む取得されたエンティティレコードを表します。|
|nextLink|`string`|取得するレコードの数が要求の ' maxPageSize ' パラメーターに指定されている値を超えている場合、この属性は、次のレコードのセットを返す URL を返します。|


### <a name="related-topics"></a>関連トピック

[Web API](../webapi.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)