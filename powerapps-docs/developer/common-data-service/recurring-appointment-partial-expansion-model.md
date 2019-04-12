---
title: 定期的な予定の部分展開モデル (Common Data Service) | Microsoft Docs
description: この部分展開モデルは、あらかじめ指定された間隔で実行される非同期ジョブです。このジョブは組織レベルで定義され、定期的な予定インスタンスを作成するために使用されます。
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
# <a name="recurring-appointment-partial-expansion-model"></a>定期的な予定の部分展開モデル

Common Data Service は、データベース内に定期的な予定のインスタンスを作成する目的で部分展開モデルというものを実装しています。 `RecurringAppointmentMaster` レコードの作成時に指定する繰り返し情報が、個々のインスタンスの作成や同期を段階的に調整しながら行うために使われます。 これで Common Data Service の大量の予定レコードがコントロールされることになりますが、それは作成または同期させる定期的な予定の繰り返しの範囲が非常に長いか、不定 (終了日がない) からです。  

 この部分展開モデルは、Common Data Service の非同期ジョブとして、あらかじめ指定された間隔で実行されます。このジョブは組織レベルで `Organization.RecurrenceExpansionJobBatchInterval` 属性により定義されます。 さらに、このインスタンス展開モデルは、組織レベルのあるパラメーターに依存します。これを "N" とすると、"N" は同時的に作成できるインスタンスの最大数を表します。 この変数の値は、`Organization.RecurrenceExpansionSynchCreateMax` 属性で指定できます。 これらのプロパティは、「[部分展開ジョブのパラメーター](#Parameter)」セクションで後で詳細に取り上げます。  

<a name="Scenario1"></a>   
## <a name="when-the-recurring-appointment-instances-are-less-than-or-equal-to-n"></a>定期的な予定のインスタンス数が "N" 以下のとき  
 繰り返し情報のために生成されるインスタンス数が "N" 以下の場合は、実際の数のインスタンスが予定の有効開始日から同時的に作成されます。 個々のインスタンスは予定レコードとして Common Data Service に格納されます。  

<a name="Scenario2"></a>   

## <a name="when-the-recurring-appointment-instances-are-more-than-n"></a>定期的な予定のインスタンス数が "N" より大のとき  
 Common Data Service 内で作成される定期的な予定ごとに、非同期展開ジョブが作成されます。 定期的な予定のインスタンスは、以下の段階で展開されます。  

1. **同期展開**: 定期的な予定の最初の "N" 個のインスタンスが有効開始日から同時的に作成されます。 各インスタンスは予定レコードとして保存され、その `Appointment.InstanceTypeCode` 属性は "2" (定期的なインスタンス) に設定されます。 残りのインスタンスの展開は、非同期ジョブに引き継がれます。 定期的な予定の系列をどうしても展開しなければならなくなったときの日付が有効開始日とされます。  

2. **非同期展開**: 非同期ジョブは残りの展開ジョブを処理し、繰り返し情報に従って定期的にインスタンスを展開します。 非同期展開が行われるのは、将来の展開ウィンドウ (`Organization.FutureExpansionWindow`) が現れるまでの間だけです。 その後は、次の将来の展開ウィンドウまでの展開を処理する別の新しい非同期ジョブが作成されます。 この非同期サービスはインスタンスを定期的に展開し、予定レコードとしてシステムに保存します。  

<a name="Parameter"></a>   
## <a name="parameters-for-the-partial-expansion-job"></a>部分展開ジョブのパラメーター  
 要件どおりに展開モデルを動作させるためには、`Organization` レコード内のこれらの組織レベルの属性に適切な値を設定しなければなりません。 これを行うには、System Administrator ロールまたはそれに相当する権限が必要です。 次の表に、これらのプロパティに関する情報を示します。  


|                    属性                     |                                                                                                                                                                                                                    内容                                                                                                                                                                                                                    |
|--------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  Organization.RecurrenceExpansionSynchCreateMax  |                                                                                             これは、定期的な予定の作成時または同期時に作成される予定インスタンスの最大数です。 インスタンスの数に見合った整数値を指定する必要があります。 この値が "N" に相当します。                                                                                              |
|         Organization.PastExpansionWindow         |    これは、定期的な予定の展開または同期を Dynamics 365 for Outlook で行える有効な最大の期間 (過去方向) です。 その月数に相当する整数を指定する必要があります。<br /><br /> この属性の値によって、定期的な予定インスタンスの展開または同期のための過去方向のインスタンスの締め日が決まります。    |
|        Organization.FutureExpansionWindow        | これは、定期的な予定の展開または同期を Dynamics 365 for Outlook で行える有効な最大の期間 (将来方向) です。 その月数に相当する整数を指定する必要があります。<br /><br /> この属性の値によって、定期的な予定インスタンスの展開または同期のための未来方向のインスタンスの締め日が決まります。 |
| Organization.RecurrenceExpansionJobBatchInterval |                                                                                                                                                                               これは、部分展開ジョブの起動周期 (秒単位) です。                                                                                                                                                                                |
|   Organization.RecurrenceExpansionJobBatchSize   |                                                                                                                                                                                  これは、非同期ジョブが実行されるたびに展開されるインスタンスの個数です。                                                                                                                                                                                   |

### <a name="see-also"></a>関連項目  
 [定期的な予定エンティティ](/dynamics365/customer-engagement/developer/recurring-appointment-entities)   
 [定期的な予定の系列、インスタンス、または例外の作成](create-recurring-appointment-series-instance-exception.md)   
 [定期的な予定の系列またはインスタンスの削除または終了](/dynamics365/customer-engagement/developer/delete-or-end-a-recurring-appointment-series-or-instance)   
 [定期的な予約の更新](update-recurring-appointment.md)
