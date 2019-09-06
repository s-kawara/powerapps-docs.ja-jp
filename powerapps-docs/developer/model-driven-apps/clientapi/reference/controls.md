---
title: Dynamics 365 におけるモデル駆動型アプリのコントロール | MicrosoftDocs
ms.date: 08/12/2019
ms.service: powerapps
ms.topic: reference
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
<li><a href="controls/addNotification.md" data-raw-source="[addNotification](controls/addNotification.md)">addNotification</a></li>
<li><a href="controls/clearNotification.md" data-raw-source="[clearNotification](controls/clearNotification.md)">clearNotification</a></li>
<li><a href="controls/getAttribute.md" data-raw-source="[getAttribute](controls/getAttribute.md)">getAttribute</a></a></li>
<li><a href="controls/getControlType.md" data-raw-source="[getControlType](controls/getControlType.md)">getControlType</a></li>
<li><a href="controls/getDisabled.md" data-raw-source="[getDisabled](controls/getDisabled.md)">getDisabled</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="controls/getLabel.md" data-raw-source="[getLabel](controls/getLabel.md)">getLabel</a></li>
<li><a href="controls/getName.md" data-raw-source="[getName](controls/getName.md)">getName</a></li>
<li><a href="controls/getParent.md" data-raw-source="[getParent](controls/getParent.md)">getParent</a></li>
<li><a href="controls/getVisible.md" data-raw-source="[getVisible](controls/getVisible.md)">getVisible</a></li>
<li><a href="controls/setDisabled.md" data-raw-source="[setDisabled](controls/setDisabled.md)">setDisabled</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="controls/setFocus.md" data-raw-source="[setFocus](controls/setFocus.md)">setFocus</a></li>
<li><a href="controls/setLabel.md" data-raw-source="[setLabel](controls/setLabel.md)">setLabel</a></li>
<li><a href="controls/setNotification.md" data-raw-source="[setNotification](controls/setNotification.md)">setNotification</a></li>
<li><a href="controls/setVisible.md" data-raw-source="[setVisible](controls/setVisible.md)">setVisible</a></li>
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
<li><a href="controls/getControlType.md" data-raw-source="[getControlType](controls/getControlType.md)">getControlType</a></li>
<li><a href="controls/getDisabled.md" data-raw-source="[getDisabled](controls/getDisabled.md)">getDisabled</a></li>
<li><a href="controls/getInitialUrl.md" data-raw-source="[getInitialUrl](controls/getInitialUrl.md)">getInitialUrl</a></li>
<li><a href="controls/getLabel.md" data-raw-source="[getLabel](controls/getLabel.md)">getLabel</a></li>
<li><a href="controls/getName.md" data-raw-source="[getName](controls/getName.md)">getName</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="controls/getObject.md" data-raw-source="[getObject](controls/getObject.md)">getObject</a></li>
<li><a href="controls/getParent.md" data-raw-source="[getParent](controls/getParent.md)">getParent</a></li>
<li><a href="controls/getSrc.md" data-raw-source="[getSrc](controls/getSrc.md)">getSrc</a></li>
<li><a href="controls/getVisible.md" data-raw-source="[getVisible](controls/getVisible.md)">getVisible</a></li>
<li><a href="controls/setDisabled.md" data-raw-source="[setDisabled](controls/setDisabled.md)">setDisabled</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="controls/setFocus.md" data-raw-source="[setFocus](controls/setFocus.md)">setFocus</a></li>
<li><a href="controls/setLabel.md" data-raw-source="[setLabel](controls/setLabel.md)">setLabel</a></li>
<li><a href="controls/setSrc.md" data-raw-source="[setSrc](controls/setSrc.md)">setSrc</a></li>
<li><a href="controls/setVisible.md" data-raw-source="[setVisible](controls/setVisible.md)">setVisible</a></li>
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
<li><a href="controls/addOnPostSearch.md" data-raw-source="[addOnPostSearch](controls/addOnPostSearch.md)">addOnPostSearch</a></li>
<li><a href="controls/addOnResultOpened.md" data-raw-source="[addOnResultOpened](controls/addOnResultOpened.md)">addOnResultOpened</a></li>
<li><a href="controls/addOnSelection.md" data-raw-source="[addOnSelection](controls/addOnSelection.md)">addOnSelection</a></li>
<li><a href="controls/getControlType.md" data-raw-source="[getControlType](controls/getControlType.md)">getControlType</a></li>
<li><a href="controls/getDisabled.md" data-raw-source="[getDisabled](controls/getDisabled.md)">getDisabled</a></li>
<li><a href="controls/getLabel.md" data-raw-source="[getLabel](controls/getLabel.md)">getLabel</a></li>
<li><a href="controls/getName.md" data-raw-source="[getName](controls/getName.md)">getName</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="controls/getParent.md" data-raw-source="[getParent](controls/getParent.md)">getParent</a></li>
<li><a href="controls/getSearchQuery.md" data-raw-source="[getSearchQuery](controls/getSearchQuery.md)">getSearchQuery</a></li>
<li><a href="controls/getSelectedResults.md" data-raw-source="[getSelectedResults](controls/getSelectedResults.md)">getSelectedResults</a></li>
<li><a href="controls/getTotalResultCount.md" data-raw-source="[getTotalResultCount](controls/getTotalResultCount.md)">getTotalResultCount</a></li>
<li><a href="controls/getVisible.md" data-raw-source="[getVisible](controls/getVisible.md)">getVisible</a></li>
<li><a href="controls/openSearchResult.md" data-raw-source="[openSearchResult](controls/openSearchResult.md)">openSearchResult</a></li>
<li><a href="controls/removeOnPostSearch.md" data-raw-source="[removeOnPostSearch](controls/removeOnPostSearch.md)">removeOnPostSearch</a></li>

