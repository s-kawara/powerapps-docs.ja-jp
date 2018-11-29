---
title: フィールド セキュリティ エンティティ (アプリ用 Common Data Service) | Microsoft Docs
description: フィールド セキュリティ エンティティを使用して、フィールド アクセスを指定のユーザーとチームに限定できる、フィールドレベルのセキュリティを適用する方法について説明します。
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
# <a name="field-security-entities"></a>フィールド セキュリティ エンティティ

フィールドレベルのセキュリティを適用するには、フィールド セキュリティ エンティティを使用します。これにより、フィールド アクセスを指定のユーザーとチームに限定できます。 フィールドレベルのセキュリティの適用範囲はグローバルです。つまり、レコードやユーザーが属している部署階層レベルに関係なく、組織内のすべてのレコードに適用されます。 フィールド セキュリティは、Web クライアント、Dynamics 365 for Outlook、Dynamics などのすべてのアプリ用 Common Data Service クライアントで動作します。 これは、アプリ用 CDS Web サービス、レポート、検索、オフライン、フィルター ビュー、監査、重複データ検出など、すべてのコンポーネントに適用されます。 このリリースでは、フィールドのセキュリティはカスタム フィールドと多くの標準 (OOB) フィールドの両方に適用できます。  
  
 セキュリティで保護されたフィールドでのメソッドの動作変更方法の詳細については、「[フィールド セキュリティを使用して Dynamics 365 でフィールド値へのアクセスを制御する方法](/dynamics365/customer-engagement/developer/security-dev/use-field-security-control-access-field-values)」を参照してください。  
  
