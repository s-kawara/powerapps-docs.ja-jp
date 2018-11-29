---
title: つながりロールを使用してエンティティ間の関係を記述する (アプリ用 Common Data Service) | Microsoft Docs
description: つながりロールおよびつながりロールのカテゴリを使用してエンティティ間の関連付けを記述する
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
# <a name="describe-a-relationship-between-entities-with-connection-roles"></a>つながりロールを使用してエンティティ間の関係を記述する

ロールの割り当てを通じてレコード間の関係を表すことができます。  
  
 つながりの中で、さまざまな方法でつながりロールを使用できます。  
  
-   ソース レコードとターゲット レコードに同じロールを適用します。 "友人"、"チーム メンバー"、"同僚" などは、つながりを持つ両方のレコードに適用できるロールの例です。  
  
-   ソース レコードとターゲット レコードのどちらか一方にロールを適用します。 取引先担当者と営業案件のつながりにおける "営業担当者" ロールが、このようなロールの例です。 営業案件、請求書、受注などのレコードには、通常、表す内容に関する十分な情報が格納されており、これらにロールを割り当てる必要はありません。  
  
-   2 つの一致ロールを割り当てます (相互ロールとも呼ばれます)。 一方のロールはソース レコードに適用され、他方のロールはターゲット レコードに適用されます。 "医者" と "患者"、"親" と "子" などが、一致ロールの例です。  
  
## <a name="connection-role-categories"></a>つながりロールのカテゴリ  
 つながりロールの作成時には、属するカテゴリを指定できます。 たとえば、次のカテゴリを使用できます。  
  
- 業務 (納入業者、バイヤー、競合企業)  
  
- 家族 (父親、姉妹、いとこ)  
  
- 社会 (テニス仲間、クラブ会員、友人)  
  
  カテゴリの一覧はカスタマイズできます。 各自のビジネス モデルに最適なカテゴリを追加できます。  
  
## <a name="create-connection-roles"></a>つながりロールの作成  
 つながりロールを作成するには、次の情報を指定する必要があります。  
  
- `ConnectionRole.Name` 属性を使用して、ロールの名前を指定します。  
  
- `ConnectionRole.Description` 属性を使用して、ロールの説明を追加します。  
  
- `ConnectionRole.Category` 属性を使用して、ロールのカテゴリを指定します。 `connectionrole_category` グローバル オプション セットで、この属性に指定できる値が定義されます。  
  
- つながりロールの作成時には、潜在顧客、取引企業、競合企業など、ロールが適用されるエンティティの種類を指定できます。 特定のエンティティの種類を指定しない場合、つながりロールはすべてのアプリ用 CDS エンティティに適用されます。 エンティティの種類を指定するには、`ConnectionRoleObjectTypeCode.AssociatedObjectTypeCode` 属性を使用します。 つながりロールを特定のエンティティの種類にリンクするには、`ConnectionRoleObjectTypeCode.ConnectionRoleId` 属性を使用します。 つながりロール レコードは、複数のつながりロール オブジェクトの種類コード レコードによって参照できます。 つながりロール レコードへの参照をすべて削除すると、このつながりロールをすべてのアプリ用 CDS エンティティに適用できます。  
  
  > [!TIP]
  >  取引先企業エンティティのつながりロールを検索するには、クエリに、取引先企業エンティティ (エンティティの種類コード = 1) またはすべてのエンティティ (エンティティの種類コード = 0) にリンクされているすべてのロールを指定します。  
  
## <a name="associate-and-disassociate-connection-roles"></a>つながりロールの関連付けと関連付けの解除  
 つながりにロールを関連付けるには、<xref:Microsoft.Xrm.Sdk.IOrganizationService.Associate*> メソッドを使用します。 ロールの関連付けを解除するには、<xref:Microsoft.Xrm.Sdk.IOrganizationService.Disassociate*> メソッドを使用します。 `Associate` メッセージおよび `Disassociate` メッセージの詳細については、[Dynamics 365 のエンティティの概要](/dynamics365/customer-engagement/developer/introduction-entities) を参照してください。  
  
### <a name="see-also"></a>関連項目  
 [つながりエンティティ](connection-entities.md)   
 [つながりエンティティのサンプル コード](/dynamics365/customer-engagement/developer/sample-code-connection-entities)   
 [サンプル: 相互つながりロールの作成 (事前バインド)](/dynamics365/customer-engagement/developer/sample-create-reciprocal-connection-role-early-bound)   
 [つながりエンティティ](/reference/entities/connection.md)