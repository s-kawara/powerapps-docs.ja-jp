---
title: データ インポートの構成 (アプリ用 Common Data Service) | Microsoft Docs
description: データ インポートの構成に必要な構成情報は、データ インポート エンティティとインポート ソース ファイル エンティティに格納されます。
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
# <a name="configure-data-import"></a>データ インポートの構成

<!-- 
Was Mike Carter's

https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/configure-data-import 

Child topic of 
powerapps-docs/developer/common-data-service/import-data.md
-->

データ インポートの実行に必要な構成情報は、データ インポート (`Import`) エンティティとインポート ソース ファイル (`ImportFile`) エンティティに格納されます。  
  
 データ インポートを構成するには、次の手順を実行します。  
  
- `Import.ModeCode` 属性を使用して、インポート中にデータを作成するか更新するかを指定します。 事前バインド型を使用している場合は、`ImportModeCode` 列挙体を使用できます。 ModeCode値の一覧については、エンティティの候補リスト値を参照してください。 組織のエンティティ メタデータを表示するには、メタデータ ブラウザー ソリューションをインストールしてください。メタデータ ブラウザー ソリューションについては、「[組織のメタデータの参照](/dynamics365/customer-engagement/developer/browse-your-metadata)」を参照してください。 「[エンティティ参照](/dynamics365/customer-engagement/developer/about-entity-reference)」でエンティティの参照ドキュメントを参照することもできます。  
  
- `ImportFile.FileTypeCode` 属性を使用して、インポート ファイルの種類を指定します。 事前バインド型を使用している場合は、`ImportFileType` 列挙体を使用できます。 FileTypeCode値の一覧については、エンティティの候補リスト値を参照してください。  
  
- `ImportFile.DataDelimiterCode` 属性を使用して、インポート ファイルの 1 文字のデータ区切り文字を指定します。 事前バインド型を使用している場合は、`ImportDataDelimiter` 列挙体を使用できます。 ImportDataDelimiter値の一覧については、エンティティの候補リスト値を参照してください。  
  
- `ImportFile.FieldDelimiterCode` 属性を使用して、インポート ファイルの 1 文字のフィールド区切り文字を指定します。 事前バインド型を使用している場合は、`ImportFieldDelimiter` 列挙体を使用できます。 FieldDelimiterCode値の一覧については、エンティティの候補リスト値を参照してください。  
  
- `ImportFile.IsFirstRowHeader` を `true` に設定してソース ファイルの 1 行目に列見出しを含めるか、`false` に設定して 1 行目に実際のデータを含めます。 `false` に設定すると、既定の列見出しが生成されます。  
  
- `ImportFile.ImportId` を、インポート ファイルが関連付けられているインポート (データ インポート) の ID に設定します。  
  
- `ImportFile.ImportMapId` を、関連付けられているインポート マップ (データ マップ) の ID に設定します。  
  
- `ImportFile.EnableDuplicateDetection` を `true` に設定して、データ インポート中の重複の検出を有効にします。  
  
- ソース ファイルの内容を `ImportFile.Content` に読み込みます。  
  
> [!IMPORTANT]
>  プログラムでのデータ インポートを使用してレコードを更新することはお勧めしません。 それを更新するには、アプリ用 CDS Web アプリケーションのデータのエクスポートおよびインポートの機能を使用してください。 **Excel にエクスポート**を使用して、レコードを XML Spreadsheet 2003 (.xml) ファイルにエクスポートします。 これは更新モードで有効な唯一のソース ファイルの種類です。 データを XML Spreadsheet 2003 (.xml) ソース ファイルから再インポートすると、アプリ用 CDS のデータ整合性が保持されます。 更新されたデータをインポートするには、アプリ用 CDS データ インポート ウィザードを使用します。 データ インポート ウィザードの詳細については、アプリ用 CDS ヘルプを参照してください。  
 
### <a name="see-also"></a>関連項目

[データのインポート](import-data.md)<br />
[ブログの投稿: 添付をプログラムでインポートする方法](http://blogs.msdn.com/b/crm/archive/2012/08/06/how-to-import-attachments-programmatically.aspx)<br />
[ソース ファイルのインポートを準備する](prepare-source-files-import.md)<br />
[インポート用データ マップの作成](create-data-maps-for-import.md)<br />
[インポート用の変換マッピングの追加](add-transformation-mappings-import.md)<br />
[データ インポートの実行](run-data-import.md)<br />
[データ インポート エンティティ](data-import-entities.md)<br />
[サンプル: データ マップのエクスポートおよびインポート](org-service/samples/export-import-data-map.md)<br />
[サンプル: 複雑なデータ マップを使用してデータをインポートする](org-service/samples/import-data-complex-data-map.md)<br />