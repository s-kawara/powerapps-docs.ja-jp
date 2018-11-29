---
title: ActivityParty エンティティ (アプリ用 Common Data Service) | Microsoft Docs
description: 活動関係者は、活動に関連付けられたユーザーまたはグループを表します。 1 つの活動に複数の活動関係者を関連付けることができます
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
# <a name="activityparty-entity"></a>ActivityParty エンティティ

活動関係者は、活動に関連付けられたユーザーまたはグループを表します。 1 つの活動に複数の活動関係者を関連付けることができます。  
  
<a name="ActivityPartyTypes"></a>   

## <a name="activity-party-types"></a>活動関係者の種類  

 アプリ用 Common Data Service には 11 の活動関係者の種類があります。 活動関係者の種類は、整数値として `ActivityParty.ParticipationTypeMask` 属性に保存されます。 次の表は、さまざまな活動関係者の種類、`ActivityParty.ParticipationTypeMask` 属性の対応する整数値、および説明を一覧表示しています。  
  
|活動関係者の種類|Value|内容|  
|-------------------------|-----------|-----------------|  
|発信者|1|送信者を指定します。|  
|ToRecipient|2|[宛先] フィールドに受信者を指定します。|  
|CCRecipient|3|[CC] フィールドに受信者を指定します。|  
|BccRecipient|4|[BCC] フィールドに受信者を指定します。|  
|RequiredAttendee|5|必須の出席者を指定します。|  
|OptionalAttendee|6|任意の出席者を指定します。|  
|開催者|7|活動の開催者を指定します。|  
|関連|8|関連アイテムを指定します。|  
|所有者 |9|活動の所有者を指定します。|  
|リソース |10|リソースを指定します。|  
|Customer|11|顧客を指定します。|  
  
<a name="SupportedActivityPartyTypes"></a>   
## <a name="activity-party-types-available-for-each-activity"></a>それぞれの活動で使用可能な活動関係者の種類  
 アプリ用 CDS のそれぞれの活動において (カスタム活動を除く)、活動関係者のすべての種類が使用可能なわけではありません。 カスタム活動ではすべての活動関係者の種類をサポートします。 活動のそれぞれの属性を使用することにより、活動の活動関係者の種類を関連付けることができます。 たとえば、活動関係者の種類 `Organizer` を予定活動に関連付けるには、`Appointment.Organizer` 属性の `ActivityParty` 種類の値の配列を指定する必要があります。  
  
 活動関係者に電子メールを送信するために使用する電子メール アドレス、または活動関係者からの電子メールに返信するために使用する電子メール アドレスを制御するには、`ActivityParty.AddressUsed` 属性を設定します。  
  
 次の表では、それぞれの活動でサポートされている活動関係者の種類、およびそれらの活動関係者の種類を指定するための対応する活動プロパティを一覧表します。  
  
|活動エンティティ名|サポート対象の活動関係者の種類|活動属性|  
|--------------------------|-----------------------------------|------------------------|  
|予定​​|OptionalAttendee<br />開催者<br />RequiredAttendee|Appointment.OptionalAttendees<br />Appointment.Organizer<br />Appointment.RequiredAttendees|  
|CampaignActivity|発信者|CampaignActivity.Partners<br />CampaignActivity.From|  
|CampaignResponse|Customer|CampaignResponse.Customer<br />CampaignResponse.Partner<br />CampaignResponse.From|  
|電子メールの送信|BccRecipient<br />CcRecipient<br />発信者<br />ToRecipient|Email.Bcc<br />Email.Cc<br />Email.From<br />Email.To|  
|FAX |発信者<br />ToRecipient|Fax.From<br />Fax.To|  
|レター |BccRecipient<br />発信者<br />ToRecipient|Letter.Bcc<br />Letter.From<br />Letter.To|  
|PhoneCall|発信者<br />ToRecipient|PhoneCall.From<br />PhoneCall.To|  
|RecurringAppointmentMaster|OptionalAttendee<br />開催者<br />RequiredAttendee|RecurringAppointmentMaster.OptionalAttendees<br />RecurringAppointmentMaster.Organizer<br />RecurringAppointmentMaster.RequiredAttendees|  
|ServiceAppointment|Customer<br />リソース |ServiceAppointment.Customers<br />ServiceAppointment.Resources|  
  
### <a name="see-also"></a>関連項目  
 [活動エンティティ](activity-entities.md)   
 [タスク活動、FAX 活動、電話活動、およびレター活動のエンティティ](task-fax-phone-call-letter-activity-entities.md)   
 [ActivityParty エンティティ](reference/entities/activityparty.md)   
 [サンプル: 予定の予約](/dynamics365/customer-engagement/developer/sample-book-appointment)<br>
 [サンプル: FAX をタスクに変換する](/dynamics365/customer-engagement/developer/sample-convert-fax-task)   
 [サンプル: 目標の合計件数の上書きおよび目標のクローズ](/dynamics365/customer-engagement/developer/sample-override-goal-total-count-close-goal)   
 [サンプル: 件数の拡大対象に対する、会計期間の目標データのロールアップ](/dynamics365/customer-engagement/developer/sample-rollup-goal-data-fiscal-period-stretch-target-count)   
 [サンプル: テンプレートを使用した電子メールの送信](/dynamics365/customer-engagement/developer/sample-send-email-template)   
 [サンプル: 予定の検証](/dynamics365/customer-engagement/developer/sample-validate-appointment)
