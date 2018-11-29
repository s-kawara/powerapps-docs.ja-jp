---
title: ソリューション コンポーネント ファイル リファレンス (Common Data Service for Apps) | Microsoft Docs
description: このトピックでは、SolutionPackagerツールで使用されるフォルダー構造とそのファイル命名について説明します。 このツールは、Dynamics 365 ソリューション ファイルをソース コード管理システムで管理できる XML ファイルに分解 (解凍)するために使用されます。
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
# <a name="solution-component-file-reference-solutionpackager"></a>ソリューション コンポーネント ファイル リファレンス (SolutionPackager)

このトピックでは、SolutionPackagerツールで使用されるフォルダー構造とそのファイル命名について説明します。 このツールは、Common Data Service for Apps ソリューション ファイルをソース コード管理システムで管理できる XML ファイルに分解 (解凍) するために使用されます。 ツールは、これらの個々の XML ファイルを CDS for Apps にインポートできるソリューションファイルにコンパイル (パック) することもできます。 SolutionPackager ツールの詳細については、[SolutionPackager ツール ](compress-extract-solution-file-solutionpackager.md)を参照してください。  
  
 以下のセクションでは、各ソリューション コンポーネントの種類に対して作成されるファイルと、ソース管理に含めるのに適していないファイルについて説明します。 セクションに示されているフォルダーはすべて、**SolutionPackager**コマンドの `/folder` パラメーターで指定されたフォルダーに関連しています。  
  
<a name="entity_bm"></a>   
## <a name="entity"></a>Entity  
 管理ソリューションでは異なります: 可能  
  
### <a name="notes"></a>メモ​​  
  
1.  各エンティティには個別のフォルダーがあります。  
  
2.  各フォーム、ビューおよびビジュアル化は、それぞれのサブフォルダー内に独自のファイルを取得します。  
  
3.  フォームファイル名は、管理またはアンマネージド ソリューションの種類によって異なります。  
  
4.  特定のエンティティのリボンをカスタマイズするための RibbonDiff.xml の直接編集がサポートされています。  
  
5.  FormXml および SavedQueries フォルダーの XML ファイルの手動編集はサポートされていますがオプションです。  
  
### <a name="files"></a>ファイル  
 \Entities\\<Entity Schema Name\>\  
  
 Entity.xml  
RibbonDiff.xml  
  
 FormXml\Main\  
  
 {guid 1}.xml  
{guid 1_managed}.xml  
{guid n}.xml  
{guid n_managed}.xml  
  
 FormXml\Mobile\  
  
 {guid 1}.xml  
{guid 1_managed}.xml  
{guid n}.xml  
{guid n_managed}.xml  
  
 SavedQueries\  
  
 {guid 1}.xml  
{guid n}.xml  
  
 Visualizations\  
  
 {guid 1}.xml  
{guid n}.xml  
  
<a name="optionset_bm"></a>   
## <a name="option-set"></a>オプション セット  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
 各オプション セットは個々のファイルに保存されます。  
  
### <a name="files"></a>ファイル  
 \OptionSets\  
  
 \<schema name 1>.xml  
\<schema name n>.xml  
  
<a name="relationship_bm"></a>   
## <a name="entity-relationship"></a>エンティティの関連付け  
 管理ソリューションでは異なります: 可能  
  
### <a name="notes"></a>メモ​​  
  
1.  各エンティティには、すべての関連付けを含む個別ファイルがあります:  
  
    1.  N: N 最初にリストされているエンティティです  
  
    2.  1:N 参照先エンティティです  
  
### <a name="files"></a>ファイル  
 \Other\Relationships\  
  
 \<Entity schema name 1>.xml  
\<Entity schema name n>.xml  
  
<a name="ribbon_bm"></a>   
## <a name="ribbon-customization"></a>リボンのカスタマイズ  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
  
1.  すべてのエンティティ固有のリボン XML は、そのエンティティのそれぞれのフォルダーにあります。 その他のリボン XML は、このファイルにあります。  
  
2.  グローバル リボンをカスタマイズするための RibbonCustomizations.xml の直接編集がサポートされています。  
  
### <a name="files"></a>ファイル  
 \Other\RibbonCustomizations.xml  
  
<a name="sitemap_bm"></a>   
## <a name="site-map"></a>サイト マップ  
 管理ソリューションでは異なります: 可能  
  
