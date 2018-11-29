---
title: キュー エンティティ (Common Data Service for Apps) | Microsoft Docs
description: PowerApps のキューは、キューは作業の進捗状況の編成、優先順位の指定、および監視を行う手段です。
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
# <a name="queue-entities"></a>キュー エンティティ

*キュー*は、作業の進捗状況の編成、優先順位の指定、および監視を行う手段です。 作業を集中管理する手段として、サポート案件の処理、サービス呼び出しの対応、または見込みのある顧客への製品情報の送信でキューが役立ちます。 プログラム的には、キューはキュー アイテムの集合です。 キュー アイテムは、処理が必要なタスク、電子メール、またはサポート案件などのエンティティ レコードのコンテナーの役割を果たします。 [キュー エンティティ](reference/entities/queue.md)を参照

> [!NOTE]
> UI を使用したキューの使用の詳細については、[キューの概要](/dynamics365/customer-engagement/customer-service/set-up-queues-manage-activities-cases)を参照してください。  
  
キューには次のような機能があります。  
  
-   すべてのカスタマイズ可能なエンティティをキューに対して有効化できます。  
  
-   キューはパブリックまたはプライベートを選択できます。 プライベート キュー アイテムは、キューのメンバーにのみ表示されます。  
  
-   新しいユーザーまたはチームごとに、プライベート キューが自動的に作成されます。  
  
-   キューには、タスク、電子メール、サポート案件などの複数の種類のエンティティを含めることができます。  
  
-   キューには、特定のキュー アイテムで作業しているユーザーに関する情報が含まれます。 これにより、リソースを効率よく管理でき、作業の重複を回避できます。  
  
-   ワークフローおよび監査に対して、キューを有効化できます。 これにより、生産性が向上し、将来行う分析やレポート作成のためにエンティティおよび属性データの変更を追跡できます。  
  
<a name="BKMK_MemberCapabilities"></a>   
## <a name="members-capabilities"></a>メンバーの機能  
 キューが*パブリック* キューまたは*プライベート* キューに分類されるようになりました。 キューへのアクセスをより簡単に制御できるようにするため、プライベート キューは、個々のユーザーをメンバーとします。 プライベート キューにチームを追加する場合は、そのチームのすべてのメンバーが、プライベート キューのメンバーになります。  
  
