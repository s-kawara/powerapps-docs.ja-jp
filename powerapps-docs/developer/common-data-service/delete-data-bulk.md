---
title: データの一括削除 (Common Data Service) | Microsoft Docs
description: データの一括削除は、不必要になったデータを削除することにより、データ品質の維持およびシステム ストレージの消費管理を支援します。
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
# <a name="delete-data-in-bulk"></a>データの一括削除

*一括削除* 機能を使用すると、データ品質を維持し、必要なくなったデータを削除して Common Data Service のシステム ストレージ消費を管理するために役立ちます。 たとえば、次のデータを一括で削除できます。  
  
- 古いデータ。  
  
- 業務に無関係なデータ。  
  
- 不要なテスト データやサンプル データ。  
  
- 他のシステムから誤ってインポートされたデータ。  
  
一括削除を使用して、以下の操作を実行できます:  
  
- 複数のエンティティにまたがるデータを削除する。  
  
- 特定のエンティティのレコードを削除する。  
  
- 一括削除の完了時に、電子メールで通知を受信します。  
  
- データを定期的に削除する。  
  
- 定期的な一括削除の開始時間をスケジュールする。  
  
- 一括削除の間に発生した失敗に関する情報を取得する。  
  
## <a name="run-bulk-delete"></a>一括削除の実行

大量のデータを削除するには、<xref:Microsoft.Crm.Sdk.Messages.BulkDeleteRequest> メッセージを使用して一括削除ジョブを送信する必要があります。 一括削除ジョブはバックグラウンドで非同期的に実行されるので他の活動を中断することはありません。 一括削除ジョブを実行するレコードを記述するクエリ式は、この要求の <xref:Microsoft.Crm.Sdk.Messages.BulkDeleteRequest.QuerySet> プロパティで指定されます。  
  
 一括削除ジョブは、一括削除操作エンティティによって表されます。 このエンティティのスキーマ名は `BulkDeleteOperation` です。 一括削除操作レコードには次の情報が含まれています。  
  
- 一括削除ジョブで削除したレコードの数。  
  
- 一括削除ジョブで削除できなかったレコードの数。  
  
- 一括削除ジョブが定期的なジョブかどうか。  
  
- 一括削除ジョブの開始時刻。  
  
  一括削除ジョブは、ジョブの実行開始前に作成されたレコードのみを削除します。  
  
> [!NOTE]
>  一括削除ジョブが失敗するか途中で終了した場合、ジョブが失敗する前または終了する前に削除されたレコードはロールバックされず、削除されたままとなります。 `BulkDeleteOperation` の失敗は `BulkDeleteFailure` レコードに保存され、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveRequest> メッセージまたは <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMultipleRequest> メッセージを使用して取得できます。  
  
 一括削除ジョブは、伝播規則に従って特定のレコードを削除します。 これらの規則は、エンティティ間の関連付けの種類に基づいています。 詳細については、「[エンティティの関連付けの動作](/dynamics365/customer-engagement/developer/entity-relationship-behavior)」を参照してください。  
  
 一括削除ジョブを実行するには、削除するエンティティの種類に対する `BulkDelete` および `Delete` 特権が必要です。 また、<xref:Microsoft.Crm.Sdk.Messages.BulkDeleteRequest> メッセージで指定されているエンティティ レコードに対する読み取りアクセス許可も必要です。 既定では、システム管理者には必要なアクセス許可が与えられていますが、他のユーザーにはこれらのアクセス許可を与える必要があります。  
  
 一括削除は、削除アクションでサポートされているすべてのエンティティに対して実行できます。 エンティティ レコードに使用可能なアクションについては、「[エンティティ レコードに対する操作](/dynamics365/customer-engagement/developer/introduction-entities#ActionsOnEntityRecords)」を参照してください。  
  
 プラグインまたはワークフロー (プロセス) が、特定の種類のエンティティに対する削除アクションによってトリガーされる場合は、この種類のエンティティ レコードが一括削除ジョブで削除されるたびにトリガーされます。  
  
## <a name="samples"></a>サンプル

一括削除機能については次の組織サービス サンプルを参照してください:

- [サンプル: エクスポート済みレコードの一括削除](org-service/samples/bulk-delete-exported-records.md)   
- [サンプル: 共通の条件に合致するレコードを一括して削除する](org-service/samples/bulk-delete-records-match-common-criteria.md)

### <a name="see-also"></a>関連項目

[BulkDeleteOperation エンティティ](reference/entities/bulkdeleteoperation.md)