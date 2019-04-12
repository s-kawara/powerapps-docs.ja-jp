---
title: 重複ルール エンティティ (Common Data Service) | Microsoft Docs
description: これらのエンティティには重複データ検出ルールを定義するデータが含まれています。
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
# <a name="duplicate-rule-entities"></a>重複ルール エンティティ

アプリケーションで重複ルールを構成する方法については、[管理者ガイド: データを整理するための重複データ検出ルールの設定](/dynamics365/customer-engagement/admin/set-up-duplicate-detection-rules-keep-data-clean) を参照してください。

重複データ検出ルールは次のエンティティを使用して定義されます。

- [DuplicateRule](reference/entities/duplicaterule.md): システム内で重複を削除するには、特定のエンティティ タイプの*重複検出ルール*を作成します。 同じエンティティの種類に対して複数の検出ルールを作成できます。 ただし、エンティティの種類ごとに一度に公開できる重複データ検出ルールは最大で 5 つです。  
- [DuplicateRuleCondition](reference/entities/duplicaterulecondition.md): 1 つのルールに、エンティティで表す*重複検出ルールの条件*を 1 つ以上設定できます。 条件は、論理 `AND` 演算子を使用した場合と同様に結合されます。 重複データ検出ルールでは、基本エンティティの種類および一致するエンティティの種類を指定します。 重複ルールの条件では、基本属性の名前と一致する属性の名前を指定します。 たとえば、取引先企業を基本エンティティとして、また取引先担当者を一致するエンティティとして指定し、双方の姓と住所を比較します。 一致基準は、完全一致、最初の n 文字、最後の n 文字などの演算子で構成されます。 