</ul>
</td>
<td>
<ul>
<li><a href="controls/removeOnResultOpened.md" data-raw-source="[removeOnResultOpened](controls/removeOnResultOpened.md)">removeOnResultOpened</a></li>
<li><a href="controls/removeOnSelection.md" data-raw-source="[removeOnSelection](controls/removeOnSelection.md)">removeOnSelection</a></li>
<li><a href="controls/setFocus.md" data-raw-source="[setFocus](controls/setFocus.md)">setFocus</a></li>
<li><a href="controls/setLabel.md" data-raw-source="[setLabel](controls/setLabel.md)">setLabel</a></li>
<li><a href="controls/setSearchQuery.md" data-raw-source="[setSearchQuery](controls/setSearchQuery.md)">setSearchQuery</a></li>
<li><a href="controls/setVisible.md" data-raw-source="[setVisible](controls/setVisible.md)">setVisible</a></li>
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
<li><a href="controls/addCustomFilter.md" data-raw-source="[addCustomFilter](controls/addCustomFilter.md)">addCustomFilter</a></li>
<li><a href="controls/addCustomView.md" data-raw-source="[addCustomView](controls/addCustomView.md)">addCustomView</a></li>
<li><a href="controls/addNotification.md" data-raw-source="[addNotification](controls/addNotification.md)">addNotification</a></li>
<li><a href="controls/addPreSearch.md" data-raw-source="[addPreSearch](controls/addPreSearch.md)">addPreSearch</a></li>
<li><a href="controls/clearNotification.md" data-raw-source="[clearNotification](controls/clearNotification.md)">clearNotification</a></li>
<li><a href="controls/getAttribute.md" data-raw-source="[getAttribute](controls/getAttribute.md)">getAttribute</a></a></li>
<li><a href="controls/getControlType.md" data-raw-source="[getControlType](controls/getControlType.md)">getControlType</a></li>
<li><a href="controls/getDefaultView.md" data-raw-source="[getDefaultView](controls/getDefaultView.md)">getDefaultView</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="controls/getDisabled.md" data-raw-source="[getDisabled](controls/getDisabled.md)">getDisabled</a></li>
<li><a href="controls/getEntityTypes.md" data-raw-source="[getEntityTypes](controls/getEntityTypes.md)">getEntityTypes</a></li>
<li><a href="controls/getLabel.md" data-raw-source="[getLabel](controls/getLabel.md)">getLabel</a></li>
<li><a href="controls/getName.md" data-raw-source="[getName](controls/getName.md)">getName</a></li>
<li><a href="controls/getParent.md" data-raw-source="[getParent](controls/getParent.md)">getParent</a></li>
<li><a href="controls/getVisible.md" data-raw-source="[getVisible](controls/getVisible.md)">getVisible</a></li>
<li><a href="controls/removePreSearch.md" data-raw-source="[removePreSearch](controls/removePreSearch.md)">removePreSearch</a></li>
<li><a href="controls/setDefaultView.md" data-raw-source="[setDefaultView](controls/setDefaultView.md)">setDefaultView</a></li>

