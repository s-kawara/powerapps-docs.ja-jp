---
title: <Topic Title> (アプリ用 Common Data Service) | Microsoft Docs
description: <Description>
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
# <a name="asynchronous-service"></a>非同期サービス

非同期サービスは、アプリ用 Common Data Service のメインのコア操作から独立して長時間の操作を実行します。 そのため、システム全体のパフォーマンスとスケーラビリティが向上します。 非同期サービスの機能として、非同期の登録プラグイン、ワークフロー、および大容量メール、一括インポート、キャンペーン活動の伝達などの非同期の操作を実行するための管理された先入先出 (FIFO) キューがあります。 これらの操作は非同期サービスに登録され、サービスによってキューが処理されるときに定期的に実行されます。


イベントが発生して同期拡張が処理された後、プラットフォームは非同期拡張のコンテキストをシリアル化し、[AsyncOperation エンティティ](reference/entities/asyncoperation.md) の**システム ジョブ**としてデータベースに保存されます。 システム ジョブは非同期操作の実行を定義および追跡します。 リソースが利用可能になると、システムジョブが処理され、定義する操作が実行されます。 拡張で定義された任意のデータ操作は、イベント実行パイプラインにより再度処理されますが、今回は同期操作として処理されます。

## <a name="execution-order-and-dependencies"></a>実行順序および依存関係

