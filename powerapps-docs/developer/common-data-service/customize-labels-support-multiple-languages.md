---
title: 複数言語をサポートするためのラベルのカスタマイズ (Common Data Service) | Microsoft Docs
description: 複数の言語をサポートするためのラベルのカスタマイズについて学習します。
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
# <a name="customize-labels-to-support-multiple-languages"></a>複数言語をサポートするためのラベルのカスタマイズ

Common Data Service でカスタマイズを作成するときは、ラベルを使用することで複数の言語をサポートできます。  

<a name="BKMK_UsingLabels"></a>   

## <a name="using-labels"></a>ラベルの使用  

|Microsoft.Xrm.Sdk.dll|Web API|
|----------------|----------------|
|<xref:Microsoft.Xrm.Sdk.Label> クラス|<xref href="Microsoft.Dynamics.CRM.Label?text=Label ComplexType" />|
|<xref:Microsoft.Xrm.Sdk.LocalizedLabel> クラス|<xref href="Microsoft.Dynamics.CRM.LocalizedLabel?text=LocalizedLabel ComplexType" />|

 ラベルは、クライアント アプリケーションでユーザーに表示されるローカライズされた文字列です。 それらは、言語パックをサポートする `Label` (<xref href="Microsoft.Dynamics.CRM.Label?text=Label ComplexType" /> または <xref:Microsoft.Xrm.Sdk.Label> クラス) を使用して実装されます。 エンティティの表示名やオプション セット内のオプションなど、ユーザーに表示される文字列は複数の言語で保存できます。 ユーザーは Common Data Service でフォームおよびビューに表示する言語を選択できます。  

 次の表に、`Label` を使用するすべてのメタデータの一覧を示します。  

|メタデータ プロパティ|内容|  
|-----------------------|-----------------|  
|AttributeMetadata.Description|属性の説明。|  
|AttributeMetadata.DisplayName|属性の表示名。|  
|EntityMetadata.Description|エンティティの説明。|  
|EntityMetadata.DisplayCollectionName|エンティティの複数形での表示名。|  
|EntityMetadata.DisplayName|エンティティの表示名。|  
|AssociatedMenuConfiguration.Label|1 対 1 のエンティティ関連付けで使用されるラベル。|  
|OptionMetadata.Label|候補リスト、状態、またはステータス属性のオプションで使用されるラベル。|  

 `Label` には、インストールされている言語ごとに 1 つずつ文字列を格納することができます。 この配列は `LocalizedLabels` プロパティです。 常に、基本言語用に格納されたラベルが存在する必要があります。 その他の言語のラベルは **null** にすることができます。 ユーザーがユーザー インターフェイスをある言語で表示するときに、その言語の文字列のラベルがない場合は、基本言語のラベルが使用されます。  

 `UserLocalizedLabel` プロパティを使用して、ユーザーが選択した言語のラベルを取得できます。  

<a name="BKMK_MessagesToWorkWithLabels"></a>   

