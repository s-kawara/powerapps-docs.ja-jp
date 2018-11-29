---
title: カスタムの状態モデルの遷移を定義する (アプリ用 Common Data Service) | Microsoft Docs
description: インシデント (サポート案件) エンティティまたはユーザー定義エンティティの、カスタムの状態モデルの遷移の定義について説明します。
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
# <a name="define-custom-state-model-transitions"></a>カスタムの状態モデルの遷移の定義

`Incident` (**サポート案件**) エンティティまたはユーザー定義エンティティのカスタム状態遷移を指定できます。 <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsStateModelAware> プロパティは、状態モデル遷移をサポートするエンティティに対しては `true` です。  
  
 カスタムの状態遷移は、特定の状態のレコードに対して有効な状態遷移を定義する、任意のレベルのフィルター処理です。 有効な状態と状態値の組み合わせが多数存在する場合に特に、オプションの限定した一覧を定義すると、レコードの正確な状態を選択することが容易になります。  

<a name="BKMK_StateModel"></a>
   
## <a name="what-is-the-state-model"></a>状態モデルとは  
 状態の概念をサポートするエンティティは、表に示されているように、このデータをキャプチャする一組の属性を備えています。  
  
|論理名|表示名|内容|  
|------------------|------------------|-----------------|  
|`statecode`|**ステータス**|レコードの状態を表します。 ユーザー定義エンティティに対して、これは**アクティブ**かまたは**非アクティブ**。 インシデント (サポート案件) エンティティは**アクティブ**、**解決**、および**取り消し**を使用します。 さらなる状態オプションは追加できませんが、オプション ラベルは変更できます。|  
|`statuscode`|**ステータス**|特定の状態にリンクされている状態を表します。 各状態は、少なくとも 1 つの可能な状態を持っている必要があります。 追加の状態オプションを追加し、既存のオプションのラベルを変更できます。|  
  
 属性のメタデータは、特定の状態に対してどの状態値が有効であるかを定義します。 たとえば、`Incident` (**ケース**) エンティティについては、既定の状態と状態オプションが次の表に示されています。  
  
|完了状態|状態|  
|-----------|------------|  
|`Label`: **アクティブ**<br /><br /> `Value`: 0|`Label`: **処理中**<br /><br /> `Value`: 1<br /><br /> `State`: 0|  
|`Label`: **アクティブ**<br /><br /> `Value`: 0|`Label`: **保留中**<br /><br /> `Value`: 2<br /><br /> `State`: 0|  
|`Label`: **アクティブ**<br /><br /> `Value`: 0|`Label`: **詳細待ち**<br /><br /> `Value`: 3<br /><br /> `State`: 0|  
|`Label`: **アクティブ**<br /><br /> `Value`: 0|ラベル: **調査中**<br /><br /> `Value`: 4<br /><br /> `State`: 0|  
|`Label`: **解決済み**<br /><br /> `Value`: 1|`Label`: **問題解決済み**<br /><br /> `Value`: 5<br /><br /> `State`: 1|  
|`Label`: **解決済み**<br /><br /> `Value`: 1|Label: **情報提供済み**<br /><br /> `Value`: 1000<br /><br /> `State`: 1|  
|ラベル: **取り消し**<br /><br /> `Value`: 2|`Label`: **取り消し済み**<br /><br /> `Value`: 6<br /><br /> `State`: 2|  
|ラベル: **取り消し**<br /><br /> `Value`: 2|`Label`: **統合**<br /><br /> `Value`: 2000<br /><br /> `State`: 2|  
  
 このデータは、<xref:Microsoft.Xrm.Sdk.Metadata.StatusOptionMetadata> クラスに保存されます。このクラスは、<xref:Microsoft.Xrm.Sdk.Metadata.StatusAttributeMetadata> クラスのオプションを表します。  
  
組織のエンティティ メタデータを表示するには、メタデータ ブラウザー ソリューションをインストールしてください。メタデータ ブラウザー ソリューションについては、「[組織のメタデータの参照](browse-your-metadata.md)」を参照してください。 「[エンティティ参照](/reference/about-entity-reference.md)」でエンティティの参照ドキュメントを参照することもできます。
  
