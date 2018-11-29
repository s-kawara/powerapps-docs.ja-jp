---
title: エンティティ関係のカスケード動作の構成 (アプリ用 Common Data Service) | Microsoft Docs
description: アプリ用 Common Data Service では、データの整合性を維持してビジネス プロセスを自動化するため、一対多のエンティティ関係のカスケード動作を構成します。
services: ''
suite: powerapps
documentationcenter: na
author: mayadumesh
manager: kvivek
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/31/2018
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="configure-entity-relationship-cascading-behavior"></a>エンティティ関係のカスケード動作の構成  

 データの整合性を維持してビジネス プロセスを自動化するため、一対多のエンティティ関係に対するカスケード動作を構成できます。 Web API および組織サービスの両方は、カスケード動作の構成をサポートしています。

## <a name="using-web-api-to-configure-cascading-behavior"></a>Web API を使用してカスケード動作の構成

Web API の作業をするときは、<xref href="Microsoft.Dynamics.CRM.OneToManyRelationshipMetadata?text=OneToManyRelationshipMetadata EntityType" /> を使用して一対多の関連付けを定義することができます。 この定義には、作成する交差するエンティティの名前と <xref href="Microsoft.Dynamics.CRM.AssociatedMenuConfiguration?text=AssociatedMenuConfiguration ComplexType" /><xref href="Microsoft.Dynamics.CRM.Label?text=Label ComplexType" /> および <xref href="Microsoft.Dynamics.CRM.LocalizedLabel?text=LocalizedLabel ComplexType" /> を使用した関連付けの表示方法も含まれます。 

詳細については、[Web API を使用して一対多の関連付けを作成する](webapi/create-update-entity-relationships-using-web-api.md#create-a-one-to-many-relationship) を参照してください。

## <a name="using-organization-service-to-configure-cascading-behavior"></a>組織サービスを使用してカスケード動作の構成

<xref:Microsoft.Xrm.Sdk.Messages.CreateOneToManyRequest> または <xref:Microsoft.Xrm.Sdk.Messages.UpdateRelationshipRequest> を使用するときは、<xref:Microsoft.Xrm.Sdk.Metadata.OneToManyRelationshipMetadata> クラスのインスタンスを要求の本体に含めます。 そのクラスの <xref:Microsoft.Xrm.Sdk.Metadata.OneToManyRelationshipMetadata.CascadeConfiguration> プロパティでは、<xref:Microsoft.Xrm.Sdk.Metadata.CascadeConfiguration> クラスを使用します。  

`CascadeConfiguration` (<xref:Microsoft.Xrm.Sdk.Metadata.CascadeConfiguration> クラスまたは <xref href="Microsoft.Dynamics.CRM.CascadeConfiguration?text=CascadeConfiguration ComplexType" />) には、一対多エンティティ関係の参照先エンティティで実行できる操作を表すプロパティが含まれます。 各プロパティには、<xref href="Microsoft.Dynamics.CRM.CascadeType?text=CascadeType EnumType" /> の値のいずれかを割り当てることができます。  

|Value|アプリケーション ラベル|内容|  
|-----------|-----------------------|-----------------|  
|Active|アクティブ レコードのみに伝播|参照先エンティティ レコードと関連付けられているすべてのアクティブな参照元エンティティ レコードで操作を実行します。|  
|伝播|すべてのレコードに伝播|参照先エンティティ レコードと関連付けられているすべての参照元エンティティ レコードで操作を実行します。|  
|NoCascade|伝播しない|何もしません。|  
|リンクの解除|関連付けの解除|参照先エンティティ レコードと関連付けられているすべての参照元エンティティ レコードの参照属性の値を削除します。|  
|制限する|制限する|参照元エンティティが存在するときは、参照先エンティティ レコードが削除されないようにします。|  
|ユーザーによる所有|同一所有者のレコードのみに伝播|参照先エンティティ レコードと同じユーザーによって所有されているすべての参照元エンティティ レコードで操作を実行します。|  
  
 `CascadeConfiguration` (<xref:Microsoft.Xrm.Sdk.Metadata.CascadeConfiguration> クラスまたは <xref href="Microsoft.Dynamics.CRM.CascadeConfiguration?text=CascadeConfiguration ComplexType" />) には、一対多エンティティ関係の参照先エンティティで実行できる操作を表す次のプロパティが含まれます。  
  
|操作​​|内容|有効なオプション|  
|------------|-----------------|-------------------|  
|割り当て​​|参照先エンティティ レコードの所有者が変更されます。|Active<br />伝播<br />NoCascade<br />ユーザーによる所有|  
|削除​​|参照先エンティティ レコードが削除されます。 **注:**  この操作のオプションは制限されます。|伝播<br />リンクの解除<br />制限する|  
|結合|レコードが別のレコードと結合されます。 **注:**  結合できる参照先エンティティに対しては、Cascade のみが有効なオプションです。 それ以外の場合は NoCascade を使用します。|伝播<br />NoCascade|  
|リペアレント|後で [リペアレント操作について](#about-the-reparent-action) を参照してください。|Active<br />伝播<br />NoCascade<br />ユーザーによる所有|  
|共有|参照先エンティティ レコードが別のユーザーと共有されるとき。|Active<br />伝播<br />NoCascade<br />ユーザーによる所有|  
|共有の解除|参照先エンティティ レコードで共有が削除されるとき。|Active<br />伝播<br />NoCascade<br />ユーザーによる所有|  
  
<a name="BKMK_ReparentAction"></a>   
### <a name="about-the-reparent-action"></a>リペアレント操作について  
 リペアレント操作は共有操作ととてもよく似ていますが、明示的な読み取りアクセス権ではなく、継承された読み取りアクセス権を処理する点が異なります。 リペアレント操作とは、上位下位の関連付けで参照属性の値を変更する場合です。 リペアレント操作が発生すると、関連するエンティティの継承された読み取りアクセス権の対象範囲が変化する場合があります。 リペアレント操作に関連するカスケード操作は、関連する特定のエンティティ レコードとあらゆるエンティティ レコードに対する読み取りアクセス権に対する変更を参照します。  

### <a name="see-also"></a>関連項目

[エンティティの関連付けのメタデータ](entity-relationship-metadata.md)  