[CreatedOn](reference/entities/asyncoperation.md#BKMK_CreatedOn) 日付を使用するキューとして、システム ジョブは評価されます。 実行を遅らせる条件がない場合、リソースが利用可能になるとすぐに実行されます。 異なるタイプの操作には異なるリソースが必要となるため、`CreatedOn` 日付で設定された順序で実行されることは保証されていません。

システムジョブは別のシステムジョブに依存するため、他のシステムジョブが完了した後にのみ開始されます。 この依存関係は、[DependencyToken](reference/entities/asyncoperation.md#BKMK_DependencyToken) 属性値により確立されます。 システム ジョブが作成されると、依存関係が確立されます。 `DependencyToken` 値が null の場合、システム ジョブには依存関係がありません。 依存しているシステム ジョブには同じ `DependencyToken` 値があり、作成された順序で実行されます。 システム ジョブが延期された場合、それ以降のすべての依存システム ジョブは延期されたシステム ジョブが実行されるまで待機し続けます。

> [!NOTE]
> 依存関係システムのシステム ジョブはシステムによって作成されるため、この依存関係システムは非同期で実行するように登録されたプラグインでは使用できません。

## <a name="managing-system-jobs"></a>システム ジョブの管理

[AsyncOperation エンティティ](reference/entities/asyncoperation.md) を使用して、システム ジョブを管理する次の操作を実行できます。

- システム ジョブの取得
- システム ジョブの削除
- システム ジョブ状態の管理
- システム ジョブの延期

> [!NOTE]
> コードでのシステム ジョブの作成はサポートされていません。 `AsyncOperation` エンティティがいくつかの書き込み可能な属性と作成操作をサポートしていますが、次の属性のみは更新用にサポートされています。
> - [StateCode](reference/entities/asyncoperation.md#BKMK_StateCode)
> - [StatusCode](reference/entities/asyncoperation.md#BKMK_StatusCode)
> - [PostPoneUntil](reference/entities/asyncoperation.md#BKMK_PostponeUntil)



## <a name="retrieve-system-jobs"></a>システム ジョブの取得

**設定** > **システム** > **システム ジョブ**の順に移動してアプリケーションのシステム ジョブを表示でき、高度な検索を使用して検索もできます。

コードを使用すると、他のエンティティのようにシステムジョブを取得できます。 次の表では、システム ジョブを理解するのに重要な選択された属性が表示されます。

|**属性**|**説明**|
|--|--|
|`AsyncOperationId`|システム ジョブを表す一意識別子です。|
|`CompletedOn`|システム ジョブが完了した日時です。|
|`CreatedBy`|システム ジョブを作成したユーザーを表す一意識別子です。|
|`CreatedOn`|システム ジョブが作成された日時です。|
|`Data`|システム ジョブに関連付けられている構造化されていないデータです。|
|`DependencyToken`|同じ依存関係トークンを持つすべての操作の実行がシリアル化されます。 詳細: [実行順序および依存関係](#execution-order-and-dependencies) |
|`Depth`|最初の呼び出し以降の SDK 呼び出しの数です。|
|`ErrorCode`|取り消したシステム ジョブから返されたエラー コードです。|
|`ExecutionTimeSpan`|システム ジョブの実行にかかった時間です。|
|`FriendlyMessage`|システム ジョブによって提供されるメッセージです。|
|`IsWaitingForEvent`|システム ジョブがイベントの待機中であることを示します。|
|`Message`|システム ジョブに関連するメッセージです。|
|`MessageName`|このシステム ジョブを開始したメッセージの名前です。|
|`ModifiedBy`|システム ジョブを最後に修正したユーザーを表す一意の識別子です。|
|`ModifiedOn`|システム ジョブが最後に修正された日時です。|
|`Name`|システム ジョブの名前です。|
|`OperationType`|システム ジョブの種類です。 詳細: [操作の種類](#operation-types)|
|`OwnerId`|システム ジョブを所有するユーザーまたはチームを表す一意識別子です。|
|`OwningBusinessUnit`|システム ジョブを所有する部署を表す一意の識別子です。|
|`OwningExtensionId`|システム ジョブが関連付けられている所有する拡張を表す一意識別子です。|
|`OwningTeam`|レコードを所有するチームを表す一意識別子です。|
|`OwningUser`|レコードを所有するユーザーを表す一意識別子です。|
|`PostponeUntil`|システム ジョブの実行時期を、指定された日時の後のみに制限するかどうかを表します。 詳細: [システム ジョブの延期](#postpone-system-jobs)|
|`PrimaryEntityType`|システム ジョブが主に関連付けられているエンティティの種類です。|
|`RecurrencePattern`|システム ジョブの定期的なアイテムのパターンです。 詳細: [定期的なアイテムの開始時刻とパターン](#recurrence-start-times-and-patterns)|
|`RecurrenceStartTime`|定期的なアイテムのパターンの開始時間 (UTC) です。 詳細: [定期的なアイテムの開始時刻とパターン](#recurrence-start-times-and-patterns)|
|`RegardingObjectId`|システム ジョブが関連付けられているオブジェクトを表す一意の識別子です。|
|`RetryCount`|システム ジョブの再試行回数です。|
|`Sequence` |操作が提出された順序です。|
|`StartedOn`|システム ジョブが開始された日時です。|
|`StateCode`|システム ジョブの状態です。 詳細: [システム ジョブ状態の管理](#manage-system-job-states)|
|`StatusCode`|システム ジョブの状態の理由です。 詳細: [システム ジョブ状態の管理](#manage-system-job-states)|
|`UTCConversionTimeZoneCode` |レコードが作成されたときに使用中だったタイム ゾーン コードです。|
|`WorkflowStageName` |ワークフロー段階の名前です。 |

### <a name="examples"></a>例

システム ジョブ データを取得する次の例を使用できます。

#### <a name="web-api"></a>Web API

次の Web API クエリを使用して、上記の表にある属性を取得できます。 詳細: [Web API を使用するクエリ データ](webapi/query-data-web-api.md)

```
<organization URL>/api/data/v9.0/asyncoperations?
$select=
asyncoperationid,
completedon,
createdon,
data,
dependencytoken,
depth,
errorcode,
executiontimespan,
friendlymessage,
iswaitingforevent,
message,
messagename,
modifiedon,
name,
operationtype,
_ownerid_value,
postponeuntil,
primaryentitytype,
recurrencepattern,
recurrencestarttime,
_regardingobjectid_value,
retrycount,
sequence,
startedon,
statecode,
utcconversiontimezonecode,
workflowstagename
&$expand=
createdby($select=fullname),
modifiedby($select=fullname),
owningbusinessunit($select=name),
owningextensionid($select=name),
owningteam($select=name),
owninguser($select=fullname)

```

> [!NOTE]
> Web API には、システム ジョブをサポートする各エンティティーに対して、単一値のナビゲーション プロパティがあります。 このナビゲーション プロパティの名前は、パターン `regardingobjectid_<entity logical name>` に従います。

#### <a name="fetchxml"></a>FetchXml

次の FetchXML クエリを使用して、上記の表にある属性を取得できます。 詳細: [FetchXML の使用によるクエリの作成](use-fetchxml-construct-query.md)

```xml
<fetch>
  <entity name="asyncoperation" >
    <attribute name="asyncoperationid" />
    <attribute name="completedon" />
    <attribute name="createdby" />
    <attribute name="createdon" />
    <attribute name="data" />
    <attribute name="dependencytoken" />
    <attribute name="depth" />
    <attribute name="errorcode" />
    <attribute name="executiontimespan" />
    <attribute name="friendlymessage" />
    <attribute name="iswaitingforevent" />
    <attribute name="message" />
    <attribute name="messagename" />
    <attribute name="modifiedby" />
    <attribute name="modifiedon" />
    <attribute name="name" />
    <attribute name="operationtype" />
    <attribute name="ownerid" />
    <attribute name="owningbusinessunit" />
    <attribute name="owningextensionid" />
    <attribute name="owningteam" />
    <attribute name="owninguser" />
    <attribute name="postponeuntil" />
    <attribute name="primaryentitytype" />
    <attribute name="recurrencepattern" />
    <attribute name="recurrencestarttime" />
    <attribute name="regardingobjectid" />
    <attribute name="retrycount" />
    <attribute name="sequence" />
    <attribute name="startedon" />
    <attribute name="statecode" />
    <attribute name="utcconversiontimezonecode" />
    <attribute name="workflowstagename" />
  </entity>
</fetch>
```

> [!NOTE]
> システムジョブをサポートする各エンティティには、`RegardingObjectId` 検索属性を経由する `AsyncOperation` エンティティとの表示された多対一の関係があります。 この関係の名前は、パターン `<entity schema name>_AsyncOperations` に従います。

### <a name="operation-types"></a>操作の種類

[OperationType](reference/entities/asyncoperation.md#BKMK_OperationType) 属性はシステム ジョブのカテゴリを記述します。 これらの種類の多くは、メンテナンス作業を実行するためのプラットフォームによって開始されます。 

> [!NOTE]
> プラットフォームによりで生成されるシステム ジョブで、操作のキャンセル、一時停止、または再開を実行することはできません。 

これらのプラットフォーム生成ジョブの種類の一部は、次の表に含まれています。

|**OperationType 値**|**OperationType ラベル**|
|--|--|
|9|SQM データ収集|
|16|組織統計の収集|
|18|組織の記憶域サイズの計算|
|19|組織のデータベース統計の収集|
|20|組織規模統計の収集|
|22 |組織の最大記憶域サイズの計算|
|24|統計の更新間隔|
|25 |組織のフル テキスト カタログ インデックス|
|27|契約の状態の更新|
|31|記憶域制限の通知|

### <a name="recurrence-start-times-and-patterns"></a>定期実行の開始時刻とパターン

定期実行のシステム ジョブには、開始時期および頻度に関する情報が必要です。 これらの値は `AsyncOperation` エンティティ `RecurrenceStartTime` および `RecurrencePattern` 属性に格納されます。

コードで直接 `AsyncOperation` エンティティを作成しないため、データをクエリする場合、これらの値を解釈するだけで済みます。 新しいシステム ジョブを作成するメッセージを使用して、間接的にこれらのプロパティのみを設定します。 `BulkDelete` および `BulkDeleteDuplicates` メッセージの両方には、対応する Web API アクションまたは組織サービス要求クラスのパラメータまたはプロパティが含まれます。 詳細: <xref:Microsoft.Crm.Sdk.Messages.BulkDetectDuplicatesRequest> クラス、<xref href="Microsoft.Dynamics.CRM.BulkDetectDuplicates?text=BulkDetectDuplicates Action" />、<xref:Microsoft.Crm.Sdk.Messages.BulkDeleteRequest> クラス、および <xref href="Microsoft.Dynamics.CRM.BulkDelete?text=BulkDelete Action" />

`RecurrenceStartTime` は、単にシステムジョブがいつ開始されるべきかを示す日時の値です。 それが設定されていない場合、システム ジョブはすぐに開始すると想定されます。

`RecurrencePattern` 属性は、定期的なシステム ジョブの発生頻度に関する情報を格納します。 この値は、新しい asyncoperation エンティティが作成されたときにプラットフォームにより設定されていることがあります。 この値を設定してパターンを変更することができます。

この属性の値は [RFC2445 Internet standard (Internet Calendaring and Scheduling Core Object Specification)](http://www.rfc-editor.org/info/rfc2445) の一部を使用します。

以下の表で、例を示します。

|定期的なパターン|ジョブ実行の頻度|
|--|--|
|`FREQ=MONTHLY;`|1 か月に 1 回|
|`FREQ=WEEKLY;`|1 週間に 1 回|
|`FREQ=DAILY;`|1 日に 1 回|
|`FREQ=DAILY;INTERVAL=3;`|3 日ごと|
|`FREQ=HOURLY;`|1 時間に 1 回|

`INTERVAL` 値が設定されていない場合、`1` として解釈されます。

## <a name="delete-system-jobs"></a>システム ジョブの削除

必要な特権を持っている場合は、アプリケーションまたはコード内のシステム ジョブを他のエンティティと同じように削除できます。

> [!NOTE]
> 非同期プラグインを登録する場合、成功した操作を自動的に削除するオプションがあります。 そのオプションを使用することをお勧めします。 詳細: [プラグインを記述する](write-plug-in.md)

一般的な方法は、成功したジョブを削除する定期的な一括削除ジョブを作成することです。 詳細: [大容量の特定の対象データを一括削除で削除する](/dynamics365/customer-engagement/admin/delete-bulk-records)

## <a name="manage-system-job-states"></a>システム ジョブ状態の管理

システム ジョブの状態は、操作が完了するまで何度か変更されます。 以下は使用可能な状態およびステータス値を表す `StateCode` および `StatusCode` オプションです。

|StateCode 値|StateCode ラベル|StatusCode 値|StatusCode ラベル|
|--|--|--|--|
|`0`|準備完了|`0`|リソースの待機中|
|`1`|中止|`10`|待機中|
|`2`|Locked|`20`|処理中|
|`2`|Locked|`21`|一時停止の処理中|
|`2`|Locked|`22`|取り消し中|
|`3`|完了|`30`|成功|
|`3`|完了|`31`|失敗|
|`3`|完了|`32`|キャンセル|

**設定** > **システム** > **システム ジョブ**の順に移動して、および**その他の操作**メニューで利用可能なコマンドを使用して、アプリケーションのシステム ジョブの状態を表示できます。

![アプリケーションのシステム ジョブに対して使用可能なアクション コマンド](media/system-jobs-more-actions-commands.png)

> [!NOTE]
> この UI 経由で実行できる任意のアクションは、コードを使用して実行することもできます。 プラットフォームによりで生成されるシステム ジョブで、操作のキャンセル、一時停止、または再開を実行することはできません。 詳細: [操作の種類](#operation-types)

ビューを管理するオプションと共に、システム ジョブを管理するための次のオプションが利用できます。 

|オプション|説明|
|--|--|
|削除|コントロール ID およびカスタム アクションの場所で ![削除コマンド](../../maker/common-data-service/media/delete.gif) コマンド。<br />システム ジョブを削除します|
|一括削除|**その他の操作**メニューを使用しています。<br />条件を定義するウィザードを開き、一致するシステム ジョブを削除する新しい一括削除システム ジョブを作成します。|
|キャンセル|**その他の操作**メニューを使用しています。<br />システム ジョブをキャンセルします。|
|[再開]|**その他の操作**メニューを使用しています。<br />一時停止したシステム ジョブを再開します。|
|[後で再起動]|**その他の操作**メニューを使用しています。<br />システム ジョブのスケジュール変更|
|[一時停止]|**その他の操作**メニューを使用しています。<br />システム ジョブを一時停止します。|

要求された操作が実行されるかどうかは、システム ジョブの状態によって異なります。 たとえば、すでに完了した、またはまだ開始していないジョブを一時停止することはできません。 以下の表は、各変更の条件と、変更が選択されたときに何が起こるかを示しています。

|オプション|有効な StateCode 値|変更|
|--|--|--|
|削除|指定なし|システム ジョブを削除します|
|キャンセル|0 (準備完了) <br /> 1 (中止) <br /> 2 (ロック)|`StateCode` が 3 (完了済み) に変更され、`StatusCode` が 32 (キャンセル済み) に変更されました|
|[再開]|1 (中止)|StateCode が 0 (準備完了) に変更されました|
|[後で再起動]|0 (準備完了) <br />2 (ロック)|ジョブの延期ダイアログでは、ユーザーは日時の値に関してシステム ジョブを延期するよう求められます。 詳細: [システム ジョブの延期](#postpone-system-jobs)|
|[一時停止]|2 (ロック)|StateCode が 1 (中止) に変更されました|


## <a name="postpone-system-jobs"></a>システム ジョブの延期

システム ジョブが 1 (中止) から 0 (準備完了) に変更されると、`PostPoneUntil` 属性には日時の値が含まれます。 `StateCode` および `StatusCode` 属性と共に、 これらは `AsyncOperation` エンティティを使用するときに更新に対してサポートされる唯一の属性です。

### <a name="see-also"></a>関連項目

[プラグインを記述する](write-plug-in.md)<br />
[ビジネス プロセスを拡張するためのプラグインを記述する](plug-ins.md) <br />

