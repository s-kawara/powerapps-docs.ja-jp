---
title: イメージ属性 (Common Data Service) | Microsoft Docs
description: アプリケーション内にデータを含めるイメージ属性、および、サポートされている属性、イメージ データの取得、およびイメージ データのアップロードについて説明します。
ms.custom: ''
ms.date: 11/26/2018
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
# <a name="image-attributes"></a>イメージ属性

イメージ データを含むエンティティ レコードにより、アプリケーションで独特なエクスペリエンスを提供します。 開発者は、イメージ データの使用方法について理解する必要があります。  
  
 特定のシステム エンティティとユーザー定義エンティティだけがイメージをサポートしています。 イメージをサポートしているシステム エンティティの詳細については、「[エンティティ イメージ](/dynamics365/customer-engagement/developer/introduction-entities#entity-images)」を参照してください。  
  
<a name="BKMK_SupportingAttributes"></a>   
## <a name="supporting-attributes"></a>属性のサポート  
 イメージ属性をサポートするエンティティでは、エンティティ イメージ属性の<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.SchemaName>は常に `EntityImage`です。 イメージ属性がエンティティに追加されると、一部の追加の属性がそれをサポートするために作成されます。  
  
> [!NOTE]
>  現在の .NET アセンブリを使用しないクライアントに、"6.0.0.0"以上の値の <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy.SdkClientVersion> を含める必要があるのは、<xref:Microsoft.Xrm.Sdk.Metadata.ImageAttributeMetadata> 属性を受け取るためです。 詳細については、「<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy.SdkClientVersion>」を参照してください。  
  
### <a name="entityimagetimestamp-attribute"></a>EntityImage_Timestamp 属性  
 属性の種類名: `BigIntType`  
  
 値は、イメージが最後に更新されときに表され、イメージの最新版がクライアントでダウンロードされ、キャッシュされることが確実にできるように使用されます。  
  
### <a name="entityimageurl-attribute"></a>EntityImage_URL 属性  
 属性の種類名: `StringType`  
  
 クライアントでエンティティ イメージを表示する絶対 URL。  
  
 この URL はこのように構成されます:  
  
```http  
{0}/image/download.aspx?entity={1}&attribute={2}&id={3}&timestamp={4}
```  
  
- 0 : 組織 URL  
  
- 1 : エンティティの論理名  
  
- 2 : 属性の論理名  
  
- 3: EntityImageId の値。  
  
- 4: EntityImage_Timestamp の値  
  
  たとえば、次のようになります。   
  `https://myorg.crm.dynamics.com/image/download.aspx?attribute=entityimage&entity=contact&id={ECB6D3DF-4A04-E311-AFE0-00155D9C3020}&timestamp=635120312218444444`  
  
### <a name="entityimageid"></a>EntityImageId  
 属性の種類名: `UniqueIdentifierType`  
  
 イメージの一意の識別子  
  
<a name="BKMK_RetrievingImages"></a>   
## <a name="retrieving-image-data"></a>イメージ データの取得  
 <xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*> または <xref:Microsoft.Xrm.Sdk.IOrganizationService.Retrieve*> を使用すると、<xref:Microsoft.Xrm.Sdk.Query.ColumnSet>.`AllColumns` の場合は `EntityImage` は含まれません。 プロパティが true に設定される場合です。 この属性のデータの潜在的なサイズのために、この属性を返すためには、明示的に要求する必要があります。  
  
 イメージを表すバイナリ データは、削除済みの <xref:Microsoft.Crm.Sdk.Messages.ExecuteFetchRequest> クラスを使用しては返されません。 代わりに、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMultipleRequest> を使用する必要があります。  
  
 詳細については、[サンプル: エンティティ イメージの設定および取得](/dynamics365/customer-engagement/developer/sample-set-retrieve-entity-images) を参照してください。  
  
<a name="BKMK_UploadingImages"></a>   
## <a name="uploading-image-data"></a>イメージ データのアップロード  
 イメージを更新するには、ファイルのコンテンツを含む`byte[]` に `EntityImage` の値を設定します。 すべての画像は 144x144 ピクセルの正方形で表示されます。 イメージは、保存する前にデータのサイズを減らすため切り取られ、サイズ変更されます。  
  
- 少なくとも 1 つの側面が 144 ピクセルより大きいイメージは中心で 144x144 に切り取られます。  
  
- 両側が144未満のイメージは最小のサイドに正方形に切り取られます。  
  
  次の表に2つの例を示します。  
  
|次の日付より前|次の日付より後|  
|------------|-----------|  
|![サイズ変更前の画像](media/crm-itpro-cust-imagebeforeresize.png "サイズ変更前の画像")<br /><br /> 300x428|![サイズ変更後の画像](media/crm-itpro-cust-imageafterresize.jpg "サイズ変更後の画像")<br /><br /> 144x144|  
|![2 番目のイメージ サイズ変更の例](media/crm-itpro-cust-imagebeforeresizeexample2.png "2 番目のイメージ サイズ変更の例")<br /><br /> 91x130|![2 番目のサイズ変更の例](media/crm-itpro-cust-imageafterresizeexample2.jpg "2 番目のサイズ変更の例")<br /><br /> 91x91|  
  
 詳細については、[サンプル: エンティティ イメージの設定および取得](/dynamics365/customer-engagement/developer/sample-set-retrieve-entity-images) を参照してください。  
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 のエンティティの概要](/dynamics365/customer-engagement/developer/introduction-entities)   
 [Dynamics 365 のエンティティ属性の概要](/dynamics365/customer-engagement/developer/introduction-entity-attributes)   
 [サンプル: エンティティ イメージを設定および取得する](/dynamics365/customer-engagement/developer/sample-set-retrieve-entity-images)
