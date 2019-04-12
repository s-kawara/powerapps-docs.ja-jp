---
title: 'サンプル: 定期的な予定の再スケジュールおよび取り消し (Common Data Service) | Microsoft Docs'
description: このサンプルでは、定期的な予定の再スケジュールおよび取り消し方法を示します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: samples
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-reschedule-and-cancel-a-recurring-appointment"></a>サンプル: 定期的な予定の再スケジュールおよび取り消し

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-reschedule-cancel-recurring-appointment -->

このサンプルでは、[RescheduleRequest](https://docs.microsoft.com/dotnet/api/microsoft.crm.sdk.messages.reschedulerequest?view=dynamics-general-ce-9) メッセージを使用して、一連の定期的な予定内の予定インスタンスを再スケジュールおよび取り消す方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/RecurringAppointment) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`RescheduleRequest` メッセージは、予定、定期的な予定、またはサービスの予定 (サービス活動) を再スケジュールするために必要なデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。 
2. 匿名型を定義し、使用可能な定期パターンと曜日の有効値を定義します。
3. 匿名型を定義し、定期ルール パターンの最後の型の有効値を定義します。
4. `RecurringAppointmentMaster` は、新しい定期的な予定を作成します。

### <a name="demonstrate"></a>使用方法

1. `QueryExpression` メッセージは、今日から 10 日後以降の個々の予定インスタンスを照会します。 基本的には、これは定期的な予定シリーズの 2 番目のインスタンスです。
3. `RescheduleRequest` メッセージは、予定のスケジュールの開始日と終了日を更新します。
4. `SetStateRequest` メッセージは、予定の最後のインスタンスを取り消します。 この予定インスタンスの状態は `canceled` に設定されます。 `All Activities` ビューでこの予定インスタンスを表示できます。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup)で作成されたサンプル データを削除するオプションを表示します。
    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。
