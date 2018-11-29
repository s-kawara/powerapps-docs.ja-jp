---
title: エンティティ メタデータのカスタマイズ (アプリ用 Common Data Service) | MicrosoftDocs
description: エンティティは、メタデータによって定義されます。 エンティティ メタデータを定義または変更することによって、エンティティの機能を制御できます。
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
# <a name="customize-entity-metadata"></a>エンティティ メタデータのカスタマイズ

エンティティは、メタデータによって定義されます。 エンティティ メタデータを定義または変更することによって、エンティティの機能を制御できます。 組織のメタデータを表示するには、メタデータ ブラウザーを使用します。 [メタデータ ブラウザーのダウンロード](http://download.microsoft.com/download/8/E/3/8E3279FE-7915-48FE-A68B-ACAFB86DA69C/MetadataBrowser_3_0_0_5_managed.zip)。

詳細: [組織のメタデータの参照](browse-your-metadata.md)  
  
 このトピックでは、プログラムでエンティティを処理する方法について説明します。 アプリケーションでエンティティを処理する方法の詳細については、[エンティティ (レコードの種類) の作成または編集](/dynamics365/customer-engagement/customize/create-edit-entities) を参照してください。  

エンティティは、組織または Web API のいずれかを使用して作成することができます。 以下の情報は両方に適用することができます。

- 組織サービスでは、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata> クラスを使用します。 詳細: [ユーザー定義エンティティの作成](/dynamics365/customer-engagement/developer/org-service/create-custom-entity) および [エンティティの取得、更新、および削除](/dynamics365/customer-engagement/developer/org-service/retrieve-update-delete-entities)
- Web API では、<xref:Microsoft.Dynamics.CRM.EntityMetadata> EntityType を使用します。 詳細については、[Web API を使用してエンティティ定義を作成および更新](/dynamics365/customer-engagement/developer/webapi/create-update-entity-definitions-using-web-api) を参照してください。
 
<a name="BKMK_EntityMetadataMessages"></a>

## <a name="entity-metadata-operations"></a>エンティティ メタデータの操作
エンティティ メタデータでの作業方法は使用するサービスにより異なります。

Web API は RESTful エンドポイントであるため、メタデータの作成、取得、更新、および削除に異なる方法を使用します。 `POST`、`GET`、`PUT`、および `DELETE` HTTP 動詞を使用して、メタデータ エンティティの種類で作業します。 詳細については、[Web API を使用してエンティティ定義を作成および更新](/dynamics365/customer-engagement/developer/webapi/create-update-entity-definitions-using-web-api) を参照してください。

これに対する 1 つの例外は、<xref href="Microsoft.Dynamics.CRM.RetrieveMetadataChanges?text=RetrieveMetadataChanges Function" /> にはメタデータ クエリを構成して時間に伴う変化を追跡するための方法が用意されていることです。 

組織サービスを使用している場合は、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest> クラスを使用します。 このクラスには、指定した条件を満たすメタデータ レコードのコレクションを取得するために必要なデータが含まれます。 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse> は、最後の要求後のメタデータ変更内容に関する情報を戻すために、後からこの要求を使用することができるタイムスタンプ値を返します。
   

|                                                                                                                                                                          メッセージ                                                                                                                                                                           |                                               Web API                                                |                           SDK アセンブリ                           |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
|                                                                                                                                                                        CreateEntity                                                                                                                                                                        |                         POST 要求を使用してエンティティを作成するデータを送信します。                         |      <xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest>       |
|                                                                                                                                                                        DeleteEntity                                                                                                                                                                        |                              DELETE 要求を使用してエンティティを削除します。                               |      <xref:Microsoft.Xrm.Sdk.Messages.DeleteEntityRequest>       |
|                                                                                                                                                                    RetrieveAllEntities                                                                                                                                                                     |                               GET 要求を使用してエンティティ データを取得します。                               |   <xref:Microsoft.Xrm.Sdk.Messages.RetrieveAllEntitiesRequest>   |
|                                                                                                                                                                       RetrieveEntity                                                                                                                                                                       |          <xref href="Microsoft.Dynamics.CRM.RetrieveEntity?text=RetrieveEntity Function" />          |     <xref:Microsoft.Xrm.Sdk.Messages.RetrieveEntityRequest>      |
|                                                                                                                                                                        UpdateEntity                                                                                                                                                                        |                                PUT 要求を使用してエンティティを更新します。                                |      <xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest>       |
| RetrieveMetadataChanges</br><xref:Microsoft.Xrm.Sdk.Metadata.Query> 名前空間のオブジェクトと共に使用してクエリを作成し、特定のメタデータに対する変更を効率よく取得および検出します。 詳細: [メタデータへの変更の取得および検出](/dynamics365/customer-engagement/developer/retrieve-detect-changes-metadata)。 | <xref href="Microsoft.Dynamics.CRM.RetrieveMetadataChanges?text=RetrieveMetadataChanges Function" /> | <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest> |

<a name="BKMK_CreationOptions"></a>   
## <a name="options-available-when-you-create-a-custom-entity"></a>ユーザー定義エンティティの作成時に利用可能なオプション  
 次の表は、ユーザー定義エンティティを作成するときに使用できるオプションを示します。 ユーザー定義エンティティを作成するときにのみ、これらのプロパティを設定できます。  

|オプション|説明|  
|------------|-----------------|  
|**ユーザー定義の活動として作成**|組織サービスまたは Web API をそれぞれ使用するときに `IsActivity` プロパティを設定することにより、活動であるエンティティを作成することができます。 詳細については、[Dynamics 365 のユーザー定義活動](custom-activities.md) を参照してください。|  
|**エンティティ名**|名前には 2 種類あり、どちらもカスタマイズの接頭辞が付いている必要があります。<br /><br /> `LogicalName`: エンティティ名のバージョンであり、すべて小文字で設定される名前。<br /><br /> `SchemaName`: エンティティのデータベース テーブルの作成に使用される名前。 この名前は大文字小文字が混在できます。 使用する大文字と小文字は、厳密な型を使用するプログラミングのとき、または REST エンドポイントを使用するときに生成されるオブジェクトの名前を設定します。<br /><br /> **注**: 論理名がスキーマ名と異なる場合、論理名に設定した値をスキーマ名が上書きします。<br /><br /> 特定のソリューションのコンテキスト内のアプリケーションでエンティティが作成される場合、使用されるカスタマイズの接頭辞は、ソリューションの `Publisher` で設定される接頭辞です。 エンティティがプログラム的に作成される場合、カスタマイズの接頭辞は、長さが 2 文字から 8 文字の間の文字列で、すべて英数文字であり、最初の 1 文字を英字にする必要があります。 接頭辞を "mscrm" で始めることはできません。 ソリューションが関連付けられている発行者が定義するカスタマイズの接頭辞を使用することをお勧めしますが、必須ではありません。 カスタマイズの接頭辞と論理名またはスキーマ名との間に、アンダースコアを使用する必要があります。|  
|**企業形態**|`OwnershipType` プロパティを使用してこれを設定します。 <xref:Microsoft.Xrm.Sdk.Metadata.OwnershipTypes> 列挙体または <xref:Microsoft.Dynamics.CRM.OwnershipTypes> EnumType を使用してエンティティの所有権の種類を設定します。 ユーザー定義エンティティで有効な値は、`OrgOwned` または `UserOwned` のみです。 詳細については、[エンティティの所有権](/dynamics365/customer-engagement/developer/introduction-entities#EntityOwnership) を参照してください。|  
|**主属性**|組織サービスの場合、<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest>.<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest.PrimaryAttribute> プロパティを使用してこれを設定します。<br /><br />JSON がエンティティを定義する Web API には、`IsPrimaryName` プロパティを true にセットした <xref:Microsoft.Dynamics.CRM.StringAttributeMetadata> を 1 つ含める必要があります。<br /><br /> どちらの場合も、文字列属性は `Text` として書式設定される必要があります。 この属性の値は、関連するエンティティの検索で表示される内容です。 このため、フィールドの値は、エンティティ レコードの名前を表す必要があります。|  

<a name="BKMK_OptInOptions"></a>

## <a name="enable-entity-capabilities"></a>エンティティの機能の有効化  
 次の表にエンティティ機能の一覧を示します。 エンティティを作成するときにこれらの機能を設定することも、後で有効にすることもできます。 これらの機能は、一度有効にすると無効にすることはできません。  

|機能|内容|  
|----------------|-----------------|  
|**業務プロセス フロー**|業務プロセス フローのエンティティを有効にするためには、`IsBusinessProcessEnabled` を true に設定します。|  
|**メモ**| `Annotation` エンティティとのエンティティ関連付けを作成し、エンティティ フォームの **Notes** 領域を含めることができるようにします。 **メモ**を含めることにより、レコードに添付ファイルを追加することもできます。 <br /><br />組織サービスでは、<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest> または <xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest> `HasNotes` プロパティを使用します <br /><br />Web API で、<xref:Microsoft.Dynamics.CRM.EntityMetadata>.`HasNotes` プロパティをセットします。|  
|**活動**|すべての活動の種類エンティティをこのエンティティと関連付けることができるように、`ActivityPointer` エンティティとのエンティティ関連付けを作成します。<br /><br /> 組織サービスでは、<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest> または <xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest> `HasActivities` プロパティを使用します。 <br /><br /> Web API で、<xref:Microsoft.Dynamics.CRM.EntityMetadata>.`HasActivities` プロパティをセットします。| 
|**接続**|このエンティティを他の接続エンティティと関連付ける接続レコードの作成を有効にするには、`IsConnectionsEnabled.Value` プロパティを true にセットします。|  
|**キュー**|キューのサポートを追加するには、`IsValidForQueue` プロパティを使用します。 このオプションを有効にすると、この種類のレコードが作成または割り当てられたときに、レコードを所有者の既定のキューに自動的に移動するように `AutoRouteToOwnerQueue` プロパティを設定することもできます。|  
|**電子メール**|この種類のレコードの電子メール アドレスに、電子メールを送信できるように `IsActivityParty` プロパティを設定します。|  

<a name="BKMK_OpenOptions"></a>   

## <a name="editable-entity-properties"></a>編集可能なエンティティ プロパティ  
 次の表では、編集できるエンティティ プロパティを示します。 これらのオプションは、マネージド プロパティによって無効にしている場合を除き、いつでも更新できます。  


|                                        プロパティ                                        |                                                                                                                                                                                                     内容                                                                                                                                                                                                     |
|----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                 **簡易作成を許可**                                 |                                                                                   エンティティの簡易作成フォームを有効にするには、`IsQuickCreateEnabled` を使用します。 簡易作成フォームを使用する前に、まず簡易作成フォームを作成および公開する必要があります。<br /> **メモ**:<br /> 活動エンティティは簡易作成フォームをサポートしません。                                                                                   |
|                                    **アクセス チーム**                                    |                                                                                                                                アクセス チームのエンティティを有効にするには、`AutoCreateAccessTeams` を使用します。 詳細については、[チーム テンプレートについて](/dynamics365/customer-engagement/admin/about-team-templates) を参照してください。                                                                                                                                |
|                                   **プライマリ イメージ**                                    |                                                                                             エンティティにイメージ属性がある場合、`PrimaryImageAttribute`を使用してアプリケーションへのその画像の表示を有効または無効にできます。 詳細については、[エンティティ イメージ](/dynamics365/customer-engagement/developer/introduction-entities#BKMK_EntityImages)を参照してください。                                                                                             |
|                                **表示テキストの変更**                                 |                                                                                             マネージド プロパティ `IsRenameable` のために、アプリケーションで表示名を変更できません。 `DisplayName` および `DisplayCollectionName` プロパティを更新することによって、ラベルをプログラム的に変更することができます。                                                                                             |
|                            **エンティティの説明の編集**                             |                                                                                                         マネージド プロパティ `IsRenameable` のために、アプリケーションでエンティティの説明を変更できません。 `Description` プロパティを更新することによって、ラベルをプログラム的に変更することができます。                                                                                                         |
|                            **オフライン時の使用の有効化**                            |                                                                                                          オフライン アクセス対応 Dynamics 365 for Microsoft Office Outlook のユーザーが、オフライン時にこのエンティティのデータを取得できるかどうかを切り替えるには、`IsAvailableOffline`を使用します。                                                                                                           |
|                          **Outlook の閲覧ウィンドウの有効化**                           | **メモ**:<br /><br /> `IsReadingPaneEnabled`エンティティは内部のみで使用します。<br /><br /> Office Outlook のユーザーがこのエンティティのデータを表示できるかどうかを切り替えるには、Outlook の閲覧ウィンドウを使用します。 このプロパティは、アプリケーションで設定する必要があります。 |
|                                 **差し込み印刷の有効化**                                  |                                                                                                                 このエンティティからのデータを使用する Office Word の結合された文書を生成できるかどうかを切り替えるには、`IsMailMergeEnabled`を使用します。                                                                                                                  |
|                             **重複データ検出の有効化**                             |                                                                                                       エンティティの重複データ検出の有効と無効を切り替えるには、`IsDuplicateDetectionEnabled` を使用します。 詳細については、[Dynamics 365 の重複データの検出](/dynamics365/customer-engagement/developer/detect-duplicate-data-for-developers) を参照してください。                                                                                                        |
|                           **SharePoint の統合の有効化**                            |                                                          エンティティの SharePoint サーバー統合の有効と無効を切り替えるには、`IsDocumentManagementEnabled`を使用します。 詳細については、[エンティティに対するドキュメント管理の有効化](/dynamics365/customer-engagement/developer/integration-dev/enable-document-management-entities) を参照してください。                                                          |
| **Dynamics 365 for phones の有効化** |                                                                                                                      Dynamics 365 for phones のユーザーがこのエンティティのデータを表示できるかどうかを切り替えるには、`IsVisibleInMobile`を使用します。                                                                                                                       |
|              **Dynamics 365 for tablets**               |                             Dynamics 365 for tablets のユーザーがこのエンティティのデータを表示できるかどうかを切り替えるには、`IsVisibleInMobileClient`を使用します。<br /><br /> エンティティが Dynamics 365 for tablets で利用可能な場合は、レコードのデータが読み取り専用であることを指定するために`IsReadOnlyInMobileClient`を使用することができます。                              |
|                                  **監査の有効化**                                   |                                                                                                              エンティティの監査の有効と無効を切り替えるには、`IsAuditEnabled` を使用します。 詳細については、[監査のエンティティおよび属性の構成](configure-entities-attributes-auditing.md) を参照してください。                                                                                                              |
|                        **エンティティが表示される領域の変更**                        |                                                                                                                                                  アプリケーションのナビゲーション ウィンドウのエンティティ グリッドが表示される場所を制御できます。 これはサイトマップによって制御されます。                                                                                                                                                   |
|                              **属性の追加と削除**                              |                                                                                     マネージド プロパティ `CanCreateAttributes.Value` によって属性の作成が許可されている場合に限り、エンティティに属性を追加することができます。 詳細については、[エンティティ属性メタデータのカスタマイズ](/dynamics365/customer-engagement/developer/customize-entity-attribute-metadata) を参照してください。                                                                                      |
|                                **ビューの追加と削除**                                 |                                                                                                                                マネージド プロパティ `CanCreateViews.Value` によってビューの作成が許可されている場合に限り、`SavedQuery` エンティティを使用してエンティティのビューを作成できます。                                                                                                                                 |
|                                **グラフの追加と削除**                                |              マネージド プロパティ `CanCreateCharts.Value` によってグラフの作成が許可されており、`IsEnabledForCharts` エンティティ プロパティが true の場合に限り、[SavedQueryVisualization エンティティ](/reference/entities/savedqueryvisualization.md) を使用してエンティティのグラフを作成することができます。 詳細については、[ビジュアル化を使用したデータの表示 (グラフ)](/dynamics365/customer-engagement/developer/customize-dev/view-data-with-visualizations-charts) を参照してください。              |
|                         **エンティティの関連付けの追加または削除**                         |                                                                                        エンティティに対して作成できるエンティティの関連付けの種類を制御するマネージド プロパティは複数あります。 詳細については、[エンティティ関係メタデータをカスタマイズする](/dynamics365/customer-engagement/developer/customize-entity-relationship-metadata) を参照してください。                                                                                        |
|                                    **アイコンの変更**                                    |                                                                                                                                             ユーザー定義エンティティで使用されているアイコンは変更できます。 詳細については、[エンティティのアイコンの変更](/dynamics365/customer-engagement/developer/modify-icons-entity)を参照してください。                                                                                                                                             |
|                        **階層関連付けを変更できる**                        |                                                                                        `CanChangeHierarchicalRelationship.Value` は、マネージド ソリューションに含まれるエンティティ関係の階層状態を変更できるかどうかを制御します。 詳細:                                                                                         |
  
<a name="BKMK_MessagesForCustomEntites"></a>
 
## <a name="messages-supported-by-custom-entities"></a>ユーザー定義エンティティでサポートされているメッセージ  
 ユーザー定義エンティティは、システム エンティティと同じベース メッセージをサポートしています。 使用できるメッセージのセットは、ユーザー定義エンティティがユーザー所有か組織所有のいずれかでによって異なります。 詳しくは、「[エンティティ レコードに対する操作](/dynamics365/customer-engagement/developer/introduction-entities#ActionsOnEntityRecords)」をご覧ください。  
  
### <a name="see-also"></a>関連項目  
[Web API をメタデータで使用する](webapi/use-web-api-metadata.md)

[組織サービスを使用したメタデータに関する作業](org-service/work-with-metadata.md)