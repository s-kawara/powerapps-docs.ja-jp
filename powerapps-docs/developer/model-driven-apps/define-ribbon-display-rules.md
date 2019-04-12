---
title: リボン表示ルールを定義する (モデル駆動型アプリ) | MicrosoftDocs
description: 'リボン要素の構成中にそのリボン要素をいつ表示するかを制御する、特定のルールを定義することについて学習します。 '
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 70e5687f-4d0e-3d43-03f3-10e5aa5b0713
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

# <a name="define-ribbon-display-rules"></a>リボンの表示ルールの定義

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/define-ribbon-display-rules -->

リボン要素を構成する場合は、そのリボン要素をいつ表示するかを制御する特定のルールを定義できます。  

-   リボン要素をいつ表示する必要があるかを制御するルールを定義するには、/`RuleDefinitions`/DisplayRules/`<DisplayRule>` 要素を使用します。  

-   コマンド定義に対して特定の表示ルールを関連付けるには、/CommandDefinitions/`CommandDefinition`/DisplayRules/`<DisplayRule>` 要素を使用します。  

## <a name="control-when-ribbon-elements-are-displayed"></a>リボン要素をいつ表示するかの制御  
 ルール定義と一緒に定義することで、同じ表示ルールを複数のコマンド定義で使用できます。 1 つのコマンド定義に対して複数の表示ルールを定義した場合、表示するリボン要素に対してすべての表示ルールを true と評価する必要があります。  

 すべての表示ルールには、ルールの既定値が true か false かを指定するための属性、およびテスト対象のアイテムが true を返す場合に負の結果を返せるようにするための `InvertResult` 属性があります。どちらの属性も省略可能です。  

 `/RuleDefinitions/DisplayRules/DisplayRule` 要素では、次の種類のルールがサポートされています。  

 `<CommandClientTypeRule>`  
[!INCLUDE[ribbon_element_CommandClientTypeRule](../../includes/ribbon-element-commandclienttyperule.md)]

 `Type` の値は、次に対応します。  


