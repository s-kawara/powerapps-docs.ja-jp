---
title: データのインポート (Common Data Service) | Microsoft Docs
description: Common Data Service にデータをインポートする場合は、*データのインポート*機能を使用できます。 "データ インポート" を使用して、さまざまな顧客関係管理システムやデータ ソースから Common Data Service にデータをアップロードできます。
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
# <a name="import-data"></a>データのインポート

<!--
Was Mike Carter


https://docs.microsoft.com/dynamics365/customer-engagement/developer/import-data



This should be the generic high-level content to support either web api or org service

Should there be a separate topic for organization service and Web API?
All these functions & actions exist:

RetrieveParsedDataImportFile Function
https://docs.microsoft.com/dynamics365/customer-engagement/web-api/retrieveparseddataimportfile?view=dynamics-ce-odata-9
GetDistinctValuesImportFile Function
https://docs.microsoft.com/dynamics365/customer-engagement/web-api/getdistinctvaluesimportfile?view=dynamics-ce-odata-9
ParseImport Function
https://docs.microsoft.com/dynamics365/customer-engagement/web-api/parseimport?view=dynamics-ce-odata-9
TransformImport Action
https://docs.microsoft.com/dynamics365/customer-engagement/web-api/transformimport?view=dynamics-ce-odata-9
ImportRecordsImport Action
https://docs.microsoft.com/dynamics365/customer-engagement/web-api/importrecordsimport?view=dynamics-ce-odata-9
ExportMappingsImportMap Action
https://docs.microsoft.com/dynamics365/customer-engagement/web-api/exportmappingsimportmap?view=dynamics-ce-odata-9
ImportMappingsImportMap Action
https://docs.microsoft.com/dynamics365/customer-engagement/web-api/importmappingsimportmap?view=dynamics-ce-odata-9

Or should the core general content simply include both?

-->
Common Data Service にデータをインポートする場合は、*データのインポート*機能を使用できます。 "データ インポート" を使用して、さまざまな顧客関係管理システムやデータ ソースから Common Data Service にデータをアップロードできます。 ほとんどのビジネスおよびユーザー定義エンティティの標準属性やカスタム属性にデータをインポートできます。 メモや添付ファイルなどの関連データを含めることもできます。  
  
Common Data Service には、データ インポート ウィザードと呼ばれる Web アプリケーションが含まれています。 このツールを使用して、データ レコードを 1 つ以上のコンマ区切り値 (.csv) ファイル、XML Spreadsheet 2003 (.xml) ファイル、またはテキスト ファイルからインポートできます。  
  
 データ インポート ウィザードの詳細については Common Data Service のヘルプを参照してください。  
  
 Common Data Service の Web サービスには、データ インポート ウィザードで利用できない以下の追加機能が用意されています。  
  
- 連結、分割、置換などの、複雑な変換マッピングを含むデータ マップを作成する。  
  
- カスタム変換マッピングを定義する。  
  
- 一時解析テーブル内のソース データを表示する。  
  
- エラー ログにアクセスしてカスタム エラー レポート ツールを構築し、エラー ログの表示を改善する。  
  
- コマンド ライン スクリプトからデータ インポートを実行する。  
  
- `LookupMap` XML タグをデータ マップに追加して、インポートに使用するソース ファイル上でデータ検索の開始と実行を指示する。  
  
- カスタム `OwnerMetadata` タグをデータ マップに追加して、ソース ファイル内のユーザー レコードと Common Data Service 内のユーザー (システム ユーザー) のレコードを突き合わせる。  
  
- オプションの検証チェックを使用する。  
  
  > [!NOTE]
  >  データ インポート ウィザードでは、検証はオプションではありません。  
  
  データ インポートを実装するには、一般に以下の操作を行います。  
  
- コンマ区切り値 (CSV) ファイル、XML Spreadsheet 2003 (XMLSS) ファイル、またはテキスト ファイルを作成する。  
  
- データ マップを作成するか、既存のデータ マップを使用する。  
  
- インポート ファイルとデータ マップを関連付ける。  
  
- ソース ファイルからコンテンツを対応するインポート ファイルにアップロードする。  
  
- インポート ファイルを解析する。  
  
- 解析したデータを変換する。  
  
- 変換したデータをターゲットの Common Data Service サーバーにアップロードする。  
  
  データを 1 つのソース ファイルまたは複数のソース ファイルからインポートできます。 ソース ファイル内のデータは、エンティティの種類が 1 つでも複数でもかまいません。  
  
  データの解析、変換、アップロードは、バックグラウンドで動作する非同期ジョブによって実行されます。  
  
> [!NOTE]
>  既定では、すべてのユーザー定義エンティティがインポートに対応しています。 ビジネス エンティティがインポートに対応しているかどうかを確認するには、特定のエンティティのエンティティ メタデータを参照してください。 エンティティがインポートに対応している場合は、エンティティ メタデータ プロパティの `IsImportable` が `true` に設定されています。 標準的なビジネス エンティティに対しては、このプロパティの値を変更できません。 <!--[!INCLUDE[metadata_browser](../includes/metadata-browser.md)]-->  


### <a name="see-also"></a>関連項目

[ソース ファイルのインポートを準備する](prepare-source-files-import.md)<br />
[インポート用データ マップの作成](create-data-maps-for-import.md)<br />
[インポート用の変換マッピングの追加](add-transformation-mappings-import.md)<br />
[データ インポートの構成](configure-data-import.md)<br />
[データ インポートの実行](run-data-import.md)<br />
[データ インポート エンティティ](data-import-entities.md)<br />
[サンプル: データ マップのエクスポートおよびインポート](org-service/samples/export-import-data-map.md)<br />
[サンプル: 複雑なデータ マップを使用してデータをインポートする](org-service/samples/import-data-complex-data-map.md)<br />
