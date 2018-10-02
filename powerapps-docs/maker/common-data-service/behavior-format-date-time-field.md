---
title: アプリ用 Common Data Service の日時フィールドの動作と形式 | MicrosoftDocs
ms.custom: ''
ms.date: 05/25/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: 73d691c7-344e-4c96-8979-c661c290bf81
caps.latest.revision: 47
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="behavior-and-format-of-the-date-and-time-field"></a>日時フィールドの動作と形式

アプリ用 Common Data Service では、日時のデータ型が多数の標準エンティティ フィールドで使用されます。 フィールドが表す日付の種類に応じて、**ユーザー ローカル**、**日付のみ**、または**タイム ゾーン非依存**という異なるフィールドの動作を選択できます。  
  
<a name="Behavior"></a>   

## <a name="date-and-time-field-behavior-and-format"></a>日時フィールドの動作と形式  

次の表には、[日付と時刻]フィールドの動作と形式に関する説明が含まれています。  
  
|動作|書式|説明|  
|--------------|------------|-------------------------------|  
|**ユーザー ローカル** |**日付のみ**<br />- または -<br />**日付と時間**|これは、ユーザー定義の日付フィールドの既定の動作です。<br /><br />フィールドの値は、ユーザーの現在のローカル時間で表示されます。<br />Web サービスでは、これらの値は、共通の UTC タイム ゾーン形式を使用して返されます。<br /><br />既定の動作を選択した場合、これを 1 回だけ変更することができます。 詳細 [ユーザー ローカル動作の変更](#change-user-local-behavior)|  
|**日付のみ**|**日付のみ**|タイム ゾーン変換はありません。<br /><br />値の時刻の部分は、常に午前 12:00 です。<br />値の日付の部分は、UI と Web サービスで指定されている通りに保存および取得されます。|  
|**タイム ゾーン非依存**|**日付のみ**<br />- または -<br />**日付と時間**|タイム ゾーン変換はありません。<br /><br />日付と時刻の値は、UI と Web サービスで指定されている通りに保存および取得されます。|  

## <a name="change-user-local-behavior"></a>ユーザー ローカル動作の変更:

マネージド ソリューションの発行者がこれを禁止しない限り、既存のカスタム日付フィールドの動作を**ユーザー ローカル**から**日付のみ**、または**タイムゾーン非依存**へ変更することができます。 これは一度のみの変更です。

フィールドの動作を変更すると、フィールドの動作の変更後に追加または変更されるフィールド値に影響があります。 既存のフィールド値は、データベース内では、UTC タイム ゾーン形式のままです。 既存のフィールド値の動作を UTC から [日付のみ] に変更するには、それをプログラムで実行するために開発者の助けが必要な場合があります。 詳細: [データベース内の既存の日時の値の動作を変更する](/dynamics365/customer-engagement/developer/behavior-format-date-time-attribute#convert-behavior-of-existing-date-and-time-values-in-the-database). 

> [!WARNING]
> 既定の日時フィールドの動作を変更するには、その前に、業務ルール、ワークフロー、計算フィールド、またはロールアップ フィールドなどのフィールドのすべての依存関係を検討して、動作の変更によって問題が発生しないことを確認する必要があります。 日時フィールドの動作を変更した後、変更したフィールドに依存する、業務ルール、ワークフロー、計算フィールド、およびロールアップ フィールドのそれぞれを開いて、情報を確認し、その情報を保存して、最後の日付フィールドの動作と値が使用されることを確認する必要があります。 

### <a name="change-behavior-during-a-solution-import"></a>ソリューションのインポート中に動作を変更する

**ユーザー ローカル**動作を使用して日付フィールドを含むソリューションをインポートする場合は、動作を**日付のみ**または**タイムゾーン非依存**に変更することもできます。  

### <a name="prevent-changing-behavior"></a>動作の変更を防ぐ

マネージド ソリューションの既存の日付フィールドを配布する場合は、**CanChangeDateTimeBehavior** 管理プロパティを **False** に設定し、ソリューションを使用するユーザーが動作を変更しないようにすることができます。 詳細: [フィールド管理プロパティ](set-managed-properties-metadata.md#field-managed-properties)
  
## <a name="use-cases"></a>使用例

次の**日付のみ**および**タイム ゾーン非依存**動作の使用例について考えてみましょう。

### <a name="date-only-scenario-birthdays-and-anniversaries"></a>日付のみの例: 誕生日と記念日

[日付のみ] の動作は、誕生日や記念日などの、時刻とタイムゾーンに関する情報が必要ない場合に適しています。 この選択の場合、 世界のすべてのアプリ ユーザーに、まったく同じ日付の値が表示されます。  
  
### <a name="time-zone-independent-scenario-hotel-check-in"></a>タイム ゾーン非依存の例: ホテルのチェックイン

ホテル チェックインの時間など、タイム ゾーン情報が必要でないときに、この動作を使用できます。 これを選択した場合、全世界のすべてのアプリ ユーザーに、同じ日時の値が表示されます。  


## <a name="date-and-time-query-operators-not-supported-for-date-only-behavior"></a>[日付のみ] の動作でサポートされない日付および時刻のクエリ演算子  

次の日付および時刻関連のクエリ演算子は、**日付のみ**に対しては無効です。 これらの演算子の 1 つが使用されると、無効な演算子の例外エラーがスローされます。  
  
- が X 分よりも古い  
- が X 時間よりも古い  
- 過去 X 時間  
- 今後 X 時間  

  
### <a name="see-also"></a>関連項目

[フィールドの作成および編集](create-edit-fields.md)<br />
[計算フィールドを定義して手動計算を自動化する](define-calculated-fields.md)<br />
[フィールド管理プロパティ](set-managed-properties-metadata.md#field-managed-properties)<br />
[マネージド プロパティ](solutions-overview.md#managed-properties)

