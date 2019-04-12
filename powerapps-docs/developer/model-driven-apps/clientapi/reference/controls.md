---
title: Dynamics 365 におけるモデル駆動型アプリのコントロール | MicrosoftDocs
ms.date: 10/31/2018
ms.service: powerapps
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="controls-client-api-reference"></a>コントロール (クライアント API 参照)



コントロールは、フォームに表示される HTML 要素を表します。 コントロールには特定の属性にバインドされるものもありますが、IFRAME、Web リソース、またはフォームに追加されたサブグリッドなど、バインドされないコントロールを表すものもあります。 

**コントロール**オブジェクトには、コントロールの表示や動作を変更して、対応する属性を指定する方法が用意されています。 以下のコレクションのいずれかを使用してコントロールにアクセスします: 
- **formContext.ui.controls**
- **formContext.ui Section.controls**
- **formContext.data.entity** **Attribute.controls**

**formContext**.[getControl](controls/getControl.md) メソッドは、 **formContext.ui.controls.get** にアクセスするためのショートカット メソッドです。 

コントロールは、種類によって分類されます。 [getControlType](controls/getControlType.md) メソッドを使用すると、コントロールの種類を判別できます。 特定のコントロールのメソッドは、特定の種類のコントロールでのみ利用できます。

このトピックでは、コントロールタイプごとに使用できるメソッドについて説明します。 

## <a name="standard-control-type"></a>標準コントロールタイプ

これらは標準コントロールで使用可能なメソッドです。

<table>
<tr>
<td>
<ul>
<li>[addNotification](controls/addNotification.md)</li>
<li>[clearNotification](controls/clearNotification.md)</li>
<li>[getAttribute](controls/getAttribute.md)</a></li>
<li>[getControlType](controls/getControlType.md)</li>
<li>[getDisabled](controls/getDisabled.md)</li>
</ul>
</td>
<td>
<ul>
<li>[getLabel](controls/getLabel.md)</li>
<li>[getName](controls/getName.md)</li>
<li>[getParent](controls/getParent.md)</li>
<li>[getVisible](controls/getVisible.md)</li>
<li>[setDisabled](controls/setDisabled.md)</li>
</ul>
</td>
<td>
<ul>
<li>[setFocus](controls/setFocus.md)</li>
<li>[setLabel](controls/setLabel.md)</li>
<li>[setNotification](controls/setNotification.md)</li>
<li>[setVisible](controls/setVisible.md)</li>
</ul>
</td>
</tr>
</table>