### <a name="notes"></a>メモ​​  
 サイトマップXML形式は、アンマネージドソリューションと管理ソリューションでは異なります。 次のような、ファイル名があります。 両方のパッケージタイプを抽出すると、両方のファイルが存在します。  
  
### <a name="files"></a>ファイル  
 \Other\  
  
 SiteMap.xml  
SiteMap_managed.xml  
  
<a name="resource_bm"></a>   
## <a name="web-resources"></a>Web リソース  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
  
1.  生の Web リソースは、個別のファイルとして保存されます。 フォルダーを作成するには、スラッシュ (/) 文字を使用します。  
  
2.  Web リソースのメタデータは、末尾が .data.xml と類似のファイル名で保存されます。  
  
3.  Web リソースの名前には自然なファイル名の拡張子が含まれることをお勧めします。  
  
4.  生ファイルをソース管理に追加すると、重複が発生する可能性があります。  
  
### <a name="files"></a>ファイル  
 \WebResources\  
  
 \<name 1>  
\<name 1>.data.xml  
\<name n>  
\<name n>.data.xml  
  
<a name="role_bm"></a>   
## <a name="role"></a>ロール  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
 各ロールは個々のファイルに保存されます。  
  
### <a name="files"></a>ファイル  
 \Roles\  
  
 \<schema name>.xml  
  
<a name="connectionrole_bm"></a>   
## <a name="connection-role"></a>つながりロール   
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
 すべてのつながりロールは、1 つのファイルにまとめて保存されます。  
  
### <a name="files"></a>ファイル  
 \Other\ConnectionRoles.xml  
  
<a name="dashboard_bm"></a>   
## <a name="dashboard"></a>ダッシュボード​​  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
 各ダッシュボードは個々のファイルに保存されます。  
  
### <a name="files"></a>ファイル  
 \Dashboards\  
  
 {guid 1}.xml  
{guid n}.xml  
  
<a name="workflow_bm"></a>   
## <a name="workflow"></a>ワークフロー  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
  
1.  各ワークフローの XAML は個別のファイルに保存されます。  
  
2.  各ワークフローのメタデータは、末尾が .data.xml と類似のファイル名にあります。  
  
### <a name="files"></a>ファイル  
 \Workflows\  
  
 \<XamlFileName 1>.xaml  
\<XamlFileName 1>.xaml.data.xml  
\<XamlFileName n>.xaml  
\<XamlFileName n>.xaml.data.xml  
  
<a name="emailtemplate_bm"></a>   
## <a name="email-template"></a>電子メール テンプレート  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
  
1.  すべての電子メール テンプレートのメタデータは、単一のファイルに保存されます。  
  
2.  各電子メール テンプレートは、言語ごとに 4 つの個別のファイルを使用します。  
  
### <a name="files"></a>ファイル  
 \Templates\  
  
 EmailTemplates.xml  
  
 EmailDocuments\  
  
 \<LCID 1>\\{guid 1}\  
  
 Body.xsl  
Presentation.xml  
Subject.xsl  
Subjectpresentation.xml  
  
 \<LCID 1>\\{guid n}\  
  
 Body.xsl  
Presentation.xml  
Subject.xsl  
Subjectpresentation.xml  
  
 \<LCID n>\\{guid 1}\  
  
 Body.xsl  
Presentation.xml  
Subject.xsl  
Subjectpresentation.xml  
  
 \<LCID n>\\{guid n}\  
  
 Body.xsl  
Presentation.xml  
Subject.xsl  
Subjectpresentation.xml  
  
<a name="contracttemplate_bm"></a>   
## <a name="contract-template"></a>契約テンプレート   
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
 すべての契約テンプレートのメタデータは、単一のファイルに保存されます。  
  
### <a name="files"></a>ファイル  
 \Templates\ContractTemplates.xml  
  
<a name="kbarticle_bm"></a>   
## <a name="kb-article-template"></a>サポート技術情報の記事のテンプレート  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
  
1.  すべての契約テンプレートのメタデータは、単一のファイルに保存されます。  
  
2.  各契約テンプレートは、言語ごとに 2 つの個別のファイルを使用します。  
  
### <a name="files"></a>ファイル  
 \Templates\  
  
 KBArticleTemplates.xml  
  
 KBArticleTemplates\  
  
 \<LCID 1>\\{guid 1}\  
  
 formatxml.xsl  