<a name="BKMK_DetectValidStatusTransitions"></a>   

## <a name="detect-valid-status-transitions"></a>有効な状態遷移の検出  
 `statuscode` 属性を変更して、現在の状態からの有効な遷移を表すその他の状態オプションを定義できます。 手順については、カスタマイズ ガイドのトピック、[ステータスの遷移の定義](http://go.microsoft.com/fwlink/p/?LinkId=393657) を参照してください。  
  
 ユーザー定義の状態遷移をエンティティに適用するとき、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.EnforceStateTransitions> プロパティは `true` になります。 また、<xref:Microsoft.Xrm.Sdk.Metadata.StatusAttributeMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.OptionSetMetadata.Options> 内の各 <xref:Microsoft.Xrm.Sdk.Metadata.StatusOptionMetadata> コレクションには新しい <xref:Microsoft.Xrm.Sdk.Metadata.StatusOptionMetadata.TransitionData> プロパティがあります。 このプロパティには、XML ドキュメントを表す文字列値が含まれます。 このドキュメントには、有効な遷移の定義が含まれます。 たとえば、既定の `Incident` (**ケース**) `StatusCode`属性オプションは、次の `TransitionData` 値を持つことができます。  
  
```xml  
<allowedtransitions xmlns="http://schemas.microsoft.com/crm/2009/WebServices">  
<allowedtransition sourcestatusid="1" tostatusid="6" />  
<allowedtransition sourcestatusid="1" tostatusid="1000" />   
<allowedtransition sourcestatusid="1" tostatusid="2000" />  
<allowedtransition sourcestatusid="1" tostatusid="5" />  
</allowedtransitions>  
```  
  
> [!NOTE]
>  このデータが Web サービスからアンマネージ コードで読み込まれるとき、たとえば JavaScript を使用するとき、このデータはエスケープされ、次の例のように表示されます。  
  
```xml  
<allowedtransitions xmlns="http://schemas.microsoft.com/crm/2009/WebServices">  
<allowedtransition sourcestatusid="1" tostatusid="6">  
<allowedtransition sourcestatusid="1" tostatusid="1000">  
<allowedtransition sourcestatusid="1" tostatusid="2000">  
<allowedtransition sourcestatusid="1" tostatusid="5">  
</allowedtransitions>  
```  
  
 このデータが存在し、エンティティ `EnforceStateTransitions` プロパティが `true` のとき、インシデント インスタンスは許可された `statuscode` 値の 1 つにのみ変更できます。 <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*> を使用して `statuscode`<xref:Microsoft.Xrm.Sdk.OptionSetValue> を状態の変更を表さない許可された値のいずれかに設定できます。 状態を変更するには、許可された <xref:Microsoft.Crm.Sdk.Messages.SetStateRequest.State> プロパティ値と <xref:Microsoft.Crm.Sdk.Messages.SetStateRequest.Status> プロパティ値を設定する <xref:Microsoft.Crm.Sdk.Messages.SetStateRequest> か、または　<xref:Microsoft.Crm.Sdk.Messages.CloseIncidentRequest.Status> プロパティを現在の `statuscode` 値に対して許可された値の 1 つに設定する <xref:Microsoft.Crm.Sdk.Messages.CloseIncidentRequest> を使用します。 無効な値を設定しようとすると、エラーがスローされます。  
  
### <a name="see-also"></a>関連項目  
 [サンプル: 有効な状態の遷移を取得する](org-service/samples/retrieve-valid-status-transitions.md)   
 [レコードの状態とステータス](/dynamics365/customer-engagement/developer/introduction-entities#bkmk_RecordStateandStatus)   
 [メタデータの変更の取得および検出](/dynamics365/customer-engagement/developer/retrieve-detect-changes-metadata)   
 [ステータスの遷移の定義](http://go.microsoft.com/fwlink/p/?LinkId=393657)
