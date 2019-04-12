---
title: 定期的な予定の系列を更新する (Common Data Service) | Microsoft Docs
description: RecurringAppointmentMaster エンティティに対して IOrganizationService.Entity メソッドまたは UpdateRequest メッセージを使用して、定期的な予定の系列を更新します。
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
# <a name="update-a-recurring-appointment"></a>定期的な予約の更新

定期的な予定の系列全体、または 1 つのインスタンスを更新できます。  
  
## <a name="update-a-recurring-appointment-series"></a>定期的な予定の系列を更新する  
 <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*> メソッドまたは `RecurringAppointmentMaster` エンティティ上の <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> メッセージを使用して一連の定期的な予定を更新することができます。 *基本* 情報または *繰り返し* 情報を更新できます。  
  
### <a name="update-basic-information"></a>基本情報の更新  
 件名、場所、出席者など、定期的な予定の系列の基本情報を更新すると、同じ属性に対して例外を持つインスタンスを除き、定期的な予定の系列のすべてのインスタンスが更新されます。  
  
### <a name="update-recurrence-information"></a>繰り返し情報の更新  
 パターンや範囲など、定期的な予定の系列の繰り返し情報を更新すると、以下の処理が行われます。  
  
1. 元の系列と同じ情報を持つ新しい系列が、新しい `RecurringAppointmentMaster.ActivityId` で作成されます。新しい系列の `RecurringAppointmentMaster.EffectiveEndDate` 属性の日付は、元の系列で最後に発生した過去のインスタンスに設定されます。 元の系列の将来のインスタンスはすべて削除されます。 このようにして、元の系列が終了されます。過去のインスタンスの履歴は新しい系列に保存され、システム内に保持されます。  
  
2. 新しい情報を使用して、新しい系列の将来のインスタンスが実効開始日 (`RecurringAppointmentMaster.EffectiveStartDate`) から作成されます。  
  
   また、元の系列と新しい系列の `RecurringAppointmentMaster.GroupId` 属性は、同じ値に設定されます。 これは、定期的な予定の系列の繰り返し情報を更新すると常に、作成された新しい系列のすべてが、`RecurringAppointmentMaster.GroupId` 属性に対して、更新された定期的な予定の系列と同じ値を持つことを意味します。ただし、予定の系列はそれぞれ一意の系列 ID を持ちます。  
  
> [!NOTE]
>  将来発生する予定になっているすべてのインスタンスを持つ定期的な予定の系列の繰り返し情報を更新すると、すべてのインスタンスが削除され、新しい繰り返し情報を使用して、新しいインスタンスが作成または展開されます。  
  
 定期的な予定の繰り返しを更新する方法を示すサンプル コードを参照するには、「[サンプル: 定期的な予定の更新](org-service/samples/reschedule-cancel-recurring-appointment.md)」を参照してください。  
  
## <a name="update-a-recurring-appointment-instance"></a>定期的な予定インスタンスの更新  
 定期的な予定のレコードは予定オブジェクトとして保存されるため、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*> メソッドを `Appointment` エンティティ上で使用して、定期的な予定のインスタンスを更新することができます。 定期的な予定インスタンスを更新すると、そのインスタンスは定期的な予定の系列の例外としてマークされます。 詳細: [定期的な予定の例外を作成する](create-recurring-appointment-series-instance-exception.md#bkmk_createexception)  
  
 `Appointment` エンティティに対して <xref:Microsoft.Crm.Sdk.Messages.CreateExceptionRequest> クラスを使用して、定期的な予定インスタンスを更新することもできます。  
  
> [!TIP]
>  定期的な予定インスタンスは、`Appointment.InstanceTypeCode` 属性を使用して識別できます。この属性は値 "2" (定期的なインスタンス) を持ちます。 詳細: [Appointment エンティティ](reference/entities/appointment.md)  
  
### <a name="see-also"></a>関連項目  
 [定期的な予定エンティティ](/dynamics365/customer-engagement/developer/recurring-appointment-entities)   
 [定期的な予定の系列またはインスタンスの削除または終了](/dynamics365/customer-engagement/developer/delete-or-end-a-recurring-appointment-series-or-instance)   
 [サンプル: 定期的な予定を作成、取得、更新、および削除する (CRUD)](org-service/samples/create-retrieve-update-delete-recurring-appointment.md)   
 [サンプル: 定期的な予定の再スケジュールおよび取り消し](org-service/samples/reschedule-cancel-recurring-appointment.md)