Structurexml.xml  
  
 \<LCID 1>\\{guid n}\  
  
 formatxml.xsl  
Structurexml.xml  
  
 \<LCID n>\\{guid 1}\  
  
 formatxml.xsl  
Structurexml.xml  
  
 \<LCID n>\\{guid n}\  
  
 formatxml.xsl  
Structurexml.xml  
  
<a name="mailmerge_bm"></a>   
## <a name="mail-merge-template"></a>差し込み印刷テンプレート  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
  
1.  すべての差し込み印刷テンプレートのメタデータは、単一のファイルに保存されます。  
  
2.  各差し込み印刷テンプレートは、言語ごとに 2 つの個別のファイルを使用します。  
  
3.  複数のテンプレートで共有されているドキュメントは、単一の個別のファイルに保存されます。  
  
### <a name="files"></a>ファイル  
 \Templates\  
  
 MailMergeTemplates.xml  
  
 MailMergeDocuments\  
  
 \<LCID 1>\\{guid 1}\\<document name 1>.xml  
\<LCID 1>\\{guid n}\\<document name n\>.xml  
\<LCID n>\\{guid 1}\\<document name 1>.xml  
\<LCID n>\\{guid n}\\<document name n\>.xml  
  
<a name="pluginassembly_bm"></a>   
## <a name="pluginassembly"></a>PluginAssembly  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
  
1.  各プラグインアセンブリには、生のアセンブリバイトの個別のファイルがあります。  
  
2.  プラグイン アセンブリのメタデータは、末尾が .data.xml と類似のファイル名で保存されます。  
  
3.  生アセンブリをソースコントロールに含めることはお勧めしません。  
  
### <a name="files"></a>ファイル  
 \PluginAssemblies\  
  
 \<アセンブリ名 1>-{guid 1}\  
  
 \<Assembly Name 1>.dll  
\<Assembly Name 1>.dll.data.xml  
  
 \<Assembly Name n>-{guid n}\  
  
 \<Assembly Name n>.dll  
\<Assembly Name n>.dll.data.xml  
  
<a name="step_bm"></a>   
## <a name="sdkmessageprocessingstep"></a>SdkMessageProcessingStep  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
 各 SDK メッセージ処理ステップは、個別のファイルに保存されます。  
  
### <a name="files"></a>ファイル  
 \SdkMessageProcessingSteps\  
  
 {guid 1}.xml  
{guid n}.xml  
  
<a name="serviceendpoint_bm"></a>   
## <a name="serviceendpoint"></a>ServiceEndpoint  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
 すべてのサービス エンド ポイントのメタデータは、1 つのファイルにまとめて保存されます。  
  
### <a name="files"></a>ファイル  
 \PluginAssemblies\ServiceEndpoints.xml  
  
<a name="reports_bm"></a>   
## <a name="reports"></a>レポート   
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
  
1.  レポートは言語ごとに個別のサブフォルダーに保存されます。  
  
2.  各レポートには、そのフォルダー内に別個のファイルがあります。  
  
3.  各レポートのメタデータは、末尾が .data.xml と類似のファイル名で保存されます。  
  
### <a name="files"></a>ファイル  
 \Reports\  
  
 ReportSignatureIdMappings.xml  
  
 ReportLinks.xml  
  
 \<LCID 1>\\{guid 1}\  
  
 \<Report Name 1>.rdl  
\<Report Name 1>.rdl.data.xml  
  
 \<LCID 1>\\{guid n}\  
  
 \<Report Name n>.rdl  
\<Report Name n>.rdl.data.xml  
  
 \<LCID n>\\{guid 1}\  
  
 \<Report Name 1>.rdl  
\<Report Name 1>.rdl.data.xml  
  
 \<LCID n>\\{guid n}\  
  
 \<Report Name n>.rdl  
\<Report Name n>.rdl.data.xml  
  
<a name="entitymap_bm"></a>   
## <a name="entitymap"></a>EntityMap  
 管理ソリューションでは異なります: いいえ  
  
### <a name="notes"></a>メモ​​  
 すべてのエンティティ マップは単一のファイルに保存されます。  
  
### <a name="files"></a>ファイル  
 \Other\EntityMaps.xml  
  
### <a name="see-also"></a>関連項目  
 [SolutionPackager ツールを使用したソリューション ファイルの圧縮および展開](compress-extract-solution-file-solutionpackager.md)   