> [!IMPORTANT]
>  フィールド レベルのセキュリティ プロファイルは、意図しないユーザーがプロファイル定義に基づいてアプリ用 CDS データにアクセスできないようにします。 SQL Server ACL が不適切に構成されている場合、または、SQL インジェクションに問題がある場合、無効なユーザーがフィールド レベル セキュリティ制限を回避して SQL Server のデータに直接アクセスできることがあります。 詳細については、「[Web アプリケーションのセキュリティ上の脅威の概要](https://msdn.microsoft.com/library/f13d73y6.aspx)」を参照してください。  
  
<a name="bkmk_setup"></a>   

## <a name="set-up-and-use-field-security"></a>フィールド セキュリティの設定と使用  
 フィールド セキュリティを使用するには、次のことを行います。  
  
1. フィールド セキュリティ プロファイル レコードの作成  
  
2. ユーザーまたはチームをプロファイルに追加する  
  
3. フィールド レベルで保護する属性を見つける  
  
4. 属性の作成時または属性メタデータの更新によって属性をセキュリティで保護する  
  
5. 属性のカスタマイズを公開する  
  
6. カスタム属性に対するプロファイルのアクセス権 (作成、更新、読み取り) を定義したフィールドのアクセス許可レコードを作成する  
  
   これらの手順の実行方法に関するサンプル コードについては、「[サンプル: エンティティでのフィールド セキュリティの有効化](/dynamics365/customer-engagement/developer/sample-enable-field-security-entity)」を参照してください。  
  
   指定したフィールド セキュリティ プロファイルで属性の作成、読み取り、または更新ができるかどうかを設定するには、次のフィールドのアクセス許可属性を使用します。 
   これらの属性の値を設定または比較するには、`field_security_permission_type` グローバル オプション設定を使用します。  
  
-   `FieldPermission`.`CanCreate`  
  
-   `FieldPermission`.`CanRead`  
  
-   `FieldPermission`.`CanUpdate`  
  
> [!IMPORTANT]
>  特権の低いユーザーは、フィールド セキュリティ プロファイルのエンティティへの読み取りアクセス権が与えられている場合、他のユーザーのプロファイルの内容を確認して、関心のあるセキュリティで保護された属性へのアクセス許可を持つ他のユーザーを見つけることができます。 次に、彼らは、ソーシャル エンジニアリング技術を使用して、これらのセキュリティで保護された属性へのアクセス権のあるプロファイルを割り当てることができます。  
  
<a name="bkmk_whichattributes"></a>   

## <a name="which-attributes-can-be-secured"></a>どの属性を保護できますか。  
 どの属性を保護できるかを確認するには、次のプロパティのエンティティ メタデータを照会できます。  
  
- <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.CanBeSecuredForCreate>  
  
- <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.CanBeSecuredForRead>  
  
- <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.CanBeSecuredForUpdate>  
  
  特定の属性のデータの種類に適用するそのほかのいくつかのルールがあります。  
  
- ブール型属性は、作成、更新操作に保護されていますが、読み取りには保護されていません。  
  
- オプション セット属性は、既定値が指定されていない場合、作成、更新、および読み取りに保護されています。  
  
  保護できる属性は数千とあります。この情報を検索する 2 つの簡単な方法があります。 組織のエンティティ メタデータを表示するには、メタデータ ブラウザー ソリューションをインストールしてください。メタデータ ブラウザー ソリューションについては、「[組織のメタデータの参照](/dynamics365/customer-engagement/developer/browse-your-metadata)」を参照してください。 「[エンティティ参照](/dynamics365/customer-engagement/developer/about-entity-reference)」でエンティティの参照ドキュメントを参照することもできます。  
  
<a name="bkmk_sharing"></a>   
## <a name="share-secured-fields"></a>セキュリティで保護されたフィールドの共有  
 セキュリティで保護されたフィールドは、レコードを共有するのと同様に共有できます。 それには、`PrincipalObjectAttributeAccess` (フィールド共有) レコードを作成、更新、または削除します。このとき、ユーザーまたはチーム、エンティティ、およびアクセス許可を指定します。  
  
 次の表は、レコードのセキュリティを保護するためのメソッドとフィールドのセキュリティを保護するためのメソッドの一覧です。  
  
|レコードの共有|フィールド アクセスの共有|  
|--------------------|--------------------------|  
|ユーザーまたはチームによるレコードへのアクセスを許可するには、<xref:Microsoft.Crm.Sdk.Messages.GrantAccessRequest> メッセージを使用します。|<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> メッセージまたは <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*> メソッドを使用してユーザーまたはチームに対してセキュリティ保護されたフィールド アクセス権を付与します。|  
|ユーザーまたはチームによるレコードへのアクセスを更新するには、<xref:Microsoft.Crm.Sdk.Messages.ModifyAccessRequest> メッセージを使用します。|<xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> メッセージまたは <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*> メソッドを使用してユーザーまたはチームに対してセキュリティ保護されたフィールド アクセス権を更新します。|  
|ユーザーまたはチームによるレコードへのアクセスを削除するには、<xref:Microsoft.Crm.Sdk.Messages.RevokeAccessRequest> メッセージを使用します。|<xref:Microsoft.Xrm.Sdk.Messages.DeleteRequest> メッセージまたは <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Delete*> メソッドを使用してユーザーまたはチームに対するセキュリティ保護されたフィールド アクセス権を削除します。|  
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 のセキュリティ モデル](security-model.md)   
 [管理およびセキュリティ エンティティ](/dynamics365/customer-engagement/developer/administration-security-entities)   
 [FieldSecurityProfile エンティティ](/reference/entities/fieldsecurityprofile.md)   
 [フィールドのアクセス許可 (FieldPermission) エンティティ](/reference/entities/fieldpermission.md)   
 [プリンシパル オブジェクト属性アクセス (PrincipalObjectAttributeAccess) エンティティ](/reference/entities/principalobjectattributeaccess.md)   
 [フィールド レベルのデータ暗号化](field-level-data-encryption.md)   
 [サンプル: フィールドのアクセス許可の取得](/dynamics365/customer-engagement/developer/sample-retrieve-field-permissions)   
 [サンプル: エンティティでのフィールド セキュリティの有効化](org-service/samples/enable-field-security-entity.md)   
 [サンプル: フィールド共有レコードの取得](/dynamics365/customer-engagement/developer/sample-retrieve-field-sharing-records)