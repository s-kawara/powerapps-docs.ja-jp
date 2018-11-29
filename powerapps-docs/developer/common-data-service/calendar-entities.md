---
title: カレンダー エンティティ (アプリ用 Common Data Service) | Microsoft Docs
description: カレンダー エンティティを使用して、顧客サービス カレンダーおよび祝日スケジュールのためのデータを格納する方法をご覧ください。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="calendar-entities"></a>カレンダー エンティティ

カレンダー エンティティは、業務カレンダーに加え、顧客サービス カレンダーおよび祝日スケジュールのためのデータを格納します。 各カレンダーは、特定のタイム ゾーンに設定されます。  
  
 カレンダーは、サービスやリソースの可用性を示します。 カレンダーは、`calendarrule` レコードに関連付けられます。このレコードには、期間、開始と終了時刻、およびカレンダーに含まれるイベントの定期的なパターンの詳細が含まれています。  
  
 アプリ用 Common Data Service には 2 種類のカレンダー ルールがあります。  
  
- **ルート**: 内部カレンダーを含むか入れ子になった (リーフ) ルールがあるカレンダー ルール。 `CalendarRule.InnerCalendarId` 属性を使用して、ルート カレンダー ルールの内部カレンダーを指定できます。 ルート ルールの `CalendarRule.InnerCalendarId` の属性値は、そのリーフ ルールの `CalendarRule.CalendarId` の属性値と同じです。  
  
- **リーフ**: 内部カレンダーを含まないため、"分岐" の最後であるカレンダー ルール。  
  
 カレンダー ルールには、それらの優先順位を記述する順序 (ランク) が設定されており、場合によってはルールが重複することもあります。 入れ子になったルール拡張によって、ルールの時間帯 (範囲) が定義されます。 `CalendarRule.ExtentCode` 属性を使用して、ルール拡張の重複がどのように処理されるかを定義します。たとえば、時間帯またはルールの拡張の両方が表示されるか、一方のみが表示されるかなどが設定されます。 これらの機能によって、定期的なパターンを表現できます。たとえば、単一のサービス カレンダーで、冬期と夏期で異なるシフト スケジュールを設定できます。  
  
 カレンダーが、ルールおよび入れ子になったカレンダーの複合ツリーとして、作業スケジュールを高レベルで抽象化している場合があります。 カレンダー エンティティは、簡易ビュー、つまり特定範囲における空き時間を決定する時間ブロックの配列に変換するための <xref:Microsoft.Crm.Sdk.Messages.ExpandCalendarRequest> メッセージをサポートしています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [カレンダーの種類](types-calendars.md)  
  
 [カレンダー エンティティ](/reference/entities/calendar.md)  
  
## <a name="related-sections"></a>関連セクション  
 [予定エンティティ](/dynamics365/customer-engagement/developer/appointment-entities)  
  
 [定期的な予定エンティティ](/dynamics365/customer-engagement/developer/recurring-appointment-entities)  
  
 [リソース エンティティ](/dynamics365/customer-engagement/developer/resource-entities)  
  
 [サービス エンティティ](/dynamics365/customer-engagement/developer/service-entity)  
  
 [スケジュールおよび予定エンティティのサンプル コード](/dynamics365/customer-engagement/developer/sample-code-schedule-appointment-entities)