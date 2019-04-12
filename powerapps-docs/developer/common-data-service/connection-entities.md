---
title: レコードを相互にリンクする接続の使用 (Common Data Service) | MicrosoftDocs
description: つながりエンティティは、接続を有効化、作成および照会するのに役立ちます。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: mayadumesh
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-connections-to-link-records-to-each-other"></a>レコードを相互にリンクする接続の使用

*接続* により Common Data Service の 2 つのエンティティ レコード間の関係を柔軟に接続および記述することができます。 この機能は、チームワーク、コラボレーション、およびビジネスや営業プロセスの効果的な管理に役立ちます。 接続を使用すると、ユーザー、連絡先、見積もり、受注、およびその他多くのエンティティ レコード同士を簡単に関連付けることができます。 関連付け内のレコードを特定のロールに割り当てると、関係の目的の定義に役立ちます。  
  
 接続では次の機能が提供されます。  
  
- ほとんどの Common Data Service エンティティ タイプの 2 つのレコード間の接続を作成する簡単で柔軟な方法。 カスタマイズ可能なすべてのビジネス エンティティおよび カスタム エンティティを接続できます。  
  
- 有用な情報 (接続と期間の説明など) を追加するオプション。  
  
- 2 つのレコード間の関係を表すつながりロールの作成。たとえば医者と患者の関係、管理者と従業員の関係など。  
  
- 特定のレコードについて、複数の接続およびロールを素早く作成する方法。 たとえば、1 つの連絡先が他の連絡先、取引先企業、または契約と多くの関係を持っている場合があります。 それぞれの関係について、その連絡先に異なるロールを割り当てることができます。  
  
- クエリのビルドおよびグラフの作成に使用できる情報。 特定のレコードのすべての接続およびつながりロールを検索し、それらを視覚的に表現するグラフを作成できます。  
  
- ビジネス プロセスを自動化および向上するワークフローおよび監査のサポート。  
  
## <a name="enabling-and-creating-connections"></a>つながりの有効化および作成  
 エンティティのメタデータを更新することで、任意のカスタム エンティティおよびカスタマイズ可能なエンティティで接続を有効化できます。 <xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest> メッセージを使用して、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsConnectionsEnabled> プロパティを `true` に設定します。  
  
 2 つのレコード間につながりを作成するには、`Connection` エンティティを使用します。 接続の作成元レコード (ソース) および接続先となるレコード (ターゲット) を指定する必要があります。 ソース エンティティ レコードの指定には `Connection.Record1Id` 属性、ターゲット レコード エンティティの指定には `Connection.Record2Id` 属性を使用します。 接続の期間と説明をオプションとして指定できます。 接続の関係者間の説明を記述するには、つながりロールを使用します。 つながりロールを指定するには、`Connection.Record1RoleId` 属性および `Connection.Record2RoleId` 属性を使用します。  
  
## <a name="querying-connections"></a>つながりの照会  
 接続の照会では、レポートまたはグラフの作成に使用できる有用なデータが提供されます。 エンティティ レコード、エンティティの種類 (エンティティ種類コード)、ロール、またはその他の基準によって接続を照会できます。 次に接続の照会の例を示します。  
  
 エンティティ レコードによる場合  
  
- 取引先 A のすべての接続を表示。  
  
- 取引先 A のすべてのロールを表示。  
  
  エンティティの種類による場合 (エンティティ種類コードを使用)  
  
- 競合企業エンティティのすべてのロールを表示。  
  
- 取引先企業エンティティのロールの総数を検索。  
  
  ロールによる場合  
  
- 取引先企業が "ベンダー" であるすべての接続を検索。  
  
- オープンしている営業案件のうち、$20,000 を超え、取引先 B が "営業担当者" であるものを検索。  
  
- "医師" ロールに対応するすべてのロール ("患者"、"看護師"、または "医療アシスタント" など) を検索。  
  
- ロール "友人" を持つすべての連絡先を検索。  
  
> [!IMPORTANT]
>  つながりエンティティ レコードを作成すると、データベース内に 2 つのレコードが作成されます。 1 つ目のレコードはソースからターゲットの関係を表し、2 つ目のレコードはターゲットからソースの関係を表します。 これにより、レコードが接続のソースであるか、またはターゲットであるかに関わらず、照会ですべての関連レコードの接続を確実に検索できます。  
  
### <a name="see-also"></a>関連項目  
 [つながりロールを使用してエンティティ間の関係を記述する](describe-relationship-entities-connection-roles.md)   
 [つながりエンティティ](/reference/entities/connection.md)   
 [ConnectionRoleエンティティ](/reference/entities/connectionrole.md)   
 [つながりエンティティのサンプル コード](/dynamics365/customer-engagement/developer/sample-code-connection-entities)   
 [事業部管理エンティティ](/dynamics365/customer-engagement/developer/business-management-entities)   
 [Dynamics 365 でのビジュアル化とダッシュボードを使用したデータの表示および分析](/dynamics365/customer-engagement/developer/customize-dev/customize-visualizations-dashboards)   
 [会計カレンダー エンティティおよび担当地域エンティティ](/dynamics365/customer-engagement/developer/fiscal-calendar-and-territory-entities)