---
title: 顧客エンティティ (取引先企業、取引先担当者) (アプリ用 Common Data Service) | Microsoft Docs
description: Dynamics 365 の取引先企業および取引先担当者エンティティは、顧客の特定および管理、製品やサービスの販売、および顧客への優れたサービスの提供に必要なエンティティです。 "顧客住所" エンティティは、顧客の住所と発送情報の保存に使用します。
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
# <a name="customer-entities-account-contact"></a>顧客エンティティ (取引先企業、取引先担当者)

<!-- 
Was Mike Carter

https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customer-entities-account-contact

Refactor so that the links to entity reference are in the body, not just in the See allso.
Add some h2 sections so it is skimmable
 -->

アプリ用 Common Data Service の*アカウント*および*取引先担当者*エンティティは、顧客の特定、顧客の管理、製品やサービスの販売、および顧客への優れたサービスの提供に必要なエンティティです。 *顧客住所* エンティティは、顧客の住所と発送情報の保存に使用します。  
  
## <a name="account-entity"></a>取引先企業エンティティ
 
取引先企業エンティティは、アプリ用 CDS のエンティティの 1 つであり、その他の多くのエンティティが子として関連付けられます。 アプリ用 CDS では、取引先企業は部署と顧客間関係を持つ企業を表します。 取引先企業に含まれている情報は、関連するすべての取引先担当者情報、会社情報、カテゴリ、関係の種類、および住所情報です。 適用されるその他の情報には、次の項目が含まれています。  
  
- 取引先企業は、その他のほとんどのエンティティの上位として存在することができます。 これには別の取引先企業も含まれます。  
  
- 取引先企業は、スタンドアロン エンティティとすることもできます。  
  
- 1 つの取引先企業の上位にできる取引先企業は 1 つだけです。  
  
- 取引先企業は、複数の下位取引先企業および下位取引先担当者を持つことができます。  
  
組織は、別の企業と行っているすべての活動を確認する必要があるため、取引先企業の管理は、企業間の顧客間関係管理 (Dynamics 365) の重要な概念の 1 つです。これらのすべての活動は取引先企業レベルでは一体となっています。  

詳細: [取引先企業エンティティ](reference/entities/account.md)。
  
## <a name="contact-entity"></a>取引先担当者エンティティ

アプリ用 CDS では、取引先担当者は、通常は部署と関係がある人物 (顧客、納入業者、同僚など) を表します。 取引先担当者エンティティは、その他の多くのエンティティがリンクされるエンティティの 1 つです。 取引先担当者は、スタンドアロン エンティティとすることもできます。 このエンティティには、職業、個人、および家族の情報に加え、複数の住所を含めることができます。 詳細: [取引先担当者エンティティ](reference/entities/contact.md)。
  
取引先企業も取引先担当者も顧客管理の一部であり、相互の関係は次のとおりです。  
  
- 取引先担当者は、取引先企業および取引先担当者を除く、他のすべてのエンティティの上位に存在できます。  
  
- 1 つの取引先担当者の上位に存在できる取引先企業は 1 つだけです。  
  
- <xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*> メソッドを使用すると、取引先担当者を取引先企業の取引先責任者に設定できます。  
  
取引先担当者エンティティには、電子メール アドレス、住所、電話番号など、ある人物に関するすべての情報が格納されます。また、生年月日や記念日など、取引先担当者に関するその他の情報も格納されます。 顧客の全体像が見えるようにするには、部署が抱える顧客の種類に応じて、取引先担当者のみ、または取引先担当者と取引先企業の両方が必要になります。  
  
取引先担当者に対して実行できる基本操作には、作成、読み取り、更新、および削除があります。  
  
活動やメモなどのエンティティを取引先担当者エンティティにリンクすると、ユーザーは、顧客との間の通信、顧客のためにとったアクション、および顧客に関する必要な情報のすべてを確認できるようになります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [取引先企業エンティティ](reference/entities/account.md)  
  
 [取引先担当者エンティティ](reference/entities/contact.md)  
  
 [CustomerAddress エンティティ](reference/entities/customeraddress.md)  
  
## <a name="related-sections"></a>関連セクション  
 [Dynamics 365 によるビジネス データのモデル化](/dynamics365/customer-engagement/developer/model-business-data)  
  
 [事業部管理エンティティ](/dynamics365/customer-engagement/developer/business-management-entities)