これらの 2 つのエンティティは、[DuplicateRule_DuplicateRuleConditions](/reference/entities/duplicaterule.md#BKMK_DuplicateRule_DuplicateRuleConditions) 関連付けを使用して関連付けられます。

重複データ検出は、既存のレコードの生成されたマッチ コードと、作成した新しい各レコードとを比較することにより機能します。 これらのマッチ コードは、各新しいレコードの作成時に作成されます。 したがって、ちょうど同じ時点で処理される場合は、一つ以上の重複レコードが作成される可能性があります。 作成される重複データ検出に加えて、他の重複の可能性があるレコードをチェックするため、重複データ検出ジョブをスケジュールする必要があります。
 
 重複データ検出ルールはシステム全体で有効になります。 これらのルールを公開するまで、重複データ検出ジョブを実行して大量データから重複データを検出する、あるいは特定のエンティティ レコードの重複データを取得することはできません。 重複データ検出ルールを公開するには、`PublishDuplicateRule` メッセージ (<xref href="Microsoft.Dynamics.CRM.PublishDuplicateRule?text=PublishDuplicateRule Action" /> または <xref:Microsoft.Crm.Sdk.Messages.PublishDuplicateRuleRequest>) を使用します。 重複ルールは、バックグラウンドで実行される非同期処理として公開されます。

これらのエンティティの以下の書き込み可能な属性は、重複データ検出ルールの動作を制御します。

## <a name="duplicaterule"></a>DuplicateRule

|属性|内容|
|-|-|
|[BaseEntityName](/reference/entities/duplicaterule.md#BKMK_BaseEntityName)| 重複の可能性を評価するレコードのレコードの種類です。|
|[説明](/reference/entities/duplicaterule.md#BKMK_Description)|重複データ検出ルールの説明です。|
|[DuplicateRuleId](/reference/entities/duplicaterule.md#BKMK_DuplicateRuleId)|重複データ検出ルールを表す一意の識別子です。|
|[ExcludeInactiveRecords](/reference/entities/duplicaterule.md#BKMK_ExcludeInactiveRecords)|非アクティブなレコードに重複フラグを設定するかどうかを設定します。<br /> **メモ**: <br />既定値は `false` です。 非アクティブなレコードについては、重複データ検出ルールの条件を満たしていても重複と見なさない場合は、この属性を `true` に設定します。 <br /> 詳細: [非アクティブ状態](#inactive-states)|
|[IsCaseSensitive](/reference/entities/duplicaterule.md#BKMK_IsCaseSensitive)|演算子の大文字と小文字が区別されるかどうかを示します。|
|[MatchingEntityName](/reference/entities/duplicaterule.md#BKMK_MatchingEntityName)|重複の可能性があるとして評価されるレコードのレコードの種類です。|
|[名前](/reference/entities/duplicaterule.md#BKMK_Name)|重複データ検出ルールの名前です|
|[所有者 ID](/reference/entities/duplicaterule.md#BKMK_OwnerId)|重複データ検出ルールを所有するユーザーまたはチームを表す一意識別子です。|
|[OwnerIdType](/reference/entities/duplicaterule.md#BKMK_OwnerIdType)|所有者がユーザーまたはチームであるかどうか。|
|[StatusCode](/reference/entities/duplicaterule.md#BKMK_StatusCode)|重複データ検出ルールの状態の理由です。|

### <a name="inactive-states"></a>非アクティブ状態

大半のシステム エンティティおよびすべてのユーザー定義エンティティには、以下の 2 つの `StateCode` 属性オプションがあります。

- `Value`: 0 `InvariantName`: `Active`
- `Value`: 1 `InvariantName`: `Inactive`

オプションのラベルは変更することができますが、`InvariantName` の値は変更することができません。

一部のシステム エンティティには複数のアクティブまたは非アクティブ状態があります。次の表には複数のアクティブまたは非アクティブ状態のエンティティの例が示されます。

|エンティティ StateCode |アクティブな状態|非アクティブ状態|  
|--|--|--|  
|[Appointment.StateCode](/reference/entities/appointment.md#BKMK_StateCode)|`Open`、`Scheduled`|`Completed`、`Canceled`|  
|[CampaignActivity.StateCode](/reference/entities/CampaignActivity.md#BKMK_StateCode)|`Open`|`Closed`、`Canceled`|  
|[CampaignResponse.StateCode](/reference/entities/CampaignResponse.md#BKMK_StateCode)|`Open`|`Completed`、`Canceled`|  
|[Contract.StateCode](/reference/entities/Contract.md#BKMK_StateCode)|`Draft`、`Invoiced`、`On Hold`|`Canceled`、`Expired`|  
|[ContractDetail.StateCode](/reference/entities/ContractDetail.md#BKMK_StateCode)|`Existing`、`Renewed`|`Canceled`、`Expired`|  
|[Email.StateCode](/reference/entities/Email.md#BKMK_StateCode)|`Open`|`Completed`、`Canceled`|  
|[Fax.StateCode](/reference/entities/Fax.md#BKMK_StateCode)|`Open`|`Completed`、`Canceled`|  
|[Incident.StateCode](/reference/entities/Incident.md#BKMK_StateCode)|`Active`|`Resolved`、`Canceled`、`Closed`|  
|[Invoice.StateCode](/reference/entities/Invoice.md#BKMK_StateCode)|`Active`|`Closed`、`Paid`、`Canceled`|  
|[KbArticle.StateCode](/reference/entities/KbArticle.md#BKMK_StateCode)|`Draft`、`Unapproved`、`Published`|なし|  
|[Lead.StateCode](/reference/entities/Lead.md#BKMK_StateCode)|`Open`|`Qualified`、`Disqualified`|  
|[Letter.StateCode](/reference/entities/Letter.md#BKMK_StateCode)|`Open`|`Completed`、`Canceled`|  
|[Opportunity.StateCode](/reference/entities/Opportunity.md#BKMK_StateCode)|`Open`|`Won`、`Lost`|  
|[PhoneCall.StateCode](/reference/entities/PhoneCall.md#BKMK_StateCode)|`Open`|`Completed`、`Canceled`|  
|[Quote.StateCode](/reference/entities/Quote.md#BKMK_StateCode)|`Draft`、`Active`|`Won`、`Closed`|  
|[SalesOrder.StateCode](/reference/entities/SalesOrder.md#BKMK_StateCode)|`Active`、`Submitted`、`Invoiced`|`Canceled`、`Fulfilled`|  
|[ServiceAppointment.StateCode](/reference/entities/ServiceAppointment.md#BKMK_StateCode)|`Open`、`Scheduled`|`Closed`、`Canceled`|  
|[Task.StateCode](/reference/entities/Task.md#BKMK_StateCode)|`Open`|`Completed`、`Canceled`|  

 たとえば、`ExcludeInactiveRecords` 属性を `true` にセットした場合、`Active`、`Submitted`、および `Invoiced` の受注のみが重複データ検出中に一致と見なされます。 


> [!NOTE]
> [組織のメタデータの参照](browse-your-metadata.md) で説明されているメタデータ ブラウザーを使用して、エンティティで使用可能な `StateCode` オプションを確認することができます。
>
> エンティティの `StateCode` オプションを取得するため、エンティティの `LogicalName` を下記で使用する `appointment` に置き換えることにより、以下の Web API クエリを使用することができます。
> ```HTTP
> GET [organization URI]/api/data/v9.0/EntityDefinitions(LogicalName='appointment')/Attributes(LogicalName='statecode')/Microsoft.Dynamics.CRM.StateAttributeMetadata/OptionSet?$select=Options
> ```

## <a name="duplicaterule-special-messages"></a>DuplicateRule 特殊メッセージ

[DuplicateRule](/reference/entities/duplicaterule.md) はユーザー所有のエンティティで、通常作成、取得、更新、割り当て、および削除オペレーションと共に、アクセスをコントロールするオペレーションが許可されます。 詳細については、[DuplicateRule メッセージ](/reference//reference/entities/duplicaterule.md#messages) を参照してください。

次の特殊メッセージも使用することができます。

|メッセージ|Web API 操作|SDK アセンブリ|
|-|-|-|
|CompoundUpdateDuplicateDetectionRule|<xref href="Microsoft.Dynamics.CRM.CompoundUpdateDuplicateDetectionRule?text=CompoundUpdateDuplicateDetectionRule Action" />|<xref:Microsoft.Crm.Sdk.Messages.CompoundUpdateDuplicateDetectionRuleRequest>|
|PublishDuplicateRule|<xref href="Microsoft.Dynamics.CRM.PublishDuplicateRule?text=PublishDuplicateRule Action" />|<xref:Microsoft.Crm.Sdk.Messages.PublishDuplicateRuleRequest>|
|PublishXml|<xref href="Microsoft.Dynamics.CRM.PublishXml?text=PublishXml Action" />|<xref:Microsoft.Crm.Sdk.Messages.PublishXmlRequest>|
|UnpublishDuplicateRule|<xref href="Microsoft.Dynamics.CRM.UnpublishDuplicateRule?text=UnpublishDuplicateRule Action" />|<xref:Microsoft.Crm.Sdk.Messages.UnpublishDuplicateRuleRequest>|


## <a name="duplicaterulecondition"></a>DuplicateRuleCondition

|属性|内容|
|-|-|
|[BaseAttributeName](/reference/entities/duplicaterulecondition.md#BKMK_BaseAttributeName)|比較の対象となるフィールドです。|
|[DuplicateRuleConditionId](/reference/entities/duplicaterulecondition.md#BKMK_DuplicateRuleConditionId)|条件を表す一意の識別子です。|
|[IgnoreBlankValues](/reference/entities/duplicaterulecondition.md#BKMK_IgnoreBlankValues)|空白の値を重複していない値と見なすかどうかを設定します。 <br /> **メモ**: <br />この属性の既定値は `false` です。 重複データ検出ルールで `null` 値を一致と見なさない場合は、この属性を `true` に設定します。 <br /> **重要**: <br /> 条件が 1 つだけ指定された重複データ検出ルールの場合は、この属性を `false` に設定しても、システムによって `true` 値と見なされます。 |
|[MatchingAttributeName](/reference/entities/duplicaterulecondition.md#BKMK_MatchingAttributeName)|基本フィールドと比較されるフィールドです。|
|[OperatorCode](/reference/entities/duplicaterulecondition.md#BKMK_OperatorCode)|このルール条件の演算子です。<br /> **重要**: <br />`OperatorCode` 属性に `ExactMatch` をセットする場合、`OperatorParam` 属性には値をセットしません|
|[OperatorParam](/reference/entities/duplicaterulecondition.md#BKMK_OperatorParam)|演算子が "最初の文字が同じ" または "最後の文字が同じ" である場合の N のパラメーター値です。<br /> **重要**: <br />作成または更新オペレーション中は、`OperatorParam` をゼロに設定しないでください。|
|[RegardingObjectId](/reference/entities/duplicaterulecondition.md#BKMK_RegardingObjectId)|条件が関連付けられているオブジェクトを表す一意の識別子です。|

## <a name="duplicaterulecondition-special-messages"></a>DuplicateRuleCondition 特殊メッセージ

[DuplicateRuleCondition](/reference/entities/duplicaterulecondition.md) は `DuplicateRule` の子エンティティです。 これらのエンティティを取得または修正するためのアクセスは、関連付けられている `DuplicateRule` に対するアクセスに依存します。 詳細については、[DuplicateRuleCondition メッセージ](/reference/entities/duplicaterulecondition.md#messages) を参照してください。

次の特殊メッセージも使用することができます。

|メッセージ|Web API 操作|SDK アセンブリ|
|-|-|-|
|CompoundUpdateDuplicateDetectionRule|<xref href="Microsoft.Dynamics.CRM.CompoundUpdateDuplicateDetectionRule?text=CompoundUpdateDuplicateDetectionRule Action" />|<xref:Microsoft.Crm.Sdk.Messages.CompoundUpdateDuplicateDetectionRuleRequest>|


### <a name="see-also"></a>関連項目
<xref href="Microsoft.Dynamics.CRM.duplicaterule?text=duplicaterule EntityType" /><br/><xref href="Microsoft.Dynamics.CRM.duplicaterulecondition?text=duplicaterulecondition EntityType" /><br/><a href="detect-duplicate-data-with-code.md" data-raw-source="[Detect duplicate data](detect-duplicate-data-with-code.md)">重複データの検出</a><br />
<a href="enable-disable-duplicate-detection.md" data-raw-source="[Enable and disable duplicate detection](enable-disable-duplicate-detection.md)">重複データ検出の有効化と無効化</a><br />
<a href="run-duplicate-detection.md" data-raw-source="[Run duplicate detection](run-duplicate-detection.md)">重複データ検出を実行する</a><br />
<a href="duplicate-detection-messages.md" data-raw-source="[Duplicate detection messages](duplicate-detection-messages.md)">重複データ検出のメッセージ</a><br />
<a href="org-service/samples/enable-duplicate-detection-and-retrieve-duplicates.md" data-raw-source="[Sample: Enable duplicate detection and retrieve duplicates](org-service/samples/enable-duplicate-detection-and-retrieve-duplicates.md)">サンプル: 重複データ検出を有効にし、重複を取得する</a><br />
<a href="org-service/samples/use-duplicate-detection-when-creating-and-updating-records.md" data-raw-source="[Sample: Use duplicate detection when creating and updating records](org-service/samples/use-duplicate-detection-when-creating-and-updating-records.md)">サンプル: レコードの作成および更新時の重複データ検出の使用</a><br />
<a href="/dynamics365/customer-engagement/developer/org-service/sample-detect-multiple-duplicate-records" data-raw-source="[Sample: Detect multiple duplicate records](org-service/samples/detect-multiple-duplicate-records.md)">サンプル: 複数の重複レコードを検出する</a><br />