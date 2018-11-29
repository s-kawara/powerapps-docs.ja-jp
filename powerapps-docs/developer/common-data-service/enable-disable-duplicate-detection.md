---
title: 重複データ検出を有効化および無効化 (Common Data Service for Apps) | Microsoft Docs
description: このトピックでは、組織のすべてのエンティティ、特定のエンティティおよび特定のオペレーションに対する重複データ検出を有効にする方法、および重複データ検出ルールを非公開にすることによりまたは公開済みルールを削除することにより、グローバルまたはエンティティの種類に対して重複データ検出を無効にする方法に関する情報をカバーしています。
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
# <a name="enable-and-disable-duplicate-detection"></a>重複データ検出の有効化と無効化

このトピックでは、Dynamics 365 の重複データ検出を有効または無効にする方法をカバーしています。

<a name="bkmk_enable"></a>

## <a name="enable-duplicate-detection"></a>重複データ検出の有効化

重複データ検出を実行する前に、次のいずれかを有効にします。  
  
-   グローバルに有効化 (組織のすべてのエンティティが対象)  
  
-   1 つのエンティティに対して有効化  
  
-   特定の操作に対して有効化  
  
> [!NOTE]
>  重複データを 1 つのエンティティを対象にして、またはエンティティの特定の操作を対象にして検出するには、3 つの領域すべてにおいて有効にする必要があります。  
  
### <a name="enable-duplicate-detection-globally"></a>重複データ検出をグローバルに有効にする  
  
-   <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> メッセージを使用して、`Organization.IsDuplicateDetectionEnabled` 属性を `true` に設定します。
-   組織全体に対して重複データ検出を有効にするためのユーザー インターフェイスを使用する方法については、[組織全体の重複データ検出ルールをオン/オフする](/dynamics365/customer-engagement/admin/turn-duplicate-detection-rules-off-whole-organization) を参照してください。
  
### <a name="enable-duplicate-detection-for-an-entity"></a>1 つのエンティティに対して重複データ検出を有効にする  
  
-   <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> メッセージを使用して、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsDuplicateDetectionEnabled> プロパティを `true` に設定します。  
  
### <a name="enable-duplicate-detection-for-specific-operations"></a>特定の操作に対して重複データ検出を有効にする  
  
- 次の属性を `true` に設定します。  
  
  - `Organization.IsDuplicateDetectionEnabledForOnlineCreateUpdate`。 Web アプリケーションまたは Dynamics 365 for Outlook を使用して、アプリ用 CDS のレコードを作成および更新します。 この属性は、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> メッセージや <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> メッセージで作成または更新されたレコードの重複データ検出を有効または無効にします。 ただし、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*> および <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*> メソッドで作成または更新されたレコードが、この属性の影響を受けることはありません。  
  
  - `Organization.IsDuplicateDetectionEnabledForOfflineSync`。 Dynamics 365 for Outlook をオフラインからオンラインに切り替えたときにオフライン レコードを同期します。  
  
  - `Organization.IsDuplicateDetectionEnabledForImport`。 データを一括インポートします。  
  
  > [!NOTE]
  >  重複データ検出ルールを公開しなくても、これらの操作を有効にすることはできます。 ただし、操作を実行する場合は、あらかじめ重複データ検出ルールを公開しておく必要があります。  

<a name="bkmk_disable"></a>

## <a name="disable-duplicate-detection"></a>重複データ検出を無効にする

重複データ検出はグローバルに無効にすることも、特定の種類のエンティティについてのみ無効にすることもできます。それには、重複データ検出ルールの公開を取り下げるか、公開済みのルールを削除します。  
  
 **重複データ検出をグローバルに無効にする**  
  
 重複データ検出をグローバルに無効にするには、<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> メッセージを使用して、`Organization.IsDuplicateDetectionEnabled` 属性を `false` に設定します。 これにより、組織内の全種類のエンティティに対するすべての重複データ検出ルールの公開が自動的に取り下げられます。  
  
 **1 種類のエンティティに対して重複データ検出を無効にする**  
  
 1 種類のエンティティに対して重複データ検出を無効にするには、次のいずれかの方法を使用します。  
  
-   <xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest> メッセージを使用して、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsDuplicateDetectionEnabled> プロパティを `false` に設定します。 これにより、1 種類のエンティティに対するすべての重複データ検出ルールの公開が自動的に取り下げられます。 この種類のエンティティに対しては、重複データ検出がサポートされなくなり、新しい重複データ検出ルールも作成できなくなります。  
  
-   <xref:Microsoft.Crm.Sdk.Messages.UnpublishDuplicateRuleRequest> メッセージを使用して、1 種類のエンティティに対するすべての重複データ検出ルールの公開を取り下げます。  
  
**公開済みの重複データ検出ルールを削除する**  
  
システム内のすべての公開済みルールを削除して重複データ検出をグローバルに無効にすることも、特定の種類のエンティティに対する公開済みルールを削除することもできます。それには、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Delete*>   メソッド。  

## <a name="see-also"></a>関連項目

[重複データ検出](detect-duplicate-data-with-code.md)  
[重複データ検出を実行](run-duplicate-detection.md)   
[重複ルール エンティティ](duplicaterule-entities.md) 