標準コントロールの次のメソッドは、このリリースの [廃止済](/dynamics365/get-started/whats-new/customer-engagement/important-changes-coming#some-client-apis-are-deprecated) にあります: addOnKeyPress、fireOnKeyPress および removeOnKeyPress。

## <a name="iframe-control-type"></a>IFRAME コントロールタイプ

これらはIFRAMEコントロールで使用可能なメソッドです。

<table>
<tr>
<td>
<ul>
<li>[getControlType](controls/getControlType.md)</li>
<li>[getDisabled](controls/getDisabled.md)</li>
<li>[getInitialUrl](controls/getInitialUrl.md)</li>
<li>[getLabel](controls/getLabel.md)</li>
<li>[getName](controls/getName.md)</li>
</ul>
</td>
<td>
<ul>
<li>[getObject](controls/getObject.md)</li>
<li>[getParent](controls/getParent.md)</li>
<li>[getSrc](controls/getSrc.md)</li>
<li>[getVisible](controls/getVisible.md)</li>
<li>[setDisabled](controls/setDisabled.md)</li>
</ul>
</td>
<td>
<ul>
<li>[setFocus](controls/setFocus.md)</li>
<li>[setLabel](controls/setLabel.md)</li>
<li>[setSrc](controls/setSrc.md)</li>
<li>[setVisible](controls/setVisible.md)</li>
</ul>
</td>
</tr>
</table>

## <a name="kbsearch-knowledge-base-search-control-type"></a>kbsearch(サポート情報検索コントロール)タイプ

これらはサポート情報検索コントロールに使用可能なメソッドです。

<table>
<tr>
<td>
<ul>
<li>[addOnPostSearch](controls/addOnPostSearch.md)</li>
<li>[addOnResultOpened](controls/addOnResultOpened.md)</li>
<li>[addOnSelection](controls/addOnSelection.md)</li>
<li>[getControlType](controls/getControlType.md)</li>
<li>[getDisabled](controls/getDisabled.md)</li>
<li>[getLabel](controls/getLabel.md)</li>
<li>[getName](controls/getName.md)</li>
</ul>
</td>
<td>
<ul>
<li>[getParent](controls/getParent.md)</li>
<li>[getSearchQuery](controls/getSearchQuery.md)</li>
<li>[getSelectedResults](controls/getSelectedResults.md)</li>
<li>[getTotalResultCount](controls/getTotalResultCount.md)</li>
<li>[getVisible](controls/getVisible.md)</li>
<li>[openSearchResult](controls/openSearchResult.md)</li>
<li>[removeOnPostSearch](controls/removeOnPostSearch.md)</li>

</ul>
</td>
<td>
<ul>
<li>[removeOnResultOpened](controls/removeOnResultOpened.md)</li>
<li>[removeOnSelection](controls/removeOnSelection.md)</li>
<li>[setFocus](controls/setFocus.md)</li>
<li>[setLabel](controls/setLabel.md)</li>
<li>[setSearchQuery](controls/setSearchQuery.md)</li>
<li>[setVisible](controls/setVisible.md)</li>
</ul>
</td>
</tr>
</table>

>[!NOTE]
>サポート情報の検索コントロールがソーシャル ウィンドウに追加されると、そのコントロール名前は "searchwidgetcontrol_notescontrol" となります。 この名前は変更できません。 

## <a name="lookup-control-type"></a>検索コントロールタイプ

これらは検索コントロールで使用可能なメソッドです。

<table>
<tr>
<td>
<ul>
<li>[addCustomFilter](controls/addCustomFilter.md)</li>
<li>[addCustomView](controls/addCustomView.md)</li>
<li>[addNotification](controls/addNotification.md)</li>
<li>[addPreSearch](controls/addPreSearch.md)</li>
<li>[clearNotification](controls/clearNotification.md)</li>
<li>[getAttribute](controls/getAttribute.md)</a></li>
<li>[getControlType](controls/getControlType.md)</li>
<li>[getDefaultView](controls/getDefaultView.md)</li>
</ul>
</td>
<td>
<ul>
<li>[getDisabled](controls/getDisabled.md)</li>
<li>[getEntityTypes](controls/getEntityTypes.md)</li>
<li>[getLabel](controls/getLabel.md)</li>
<li>[getName](controls/getName.md)</li>
<li>[getParent](controls/getParent.md)</li>
<li>[getVisible](controls/getVisible.md)</li>
<li>[removePreSearch](controls/removePreSearch.md)</li>
<li>[setDefaultView](controls/setDefaultView.md)</li>

</ul>
</td>
<td>
<ul>
<li>[setDisabled](controls/setDisabled.md)</li>
<li>[setEntityTypes](controls/setEntityTypes.md)</li>
<li>[setFocus](controls/setFocus.md)</li>
<li>[setLabel](controls/setLabel.md)</li>
<li>[setNotification](controls/setNotification.md)</li>
<li>[setVisible](controls/setVisible.md)</li>
</ul>
</td>
</tr>
</table>

## <a name="multiselectoptionset-and-optionset-control-types"></a>multiSelectOptionSet および optionSet コントロールタイプ

複数選択オプション セットおよびオプション セットコントロールの両方には、利用可能な同じメソッド セットがあります。

<table>
<tr>
<td>
<ul>
<li>[addNotification](controls/addNotification.md)</li>
<li>[addOption](controls/addOption.md)</li>
<li>[clearNotification](controls/clearNotification.md)</li>
<li>[clearOptions](controls/clearOptions.md)</li>
<li>[getAttribute](controls/getAttribute.md)</a></li>
<li>[getControlType](controls/getControlType.md)</li>
</ul>
</td>
<td>
<ul>
<li>[getDisabled](controls/getDisabled.md)</li>
<li>[getLabel](controls/getLabel.md)</li>
<li>[getName](controls/getName.md)</li>
<li>[getParent](controls/getParent.md)</li>
<li>[getVisible](controls/getVisible.md)</li>
<li>[removeOption](controls/removeoption.md)</li>
</ul>
</td>
<td>
<ul>
<li>[setDisabled](controls/setDisabled.md)</li>
<li>[setFocus](controls/setFocus.md)</li>
<li>[setLabel](controls/setLabel.md)</li>
<li>[setNotification](controls/setNotification.md)</li>
<li>[setVisible](controls/setVisible.md)</li>
</ul>
</td>
</tr>
</table>

## <a name="quickform-control-type"></a>quickformコントロールタイプ

このコントロールタイプでサポートされているメソッドの情報については、「 [formContext.ui.quickForms](formcontext-ui-quickforms.md) 」を参照してください。

## <a name="subgrid-control-type"></a>サブグリッド コントロールタイプ

このコントロールタイプでサポートされているメソッドの情報については、 [グリッドおよびサブグリッド](grids.md) を参照してください。

## <a name="timelinewall-control-type"></a>timelinewallコントロールタイプ

タイムライン コントロールは、1 本化したビューで投稿、活動およびメモを表示する、モデル駆動型アプリ (オンライン) バージョン 9.0 に導入された新しいコントロールタイプです。 これらはこのコントロールタイプに使用可能なメソッドです。

<table>
<tr>
<td>
<ul>
<li>[getControlType](controls/getControlType.md)</li>
<li>[getDisabled](controls/getDisabled.md)</li>
<li>[getLabel](controls/getLabel.md)</li>
<li>[getName](controls/getName.md)</li>
</ul>
</td>
<td>
<ul>

<li>[getParent](controls/getParent.md)</li>
<li>[getVisible](controls/getVisible.md)</li>
<li>[最新の情報に更新](controls/refresh.md)</li>
<li>[setDisabled](controls/setDisabled.md)</li>
</ul>
</td>
<td>
<ul>
<li>[setFocus](controls/setFocus.md)</li>
<li>[setLabel](controls/setLabel.md)</li>
<li>[setVisible](controls/setVisible.md)</li>
</ul>
</td>
</tr>
</table>

## <a name="timer-control-type"></a>タイマー コントロールタイプ

これらはタイマー コントロールに使用可能なメソッドです。

<table>
<tr>
<td>
<ul>
<li>[getControlType](controls/getControlType.md)</li>
<li>[getDisabled](controls/getDisabled.md)</li>
<li>[getLabel](controls/getLabel.md)</li>
<li>[getName](controls/getName.md)</li>
</ul>
</td>
<td>
<ul>

<li>[getParent](controls/getParent.md)</li>
<li>[getState](controls/getState.md)</li>
<li>[getVisible](controls/getVisible.md)</li>
<li>[最新の情報に更新](controls/refresh.md)</li>

</ul>
</td>
<td>
<ul>
<li>[setDisabled](controls/setDisabled.md)</li>
<li>[setFocus](controls/setFocus.md)</li>
<li>[setLabel](controls/setLabel.md)</li>
<li>[setVisible](controls/setVisible.md)</li>
</ul>
</td>
</tr>
</table>

## <a name="webresource-control-type"></a>Web リソース コントロールタイプ

Webリソース コントロールには、IFRAMEコントロールでも利用可能な同じメソッド セットがあります。 See [IFRAME コントロールの種類](#iframe-control-type)を参照してください

### <a name="related-topics"></a>関連トピック

[属性](attributes.md)