---
title: 定期的な予定マスターと予定エンティティのユーザー定義属性をリンクする (アプリ用 Common Data Service) | MicrosoftDocs
description: 定期的な予定マスター エンティティを予定エンティティのユーザー定義属性にリンクして、自動的にデータをコピーします。
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
# <a name="link-custom-attributes-of-the-recurring-appointment-master-and-appointment-entities"></a>定期的な予定マスター エンティティと予定エンティティのユーザー定義属性をリンクする

`RecurringAppointmentMaster` エンティティ用に作成したユーザー定義属性を `Appointment` 用に作成したユーザー定義属性にリンクして、リンク先の定期的な予定のインスタンス ユーザー定義属性が展開されるたびに、定期的な予定のマスター ユーザー定義属性からデータが自動的にコピーされるように設定できます。  
  
 ユーザー定義属性間には一対一のマッピングが存在します。つまり、定期的な予定のマスター エンティティは、予定エンティティの 1 つのユーザー定義属性にのみリンクできます。 また、リンクするユーザー定義属性は同じ種類である必要があります。 たとえば、`string` 型のユーザー定義属性を `decimal` のユーザー定義属性にリンクすることはできません。 属性の種類の詳細については、「[エンティティ属性メタデータのカスタマイズ](/dynamics365/customer-engagement/developer/customize-entity-attribute-metadata)」を参照してください。  
  
> [!NOTE]
>  *フィールドレベルのセキュリティ*が有効になっているユーザー定義属性はリンクできません。 同様に、リンク済みのユーザー定義属性でフィールドレベルのセキュリティを有効にすることはできません。  
  
### <a name="link-custom-attributes"></a>ユーザー定義属性のリンク  
  
1. <xref:Microsoft.Xrm.Sdk.Messages.CreateAttributeRequest> クラスを使用して、予定エンティティ用のユーザー定義属性を作成します。  
  
2. 一連の定期的な予定 (定期的な予定マスター) エンティティ用のユーザー定義属性を作成します。 カスタム属性の属性メタデータの指定中、<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.LinkedAttributeId> プロパティを使用して、手順1で作成したユーザー定義属性へリンクします。  
  
3. 変更内容をソリューションに公開します。  
  
   サンプル コードについては、「[サンプル: 系列とインスタンスとの間のユーザー定義属性のリンク](org-service/samples/link-custom-attributes-between-series-instances.md)」を参照してください。  
  
### <a name="see-also"></a>関連項目

 [定期的な予定エンティティ](/dynamics365/customer-engagement/developer/recurring-appointment-entities)   
 [RecurringAppointmentMaster エンティティ](/reference/entities/recurringappointmentmaster.md)   
 [サンプル: 系列とインスタンスとの間のユーザー定義属性のリンク](org-service/samples/link-custom-attributes-between-series-instances.md)   
 [エンティティ属性メタデータのカスタマイズ](/dynamics365/customer-engagement/developer/customize-entity-attribute-metadata)