## <a name="messages-to-use-with-labels"></a>ラベルで使用するメッセージ  
 以下の表には、複数の言語をサポートするためにローカライズされたラベルの操作に使用できるメッセージを一覧表示します。 翻訳のインポート時は、ソリューションのインポート時と同じ方法でインポート ジョブに基づいてレポートを生成できます。 詳細については、[ソリューションのインストールまたはアップグレード](work-solutions.md#BKMK_InstallUpgradeSolution) を参照してください。  


|                                                                                          メッセージ                                                                                          |                                                    Web API 操作                                                     |                                SDK アセンブリ                                |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
|                                               ExportTranslation</br>特定のソリューションのすべての翻訳を圧縮ファイルにエクスポートします。                                                |                  <xref href="Microsoft.Dynamics.CRM.ExportTranslation?text=ExportTranslation Action" />                  |         <xref:Microsoft.Crm.Sdk.Messages.ExportTranslationRequest>         |
|                                                          ImportTranslation</br>圧縮ファイルからすべての翻訳をインポートします。                                                           |                  <xref href="Microsoft.Dynamics.CRM.ImportTranslation?text=ImportTranslation Action" />                  |         <xref:Microsoft.Crm.Sdk.Messages.ImportTranslationRequest>         |
| RetrieveFormattedImportJobResults</br>インポート ジョブの結果を、Office Excel で開ける形式の XML ドキュメントとして取得します。 | <xref href="Microsoft.Dynamics.CRM.RetrieveFormattedImportJobResults?text=RetrieveFormattedImportJobResults Function" /> | <xref:Microsoft.Crm.Sdk.Messages.RetrieveFormattedImportJobResultsRequest> |
|                                                     RetrieveLocLabels</br>指定された属性のローカライズされたラベルを取得します。                                                     |                 <xref href="Microsoft.Dynamics.CRM.RetrieveLocLabels?text=RetrieveLocLabels Function" />                 |         <xref:Microsoft.Crm.Sdk.Messages.RetrieveLocLabelsRequest>         |
|                                                          SetLocLabels</br>指定された属性のローカライズされたラベルを設定します。                                                          |                       <xref href="Microsoft.Dynamics.CRM.SetLocLabels?text=SetLocLabels Action" />                       |           <xref:Microsoft.Crm.Sdk.Messages.SetLocLabelsRequest>            |

<a name="BKMK_CustomizingLabelsInBaseLanguage."></a>
   
## <a name="customize-labels-in-the-base-language"></a>基本言語のラベルのカスタマイズ  
 カスタマイズ ツールにはエンティティの表示名を編集する方法が用意されており、これらのプロパティをプログラムでカスタマイズできます。 エンティティ メッセージを編集することもできます。 ただし、すべてのメッセージが公開されるわけではありません。 アプリケーションで使用されるテキストを見つけてカスタマイズする別の方法は、翻訳をエクスポートし、基本言語の値を編集し、翻訳を再度インポートすることです。 これはこの機能の本来の目的ではありませんが、アプリケーションで使用されるテキストを識別してカスタマイズするためにサポートされている方法です。 詳細については、[エンティティのメッセージの変更](/dynamics365/customer-engagement/developer/modify-messages-entity) を参照してください。  

<a name="BKMK_TranslatingCustomizedEntityAndAttributeText"></a>   

## <a name="translate-customized-entity-and-attribute-text"></a>カスタマイズされたエンティティおよび属性のテキストの翻訳  
 アプリケーションのカスタマイズは基本言語でのみ実行できるので、カスタマイズ用のローカライズされたラベルを用意する場合は、組織で使用できる他の言語にローカライズできるように、ラベルのテキストをエクスポートする必要があります。  

### <a name="export-customized-text-for-translation"></a>カスタマイズされたテキストの翻訳用のエクスポート  
 Web アプリケーション内の翻訳は `ExportTranslation` メッセージ (<xref href="Microsoft.Dynamics.CRM.ExportTranslation?text=ExportTranslation Action" /> または <xref:Microsoft.Crm.Sdk.Messages.ExportTranslationRequest> クラス) を使用してエクスポートすることができます。  

 エクスポートされたテキストは、Office Excel を使用して開く CrmTranslations.xml を含む、圧縮ファイルとして保存されます。 翻訳担当者、翻訳会社、およびローカリゼーション会社にはこのファイルを送信できます。  

 詳細は、[Office 2003 XML リファレンス スキーマ](http://www.microsoft.com/downloads/details.aspx?FamilyID=fe118952-3547-420a-a412-00a2662442d9)を参照してください。  

### <a name="import-translated-text"></a>翻訳されたテキストのインポート  
 カスタマイズされたエンティティまたは属性のテキストをエクスポートし、翻訳したら、`ImportTranslation` メッセージ (<xref href="Microsoft.Dynamics.CRM.ImportTranslation?text=ImportTranslation Action" /> または <xref:Microsoft.Crm.Sdk.Messages.ImportTranslationRequest> クラス) を使用して、Web アプリケーション内に翻訳済みのテキスト文字列をインポートすることができます。 インポートするファイルは、エクスポートされたときの CrmTranslations.xml および [Content_Types].xml ファイルを格納する圧縮ファイルである必要があります。  

 完了した翻訳をインポートした後、カスタマイズされたテキストは、そのテキストの翻訳後の言語を使用するユーザーに表示されます。  

> [!NOTE]
> Common Data Service は 500 文字を超える長さの翻訳済みテキストをインポートすることができません。 翻訳ファイル内の任意のアイテムが 500 文字を超える長さの場合、インポート プロセスは失敗します。 インポート プロセスが失敗した場合は、失敗の原因となったファイル中の行を確認し、文字数を減らしてから再度インポートを試みてください。  

 カスタマイズは基本言語でのみサポートされるので、Common Data Service で言語選択で設定した基本言語で作業する場合があります。 翻訳済みテキストが表示されることを確認するには、Common Data Service のユーザー インターフェイスの言語選択を変更する必要があります。 カスタマイズに関する追加の作業を行うには、基本言語に戻す必要があります。  

<a name="BKMK_ManagingLanguages"></a>   

## <a name="manage-languages-for-your-organization"></a>組織で使用する言語の管理  
 Common Data Service ではサーバー上に複数の言語パックをインストールして、ユーザーが言語パックを選択することができます。 言語パックをインストールする方法については、[言語を有効にする](/dynamics365/customer-engagement/admin/enable-languages) を参照してください。 このセクションには、組織のためにインストールされた言語の管理で使用するメッセージに関する情報が含まれています。  

 次の表に、言語パックを操作する際に使用するメッセージを示します。 これらのメッセージは <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッドとともに使用します。  

|メッセージ|Web API 操作|SDK アセンブリ|  
|-------------|-----------------|----------------|  
|DeprovisionLanguage</br>言語のプロビジョニングを解除するために必要なデータを格納します。|<xref href="Microsoft.Dynamics.CRM.DeprovisionLanguage?text=DeprovisionLanguage Action" />|<xref:Microsoft.Crm.Sdk.Messages.DeprovisionLanguageRequest>|  
|ProvisionLanguage</br>新しい言語をプロビジョニングするために必要なデータを格納します。|<xref href="Microsoft.Dynamics.CRM.ProvisionLanguage?text=ProvisionLanguage Action" />|<xref:Microsoft.Crm.Sdk.Messages.ProvisionLanguageRequest>|  
|RetrieveAvailableLanguages</br>使用可能な言語の一覧を取得します。|<xref href="Microsoft.Dynamics.CRM.RetrieveAvailableLanguages?text=RetrieveAvailableLanguages Function" />|<xref:Microsoft.Crm.Sdk.Messages.RetrieveAvailableLanguagesRequest>|  
|RetrieveDeprovisionedLanguages</br>サーバーにインストール済みの言語パックのうち、無効になっているものの一覧を取得します。|<xref href="Microsoft.Dynamics.CRM.RetrieveDeprovisionedLanguages?text=RetrieveDeprovisionedLanguages Function" />|<xref:Microsoft.Crm.Sdk.Messages.RetrieveDeprovisionedLanguagesRequest>|  
|RetrieveInstalledLanguagePacks</br>サーバーにインストール済みの言語パックの一覧を取得するために必要なデータを格納します。|<xref href="Microsoft.Dynamics.CRM.RetrieveInstalledLanguagePacks?text=RetrieveInstalledLanguagePacks Function" />|<xref:Microsoft.Crm.Sdk.Messages.RetrieveInstalledLanguagePacksRequest>|  
|RetrieveInstalledLanguagePackVersion</br>インストール済みの言語パックのバージョンを取得するために必要なデータを格納します。|<xref href="Microsoft.Dynamics.CRM.RetrieveInstalledLanguagePacks?text=RetrieveLicenseInfo Function" />|<xref:Microsoft.Crm.Sdk.Messages.RetrieveInstalledLanguagePackVersionRequest>|  
|RetrieveProvisionedLanguages</br>有効になっているサーバーにインストールされている言語パックの一覧を取得します。|<xref href="Microsoft.Dynamics.CRM.RetrieveProvisionedLanguages?text=RetrieveProvisionedLanguages Function" />|<xref:Microsoft.Crm.Sdk.Messages.RetrieveProvisionedLanguagesRequest>|  
|RetrieveProvisionedLanguagePackVersion</br>サーバーにインストールされている言語パックのバージョンを取得します。|<xref href="Microsoft.Dynamics.CRM.RetrieveProvisionedLanguagePackVersion?text=RetrieveProvisionedLanguagePackVersion Function" />|<xref:Microsoft.Crm.Sdk.Messages.RetrieveProvisionedLanguagePackVersionRequest>|  

### <a name="see-also"></a>関連項目  
 [Dynamics 365 のメタデータ モデルの拡張](/dynamics365/customer-engagement/developer/org-service/use-organization-service-metadata)   
 [Dynamics 365 をカスタマイズする](/dynamics365/customer-engagement/developer/customize-dev/customize-applications)   
 [エンティティのメッセージの変更](/dynamics365/customer-engagement/developer/modify-messages-entity)     
 <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata>   
 <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>    
 <xref:Microsoft.Xrm.Sdk.Metadata.OptionMetadata> 
