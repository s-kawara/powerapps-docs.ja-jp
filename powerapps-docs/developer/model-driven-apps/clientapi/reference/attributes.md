---
title: モデル駆動型アプリにおける属性 | Microsoft Docs
description: クライアント API を使用したモデル駆動型アプリの属性の作業について検討します。
ms.date: 10/31/2018
ms.service: powerapps
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
<li><a href="attributes/controls-collection.md" data-raw-source="[controls](attributes/controls-collection.md)">controls</a></li>
<li><a href="attributes/addOnChange.md" data-raw-source="[addOnChange](attributes/addOnChange.md)">addOnChange</a></li>
<li><a href="attributes/fireOnChange.md" data-raw-source="[fireOnChange](attributes/fireOnChange.md)">fireOnChange</a></a></li>
<li><a href="attributes/getAttributeType.md" data-raw-source="[getAttributeType](attributes/getAttributeType.md)">getAttributeType</a></li>
<li><a href="attributes/getFormat.md" data-raw-source="[getFormat](attributes/getFormat.md)">getFormat</a></li>
<li><a href="attributes/getIsDirty.md" data-raw-source="[getIsDirty](attributes/getIsDirty.md)">getIsDirty</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="attributes/getName.md" data-raw-source="[getName](attributes/getName.md)">getName</a></li>
<li><a href="attributes/getParent.md" data-raw-source="[getParent](attributes/getParent.md)">getParent</a></li>
<li><a href="attributes/getRequiredLevel.md" data-raw-source="[getRequiredLevel](attributes/getRequiredLevel.md)">getRequiredLevel</a></li>
<li><a href="attributes/getSubmitMode.md" data-raw-source="[getSubmitMode](attributes/getSubmitMode.md)">getSubmitMode</a></li>
<li><a href="attributes/getUserPrivilege.md" data-raw-source="[getUserPrivilege](attributes/getUserPrivilege.md)">getUserPrivilege</a></li>
<li><a href="attributes/getValue.md" data-raw-source="[getValue](attributes/getValue.md)">getValue</a></li>
</ul>
</td>
<td>
<ul>

<li><a href="attributes/isValid.md" data-raw-source="[isValid](attributes/isValid.md)">isValid</a></li>
<li><a href="attributes/removeOnChange.md" data-raw-source="[removeOnChange](attributes/removeOnChange.md)">removeOnChange</a></li>
<li><a href="attributes/setRequiredLevel.md" data-raw-source="[setRequiredLevel](attributes/setRequiredLevel.md)">setRequiredLevel</a></li>
<li><a href="attributes/setSubmitMode.md" data-raw-source="[setSubmitMode](attributes/setSubmitMode.md)">setSubmitMode</a></li>
<li><a href="attributes/setValue.md" data-raw-source="[setValue](attributes/setValue.md)">setValue</a></li>
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
<li><a href="attributes/getInitialValue.md" data-raw-source="[getInitialValue](attributes/getInitialValue.md)">getInitialValue</a></li>
<li><a href="attributes/getOption.md" data-raw-source="[getOption](attributes/getOption.md)">getOption</a></li>
<li><a href="attributes/getOptions.md" data-raw-source="[getOptions](attributes/getOptions.md)">getOptions</a></a></li>
<li><a href="attributes/getSelectedOption.md" data-raw-source="[getSelectedOption](attributes/getSelectedOption.md)">getSelectedOption</a></li>
<li><a href="attributes/getText.md" data-raw-source="[getText](attributes/getText.md)">getText</a></li>
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
<li><a href="attributes/getMax.md" data-raw-source="[getMax](attributes/getMax.md)">getMax</a></li>
<li><a href="attributes/getMin.md" data-raw-source="[getMin](attributes/getMin.md)">getMin</a></li>
<li><a href="attributes/getPrecision.md" data-raw-source="[getPrecision](attributes/getPrecision.md)">getPrecision</a></a></li>
<li><a href="attributes/setPrecision.md" data-raw-source="[setPrecision](attributes/setPrecision.md)">setPrecision</a></li>
<li><a href="attributes/getText.md" data-raw-source="[getText](attributes/getText.md)">getText</a></li>
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




