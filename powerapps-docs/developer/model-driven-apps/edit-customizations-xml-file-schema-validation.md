---
title: スキーマ検証を使用した XML カスタマイズ ファイルの編集 (model-driven apps) | Microsoft Docs
description: customizations.xml ファイルは、ソリューションとしてエクスポートされる圧縮ファイル (.zip) に含まれています。 customizations.xml ファイルの特定の部分を手動で編集することができます。 スキーマに関する情報により、行った変更が有効であることを確認できます。
keywords: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: b77d962e-6e3c-bd28-d03c-cf2e23cd742d
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

# <a name="edit-the-customizations-xml-file-with-schema-validation"></a>スキーマ検証を使用した XML カスタマイズ ファイルの編集

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/edit-customizations-xml-file-schema-validation -->

customizations.xml ファイルは、ソリューションとしてエクスポートされる圧縮ファイル (.zip) に含まれています。 customizations.xml ファイルの特定の部分を手動で編集することができます。 スキーマに関する情報により、行った変更が有効であることを確認できます。  
  
## <a name="xsd-schema-files"></a>XSD スキーマ ファイル  
 ソリューションの customization.xml ファイルを検証するために使用される XSD スキーマ ファイルの [!INCLUDE[schema_download](../../includes/schema-download.md)]。 必要なファイルは次のとおりです。  
  
- CustomizationsSolution.xsd  
  
- fetch.xsd  
  
- FormXml.xsd  
  
- isv.config.xsd  
  
- RibbonCore.xsd  
  
- RibbonTypes.xsd  
  
- RibbonWSS.xsd  
  
- SiteMap.xsd  
  
- SiteMapType.xsd  
  
- VisualizationDataDescription.xsd  
  
  これらのファイルも`[Install Drive]\Program Files\Microsoft Dynamics CRM\Server\ApplicationFiles`のオンプレミス [!INCLUDE[pn_dynamics_crm_online](../../includes/pn-dynamics-crm-online.md)] Common Data Service サーバー にインストールされます。  
  
[!INCLUDE[cc_sdk_onpremises_note](../../includes/cc-sdk-onpremises-note.md)] CustomizationsSolution.xsd はエクスポートしたソリューションのスキーマです。 これには他の XSD ファイルへの参照が含まれます。 すべてのファイルは同じフォルダーに配置される必要があります。  
  
<a name="BKMK_UseSchemaValidation"></a>   
## <a name="using-schema-validation"></a>スキーマ検証の使用  
 エクスポートされた XML ファイルはテキスト ファイルなので、[!INCLUDE[pn_Notepad](../../includes/pn-notepad.md)] などのテキスト エディターを使用して編集できます。 ただし、XSD スキーマ検証機能を備えた [!INCLUDE[pn_Visual_Studio](../../includes/pn-visual-studio.md)] などのアプリケーションの使用を強く推奨します。 [!INCLUDE[pn_Visual_Studio](../../includes/pn-visual-studio.md)] における XSD の検証 <!-- TODO - need to fix this link. The page is not available (or [Visual Studio Express 2012 for Web](http://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web))--> エラーを防ぐのに役立つ [!INCLUDE[pn_IntelliSense](../../includes/pn-intellisense.md)] の情報とスキーマ検証を提供します。  
  
 ソリューションの customization.xml ファイルを検証するために使用される XSD スキーマ ファイルはここにあります。 [!INCLUDE[schema_download](../../includes/schema-download.md)]。 このフォルダーにあるすべてのファイルを同じディレクトリにコピーしてください。 customizations.xml ファイルを CustomizationsSolution.xsd ファイルに関連付ける必要があります。 このファイルには、フォルダー内の他のすべての XSD ファイルへのリンクが含まれます。  
  
1. XSD スキーマ ファイルをダウンロードし、コンピューターにそのすべてをコピーします。 これらのファイルを、[!INCLUDE[pn_Visual_Studio](../../includes/pn-visual-studio.md)] が XSD 検証ファイルを格納する場所に保存します。 通常、この場所は、`[install drive]\Program Files (x86)\Microsoft Visual Studio X.0\Xml\Schemas` です。ここで `X` は [!INCLUDE[pn_Visual_Studio_short](../../includes/pn-visual-studio-short.md)] のバージョンを表します。  
  
2. customizations.xml ファイルを右クリックして**プログラムから開く**を選択し、[!INCLUDE[pn_Visual_Studio_short](../../includes/pn-visual-studio-short.md)] のバージョンを選択します。  
  
3. **表示**をクリックし、**プロパティ ウィンドウ**をクリックします。  
  
4. **プロパティ**ウィンドウの、**スキーマ**フィールドで、省略記号 [**...**] ボタンをクリックします。  
  
5. **Xml スキーマ**ダイアログ ボックスには、customizationsSolution.xsd が表示されるはずです。 **使用**列で**このスキーマを使用する**を選択します。  
  
   > [!NOTE]
   >  目的のファイルが表示されていない場合は、**追加**をクリックし、ファイルの格納場所を参照します。  
  
6. **OK** をクリックします。  
  
   これで、XSD 検証機能を利用して XML を編集する準備は完了です。  
  
### <a name="see-also"></a>関連項目

[ Common Data Serviceのカスタマイズファイルを編集する場合](when-edit-customization-file.md)<br/> 
[リボン コアのスキーマ](ribbon-core-schema.md)<br/>
[リボン タイプのスキーマ](ribbon-types-schema.md)<br/>
[リボン WSS のスキーマ](ribbon-wss-schema.md)<br/>
[SiteMap スキーマ](/dynamics365/customer-engagement/developer/customize-dev/sitemap-schema)<br/>   <!-- TODO need to fix link relevant to the topic in powerapps repo-->
[フォーム XML スキーマ](form-xml-schema.md)     
[ISV Configuration File Schema](/dynamics365/customer-engagement/developer/customize-dev/isv-configuration-file-schema)<br/>   <!-- TODO need to fix link relevant to the topic in powerapps repo-->
[FetchXML を使用したクエリの構築](/dynamics365/customer-engagement/developer/org-service/build-queries-fetchxml) <!-- TODO need to fix link relevant to the topic in powerapps repo-->
