---
title: 特化された更新操作の動作 (Common Data Service for Apps) | Microsoft Docs
description: 廃止されたメッセージが原因で生じる更新イベントのプラグインおよびワークフローにおける特殊な動作について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="behavior-of-specialized-update-operations"></a>特化された更新操作の動作

更新操作を実行する複数の削除され特化されたメッセージです。 以前のバージョンではこれらのメッセージを使用する必要がありましたが、現在は同じ操作で<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>を使用して実行されます。 または<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest>クラスおよび<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*>

[!INCLUDE [cc-legacy-update-messages](includes/cc-legacy-update-messages.md)]

詳細: [従来の更新メッセージ](org-service/entity-operations-update-delete.md#legacy-update-messages) 

この変更では、プラグインとワークフローで注意する必要がある特別な動作が追加されました。 

## <a name="for-plug-ins"></a>プラグインの場合

両方の所有者フィールドのほかに部署所有のエンティティ用のその他のフィールドを含む更新要求が処理されると、**PreOperation** および/または **PostOperation** ステージの**更新**メッセージに対して登録されたプラグインは、所有者以外のすべてのフィールドに対して 1 回実行され、次に所有者フィールドに対して 1 回実行されます。 所有者フィールドの例は、`businessunit` および `manager` ([SystemUser エンティティ](reference/entities/systemuser.md)の場合) です。 ビジネスが所有するエンティティの例には、[SystemUser](reference/entities/systemuser.md)、[BusinessUnit](reference/entities/businessunit.md)、[Equipment](/dynamics365/customer-engagement/developer/entities/equipment)、[Team](reference/entities/team.md) があります。

両方の状態/ステータス フィールドのほかにその他のフィールドを含む更新要求が処理されると、**PreOperation** および/または **PostOperation** ステージの**更新**メッセージに対して登録されたプラグインは、状態/ステータス以外のすべてのフィールドに対して 1 回実行され、次に状態/ステータス フィールドに対して 1 回実行されます。

プラグイン コードが更新の完全なデータ変更を受け取るには、プラグインを **PreOperation** に登録した後、後のプラグイン (プラグインに含まれる) が消費する場合のプラグインのコンテキストで、関連情報を <xref:Microsoft.Xrm.Sdk.IExecutionContext.SharedVariables> に格納する必要があります。

## <a name="for-workflows"></a>ワークフローの場合

両方の所有者フィールドのほかにその他の標準フィールドを含む更新要求が処理されると、**更新**メッセージに対して登録されたワークフローは、所有者以外のすべてのフィールドに対して 1 回実行され、次に所有者フィールドに対して 1 回実行されます。 ユーザーによって**割り当て**メッセージに対して登録されたワークフローは、所有者フィールドの更新によって起動されます。

両方の状態 / ステータス フィールドのほかにその他の標準フィールドを含む更新要求が処理されると、**更新**メッセージに対して登録されたワークフローは、状態 / ステータス以外のすべてのフィールドに対して 1 回実行され、次に状態 / ステータス フィールドに対して 1 回実行されます。 **状態の変更**ステップに対して登録されたワークフローは、状態 / ステータス フィールドの更新によって引き続きトリガーされます。

### <a name="see-also"></a>関連項目

[組織サービスを使用したエンティティの更新と削除](org-service/entity-operations-update-delete.md)<br />
[イベント フレームワーク](event-framework.md)