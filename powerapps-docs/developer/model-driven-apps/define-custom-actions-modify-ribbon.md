---
title: ユーザー定義のアクションによるリボンの変更を定義する (モデル駆動型アプリ) | MicrosoftDocs
description: リボンを修正するユーザー定義アクションについて学習します。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 72544b02-4eed-4d70-666e-a0d880f526af
author: JimDaly
ms.author: jdaly
manager: shilpas
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="define-custom-actions-to-modify-the-ribbon"></a>ユーザー定義のアクションによるリボンの変更

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/define-custom-actions-modify-ribbon -->

既定のアプリケーションのコマンド バーまたはリボンは Common Data Service メタデータによって定義されます。 既定のデータは変更できませんが、既定のリボンを上書きする特定のアクションの定義を指定できます。  
  
## <a name="types-of-custom-actions"></a>ユーザー定義アクションの種類  
 リボンに対するユーザー定義アクションには、次の 2 種類があります。  
  
- `<CustomAction>`: [!INCLUDE[ribbon_element_CustomAction](../../includes/ribbon-element-customaction.md)]  
  
- `<HideCustomAction>` : [!INCLUDE[ribbon_element_HideCustomAction](../../includes/ribbon-element-hidecustomaction.md)]  
  
### <a name="custom-actions"></a>ユーザー定義アクション  
 ユーザー定義アクションは、既定のリボン定義をどのように変更するかを指定するステートメントです。 実行時に評価され、リボンに適用されます。 ユーザー定義アクションのコンテキストを設定するには、変更するアイテムの場所に関する情報を指定する必要があります。 変更の適用場所を指定するには、`Location` 属性を使用します。  
  
 新しいリボン要素を追加する場合は、既存のタブやグループなどの親要素を参照します。 その後、接尾辞 `._children` を使用して、このユーザー定義アクションによって既存のアイテムに何かが追加されることを示します。  
  
 既存のアイテムの定義を変更する場合は、変更するアイテムの ID と `Location` 値を一致させます。  
  
 さらに、ユーザー定義アクションの一意の ID を指定する必要があります。 この値を設定するには **Id** 属性を使用します。 値が一意であることを保証する命名規則を使用することを強くお勧めします。 整合性と可読性を保つため、一貫性のある構成要素をピリオドを使用して分割することをお勧めします。 命名規則の最初のアイテムは、ソリューション発行者またはソリューションに関連するものにします (例: `Contoso.contact.form.CustomButton.CustomAction`)。  
  
> [!TIP]
>  命名規則の `Id` 属性を一貫して適用すると、RibbonDiffXml 編集時の生産性が大幅に向上します。  
  
 指定された場所情報に基づいて、`Sequence` 属性値により、アイテムの表示順序が決定されます。 2 つの既存のコントロールの間にカスタム コントロールを表示する場合は、既存のアイテムのシーケンス値の間にあるシーケンス値を選択する必要があります。  
  
### <a name="hide-custom-actions"></a>ユーザー定義アクションを非表示にする  
 `<HideCustomAction>` は、既存のリボン要素を削除して表示されないようにする場合に使用するステートメントです。 これはリボン要素を非表示にするのではなく、実行時にリボン要素を実際に削除して、リボン内に存在しないようにします。  
  
> [!NOTE]
>  `HideCustomAction` 要素は指定されたノードをリボンから削除するため、この方法によるリボン要素の削除は、あらゆる状況に適した選択肢ではない可能性があります。  
> 
> - 特定の特権に関連付けられているボタンを削除する場合は、実装のセキュリティ ロールのエンティティに対する特権を調整する必要があります。 これにより、既定のリボンの表示と、アクションを実行するために必要な特権を持っていないユーザーに対してリボン要素を非表示または無効化するためのルールの設定が可能になります。  
>   -   既存のリボン要素をユーザー定義要素に置き換える場合は、既存の要素と同一の `CustomAction.Location` 値を指定することでその要素を上書きできます。  
  
 **HideActionId** 要素は、アクションの一意の ID を提供します。 整合性と可読性を保つため、`<CustomAction>` 要素で説明した命名規則に従います。 **Location** 属性は、削除するリボン要素の ID と一致させる必要があります。  
  
### <a name="see-also"></a>関連項目  
 [コマンド、およびリボンをカスタマイズする](customize-commands-ribbon.md)   
 [データをページからパラメーターとしてリボン操作に渡す](/dynamics365/customer-engagement/developer/customize-dev/pass-dynamics-365-data-page-parameter-ribbon-actions)<br/>   <!-- TODO need to update the relevant PowerApps repo link-->
 [リボン要素のスケーリングの定義](define-scaling-ribbon-elements.md)
