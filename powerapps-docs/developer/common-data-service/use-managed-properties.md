---
title: マネージド プロパティの使用 (アプリ用 Common Data Service) | Microsoft Docs
description: マネージド プロパティはどの管理ソリューションがカスタマイズ可能かを定義するのに役立ちます
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: shmcarth
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-managed-properties"></a>マネージド プロパティの使用

マネージド プロパティを使用すると、どのマネージド ソリューション コンポーネントがカスタマイズ可能であるかを制御できます。 ビジネス エンティティを表すそうしたソリューションでは、できるだけ多くのカスタマイズを許可する必要があります。 こうすることで、各組織はソリューションをそれぞれの要件に合わせてカスタマイズできます。 ソリューションのコア機能を提供する重要なソリューション コンポーネントのカスタマイズについては、そのサポートとメンテナンスが予測可能なものになるように、制限するか除外します。  
  
 マネージド プロパティの目的は、破壊を引き起こすおそれのある変更からソリューションを保護することにあります。 マネージド プロパティには、デジタル著作権管理 (DRM) の機能や、ソリューションをライセンスしたり、ソリューションのインストールを実行できるユーザーを制御したりする機能はありません。  
  
## <a name="apply-managed-properties"></a>マネージド プロパティの適用  
 ソリューションがアンマネージドである場合は、マネージド プロパティを適用します。 マネージド プロパティは、マネージド ソリューションをパッケージして別の組織にインストールした後に有効になります。 マネージド ソリューションをインストールした後は、元の発行者によってソリューションが更新される場合を除き、マネージド プロパティを更新できません。  
  
 ほとんどのソリューションでは、ソリューション コンポーネントの一覧を表示すると **マネージド プロパティ** ボタンが現れます。 このボタンをクリックすると、ソリューション コンポーネントのマネージド プロパティを表示または更新できます。 このボタンが表示されないソリューションのマネージド プロパティにアクセスするには、**その他の操作** ドロップダウン リストから **マネージド プロパティ** を選択します。  
  
 既定では、すべてのカスタム ソリューション コンポーネントがカスタマイズ可能です。 ソリューション コンポーネントのマネージド プロパティを変更するには、ソリューション コンポーネントのツールバーにある **マネージド プロパティ** ボタンをクリックします。 それぞれのソリューション コンポーネントには、**カスタマイズ可能** (`IsCustomizable`) というプロパティがあります。 このプロパティが true である限り、その種類のソリューション コンポーネントに特有のプロパティをさらに指定できます。 `IsCustomizable.Value` プロパティを false に設定すると、ソリューションをマネージド ソリューションとしてインストールした後、そのソリューション コンポーネントはカスタマイズできなくなります。 次の表は、各ソリューション コンポーネントのマネージド プロパティを一覧表示しています。  
  
|コンポーネント|表示名|プロパティ|  
|---------------|------------------|--------------|  
|Entity|カスタマイズ可能|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsCustomizable>。                                 `Value`|  
|Entity|修正可能な表示名|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsRenameable>。                              `Value`|  
|Entity|関連エンティティとして関係を構築可能|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.CanBeRelatedEntityInRelationship>。                                 `Value` (読み取り専用)|  
|Entity|主エンティティとして関係を構築可能|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.CanBePrimaryEntityInRelationship>。                                 `Value` (読み取り専用)|  
|Entity|多対多の関係を構築可能|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.CanBeInManyToMany>。                               `Value` (読み取り専用)|  
|Entity|新しいフォームを作成可能|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.CanCreateForms>。                              `Value`|  
|Entity|新しいグラフを作成可能|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.CanCreateCharts>。                               `Value`|  
|Entity|新しいビューを作成可能|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.CanCreateViews>。                              `Value`|  
|Entity|マネージド プロパティによって表されていない他のすべてのエンティティ プロパティを変更可能|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.CanModifyAdditionalSettings>。                                `Value`|  
|フィールド (属性)|カスタマイズ可能|<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.IsCustomizable>。                                 `Value`|  
|フィールド (属性)|修正可能な表示名|<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.IsRenameable>。                              `Value`|  
|フィールド (属性)|入力要求レベルを変更可能|<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.RequiredLevel>。                                `CanBeChanged`<br /><br /> 注意:<br /><br /> `RequiredLevel` は、`CanBeChanged` プロパティを使用する唯一のマネージド プロパティです。|  
|フィールド (属性)|マネージド プロパティによって表されていない他のすべての属性プロパティを変更可能|<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.CanModifyAdditionalSettings>。                                 `Value`|  
|エンティティ関係|カスタマイズ可能|<xref:Microsoft.Xrm.Sdk.Metadata.RelationshipMetadataBase.IsCustomizable>。                              `Value`|  
|フォーム|カスタマイズ可能|`SystemForm.IsCustomizable.Value`|  
|グラフ|カスタマイズ可能|`SavedQueryVisualization.IsCustomizable.Value`|  
|ビュー |カスタマイズ可能|`SavedQuery.IsCustomizable.Value`|  
|オプション セット|カスタマイズ可能|<xref:Microsoft.Xrm.Sdk.Metadata.OptionSetMetadataBase.IsCustomizable>。                              `Value`|  
|Web リソース |カスタマイズ可能|`WebResource.IsCustomizable.Value`|  
|ワークフロー|カスタマイズ可能|`Workflow.IsCustomizable.Value`|  
|アセンブリ|カスタマイズ可能|`SdkMessageProcessingStep.IsCustomizable.Value`|  
|アセンブリ登録|カスタマイズ可能|`ServiceEndpoint.IsCustomizable.Value`|  
|電子メール テンプレート|カスタマイズ可能|`Template.IsCustomizable.Value`|  
|サポート情報の記事のテンプレート|カスタマイズ可能|`KbArticleTemplate.IsCustomizable.Value`|  
|契約テンプレート |カスタマイズ可能|`ContractTemplate.IsCustomizable.Value`|  
|差し込み印刷用テンプレート |カスタマイズ可能|`MailMergeTemplate.IsCustomizable.Value`|  
|ダッシュボード|カスタマイズ可能|`SystemForm.IsCustomizable.Value`|  
|セキュリティ ロール |カスタマイズ可能|`Role.IsCustomizable.Value`|  
  
