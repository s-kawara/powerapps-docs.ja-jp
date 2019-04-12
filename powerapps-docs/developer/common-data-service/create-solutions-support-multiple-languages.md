---
title: 複数の言語をサポートするソリューションを作成 (Common Data Service) | Microsoft Docs
description: <Description>
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: shmcarth
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-solutions-that-support-multiple-languages"></a>複数の言語をサポートするソリューションの作成

Common Data Service は複数の言語をサポートしています。 ソリューションを、異なる基本言語を含む組織や複数言語が準備されている組織にインストールする場合は、ソリューションの計画時に検討してください。 次の表は複数の言語がサポートされるソリューションに含めるソリューション コンポーネントで使用する戦略の一覧です。  
  
|戦略|ソリューション コンポーネントの種類|  
|------------|-----------------------------|  
|[文字列 (RESX) Web リソース](#BKMK_Localizable_Web_Resources)|Web リソース|  
|[埋め込みラベル](#BKMK_EmbeddedLabels)|アプリケーションのナビゲーション (SiteMap) <br />リボン|  
|[翻訳のエクスポートおよびインポート](#BKMK_ExportAndImportTranslations)|属性<br />グラフ<br />ダッシュボード<br />Entity<br />エンティティ リレーションシップ<br />フォーム<br />メッセージ<br />オプション セット<br />ビュー|  
|[基本言語の文字列のローカライズ](#BKMK_LocalizationInBaseLanguageStrings)|契約テンプレート<br /> つながりロール<br />プロセス (ワークフロー)<br />セキュリティ ロール<br />フィールド セキュリティ プロファイル|  
|[ローカライズが不要な場合](#BKMK_LocalizationNotRequired)|SDK メッセージ処理手順<br />サービス エンドポイント|  
|[各言語の個別のコンポーネント](#BKMK_SeparateComponentForEachLanguage)|記事テンプレート<br />電子メール テンプレート<br />差し込み印刷用テンプレート<br />レポート<br />ダイアログ|  
|[言語リソースとして XML Web リソースを使用する](#BKMK_UseXMLWebResourcesAsLanguageResources)|プラグイン アセンブリ|  
  
 以下のセクションで、各戦略の詳細情報を提供します。  

 <a name="BKMK_Localizable_Web_Resources"></a>

 ## <a name="string-resx-web-resources"></a>文字列 (RESX) Web リソース
 Common Data Service で文字列 (RESX) Web リソースを追加すると、開発者は複数言語をサポートする Web リソースを作成するための強力なオプションをさらに取得することができます。 詳細については、[文字列 (RESX) Web リソース](/dynamics365/customer-engagement/developer/resx-web-resources) を参照してください。

 以前のバージョンの場合は、[開発者のオプション](https://msdn.microsoft.com/library/hh670609(v=crm.8).aspx#BKMK_DeveloperOption) を参照してください
  
<a name="BKMK_EmbeddedLabels"></a>   

## <a name="embedded-labels"></a>埋め込みラベル  
 この戦略を使用するソリューション コンポーネントごとに、ローカライズされたテキストをソリューションに含める必要があります。  
  
### <a name="ribbons"></a>リボン  
 言語パックをインストールすると、アプリケーション リボンは自動的にリボンのすべての既定のテキストがローカライズ済みのテキストで表示されます。 システム ラベルは内部使用限定の `ResourceId` 属性値で定義されます。 独自のテキストを追加するときに、`<LocLabels>` 要素を使用して、サポートする言語のローカライズ済みテキストを作成します。 詳細: [リボンでのローカライズされたラベルの使用](/dynamics365/customer-engagement/developer/customize-dev/use-localized-labels-ribbons)  
  
### <a name="sitemap"></a>SiteMap  
 言語パックをインストールすると、アプリケーション ナビゲーション バーの既定のテキストは、自動的にローカライズされたテキストで表示されます。 既定のテキストを上書きまたは独自のテキストを使用するには `<Titles>` 要素を使用します。 `Titles` 要素は、ソリューションでサポートされるすべての言語用のローカライズされたテキストを含む `<Title>` 要素も含める必要があります。 `Title` 要素をユーザーが優先する言語で使用できない場合、組織の基本言語に対応したタイトルが表示されます。  
  
 `<SubArea>` 要素で、`userlcid` パラメーターを使用して `SubArea.Url` 属性の対象コンテンツをユーザーの言語設定に対応し調整できるよう、ユーザーの言語設定を渡すことができます。 詳細: [サイトマップを使用して URL にパラメーターを渡す方法](/dynamics365/customer-engagement/developer/customize-dev/pass-parameters-url-using-sitemap)  
  
<a name="BKMK_ExportAndImportTranslations"></a>   

## <a name="export-and-import-translations"></a>翻訳のエクスポートおよびインポート  
 次の表のソリューション コンポーネントのローカライズされたラベルは、ローカライズ用にエクスポートできます。  
  
||||  
|-|-|-|  
|エンティティ|属性|関連付け|  
|グローバル オプション セット|エンティティ メッセージ|エンティティ フォーム|  
|エンティティ ビュー (SavedQuery)|グラフ|ダッシュボード|  
  
### <a name="translating-labels-and-display-strings"></a>ラベルを翻訳して文字列を表示する  
 カスタマイズは、基本言語を使用したアプリケーションでしか実行できません。 そのため、カスタマイズ用のローカライズされたラベルを用意して文字列を表示する場合は、組織で使用できる他の言語にローカライズできるように、ラベルのテキストをエクスポートする必要があります。 次の手順を実行します。  
  
1. 作業する組織に、翻訳を入力する言語用のすべての MUI パックがインストールされており、言語が用意されていることを確認します。  
  
2. ソリューションを作成し、コンポーネントを変更します。  
  
3. ソリューションの開発を終了した後、"翻訳のエクスポート" 機能を使用します。 これにより、翻訳が必要なすべてのラベルを含む Office Excel のスプレッドシート (CrmTranslations.xml) が生成されます。  
  
4. スプレッドシートに、対応する翻訳を入力します。  
  
5. "翻訳のインポート" 機能を使用して翻訳を同じ Common Data Service 組織にインポートし、変更を公開します。  
  
6. 次にソリューションをエクスポートしたときに、設定したすべての翻訳がソリューションに含まれます。  
  
   ソリューションのインポート時、ターゲット システムで使用できない言語のラベルは破棄され、警告が記録されます。  
  
   ソリューション パッケージでターゲット システムの基本言語のラベルが提供されない場合は、代わりにソースの基本言語のラベルが使用されます。 たとえば、基本言語が英語であるソリューションで、英語とフランス語のラベルを含むソリューションをインポートしたが、ターゲット システムでは基本言語が日本語で、日本語とフランス語が設定されている場合、日本語のラベルの代わりに英語のラベルが使用されます。 基本言語のラベルは、**null** にすることも空にすることもできません。  
  
#### <a name="exporting-translations"></a>翻訳をエクスポートする  
 翻訳をエクスポートする前に、言語パックをインストールし、ローカライズするすべての言語を準備する必要があります。 翻訳は Web アプリケーションにエクスポートするか、<xref:Microsoft.Crm.Sdk.Messages.ExportTranslationRequest> メッセージを使用してエクスポートできます。 詳細については、「[カスタマイズされたエンティティとフィールド テキストの翻訳用のエクスポート](/dynamics365/customer-engagement/customize/export-customized-entity-field-text-translation)」を参照してください。  
  
#### <a name="translating-text"></a>テキストの翻訳  
 Office Excel で CrmTranslations.xml ファイルを開くと、次の表に示す 3 種類のワークシートが表示されます。  
  
|ワークシート|説明|  
|---------------|-----------------|  
|情報|ラベルおよび文字列のエクスポート元の組織とソリューションに関する情報を表示します。|  
|表示文字列|メタデータ コンポーネントに関連するメッセージのテキストを表す文字列を表示します。 この表に、システム リボン要素に使用するエラー メッセージと文字列を示します。|  
|ローカライズされたラベル|メタデータ コンポーネントのラベルのテキストをすべて表示します。|  
  
 翻訳担当者、翻訳会社、およびローカリゼーション会社にはこのファイルを送信できます。 空のセルにローカライズされた文字列を指定する必要があります。  
  
> [!NOTE]
>  ユーザー定義エンティティに対しては**作成日**または**作成者**などのシステム エンティティと共有する、共通のラベルがあります。 この言語は既にインストールおよび準備されているため、既定のソリューションの言語をエクスポートすると、一部の、ローカライズされたテキストのあるユーザー定義エンティティのラベルを他のエンティティで使用する同一のラベルと一致させることができます。 これにより、ローカライズにかかるコストを削減し、一貫性を向上できます。  
  
 ワークシートのテキストをローカライズ後、CrmTranslations.xml および [Content_Types].xml の両方のファイルを 1 つの圧縮 .zip ファイルに追加します。 これで、このファイルをインポートできます。  
  
 XML ドキュメントとしてファイルをプログラムでエクスポートする場合は、これらのファイルが使用するスキーマについての情報を「[Office 2003 XML Reference Schemas (Office 2003 XML リファレンス スキーマ)](http://www.microsoft.com/downloads/details.aspx?FamilyID=fe118952-3547-420a-a412-00a2662442d9)」で参照してください。  
  
#### <a name="importing-translated-text"></a>翻訳済みテキストのインポート  
  
> [!IMPORTANT]
>  エクスポート元と同じ組織にのみ、翻訳済みテキストをインポートして戻すことができます。  
  
 カスタマイズされたエンティティまたは属性のテキストをエクスポートし、翻訳したら、<xref:Microsoft.Crm.Sdk.Messages.ImportTranslationRequest> メッセージを使用して、Web アプリケーションに翻訳済みのテキスト文字列をインポートできます。 インポートするファイルは、ルートの CrmTranslations.xml と [Content_Types].xml ファイルを含む圧縮ファイルである必要があります。 詳細については、「[エンティティおよびフィールドの翻訳済みテキストのインポート](/dynamics365/customer-engagement/customize/import-translated-entity-field-text)」を参照してください。  
  
 完了した翻訳をインポートした後、カスタマイズされたテキストは、そのテキストの翻訳後の言語を使用するユーザーに表示されます。  
  
> [!NOTE]
> Common Data Service は 500 文字を超える長さの翻訳済みテキストをインポートすることができません。 翻訳ファイル内の任意のアイテムが 500 文字を超える長さの場合、インポート プロセスは失敗します。 インポート プロセスが失敗した場合は、失敗の原因となったファイル中の行を確認し、文字数を減らしてから再度インポートを試みてください。  
  
 カスタマイズは基本言語でのみサポートされるので、Common Data Service で言語選択で設定した基本言語で作業する場合があります。 翻訳済みテキストが表示されることを確認するには、Common Data Service のユーザー インターフェイスの言語選択を変更する必要があります。 カスタマイズに関する追加の作業を行うには、基本言語に戻す必要があります。  
  
<a name="BKMK_LocalizationInBaseLanguageStrings"></a>   

## <a name="localization-in-base-language-strings"></a>基本言語の文字列のローカライズ  
 一部のソリューション コンポーネントは、複数の言語をサポートしていません。 これらのコンポーネントには、特定の言語で意味のある名前またはテキストのみが含まれます。 特定の言語用のソリューションを作成した後、目的の組織の基本言語に対してこれらのソリューション コンポーネントを定義します。  
  
 複数の言語をサポートする必要がある場合は、1 つの方法として、1 つの基本言語にローカライズを含める方法があります。 たとえば "Friend" というつながりロールがあり、英語、スペイン語、ドイツ語をサポートする必要がある場合、“Friend (Amigo / Freund)” というテキストをつながりロールの名前として使用できます。 テキストの長さに関する不具合があるため、この方法を使用してサポートできる言語数には制限があります。  
  
 このグループに含まれるソリューション コンポーネントの一部は管理者のみに表示されます。 システムのカスタマイズは、組織の基本言語でのみ実行できるので、複数の言語バージョンを提供する必要はありません。 **セキュリティ ロール**および**フィールド セキュリティ プロファイル**コンポーネントはこのグループに属します。  
  
 **契約テンプレート**で、サービス契約の種類を説明します。 これらは**名前**と**省略形**フィールドのテキストが必要です。 一意の名前および省略形を使用し、組織のすべてのユーザーに対して適用する必要があります。  
  
 **つながりロール**はわかりやすいつながりロールのカテゴリおよび名前を選択しているユーザーに依存します。 これらは比較的短くできるので、基本言語文字列にローカライズの列を含めることをお勧めします。  
  
 イベントで開始される**プロセス (ワークフロー)** は、ローカライズされたテキストでレコードを更新する必要がない場合は正常に動作します。 ローカライズされたテキストに適用される可能性があるロジックが、プラグイン アセンブリと同じ方法を使用できるようにワークフロー アセンブリを使用することができます ([言語リソースとして XML Web リソースを使用する](#BKMK_UseXMLWebResourcesAsLanguageResources))。  
  
 **オンデマンド ワークフロー**は、ユーザーがワークフローを選択できるように名前が必要です。 オンデマンド ワークフローの名前にローカライズを含める方法の他に、ローカライズされた名前の複数のワークフローを作成し、それぞれで同じ子プロセスを呼び出す方法があります。 ただし、ユーザーに該当するユーザー インターフェイスの言語のみの一覧ではなく、すべてのユーザーにオンデマンド ワークフローの完全な一覧が表示されます。  
  
<a name="BKMK_LocalizationNotRequired"></a>   
## <a name="localization-not-required"></a>ローカライズが不要な場合  
 **SDK メッセージ処理手順**および**サービス エンドポイント**ソリューション コンポーネントは、ローカライズ可能なテキストが表示されません。 これらのコンポーネントに組織の基本言語に対応する名前と説明を付けることを重視する場合、その言語で名前と説明を付けたマネージド ソリューションの作成とエクスポートができます。  
  
<a name="BKMK_SeparateComponentForEachLanguage"></a>   
## <a name="separate-component-for-each-language"></a>各言語の個別のコンポーネント  
 次のソリューション コンポーネントはそれぞれ、ローカライズしたテキストが大量に含まれる可能性があります。  
  
- 記事テンプレート  
  
- 電子メール テンプレート  
  
- 差し込み印刷用テンプレート  
  
- レポート  
  
- ダイアログ  
  
  このようなソリューション コンポーネントの場合に推奨される方法は、各言語に対して別のコンポーネントを作成する方法です。 これは通常、コアのソリューション コンポーネントを含む基本のマネージド ソリューションを作成してから、各言語に対するこれらのソリューション コンポーネントを含む個別のマネージド ソリューションを作成することを意味します。 顧客がソリューションをインストールしたら、組織で準備した言語の管理マネージド ソリューションをインストールできます。  
  
  **プロセス (ワークフロー)** とは違い、現在のユーザーの言語設定を反映し、その言語のユーザーのみにダイアログを表示する**ダイアログ**を作成できます。  
  
#### <a name="create-a-localized-dialog-box"></a>ローカライズされたダイアログを作成する  
  
1. 適切な言語パックをインストールして言語を準備します。  
  
    詳細については、「[言語パックのインストール手順](https://technet.microsoft.com/library/hh699674.aspx)」を参照してください。  
  
2. 個人用オプションを変更して、ダイアログに表示する言語を**ユーザー インターフェイスの言語**で指定します。  
  
3. **設定**に移動し、**処理センター**グループで**プロセス**を選択します。  
  
4. **新規**を選択し、指定した言語でダイアログを作成します。  
  
5. ダイアログを作成した後は、個人用オプションを変更して組織の基本言語を指定します。  
  
6. 組織の基本言語を使用している間は、**設定**の**ソリューション**領域に移動して、ソリューションの一部としてローカライズされたダイアログを追加できます。  
  
   他の言語で作成したダイアログは、その言語を使用して Common Data Service を表示するユーザーにのみ表示されます。  
  
<a name="BKMK_UseXMLWebResourcesAsLanguageResources"></a>   

## <a name="use-xml-web-resources-as-language-resources"></a>言語リソースとして XML Web リソースを使用する  
 プラグイン アセンブリ ソリューション コンポーネントでは、エンド ユーザーに <xref:Microsoft.Xrm.Sdk.InvalidPluginExecutionException> をスローしたり、レコードを作成、更新してメッセージを送信できます。 Silverlight Web リソースと違って、プラグインではリソース ファイルは使用できません。  
  
 プラグインでローカライズされたテキストが必要なときは、XML Web リソースを使用してローカライズされた文字列を格納し、必要になったときにプラグインにアクセスできるようにします。 XML の構造はオプションですが、ASP.NET リソース (.resx) ファイルで使用されている構造に従って各言語別の XML Web リソースを作成することができます。 たとえば、以下は **localizedString.en_US** という名前の XML Web リソースで、 resx ファイルで使用されるパターンに従います。  
  
```xml  
<root>  
 <data name="ErrorMessage">  
  <value>There was an error completing this action. Please try again.</value>  
 </data>  
 <data name="Welcome">  
  <value>Welcome</value>  
 </data>  
</root>  
```  
  
 次のコードは、ローカライズされたメッセージをプラグインに渡してユーザーにメッセージを表示するための方法を示します。 `Account` エンティティの `Delete` イベントの事前検証ステージで使用します。  
  
```csharp  
protected void ExecutePreValidateAccountDelete(LocalPluginContext localContext)  
  {  
   if (localContext == null)  
   {  
    throw new ArgumentNullException("localContext");  
   }  
   int OrgLanguage = RetrieveOrganizationBaseLanguageCode(localContext.OrganizationService);  
   int UserLanguage = RetrieveUserUILanguageCode(localContext.OrganizationService,  
 localContext.PluginExecutionContext.InitiatingUserId);  
   String fallBackResourceFile = "";  
   switch (OrgLanguage)  
   {  
    case 1033:  
     fallBackResourceFile = "new_localizedStrings.en_US";  
     break;  
    case 1041:  
     fallBackResourceFile = "new_localizedStrings.ja_JP";  
     break;  
    case 1031:  
     fallBackResourceFile = "new_localizedStrings.de_DE";  
     break;  
    case 1036:  
     fallBackResourceFile = "new_localizedStrings.fr_FR";  
     break;  
    case 1034:  
     fallBackResourceFile = "new_localizedStrings.es_ES";  
     break;  
    case 1049:  
     fallBackResourceFile = "new_localizedStrings.ru_RU";  
     break;  
    default:  
     fallBackResourceFile = "new_localizedStrings.en_US";  
     break;  
   }  
   String ResourceFile = "";  
   switch (UserLanguage)  
   {  
    case 1033:  
     ResourceFile = "new_localizedStrings.en_US";  
     break;  
    case 1041:  
     ResourceFile = "new_localizedStrings.ja_JP";  
     break;  
    case 1031:  
     ResourceFile = "new_localizedStrings.de_DE";  
     break;  
    case 1036:  
     ResourceFile = "new_localizedStrings.fr_FR";  
     break;  
    case 1034:  
     ResourceFile = "new_localizedStrings.es_ES";  
     break;  
    case 1049:  
     ResourceFile = "new_localizedStrings.ru_RU";  
     break;  
    default:  
     ResourceFile = fallBackResourceFile;  
     break;  
   }  
   XmlDocument messages = RetrieveXmlWebResourceByName(localContext, ResourceFile);  
   String message = RetrieveLocalizedStringFromWebResource(localContext, messages, "ErrorMessage");  
   throw new InvalidPluginExecutionException(message);  
  }  
  protected static int RetrieveOrganizationBaseLanguageCode(IOrganizationService service)  
  {  
   QueryExpression organizationEntityQuery = new QueryExpression("organization");  
   organizationEntityQuery.ColumnSet.AddColumn("languagecode");  
   EntityCollection organizationEntities = service.RetrieveMultiple(organizationEntityQuery);  
   return (int)organizationEntities[0].Attributes["languagecode"];  
  }  
  protected static int RetrieveUserUILanguageCode(IOrganizationService service, Guid userId)  
  {  
   QueryExpression userSettingsQuery = new QueryExpression("usersettings");  
   userSettingsQuery.ColumnSet.AddColumns("uilanguageid", "systemuserid");  
   userSettingsQuery.Criteria.AddCondition("systemuserid", ConditionOperator.Equal, userId);  
   EntityCollection userSettings = service.RetrieveMultiple(userSettingsQuery);  
   if (userSettings.Entities.Count > 0)  
   {  
    return (int)userSettings.Entities[0]["uilanguageid"];  
   }  
   return 0;  
  }  
  protected static XmlDocument RetrieveXmlWebResourceByName(LocalPluginContext context, string webresourceSchemaName)  
  {  
   context.TracingService.Trace("Begin:RetrieveXmlWebResourceByName, webresourceSchemaName={0}", webresourceSchemaName);  
   QueryExpression webresourceQuery = new QueryExpression("webresource");  
   webresourceQuery.ColumnSet.AddColumn("content");  
   webresourceQuery.Criteria.AddCondition("name", ConditionOperator.Equal, webresourceSchemaName);  
   EntityCollection webresources = context.OrganizationService.RetrieveMultiple(webresourceQuery);  
   context.TracingService.Trace("Webresources Returned from server. Count={0}", webresources.Entities.Count);  
   if (webresources.Entities.Count > 0)  
   {  
    byte[] bytes = Convert.FromBase64String((string)webresources.Entities[0]["content"]);  
    // The bytes would contain the ByteOrderMask. Encoding.UTF8.GetString() does not remove the BOM.  
    // Stream Reader auto detects the BOM and removes it on the text  
    XmlDocument document = new XmlDocument();  
    document.XmlResolver = null;  
    using (MemoryStream ms = new MemoryStream(bytes))  
    {  
     using (StreamReader sr = new StreamReader(ms))  
     {  
      document.Load(sr);  
     }  
    }  
    context.TracingService.Trace("End:RetrieveXmlWebResourceByName , webresourceSchemaName={0}", webresourceSchemaName);  
    return document;  
   }  
   else  
   {  
    context.TracingService.Trace("{0} Webresource missing. Reinstall the solution", webresourceSchemaName);  
    throw new InvalidPluginExecutionException(String.Format("Unable to locate the web resource {0}.", webresourceSchemaName));  
    return null;  
 // This line never reached  
   }  
  }  
  protected static string RetrieveLocalizedStringFromWebResource(LocalPluginContext context, XmlDocument resource, string resourceId)  
  {  
   XmlNode valueNode = resource.SelectSingleNode(string.Format(CultureInfo.InvariantCulture, "./root/data[@name='{0}']/value", resourceId));  
   if (valueNode != null)  
   {  
    return valueNode.InnerText;  
   }  
   else  
   {  
    context.TracingService.Trace("No Node Found for {0} ", resourceId);  
    throw new InvalidPluginExecutionException(String.Format("ResourceID {0} was not found.", resourceId));  
   }  
  }  
```  
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 ソリューションを使用した拡張機能のパッケージ化および配布](/dynamics365/customer-engagement/developer/package-distribute-extensions-use-solutions)   
 [ソリューションの概要](introduction-solutions.md)   
 [ソリューション開発の計画](/dynamics365/customer-engagement/developer/plan-solution-development)   
 [ソリューション コンポーネントの依存関係の追跡](dependency-tracking-solution-components.md)   
 [アンマネージド ソリューションの作成、エクスポート、またはインポート](create-export-import-unmanaged-solution.md)   
 [マネージド ソリューションの作成、インストール、および更新](create-install-update-managed-solution.md)   
 [ソリューションのアンインストールまたは削除](uninstall-delete-solution.md)   
 [ソリューション エンティティ](/dynamics365/customer-engagement/developer/solution-entities)   
 [製品プロパティ値をローカライズする](/dynamics365/customer-engagement/developer/localize-product-property-values)
