---
title: リボン要素のスケーリングを定義する (モデル駆動型アプリ) | MicrosoftDocs
description: リボン要素のスケーリングの定義について学習します。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: c2cc39d2-e540-0800-f04f-3fa66df21191
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

# <a name="define-scaling-for-ribbon-elements"></a>リボン要素のスケーリングの定義

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/define-scaling-ribbon-elements -->

アプリケーション リボンおよび更新されたエンティティ フォーム リボンの場合、スケーリングはありません。 スケーリングは、更新されておらず、Dynamics 365 for Outlook を使用して表示されたリボンを一覧表示するエンティティのフォームにのみ適用されます。  
  
 リボンの目標は、ウィンドウの横幅が変化しても、関連するコントロールの表示を維持することです。 これを実現するため、UI 定義を使用して、ウィンドウのサイズの変化に対応して、グループ内のコントロールのサイズを変更する方法を制御できます。 *これをスケーリング*と言います。  
  
## <a name="associate-groups-and-controls-to-layout-templates"></a>グループとコントロールをレイアウト テンプレートに関連付ける  
 リボンの各 `<Group>` 要素は、`<GroupTemplate>` に関連付けられています。 `GroupTemplate` は、グループ内のコントロールを `<Layout>` 要素を使用して表示する方法を 1 つ以上指定します。 各 `Layout` には、グループ内のコントロールの表示方法に関する 2 種類の定義のどちらかを含めることができます。  
  
- `<OverflowSection>` を使用すると、使用可能なスペースに応じて、コントロールの相対位置を変更できます。  
  
- `<Section>` は、表示する行数と各コントロールの表示場所を制御します。  
  
  リボンで使用されるほぼすべての `Layout` 要素が `OverflowSection` 要素を使用します。  
  
  各 `<Tab>` 要素では、`<Scaling>` に 1 つの `<MaxSize>` を含める必要があります。 `MaxSize` 要素は、スケーリングを適用することなく `Group`内の各 `Tab` の既定のプレゼンテーションを作成できるので、必須です。 `Tab` が 1 つ以上の `<Scale>` に関連付けられると、スケーリングが発生します。 各 `MaxSize` 要素と `Scale` 要素は、`Size` 属性によって、`Layout` 内の各 `GroupTemplate` が使用する `Group` 内の `Tab` 要素のいずれかに関連付けられます。  
  
> [!NOTE]
>  いずれかの `Size` 要素または `MaxSize` 要素の `Scale` 属性の値は、`Title` で指定された、使用可能な `Layout` 要素の `GroupTemplate` と一致している必要があります。 これらの値は文字列で、XSD では一致する値の選択に役立つ検証は行われません。 XML では常に大文字と小文字が区別されます。  
  
 以下の図に、`<OverflowSection>` 要素を使用する場合、スケーリングを有効にするために `MaxSize`、`Scale`、`Group`、`Layout`、および `OverflowSection` の要素がどのように相互参照を行う必要があるかを示します。  
  
 ![要素間の関係と OverflowSection](media/ribbon-ui-definition.png "要素間の関係と OverflowSection")  
  
 以下の図に、`<Section>` 要素を使用する場合、スケーリングを有効にするために `MaxSize`、`Scale`、`Group`、`Layout`、および `ControlRef` の要素がどのように相互参照を行う必要があるかを示します。  
  
 ![要素間の関係と Section](media/ui-definition.png "要素間の関係と Section") 
  
### <a name="use-existing-group-templates"></a>既存のグループ テンプレートを使用する  
 新しいグループ テンプレートを定義する代わりに新しいグループを作成すると、既存の `GroupTemplate` 要素を再利用できます。  
  
 新しいグループをそのテンプレートに関連付けます。 グループ内のコントロールごとに、その `TemplateAlias` が使用する `Layout` 要素のいずれかの中にある `<Section>` 要素または `<OverflowSection>` 要素のいずれかの `GroupTemplate` 値を使用します。 各 `<OverflowSection>` には、使用されない `isv``TemplateAlias` が含まれます。 `TemplateAlias` は、ISV がそのグループにコントロールを追加できるよう、提供されています。  
  
### <a name="control-how-scaling-is-applied"></a>スケーリングの適用方法を制御する  
 特定のタブの `Scale` 要素内の各 `Scaling` 要素は、1 つのスケール ステップを表します。 各 `Scale` は、`Scale` 要素が出現する順序で適用されます。 リボンに使用できる水平領域を小さくすると、各 scale 要素が上から順に適用されます。 最小の領域から使用できる水平領域を大きくすると、一番下の scale 要素が有効になります。 すべての `Scale` 要素が有効になるまで、使用可能な各 `MaxSize` 要素が下から上へという順で適用されます。  
  
> [!NOTE]
>  `Scale` 要素の `Sequence` 属性値は、スケーリングの適用順序の決定に使用されません。 スケーリングは、`MaxSize` 要素と `Scale` 要素が RibbonDiffXML に出現する相対順序で適用されます。 すべての `Sequence` 要素を `MaxSize` 要素の上にグループ化する必要があるため、`Scale` 値は `MaxSize` 要素と `Scale` 要素の両方にとって重要です。 新しい `MaxSize` 要素または `Scale` 要素を追加する場合は、すべての `Sequence` 要素と `MaxSize` 要素に割り当てられている `Scale` の規定値の範囲を必ず確認してください。 範囲が重複する可能性のある `Sequence` 値を割り当てるという誤りがよく見られます。  
  
### <a name="see-also"></a>関連項目  
 [コマンド、およびリボンをカスタマイズする](customize-commands-ribbon.md)   
 [ユーザー定義のアクションによるリボンの変更](define-custom-actions-modify-ribbon.md)   
 [リボン タブ表示ルールを定義する](define-ribbon-tab-display-rules.md)