### <a name="update-managed-properties"></a>マネージド プロパティの更新  
 マネージド ソリューションをリリースした後、マネージド プロパティを変更する必要があるかどうかを決定できます。 マネージド プロパティの変更は、それらの制限を緩和する場合にのみ行えます。 たとえば、最初のリリース後にあるエンティティのカスタマイズの許可を決定できます。  
  
 ソリューションのマネージド プロパティを更新するには、マネージド プロパティを変更したソリューションへの更新プログラムをリリースします。 マネージド ソリューションの更新は、元のマネージド ソリューションと同じ発行者レコードと関連付けられた別のマネージド ソリューションによってのみ行えます。 マネージド プロパティの制限を強化するような変更が更新プログラムに含まれる場合、そうしたマネージド プロパティの変更は無視されますが、更新プログラム内の他の変更は適用されます。  
  
 元の発行者はマネージド ソリューションのマネージド プロパティを更新するための要件なので、マネージド ソリューションのインストールに使用されている発行者をアンマネージド ソリューションに関連付けることはできません。  
  
> [!NOTE]
>  つまり、マネージド ソリューションがインストールされている組織を使用した、ソリューションの更新プログラムの開発は行えなくなります。  
  
## <a name="check-managed-properties"></a>マネージド プロパティの確認  
 ソリューション コンポーネントがカスタマイズ可能かどうかを確認するには、<xref:Microsoft.Crm.Sdk.Messages.IsComponentCustomizableRequest> を使用します。 あるいは、ソリューション コンポーネントのプロパティを確認することもできますが、その意味の最終的な決定には複数のプロパティの値が影響することを考慮する必要があります。 それぞれのソリューション コンポーネントには、`IsCustomizable` プロパティがあります。 ソリューション コンポーネントがマネージド ソリューションの一部としてインストールされている場合は、`IsManaged` プロパティが true になります。 マネージド プロパティは、マネージド ソリューションにのみ適用されます。 マネージド プロパティを確認して個々のソリューション コンポーネントがカスタマイズ可能かどうかを決定する際には、`IsCustomizable` と `IsManaged` の両方のプロパティを確認する必要があります。 `IsCustomizable` が false かつ `IsManaged` が false であるソリューション コンポーネントは、カスタマイズ可能です。  
  
 エンティティと属性には、`IsCustomizable` 以外にもマネージド プロパティがあります。 これらのマネージド プロパティは、`IsCustomizable` が false に設定されている場合、更新されません。 つまり、マネージド プロパティが適用されているかどうかを確認するには、個々のマネージド プロパティを確認するだけでなく、`IsCustomizable` プロパティも確認する必要があります。  
  
### <a name="see-also"></a>関連項目  
 [マネージド プロパティ](/dynamics365/customer-engagement/developer/introduction-solutions#BKMK_ManagedProperties)   
 [ソリューション開発の計画](/dynamics365/customer-engagement/developer/plan-solution-development)   
 [マネージド ソリューションの保守](maintain-managed-solutions.md)   
 [Dynamics 365 ソリューションを使用した拡張機能のパッケージ化および配布](/dynamics365/customer-engagement/developer/package-distribute-extensions-use-solutions)   
 <xref:Microsoft.Crm.Sdk.Messages.IsComponentCustomizableRequest>