|   Value   |                                                                               プレゼンテーション                                                                               |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Modern`  |                                       コマンド バーは、Dynamics 365 for tablets を使用して表示されます。                                       |
| `Refresh` |                                                      コマンド バーは、更新されたユーザー インターフェイスを使用して表示されます。                                                      |
| `Legacy`  | リボンは、更新されなかったエンティティのフォーム、または Dynamics 365 for Outlook のリスト ビューで表示されます。 |

 `<CrmClientTypeRule>`  
 使用されるクライアントの種類に応じてルールを定義できます。 `Type` のオプションは次のとおりです。  

- Web  

- Outlook  

  `<CrmOfflineAccessStateRule>`  
  この条件は、オフライン アクセス対応 Dynamics 365 for Microsoft Office Outlook が現在オフラインであるかどうかに基づいてリボン要素を表示する場合に使用します。  

  `<CrmOutlookClientTypeRule>`  
  特定の種類の Dynamics 365 for Outlook でボタンを表示する場合は、このルールを使用します。 `Type` のオプションは次のとおりです。  

- CrmForOutlook  

- CrmForOutlookOfflineAccess  

  `<CrmOutlookClientVersionRule>`  
  [!INCLUDE[ribbon_element_CrmOutlookClientVersionRule](../../includes/ribbon-element-crmoutlookclientversionrule.md)]

  有効な値:  

- 2003  

- 2007  

- 2010  

  `<EntityPrivilegeRule>`  
  この種類のルールは、エンティティに対する特定の特権がユーザーにある場合にリボン要素を表示するために使用します。 特権の階層および確認する特権を指定する必要があります。  

  `<EntityPropertyRule>`  
  特定のエンティティのプロパティのブール値に応じたルールの定義が可能です。 `PropertyName` のオプションは次のとおりです。  

- DuplicateDetectionEnabled  

- GridFiltersEnabled  

- HasStateCode  

- IsConnectionsEnabled  

- MailMergeEnabled  

- WorksWithQueue  

- HasActivities  

- IsActivity  

- HasNotes  

  `<EntityRule>`  
  エンティティ ルールでは、現在のエンティティを評価できます。 これは、特定のエンティティではなくエンティティ テンプレートに適用するユーザー定義のアクションを定義する場合に有効です。 たとえば、一部の特定のエンティティを除くすべてのエンティティへのリボン要素の追加が必要な場合があります。 この場合、すべてのエンティティに適用するエンティティ テンプレート用のユーザー定義のアクションを定義してから、除外する必要のあるアクションをエンティティ ルールを使用して除外すると簡単です。  

  また、エンティティ ルールには、フォームまたはリストにエンティティが表示されるかどうかを指定するための省略可能なコンテキスト属性 (HomePageGrid) が含まれています。 省略可能な `AppliesTo` 属性を `PrimaryEntity` または `SelectedEntity` に設定すると、エンティティがサブグリッドに表示されているかどうかを識別できます。  

  `<FormEntityContextRule>`  
  [!INCLUDE[ribbon_element_FormEntityContextRule](../../includes/ribbon-element-formentitycontextrule.md)]

  `<FormStateRule`  
  フォーム状態ルールは、レコードを表示している現在のフォームの種類を判断する場合に使用します。 `State` のオプションは次のとおりです。  

- 作成​​  

- 既存  

- 読み取り専用  

- 無効化  

- BulkEdit  

  `<FormTypeRule>`  
  [!INCLUDE[ribbon_element_FormTypeRule](../../includes/ribbon-element-formtyperule.md)]

  `Type` の値は、次に対応します。  

|Value|プレゼンテーション|  
|-----------|------------------|  
|`Main`|アプリケーションに表示されるエンティティ フォーム。|  
|`Preview`|グリッドの展開要素として表示されるエンティティ プレビュー フォーム。|  
|`AppointmentBook`|サービス スケジュール ユーザー インターフェイスに appointment、equipment、serviceappointment、および systemuser エンティティを使用します。|  
|`Dashboard`|ダッシュボードはフォームを定義します。|  
|`Quick`|簡易表示フォーム。|  
|`QuickCreate`|簡易作成フォーム。|  

 `<HideForTabletExperienceRule>`  
 [!INCLUDE[ribbon_element_HideForTabletExperienceRule](../../includes/ribbon-element-hidefortabletexperiencerule.md)]

 `<MiscellaneousPrivilegeRule>`  
 この種類のルールは、特定のエンティティに適用しない特権 (ExportToExcel、MailMerge、または GoOffline など) を確認する場合に使用します。  

 `<OrganizationSettingRule>`  
 このルールは、組織の特定の設定が有効な場合にリボン要素を表示するために使用します。 Setting のオプションは次のとおりです。  

- IsSharepointEnabled  

- IsSOPIntegrationEnabled  

- IsFiscalCalendarDefined  

  `<OrRule>`このルールを使用すると、複数の表示ルールの種類に対する既定の AND による比較を無効にすることができます。 確認のために使用可能な複数の有効な結合を定義するには、`OrRule` 要素を使用します。  

  `<OutlookRenderTypeRule>`  
  リボンが [!INCLUDE[pn_MS_Outlook_Short](../../includes/pn-ms-outlook-short.md)] に特定の方法で表示される場合に、これを使用してリボン要素を表示します。 `Type` のオプションは次のとおりです。  

- Web  

- Outlook  

  `<OutlookVersionRule>`  
  このルールは、特定のバージョンの Outlook のリボン要素を表示する場合に使用します。 `Version` のオプションは次のとおりです。  

- 2003  

- 2007  

- 2010  

  `<PageRule>`  
  この種類のルールでは、表示されているページの URL を確認します。 アドレスが一致する場合は true を返します。  

  `<RelationshipTypeRule>` この種類のルールは、グリッドで選択したレコードに適用されます。 このルールを使用すると、次に示すような関連付けの種類を判断できます。  

- OneToMany  

- ManyToMany  

- NoRelationship  

  `<SkuRule>`  
  この種類のルールは、次のような特定の SKU バージョンの Common Data Service のリボン要素を表示する場合に使用します。  

- OnPremise  

- オンライン  

- Spla  

  `<ValueRule>`  
  このルールは、フォームに表示されているレコード内の特定のフィールドの値を確認する場合に使用します。  

> [!NOTE]
>  更新したユーザー エクスペリエンスを使用してフォームのサブグリッドに対して定義されたコマンドには、値ルールは表示ルール内で使用することはできません。 `<EnableRule>` 内のこの要素を使用して、要素を隠します。  

### <a name="see-also"></a>関連項目  
 [コマンド、およびリボンをカスタマイズする](customize-commands-ribbon.md)   
 [リボンの有効化ルールの定義](define-ribbon-enable-rules.md)   
 [リボン アクションの定義](define-ribbon-actions.md)
