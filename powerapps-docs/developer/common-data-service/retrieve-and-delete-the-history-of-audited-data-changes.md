---
title: 監査済みデータの変更履歴の取得と削除 (Common Data Service) | Microsoft Docs
description: プログラムで監査の変更履歴を取得したり、監査レコードを削除したりします。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: paulliew
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="retrieve-and-delete-the-history-of-audited-data-changes"></a>監査済みデータの変更履歴の取得と削除

監査を有効にし、監査対象のエンティティや属性へのデータ変更を行った後、データ変更履歴の取得に進むことができます。 変更履歴の参照後にオプションで監査レコードを削除することもできます。 詳細については、このトピックの最後にあるサンプル コード リンクを参照してください。  
  
## <a name="retrieve-the-change-history"></a>変更履歴の取得 
 
 変更履歴の取得にはいくつかのメッセージ要求を使用できます。 これらの要求は取得内容で区別されます。 
<!-- Bug 696490 should make the Audit entity public again: Refer to the topic  [Audit Entity](entities/audit.md) for a list of message requests related to auditing. -->
これらの変更履歴メッセージ要求を使ったサンプル コードについては、このトピックの最後にあるサンプル リンクを参照してください。

## <a name="delete-the-change-history-for-a-record"></a>レコードの変更履歴の削除
 
 <xref:Microsoft.Crm.Sdk.Messages.DeleteRecordChangeHistoryRequest> メッセージを使用して、特定のレコードの監査変更履歴レコードすべてを削除します。 これにより、日付範囲の監査レコードすべてを削除する代わりに、レコードの監査変更履歴を削除することができます。日付範囲の監査レコードの変更は次のセクションで扱われます。 レコードの監査変更履歴を削除するには、**prvDeleteRecordChangeHistory** 特権を含むセキュリティ ロールを保持するか、システム管理者である必要があります。

## <a name="delete-the-change-history-for-a-date-range"></a>日付範囲の変更履歴の削除

 日付範囲の`audit`レコードを削除するには、<xref:Microsoft.Crm.Sdk.Messages.DeleteAuditDataRequest> 要求を使用します。 監査データ レコードは古いものから新しいものへと順に削除されます。 この要求の機能は、現在の Common Data Service サーバーで使われている Microsoft SQL Server のエディションによって若干異なります。 Common Data Service では SQL Server の Enterprise Edition を使用します。

 現在の Common Data Service サーバーで使われている SQL Server が Standard Edition の場合、データベース分割機能がサポートされていないので、<xref:Microsoft.Crm.Sdk.Messages.DeleteAuditDataRequest> 要求は、<xref:Microsoft.Crm.Sdk.Messages.DeleteAuditDataRequest.EndDate> プロパティが示す最終日までに作成されたすべての監査レコードを削除します。

 Common Data Service サーバーで使われている SQL Server が分割サポートなしの Enterprise Edition の場合、<xref:Microsoft.Crm.Sdk.Messages.DeleteAuditDataRequest> 要求は、終了日が <xref:Microsoft.Crm.Sdk.Messages.DeleteAuditDataRequest.EndDate> プロパティの日付よりも前のパーティションに含まれているすべての監査データを削除します。 空のパーティションがあれば、それも削除します。 ただし、現在の (アクティブな) パーティションと、アクティブ パーティション内の`audit`レコードを、この要求やその他の要求で削除することはできません。

 新しいパーティションは、毎年四半期ごとに Common Data Service プラットフォームが自動的に作成します。 この機能は構成も変更もできません。 パーティションの一覧を取得するには、<xref:Microsoft.Crm.Sdk.Messages.RetrieveAuditPartitionListRequest> 要求を使います。 パーティションの終了日が現在の日付よりも後の場合、そのパーティションやパーティション内の`audit`レコードを削除することはできません。  

### <a name="see-also"></a>関連項目

 [Dynamics 365 でのデータ管理](/dynamics365/customer-engagement/developer/manage-data)<br />
 [監査エンティティのデータ変更](/dynamics365/customer-engagement/developer/audit-entity-data-changes)<br />
 [ユーザー アクセスの監査](audit-user-access.md) <br />
 [サンプル: エンティティのデータ変更を監査する](org-service/samples/audit-entity-data-changes.md)