</ul>
</td>
<td>
<ul>
<li><a href="controls/setDisabled.md" data-raw-source="[setDisabled](controls/setDisabled.md)">setDisabled</a></li>
<li><a href="controls/setEntityTypes.md" data-raw-source="[setEntityTypes](controls/setEntityTypes.md)">setEntityTypes</a></li>
<li><a href="controls/setFocus.md" data-raw-source="[setFocus](controls/setFocus.md)">setFocus</a></li>
<li><a href="controls/setLabel.md" data-raw-source="[setLabel](controls/setLabel.md)">setLabel</a></li>
<li><a href="controls/setNotification.md" data-raw-source="[setNotification](controls/setNotification.md)">setNotification</a></li>
<li><a href="controls/setVisible.md" data-raw-source="[setVisible](controls/setVisible.md)">setVisible</a></li>
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
<li><a href="controls/addNotification.md" data-raw-source="[addNotification](controls/addNotification.md)">addNotification</a></li>
<li><a href="controls/addOption.md" data-raw-source="[addOption](controls/addOption.md)">addOption</a></li>
<li><a href="controls/clearNotification.md" data-raw-source="[clearNotification](controls/clearNotification.md)">clearNotification</a></li>
<li><a href="controls/clearOptions.md" data-raw-source="[clearOptions](controls/clearOptions.md)">clearOptions</a></li>
<li><a href="controls/getAttribute.md" data-raw-source="[getAttribute](controls/getAttribute.md)">getAttribute</a></a></li>
<li><a href="controls/getControlType.md" data-raw-source="[getControlType](controls/getControlType.md)">getControlType</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="controls/getDisabled.md" data-raw-source="[getDisabled](controls/getDisabled.md)">getDisabled</a></li>
<li><a href="controls/getLabel.md" data-raw-source="[getLabel](controls/getLabel.md)">getLabel</a></li>
<li><a href="controls/getName.md" data-raw-source="[getName](controls/getName.md)">getName</a></li>
<li><a href="controls/getOptions.md" data-raw-source="[getOptions](controls/getOptions.md)">getOptions</a></li>
<li><a href="controls/getParent.md" data-raw-source="[getParent](controls/getParent.md)">getParent</a></li>
<li><a href="controls/getVisible.md" data-raw-source="[getVisible](controls/getVisible.md)">getVisible</a></li>

</ul>
</td>
<td>
<ul>
<li><a href="controls/removeoption.md" data-raw-source="[removeOption](controls/removeoption.md)">removeOption</a></li>
<li><a href="controls/setDisabled.md" data-raw-source="[setDisabled](controls/setDisabled.md)">setDisabled</a></li>
<li><a href="controls/setFocus.md" data-raw-source="[setFocus](controls/setFocus.md)">setFocus</a></li>
<li><a href="controls/setLabel.md" data-raw-source="[setLabel](controls/setLabel.md)">setLabel</a></li>
<li><a href="controls/setNotification.md" data-raw-source="[setNotification](controls/setNotification.md)">setNotification</a></li>
<li><a href="controls/setVisible.md" data-raw-source="[setVisible](controls/setVisible.md)">setVisible</a></li>

</ul>
</td>
</tr>
</table>

## <a name="quickform-control-type"></a>quickformコントロールタイプ

