---
title: モデル駆動型アプリにおける属性 | Microsoft Docs
description: クライアント API を使用したモデル駆動型アプリの属性の作業について検討します。
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 32e8d1d0-4093-4588-a517-2930eec34dce
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="attributes-client-api-reference"></a>属性 (クライアント API 参照)



属性にはモデル駆動型アプリのフォームまたはグリッドのデータが含まれます。 `formContext.data.entity.attributes` コレクションまたは `formContext.getAttribute` ショートカット メソッドを使用して、属性のコレクションにアクセスします。 コレクションの詳細については、「[コレクション (クライアント API 参照)](collections.md)」を参照してください。 

コレクション内の属性にアクセスするには、メソッドに属性の名前 (文字列) またはインデックス値 (数値) を引数として渡します。 例: `formContext.getAttribute(arg)`

属性は、種類によって分類されます。 [getAttributeType](attributes/getAttributeType.md) メソッドを使用して、属性の種類を判別できます。 特定の属性のメソッドは、特定の種類の属性でのみ利用できます。

このトピックでは、属性の種類ごとに使用できるメソッドについて説明します。 

## <a name="all-attribute-types"></a>すべての属性の種類

<table>
<tr>
<td>
<ul>
<li>[controls](attributes/controls-collection.md)</li>
<li>[addOnChange](attributes/addOnChange.md)</li>
<li>[fireOnChange](attributes/fireOnChange.md)</a></li>
<li>[getAttributeType](attributes/getAttributeType.md)</li>
<li>[getFormat](attributes/getFormat.md)</li>
<li>[getIsDirty](attributes/getIsDirty.md)</li>
</ul>
</td>
<td>
<ul>
<li>[getName](attributes/getName.md)</li>
<li>[getParent](attributes/getParent.md)</li>
<li>[getRequiredLevel](attributes/getRequiredLevel.md)</li>
<li>[getSubmitMode](attributes/getSubmitMode.md)</li>
<li>[getUserPrivilege](attributes/getUserPrivilege.md)</li>
<li>[getValue](attributes/getValue.md)</li>
</ul>
</td>
<td>
<ul>

<li>[isValid](attributes/isValid.md)</li>
<li>[removeOnChange](attributes/removeOnChange.md)</li>
<li>[setRequiredLevel](attributes/setRequiredLevel.md)</li>
<li>[setSubmitMode](attributes/setSubmitMode.md)</li>
<li>[setValue](attributes/setValue.md)</li>
</ul>
</td>
</tr>
</table>


## <a name="boolean-attribute-type"></a>ブール属性の種類
前に説明したすべての属性の種類に使用できるメソッドに加えて、次のメソッドは、**ブール**属性でのみ利用できます:

- [getInitialValue](attributes/getInitialValue.md)

## <a name="lookup-attribute-type"></a>属性の種類の検索
前に説明したすべての属性の種類に使用できるメソッドに加えて、次のメソッドは、**検索**属性でのみ利用できます:

- [getIsPartyList](attributes/getIsPartyList.md)

## <a name="multiselectoptionset-and-optionset-attribute-types"></a>MultiSelectOptionSet および OptionSet 属性の種類

前に説明したすべての属性の種類に使用できるメソッドに加えて、次のメソッドは、**multiselectoption** および **optionset** 属性でのみ使用できます。

<table>
<tr>
<td>
<ul>
<li>[getInitialValue](attributes/getInitialValue.md)</li>
<li>[getOption](attributes/getOption.md)</li>
<li>[getOptions](attributes/getOptions.md)</a></li>
<li>[getSelectedOption](attributes/getSelectedOption.md)</li>
<li>[getText](attributes/getText.md)</li>
</ul>
</td>
</tr>
</table>

## <a name="number-attribute-type-decimal-double-integer-money"></a>属性の種類の数字 (小数、二重、整数、通貨)
次のメソッドは、**小数**、**二重**、および**整数**属性でのみ利用できます:

<table>
<tr>
<td>
<ul>
<li>[getMax](attributes/getMax.md)</li>
<li>[getMin](attributes/getMin.md)</li>
<li>[getPrecision](attributes/getPrecision.md)</a></li>
<li>[setPrecision](attributes/setPrecision.md)</li>
<li>[getText](attributes/getText.md)</li>
</ul>
</td>
</tr>
</table>

## <a name="string-attribute-type"></a>文字列属性の種類
前に説明したすべての属性の種類に使用できるメソッドに加えて、次のメソッドは、**文字列**属性でのみ利用できます:

- [getMaxLength](attributes/getMaxLength.md)

### <a name="related-topics"></a>関連トピック

[複合属性](composite-attributes.md)

[Xrm オブジェクト モデルの理解](../understand-clientapi-object-model.md)

[コントロール (クライアント API 参照)](controls.md)




