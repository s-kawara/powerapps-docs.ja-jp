---
title: URL を使用して Dynamics 365 モバイル クライアントでフォーム、ビュー、およびダッシュ ボードを開く (モデル駆動型アプリ) | MicrosoftDocs
description: Dynamics 365 モバイル クライアントの新しいアプリケーション ハンドラーを使用して、Dynamics 365 のフォーム、ビュー、およびダッシュボードに外部のアプリケーションから直接リンクし、外部アプリケーションでリンクをクリックしたときに、対象となる要素が電話用 Dynamics 365 またはタブレット PC 用 Dynamics 365で開くようにすることができます。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="open-forms-views-and-dashboards-in-mobile-client-with-a-url"></a>URL を使用してモバイル クライアントでフォーム、ビュー、およびダッシュ ボードを開く

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/open-forms-views-dashboards-mobile-client-url

At this point I understand this mobile client is still branded as 'Dynamics 365'
 -->
 
 モバイル クライアントの新しいアプリケーション ハンドラーを使用して、フォーム、ビュー、およびダッシュボードに外部のアプリケーションから直接リンクし、外部アプリケーションでリンクをクリックしたときに、対象となる要素が Dynamics 365 for phones または Dynamics 365 for tabletsで開くようにすることができます。 また、エンティティ レコードを作成するために空のフォームを開くことができます。  
  
 Dynamics 365 for phones または Dynamics 365 for tablets でインスタンスに既にサインインしている場合は、外部アプリケーションでリンクをクリックすると対象となるレコードがモバイル クライアントに表示されます。 それ以外の場合、 モバイル クライアントでインスタンスにサインインするように求められ、サインインすると対象の要素が表示されます。 この機能を使用するには、モバイル デバイスに Dynamics 365 for phones または Dynamics 365 for tablets をインストールしている必要があります。  
  
<a name="Parameters"></a>

## <a name="query-string-parameters-for-the-url"></a>URL のクエリ文字列パラメーター

 次のアプリケーション ハンドラーとクエリ文字列パラメーターを使用して、URL を作成します。  
  
```  
ms-dynamicsxrm://?pagetype=<VALUE>&etn=<VALUE>&id=<VALUE>  
```  
  
 次の表に示したクエリ文字列パラメーターが使用されます。  
  
|クエリ文字列パラメーター|内容|  
|----------------------------|-----------------|  
|pagetype|開くページの種類を指定します。 有効な値は、`entity`、`view`、`dashboard`、および `create` です。<br /><br /> このパラメーターは必須です。|  
|etn|レコードを開くか作成する対象のエンティティの論理名を指定します。  エンティティの論理名は小文字で、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.LogicalName> で定義されます。 プロパティ。<br /><br /> このパラメーターは、`pagetype` パラメーターが `entity`、`view`、または`create` に設定されている場合は必須です。|  
|id|開くエンティティ、ビュー、またはダッシュボード レコードの ID を指定します。<br /><br /> このパラメーターは、`pagetype` パラメーターが `entity` または `dashboard` に設定されている場合、必須です。<br /><br /> これは、`pagetype` パラメーターが `view` に設定されている場合は、省略可能です。 ビュー ID を指定しない場合、`etn` パラメーターに指定されたエンティティの既定のビューが表示されます。|  
  
<a name="Example"></a>

## <a name="example-urls"></a>例の URL

 フォーム、ビュー、およびダッシュボードを開くときに使用するいくつかの URI の例を示します。  
  
|アクション|例の URL|  
|------------|-----------------|  
|取引先企業レコード ID が 91330924-802A-4B0D-A900-34FD9D790829 の取引先企業エンティティを開きます|`ms-dynamicsxrm://?pagetype=entity&etn=account&id=91330924-802A-4B0D-A900-34FD9D790829`|  
|取引先担当者エンティティに対して、ビュー レコード ID が 899D4FCF-F4D3-E011-9D26-00155DBA3819 のビューを開きます|`ms-dynamicsxrm://?pagetype=view&etn=contact&id=899D4FCF-F4D3-E011-9D26-00155DBA3819`|  
|取引先企業エンティティの既定のビューを開く|`ms-dynamicsxrm://?pagetype=view&etn=account`|  
|ダッシュボード レコード ID が 2E3D0841-FA6D-DF11-986C-00155D2E3002 のダッシュボードを開きます|`ms-dynamicsxrm://?pagetype=dashboard&id=2E3D0841-FA6D-DF11-986C-00155D2E3002`|  
|取引先企業レコードを作成するためのフォームを開く|`ms-dynamicsxrm://?pagetype=create&etn=account`|  
  
### <a name="see-also"></a>関連項目

 [URL を使用してフォーム、ビュー、ダイアログおよびレポートを開く](open-forms-views-dialogs-reports-url.md)  
 [クライアントの拡張](/dynamics365/customer-engagement/developer/extend-client)
