---
title: タイム ゾーン エンティティ (Common Data Service) | Microsoft Docs
description: タイム ゾーン エンティティには、サポートされているタイム ゾーン、タイム ゾーン コード、ローカライズされたタイム ゾーンなどタイム ゾーンの情報が含まれ、時間の計算方法に関する情報が格納されています。
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
# <a name="time-zone-entities"></a>タイム ゾーンのエンティティ

*タイム ゾーン*のエンティティは、複数のタイム ゾーンで機能するコードを作成する際に使用します。 タイム ゾーン情報を含む Common Data Service の読み取り専用のエンティティには次の 3 種類があります。  
  
- *タイム ゾーン定義エンティティ*には、タイム ゾーン コードや標準のタイム ゾーン名など、サポートされている各タイム ゾーンの基本情報が格納されます。  
  
- *タイム ゾーンのローカライズ名* エンティティには、ローカライズされたタイム ゾーン名が格納されます。  
  
- *タイム ゾーン規則* エンティティには、時間の計算方法に関する情報が格納されます。  
  
  次の表に、タイム ゾーンに関連付けられている一方で、特定のエンティティを参照しないメッセージを示します。  
  
|メッセージ|説明|  
|-------------|-----------------|  
|<xref:Microsoft.Crm.Sdk.Messages.GetTimeZoneCodeByLocalizedNameRequest>|指定されたロケールのタイム ゾーン定義をすべて取得し、表示名属性のみを返します。|  
|<xref:Microsoft.Crm.Sdk.Messages.LocalTimeFromUtcTimeRequest>|指定された UTC 時間のローカル時間を取得します。|  
|<xref:Microsoft.Crm.Sdk.Messages.UtcTimeFromLocalTimeRequest>|指定したローカル時間の UTC 時間を取得します。|  
  
### <a name="see-also"></a>関連項目  
 [事業部管理エンティティ](/dynamics365/customer-engagement/developer/business-management-entities)   
 [サンプル: タイム ゾーン情報の取得](org-service/samples/retrieve-time-zone-information.md)   
 [timezonedefinition EntityType](reference/entities/timezonedefinition.md)   
 [timezonelocalizedname EntityType](reference/entities/timezonelocalizedname.md)   
 [timezonerule EntityType](reference/entities/timezonerule.md)   
 [サンプル: タイム ゾーン情報の取得](org-service/samples/retrieve-time-zone-information.md)   
 [トランザクション通貨 (通貨) エンティティ](transaction-currency-currency-entity.md)
