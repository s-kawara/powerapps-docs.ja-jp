---
title: 定期的な予定の系列、インスタンス、または例外の作成 (アプリ用 Common Data Service) | Microsoft Docs
description: 定期的な予定マスター (繰り返し)、個々の定期的な予定のインスタンス、これらのインスタンスの例外をプログラムで作成、または予定を定期的な予定に変換します。
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
# <a name="create-a-recurring-appointment-series-instance-or-exception"></a>定期的な予定の系列、インスタンス、または例外の作成

定期的な予定マスター (系列) を作成する場合、アプリ用 Common Data Service では、指定された定期的なアイテムの情報に基づいて個々の予定のインスタンスが作成されます。 また、個々の定期的な予定のインスタンスやこれらのインスタンスの例外を作成することも可能であり、予定を定期的な予定に変換できます。  
  
<a name="bkmk_createseries"></a>   

## <a name="create-a-recurring-appointment-series"></a>定期的な予定の系列の作成  

 定期的な予定の系列 (`RecurringAppointmentMaster` レコード) を作成するには、<xref:Microsoft.Crm.Sdk.Messages.BookRequest> メッセージ、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> メッセージ、または <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*>  メソッドを使用することができます。  
  
 定期的な予定の系列を作成すると、次のことが発生します。  
  
1. 定期的な予定の系列に関する基本情報と定期的なアイテムの情報を含む `RecurringAppointmentMaster` レコード (定期的な予定の系列) が作成されます。 各レコードは、`RecurringAppointmentMaster.ActivityId` プロパティを使用して一意に識別できます。 また、この定期的な予定の系列は、活動 (`ActivityPointer`) レコードとして作成および保存されます。 活動レコードは、`ActivityPointer.ActivityId` プロパティを使用して一意に識別できます。  
  
2. 定期的なアイテムの情報に基づいて個々の定期的な予定のインスタンスが作成され、`Appointment` レコードとして保存されます。 これらの予定オブジェクトは、`Appointment.SeriesId` プロパティを使用して、親の定期的な予定の系列に関連付けられ、このオブジェクトの値は、親の定期的な予定の系列の ID (`ActivityPointer.SeriesId`) と同じ値です。  
  
    これらの予定オブジェクトの `Appointment.InstanceTypeCode` プロパティの値は、**定期的なインスタンス** (候補リストの値 2) に設定されます。  
  
   > [!NOTE]
   >  定期的な予定のインスタンスは、拡張モデルとそれを定義するパラメーターに基づいて作成されます。 詳細: [定期的な予定の部分展開モデル](recurring-appointment-partial-expansion-model.md)。  
  
   定期的な予定の繰り返しを作成する方法を示すサンプル コードの場合、[サンプル: 定期的な予定の作成](/dynamics365/customer-engagement/developer/sample-create-retrieve-update-delete-recurring-appointment) を参照してください。  
  
<a name="bkmk_createinstance"></a>   

## <a name="create-a-recurring-appointment-instance"></a>定期的な予定のインスタンスの作成  
 定期的な予定のインスタンス (`RecurringAppointmentMaster` レコード) を作成するには、<xref:Microsoft.Crm.Sdk.Messages.CreateInstanceRequest> を使用します。 このメッセージは、次の 2 つのパラメータを取得します。作成するインスタンス数と、そのインスタンスを作成する対象となる定期的な予定の系列です。  
  
 このインスタンスは、定期的な予定の系列の最後のインスタンスの後に作成されます。 また、このインスタンスは、作成用に指定したインスタンスの数に関係なく、今後のインスタンスの締め日までにのみ作成されます。  
  
<a name="bkmk_createexception"></a>   

## <a name="create-a-recurring-appointment-exception"></a>定期的な予定の例外の作成  
 例外は、定期的な予定のインスタンスを更新または削除すると作成されます。 定期的な予定のインスタンスは、他の予定と同様に予定レコードとして保存され、予定レコードの `Appointment.InstanceTypeCode` 属性を使用して識別できます。この属性の値は**定期的なインスタンス** (候補リストの値 2) です。  
  
 例外は次の方法で作成できます。  
  
-   `Appointment` エンティティで <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> クラスを使用して、定期的な予定のインスタンスを更新し、`Appointment.InstanceTypeCode` 属性の値を**定期的な例外** (候補リストの値 3) に設定します。  
  
-   `Appointment` エンティティで <xref:Microsoft.Xrm.Sdk.Messages.DeleteRequest> クラスを使用して、定期的な予定のインスタンスを削除します。 削除された予定のインスタンスは、親の予定の系列オブジェクトの `RecurringAppointmentMaster.DeletedExceptionsList` 属性にインスタンスのエンティティを作成することによって例外としてマークされます。  
  
-   `Appointment` エンティティで <xref:Microsoft.Crm.Sdk.Messages.CreateExceptionRequest> クラスを使用します。  
  
<a name="bkmk_convert"></a>   

## <a name="convert-an-appointment-to-a-recurring-appointment"></a>予定から定期的な予定への変換  
 定期的な予定とは、定期的なアイテムの情報を含む予定です。 <xref:Microsoft.Crm.Sdk.Messages.AddRecurrenceRequest> を使用すると、アプリ用 CDS の既存の予定を定期的な予定に変換できます。 既存の予定を定期的な予定に変換すると、既存の予定のデータが新しい定期的な予定マスターのインスタンスにコピーされ、既存の予定が削除されます。  
  
### <a name="see-also"></a>関連項目  
 [定期的な予定エンティティ](/dynamics365/customer-engagement/developer/recurring-appointment-entities)   
 [定期的な予約の更新](update-recurring-appointment.md)   
 [サンプル: 定期的な予定の作成](/dynamics365/customer-engagement/developer/sample-create-retrieve-update-delete-recurring-appointment)   
 [サンプル: 予定から定期的な予定へ変換する](/dynamics365/customer-engagement/developer/sample-convert-appointment-recurring-appointment)