このコントロールタイプでサポートされているメソッドの情報については、「 [formContext.ui.quickForms](formcontext-ui-quickforms.md) 」を参照してください。

## <a name="subgrid-control-type"></a>サブグリッド コントロールタイプ

このコントロールタイプでサポートされているメソッドの情報については、 [グリッドおよびサブグリッド](grids.md) を参照してください。

## <a name="timelinewall-control-type"></a>timelinewallコントロールタイプ

タイムライン コントロールは、1本化したビューで投稿、活動およびメモを表示する、Dynamics 365 for Customer Engagement アプリ バージョン9.0に導入された新しいコントロールタイプです。 これらはこのコントロールタイプに使用可能なメソッドです。

<table>
<tr>
<td>
<ul>
<li><a href="controls/getControlType.md" data-raw-source="[getControlType](controls/getControlType.md)">getControlType</a></li>
<li><a href="controls/getDisabled.md" data-raw-source="[getDisabled](controls/getDisabled.md)">getDisabled</a></li>
<li><a href="controls/getLabel.md" data-raw-source="[getLabel](controls/getLabel.md)">getLabel</a></li>
<li><a href="controls/getName.md" data-raw-source="[getName](controls/getName.md)">getName</a></li>
</ul>
</td>
<td>
<ul>

<li><a href="controls/getParent.md" data-raw-source="[getParent](controls/getParent.md)">getParent</a></li>
<li><a href="controls/getVisible.md" data-raw-source="[getVisible](controls/getVisible.md)">getVisible</a></li>
<li><a href="controls/refresh.md" data-raw-source="[refresh](controls/refresh.md)">最新の情報に更新</a></li>
<li><a href="controls/setDisabled.md" data-raw-source="[setDisabled](controls/setDisabled.md)">setDisabled</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="controls/setFocus.md" data-raw-source="[setFocus](controls/setFocus.md)">setFocus</a></li>
<li><a href="controls/setLabel.md" data-raw-source="[setLabel](controls/setLabel.md)">setLabel</a></li>
<li><a href="controls/setVisible.md" data-raw-source="[setVisible](controls/setVisible.md)">setVisible</a></li>
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
<li><a href="controls/getControlType.md" data-raw-source="[getControlType](controls/getControlType.md)">getControlType</a></li>
<li><a href="controls/getDisabled.md" data-raw-source="[getDisabled](controls/getDisabled.md)">getDisabled</a></li>
<li><a href="controls/getLabel.md" data-raw-source="[getLabel](controls/getLabel.md)">getLabel</a></li>
<li><a href="controls/getName.md" data-raw-source="[getName](controls/getName.md)">getName</a></li>
</ul>
</td>
<td>
<ul>

<li><a href="controls/getParent.md" data-raw-source="[getParent](controls/getParent.md)">getParent</a></li>
<li><a href="controls/getState.md" data-raw-source="[getState](controls/getState.md)">getState</a></li>
<li><a href="controls/getVisible.md" data-raw-source="[getVisible](controls/getVisible.md)">getVisible</a></li>
<li><a href="controls/refresh.md" data-raw-source="[refresh](controls/refresh.md)">最新の情報に更新</a></li>

</ul>
</td>
<td>
<ul>
<li><a href="controls/setDisabled.md" data-raw-source="[setDisabled](controls/setDisabled.md)">setDisabled</a></li>
<li><a href="controls/setFocus.md" data-raw-source="[setFocus](controls/setFocus.md)">setFocus</a></li>
<li><a href="controls/setLabel.md" data-raw-source="[setLabel](controls/setLabel.md)">setLabel</a></li>
<li><a href="controls/setVisible.md" data-raw-source="[setVisible](controls/setVisible.md)">setVisible</a></li>
</ul>
</td>
</tr>
</table>

## <a name="webresource-control-type"></a>Web リソース コントロールタイプ

Webリソース コントロールには、IFRAMEコントロールでも利用可能な同じメソッド セットがあります。 See [IFRAME コントロールの種類](#iframe-control-type)を参照してください


### <a name="related-topics"></a>関連トピック

[属性](attributes.md)