<a name="BKMK_publicAndPrivateQueues"></a>   
## <a name="public-and-private-queues"></a>パブリック キューとプライベート キュー  
 [QueueViewType](reference/entities/queue.md#BKMK_QueueViewType) 属性は、キューがパブリックであるかプライベートであるかを定義する候補のリストです。  
  
-   すべてのユーザーのキューは、ユーザーのプライベート キューになります。自分のプライベート キューのキュー アイテムを表示することができるのは、そのユーザーだけです。  
  
-   チームのキューは、メンバーのプライベートとしてマークされます。チーム所有者とすべてのチーム メンバーが、アプリケーションでキューを表示できます。  
  
-   その他のすべてのキューはパブリックになります。 キュー エンティティの読み取り特権を持つすべてのユーザーは、これらのキューを表示することができます。  
  
<a name="BKMK_QueueAttributes"></a>   
## <a name="attributes-used-to-manage-queues"></a>キューを管理するために使用される属性  
 次の属性を使用して、キューを管理します。  
  
|SchemaName|DisplayName|種類|説明|  
|----------------|-----------------|----------|-----------------|  
|NumberOfItems|キュー アイテム |整数|キューに関連付けられているキュー アイテムの数です。|  
|NumberOfMembers|番号 メンバーの|整数|キューに関連付けられているメンバーの数です。|  
|QueueViewType|種類​​|候補リスト|キューをパブリックにするかプライベートにするかを選択します。 パブリック キューは、すべてのユーザーが表示できます。 プライベート キューは、キューに追加されているメンバーのみが表示できます。|  
  
<a name="BKMK_deletingQueues"></a>   
## <a name="restrictions-on-deleting-queues"></a>キューの削除の制限  
 次の場合、キューは削除できません。  
  
-   キューにキュー アイテムがある場合。  
  
-   ルーティング ルールでキューが使用されている場合。  
  
<a name="BKMK_Enabling"></a>   
## <a name="enable-entities-for-queues"></a>キューに対してエンティティを有効化する  
 キューに対してカスタマイズ可能なエンティティ (`EntityMetadata.IsCustomizable = true`) を有効化するには、<xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest> メッセージを使用して、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsValidForQueue> 属性を `true` に設定します。 キュー エンティティおよびキュー アイテム エンティティはカスタマイズ可能なエンティティですが、キューに対して有効化することはできません。  
  
 次の一覧に、Common Data Service (CDS) for Apps において既定でキューが有効化されているエンティティを示します。  
  
-   予定  
  
-   Campaignactivity  
  
-   CampaignResponse  
  
-   電子メール  
  
-   FAX  
  
-   インシデント  
  
-   レター   
  
-   PhoneCall  
  
-   RecurringAppointmentMaster  
  
-   ServiceAppointment  
  
-   ソーシャル活動  
  
-   タスク  
  
<a name="BKMK_Inheriting"></a>   
## <a name="inherit-privileges-and-provide-limited-access-to-a-queue"></a>特権の継承およびキューへの制限されたアクセスの指定  
 キューおよびキュー アイテムには、親キュー レコードの操作が子キュー アイテム レコードに伝播される上位下位の関連付けがあります。  
  
> [!NOTE]
>  この特定の上位下位の関連付けでは、削除操作のみが、親キュー エンティティから子キュー アイテム エンティティに伝播します。 割り当て、統合、共有など、その他の操作は伝播されません。  
  
 キュー アイテムの特権は、キューの特権から継承されます。  
  
- `prvReadQueue` 特権を持っている場合、キュー アイテム エンティティへの読み取り特権も持っています。  
  
- `prvAppendToQueue` 特権を持っている場合、キュー アイテム エンティティへの作成、更新、および削除の特権も持っています。  
  
  キュー アイテムへのアクセスを許可する際には、キューへのアクセスを制限しなければならない場合があります。 キューへの完全なアクセス権を持つキューの所有者が、キューへのアクセス権が制限されているチームとキューを共有する場合があります。 たとえば、キューについての読み取り特権および追加特権がサポート チームに付与されている場合、チーム メンバーはそのキューに対していかなる変更も実施できません (つまり、キュー名の変更や所有者の変更などはできません)。 ただし、キュー アイテムに対しては、作成、取得、更新、および削除の操作を実行できます。  
  
<a name="BKMK_Actions"></a>   
## <a name="actions-on-queues-and-queue-items"></a>キューおよびキュー アイテムでのアクション  
 キュー エンティティ、およびキュー アイテム エンティティに対して適切な特権を持っている場合、キュー およびキュー アイテムでさまざまなアクションを実行できます。  
  
### <a name="actions-on-queues"></a>キューでのアクション  
 キューでは次のアクションを実行できます。  
  
-   ユーザー定義属性を追加することによって、キューおよびキュー アイテムをカスタマイズします。  
  
-   キューにエンティティ レコードを追加します。  
  
    > [!NOTE]
    >  1 つのエンティティ レコードを複数のキューに追加することはできません。 例外は、ステータスが "受信" の電子メール エンティティ レコードです。  
  
-   さまざまな種類のエンティティのエンティティ レコードを同じキューに追加します。  
  
-   キューの所有権を他のユーザーまたはチームに割り当てることによって、その所有権を変更します。  
  
-   <xref:Microsoft.Crm.Sdk.Messages.AddPrincipalToQueueRequest>を使用して、プライベート キューにプリンシパルを追加します。  
  
-   完了下電話やキャンセルされた電話など、キュー内の非アクティブなキュー アイテムを削除することによって、キューの履歴をクリーンアップします。  
  
-   <xref:Microsoft.Crm.Sdk.Messages.RetrieveUserQueuesRequest>を使用して、ユーザーがアクセス権を持っているすべてのキューを取得します  
  
-   `SystemUser.QueueId` 属性をキューの ID に設定することによって、キューをユーザーの既定のキューにすることができます。 同じキューを、異なるユーザーの既定のキューとして指定できます。  
  
-   すべてのプライベート キューで動作するワークフローを作成します。 たとえば、ユーザーがタスクを作成すると、常にワークフローがそのタスクをユーザーの既定のキューに追加します。 また、特定のキューでのみ動作するワークフローを作成することもできます。  
  
-   受信電子メール メッセージをキューに配信する場合に、受信メッセージに対して電子メールを構成します。  
  
### <a name="actions-on-queue-items"></a>キュー アイテムでのアクション  
 キュー アイテムで次のアクションを実行します。  
  
- <xref:Microsoft.Crm.Sdk.Messages.PickFromQueueRequest>を使用して、キュー アイテムをユーザーに割り当てます。  
  
- <xref:Microsoft.Crm.Sdk.Messages.AddToQueueRequest> メッセージを使用して、キュー アイテムをソース キューから別のキューに移動します。 キュー アイテムは、<xref:Microsoft.Crm.Sdk.Messages.SetStateRequest> メッセージを使用して非アクティブ化されるまで、キュー間を移動できます。  
  
  > [!NOTE]
  >  キュー アイテム内のレコードの状態がアクティブから非アクティブに変わった場合、キュー アイテムは自動的に非アクティブ化されます。 このことは、アクティブ状態と非アクティブ状態を持つ、キューを有効化されたエンティティについても同様です。 エンティティがキューで有効化されているかどうか、エンティティ レコードがアクティブまたは非アクティブ状態にできるかどうかを判断するには、エンティティのメタデータ情報を参照してください。  
  
- <xref:Microsoft.Crm.Sdk.Messages.ReleaseToQueueRequest>を使用して、キューアイテムを解放してキューに戻します。  
  
- <xref:Microsoft.Xrm.Sdk.Messages.DeleteRequest> メッセージを使用して、キュー アイテムをキューから削除します。 キュー アイテムを削除するとき、参照先エンティティ レコードは削除されません。 ただし、エンティティ レコードを削除する場合は、このエンティティ レコードを参照するキュー アイテムがすべて削除されます。  
  
### <a name="see-also"></a>関連項目  
 <!--[Configure EMail for Incoming Messages](configure-email-incoming-messages.md)-->  
 
[キュー エンティティ](reference/entities/queue.md)   
[QueueItem エンティティ](reference/entities/queueitem.md)   
<xref:Microsoft.Crm.Sdk.Messages.AddToQueueRequest>   
 