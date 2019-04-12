---
title: Common Data Service のフィールドを作成および編集する方法 | MicrosoftDocs
ms.custom: ''
ms.date: 02/08/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - PowerApps
ms.assetid: d88677fa-2caf-47b0-aec6-10a25a7ec9c3
caps.latest.revision: 55
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="how-to-create-and-edit-fields"></a>フィールドの作成と編集方法

Common Data Service でフィールドはエンティティにデータを格納するために使用できる個別のデータ アイテムを定義します。 フィールドは、開発者によって*属性*と呼ばれることがあります。 
  
ユーザー定義フィールドを作成する前に、既存のフィールドの使用が要件を満たすかどうかを確認します。 詳細: [新しいメタデータを作成するか既存のメタデータを使用するか](create-edit-metadata.md#create-new-metadata-or-use-existing-metadata)

フィールドを作成または編集に使用できる 2 人のデザイナーがいます。

|デザイナー| 説明|
|--|--|
|[PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)|簡単な優れたエクスペリエンスを提供しますが、一部の特殊な設定は使用できません。<br />詳細: [PowerApps ポータルを使用した Common Data Service のフィールドの作成および編集](create-edit-field-portal.md)|
|ソリューション エクスプローラー|簡単ではありませんが、一般的な要件が少ない割に柔軟性が高くなっています。<br />詳細: [PowerApps ソリューション エクスプローラーを使用した Common Data Service のフィールドの作成および編集](create-edit-field-solution-explorer.md) |

> [!NOTE]
> 以下を使用して、環境にフィールドを作成することもできます。
> - モデル駆動型アプリで、フォーム エディターから**新しいフィールド**を選択します。
> - フィールドの定義を含むソリューションをインポートします。
> - Power Query を使用して、新しいエンティティを作成しデータを入力します。<br />詳細: [Power Query を使用してアプリ用 Common Data Service のエンティティにデータを追加する](/powerapps/maker/common-data-service/data-platform-cds-newentity-pq).
> - 開発者は[メタデータ サービス](/powerapps/developer/common-data-service/use-web-services#metadata-services) を使用して、フィールドの作成および更新のためのプログラムを作成することができます。

このトピックの情報は、使用できるデザイナーの選択に役立ちます。 

次のいずれかの要件に対処する必要がない限り、Common Data Service のフィールドを作成および編集するには PowerApps ポータルを使用する必要があります:

- 顧客検索フィールドを作成します。 
   - 詳細: [さまざまな種類の検索](types-of-fields.md#different-types-of-lookups)
- Common Data Service の既定のソリューション以外に、ソリューションにフィールドを作成します。 
   - 詳細: [ソリューションの概要](solutions-overview.md)
- ステータスの遷移を定義します。 
   - 詳細: [サポート案件またはユーザー定義エンティティのステータス遷移の定義](define-status-reason-transitions.md)
- 同時に複数のフィールドを編集します。
- 監査を有効化します。 
   - 詳細: [監査の概要](../../developer/common-data-service/auditing-overview.md)
- フィールド レベル セキュリティを有効化します。 
   - 詳細: [フィールド セキュリティ エンティティ](../../developer/common-data-service/field-security-entities.md)
- フィールドが対話型エクスペリエンスのグローバル フィルターに表示されるかどうかを選択します。 
   - 詳細: [モデル駆動型アプリの対話型エクスペリエンス ダッシュボードの構成](../model-driven-apps/configure-interactive-experience-dashboards.md)
- フィールドが対話型エクスペリエンスのダッシュボードで並び替え可能かどうかを選択します。 
   - 詳細: [モデル駆動型アプリの対話型エクスペリエンス ダッシュボードの構成](../model-driven-apps/configure-interactive-experience-dashboards.md)
- 推奨項目としてフィールドの入力要求レベルを設定します。 
   - 詳細: [モデル駆動型アプリ フォームでロジックを適用するための業務ルールと推奨事項を作成](../model-driven-apps/create-business-rules-recommendations-apply-logic-form.md)
- フィールドの管理プロパティを設定します。 
   - 詳細: [フィールドの管理プロパティの設定](set-managed-properties-for-field.md)

> [!NOTE]
> 1 対多の関連付けをエンティティ上に作成することで、PowerApps ポータルまたはソリューション エクスプローラーに検索フィールドを作成できます。 しかし、フィールドの作成時に、ソリューション エクスプローラーだけがこの関連付けを作成するオプションを提供します。

## <a name="community-tools"></a>コミュニティ ツール

**[属性マネージャー](https://www.xrmtoolbox.com/plugins/DLaB.Xrm.AttributeManager/)** は Common Data Service 用に XrmToolbox コミュニティが開発したツールです。 より多くのコミュニティ開発ツールについては、[開発者ツール](https://docs.microsoft.com/dynamics365/customer-engagement/developer/developer-tools) トピックを参照してください。

> [!NOTE]
> コミュニティ ツールは Microsoft の製品ではなく、コミュニティ ツールに対するサポートは提供されません。 このツールに関するご質問は、その発行元にお問い合わせください。 詳細: [XrmToolBox](https://www.xrmtoolbox.com)。

### <a name="see-also"></a>関連項目  
[PowerApps ポータルを使用した Common Data Service のフィールドの作成および編集](create-edit-field-portal.md)<br />
[PowerApps ソリューション エクスプローラーを使用した Common Data Service のフィールドの作成および編集](create-edit-field-solution-explorer.md)<br />
[フィールドの種類とフィールド データの種類](types-of-fields.md)<br />
[開発者ドキュメント: 属性メタデータに関する作業](/dynamics365/customer-engagement/developer/org-service/work-attribute-metadata)
 
