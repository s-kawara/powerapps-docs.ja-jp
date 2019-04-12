---
title: カスタマイズ XML リファレンス (モデル駆動型アプリ) | MicrosoftDocs
description: customizations.xml ファイルは、エクスポートされるアンマネージド ソリューションに含まれるファイルの 1 つです。 ファイルにはシステムのカスタマイズおよび構成の全てまたは選択部分が含まれます
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 864699de-c22f-3504-f120-84ca5a4aeca6
author: JimDaly
ms.author: jdaly
manager: shilpas
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="customization-xml-reference"></a>カスタマイズ XML リファレンス

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customization-xml-reference -->

customizations.xml ファイルは、エクスポートされるアンマネージド ソリューションに含まれるファイルの 1 つです。 ファイルにはシステムのカスタマイズおよび構成の全てまたは選択部分が含まれます。 
  
 ソリューション ファイルは圧縮された .zip ファイルとしてエクスポートされます。 アンマネージド ソリューション ファイルのコンテンツは、カスタマイズ ファイルを編集する前に展開する必要があります。 アンマネージド ソリューションのすべてのファイルは、インポートする前に圧縮された .zip ファイルに追加する必要があります。  

> [!NOTE]
> - マネージド ソリューション ファイルの編集はサポートされていません。  
> - customizations.xml ファイルのすべての要素を編集できるわけではありません。 詳細: [カスタマイズ ファイルの編集のサポート](../common-data-service/when-edit-customization-file.md)

## <a name="in-this-section"></a>このセクションの内容

 [リボン コアのスキーマ](ribbon-core-schema.md)[リボン タイプのスキーマ](ribbon-types-schema.md)  
 [リボン WSS のスキーマ](ribbon-wss-schema.md)  
 [SiteMap スキーマ](/dynamics365/customer-engagement/developer/customize-dev/sitemap-schema)<br/> <!-- TODO need to fix the link--> 
 [フォーム XML スキーマ](form-xml-schema.md)<br/> 
 [FetchXML スキーマ](../common-data-service/fetchxml-schema.md) 

## <a name="related-sections"></a>関連セクション

 [Dynamics 365 で使用するスキーマ](/dynamics365/customer-engagement/developer/schemas-used-dynamics-365)<br/> <!-- TODO need to fix the link--> 
 [カスタマイズ ファイルを編集するとき](../common-data-service/when-edit-customization-file.md)  
[スキーマ検証を使用したカスタマイズ ファイルの編集](edit-customizations-xml-file-schema-validation.md)  
 [Dynamics 365 のリボンのカスタマイズ](customize-commands-ribbon.md)  
 [SiteMap を使用したアプリケーション ナビゲーションの変更](/dynamics365/customer-engagement/developer/customize-dev/change-application-navigation-using-sitemap) <!-- TODO need to fix the link--> 
