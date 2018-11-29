---
title: モデル駆動型アプリの getAttribute (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 5ba037da-59f3-4e10-80f8-4e46d5410f81
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getattribute-client-api-reference"></a>getAttribute (クライアント API 参照)



コントロールがバインドされる属性を戻します。

属性にバインドされないコントロール (サブグリッド、Web リソース、および IFRAME) にはこのメソッドはありません。 これらのコントロールのいずれかでこのメソッドを使用しようとすると、エラーがスローされます。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

標準、検索、オプション セット

## <a name="syntax"></a>構文

`formContext.getControl(arg).getAttribute();`

## <a name="return-value"></a>戻り値

**種類**: オブジェクト

**説明**: 属性

## <a name="remarks"></a>備考

[簡易表示コントロール](../formContext-ui-quickForms.md) 内のコントロール コレクションには、構成コントロールが含まれ、これらのコントロールには **getAttribute** メソッドがあります。 ただし、その属性はエンティティの属性コレクションの一部ではありません。 その属性の値は [getValue](../attributes/getValue.md) を使用して取得し、[setValue](../attributes/setValue.md) を使用して変更することさえできますが、加えられた変更はエンティティで保存されません。
 
次のコードは、取引先担当者の **mobilephone** 属性が、**contactQuickForm** という名前の簡易表示コントロールを使用する取引先企業のエンティティ フォームに表示されるときに、その値を使用することを示します。 このコードは、属性値が **null** の場合にコントロールを非表示にします。

```JavaScript
var quickViewMobilePhoneControl = formContext.getControl("contactQuickForm_contactQuickForm_contact_mobilephone");
if (quickViewMobilePhoneControl.getAttribute().getValue() == null) {
    quickViewMobilePhoneControl.setVisible(false);
}
```


[簡易表示コントロール](../formContext-ui-quickForms.md)

[属性](../attributes.md)


