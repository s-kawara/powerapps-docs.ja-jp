---
title: 監査の概要 (アプリ用 Common Data Service) | Microsoft Docs
description: アプリ用 CDS の監査機能が、分析およびレポート作成の目的で使用に対して、時間の経過とともにどのように属性およびエンティティ データの変更を記録するために使用されるかについてお読みください。
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
# <a name="auditing-overview"></a>監査の概要

組織では、通常、さまざまな規制に従って、顧客とのやり取りの履歴、監査ログ、アクセス レポート、セキュリティ インシデント追跡レポートを入手できるようにしておく必要があります。 組織では、セキュリティと分析のためにアプリ用 Common Data Service データの変更を追跡することが必要な場合があります。  
  
 アプリ用 CDS がサポートする監査機能では、組織でのエンティティおよび属性データの変更を、分析やレポートで使用できるように記録できます。 監査は、すべてのユーザー定義エンティティと属性、およびほとんどのカスタマイズ可能なエンティティと属性でサポートされます。 メタデータの変更、取得操作、エクスポート操作については、または認証中は、監査はサポートされません。 監査を構成する方法の詳細については、「[監査のエンティティおよび属性の構成](configure-entities-attributes-auditing.md)」を参照してください。  
  
## <a name="supported-for-auditing"></a>監査のサポート  
 アプリ用 CDS の監査機能を次に示します:  
<!-- TODO: Jim, I don't think this is online only. Please correct the tokens here. -->
  
* カスタマイズ可能なエンティティの監査
* ユーザー定義エンティティの監査
* 監査対象のエンティティの構成
* 監査対象の属性の構成
* 特権ベースの監査記録の表示
* 特権ベースの監査概要の表示
* パーティション分割された SQL データベースの監査ログの削除  
* パーティション分割されていない SQL データベースの監査ログの削除 
* レコードの作成、更新、削除操作の監査
* 関連付け (1:N、N:N) の監査 
* 監査イベントの監査
* ユーザー アクセスの監査
* 規制基準への準拠
* 開発者のための API の監査
  
## <a name="not-supported-for-auditing"></a>監査でサポートされない内容  
 アプリ用 CDS について監査できない内容を次に示します:  
  
* 読み取り操作の監査
* メタデータ変更の監査 
  
## <a name="key-concepts"></a>重要な概念  
 監査に関する重要な概念を次に示します。  
  
-   組織、エンティティ、属性のレベルで監査を有効または無効にできます。 組織レベルで監査が有効になっていない場合、エンティティおよび属性の監査は、有効になっていたとしても行われません。 既定では、監査はすべての監査可能なエンティティ属性に対して有効になっていますが、エンティティおよび組織のレベルでは無効になっています。  
  
-   監査履歴を取得して表示する機能は、監査履歴の表示および監査の概要の表示の特定のセキュリティ特権を持つユーザーに限定されています。 パーティション固有の、監査のパーティションの表示および監査のパーティションの削除の特権もあります。 各メッセージに必要な特権については、特定のメッセージ要求のドキュメントを参照してください。  
  
-   監査済みデータの変更は、**audit** エンティティのレコードに格納されます。  
  
## <a name="data-that-can-be-audited"></a>監査可能なデータ  
 次の一覧では、監査できるデータおよび操作を示します。  
  
-   レコードの作成、更新、削除の操作。  
  
-   レコードの共有特権の変更。  
  
-   レコードの N:N 関連付けまたは関連付け解除。  
  
-   セキュリティ ロールの変更。  
  
-   エンティティ、属性、組織のレベルでの監査の変更。 エンティティに対する監査の有効化など。  
  
-   監査ログの削除。  
  
-   ユーザーがアプリ用 CDS データにアクセスする日時、期間、およびアクセスに使用するクライアント。  
  
 <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.IsSecured> 属性の設定によるフィールド レベルでのセキュリティの有効化または無効化は監査できません。  
  
### <a name="see-also"></a>関連項目
 [Dynamics 365 でのデータ管理](/dynamics365/customer-engagement/developer/manage-data)   
 [監査エンティティのデータ変更](/dynamics365/customer-engagement/developer/audit-entity-data-changes)   
 [監査のエンティティおよび属性の構成](configure-entities-attributes-auditing.md)       
 [ブログ: 削除した CRM データの復元と再作成 (CRM API を使用)](http://blogs.msdn.com/b/crm/archive/2011/05/23/recover-your-deleted-crm-data-and-recreate-them-using-crm-api.aspx)