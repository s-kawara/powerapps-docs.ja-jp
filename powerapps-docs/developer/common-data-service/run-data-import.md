---
title: データ インポートの実行 (Common Data Service for Apps) | Microsoft Docs
description: データ インポートは、Dynamics 365 Server 上で直接実行され、解析、マップ ガイド付き変換、およびアップロードのための 3 つの非同期ジョブを必要とします。
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
# <a name="run-data-import"></a>データ インポートの実行

データ インポートは、Common Data Service for Apps サーバーで直接実行されます。 データ インポートを実行するには、次の内容を実行する非同期ジョブが、次の順序でバックグラウンド実行されるように設定します。  
  
- インポート ファイルに含まれているソース データを解析します。  
  
- データ マップを使用して、解析されたデータを変換します。  
  
- 変換されたデータを CDS for Apps にアップロードします。  
  
  適切なアクセス許可を持つすべての CDS for Apps ユーザーが、データ インポートを実行できます。  
  
<a name="parse"></a>   
## <a name="parse-source-data"></a>ソース データを解析する  
 ソース データの解析時には、特定のインポート (データ インポート) に関連付けられたすべてのインポート ファイルが解析されます。  
  
 解析されたデータは、インポート ファイルごとに作成される解析テーブルに一時的に格納されます。 解析テーブルの名前は、`ImportFile.ParsedTableName` 属性に格納されます。 ソース ファイルの列見出しは、`ImportFile.HeaderRow` 見出しで指定されます。 ソース ファイルに列見出しを含んだ先頭行が存在しなかった場合、この属性により、システムによって生成された既定の列見出しが指定されます。  
  
 解析されたデータを解析テーブルに保存するには、<xref:Microsoft.Crm.Sdk.Messages.ParseImportRequest> メッセージを使用します。 解析テーブルからデータを取得するには、<xref:Microsoft.Crm.Sdk.Messages.GetDistinctValuesImportFileRequest> メッセージおよび <xref:Microsoft.Crm.Sdk.Messages.RetrieveParsedDataImportFileRequest> メッセージを使用します。  
  
 次の表は、インポート ファイルを解析し、解析されたデータを解析テーブルから取得するために使用できるメッセージの一覧です。  
  
|メッセージ|説明|  
|-------------|-----------------|  
|<xref:Microsoft.Crm.Sdk.Messages.ParseImportRequest>|指定されたインポート (データ インポート) に関連付けられたすべてのインポート ファイルを解析する非同期ジョブを送信します。 要求の <xref:Microsoft.Crm.Sdk.Messages.ParseImportRequest.ImportId> プロパティの関連付けられたインポート (データ インポート) の ID を渡します。 バックグラウンドで実行され、データの解析を行う非同期ジョブの ID が、メッセージ応答の <xref:Microsoft.Crm.Sdk.Messages.ParseImportResponse.AsyncOperationId> プロパティに返されます。|  
|<xref:Microsoft.Crm.Sdk.Messages.GetDistinctValuesImportFileRequest>|リスト値を収めたソース ファイルにある列の個別の値を返します。 要求の <xref:Microsoft.Crm.Sdk.Messages.GetHeaderColumnsImportFileRequest.ImportFileId> プロパティの関連付けられたインポート ファイル の ID を渡します。 個別の値が、メッセージ応答の <xref:Microsoft.Crm.Sdk.Messages.GetDistinctValuesImportFileResponse.Values> プロパティに、文字列の配列で返されます。 このメッセージは、<xref:Microsoft.Crm.Sdk.Messages.ParseImportRequest> メッセージを使用して解析テーブルを作成した後でのみ使用します。 **重要:** <xref:Microsoft.Crm.Sdk.Messages.ImportRecordsImportRequest> メッセージを使用した後は、このメッセージを使用しないでください。 <xref:Microsoft.Crm.Sdk.Messages.ImportRecordsImportRequest> メッセージで送信されたインポート ジョブの実行の完了後は、解析テーブルにアクセスできません。|  
|<xref:Microsoft.Crm.Sdk.Messages.RetrieveParsedDataImportFileRequest>|解析テーブルからデータを取得します。 要求の <xref:Microsoft.Crm.Sdk.Messages.RetrieveParsedDataImportFileRequest.ImportFileId> プロパティの関連付けられたインポート ファイル の ID を渡します。 解析されたデータが、メッセージ応答の <xref:Microsoft.Crm.Sdk.Messages.RetrieveParsedDataImportFileResponse.Values> プロパティに、2 次元配列の文字列で返されます。 データは、ソース ファイルと同じ列順で返されます。 このメッセージは、<xref:Microsoft.Crm.Sdk.Messages.ParseImportRequest> メッセージを使用して解析テーブルを作成した後でのみ使用します。 **重要:** <xref:Microsoft.Crm.Sdk.Messages.ImportRecordsImportRequest> メッセージを使用した後は、このメッセージを使用しないでください。 `ImportRecordsMessage` メッセージで送信されたインポート ジョブの実行の完了後は、解析テーブルにアクセスできません。|  
  
<a name="transform"></a>   
## <a name="transform-parsed-data"></a>解析されたデータを変換する  
 データの変換は、特定のインポート (データ インポート) に関連付けられている使用可能なすべてのデータ マッピングおよび変換を、解析されたデータに適用して行われます。  
  
 <xref:Microsoft.Crm.Sdk.Messages.TransformImportRequest> メッセージは、非同期ジョブを送信して、解析されたデータを変換する場合に使用します。 要求の `Import.ImportId` 属性の関連付けられたインポート (データ インポート) の一意の識別子を渡します。 バックグラウンドで実行され、変換を行う非同期ジョブの一意の識別子が、メッセージ応答の <xref:Microsoft.Crm.Sdk.Messages.TransformImportResponse.AsyncOperationId> プロパティに返されます。  
  
<a name="upload"></a>   
## <a name="upload-transformed-data-to-the-target-server"></a>変換されたデータを対象サーバーへアップロードする  
 変換が正常に完了したら、CDS for Apps サーバーにデータをアップロードすることができます。  
  
 <xref:Microsoft.Crm.Sdk.Messages.ImportRecordsImportRequest> メッセージは、非同期ジョブを送信して、変換されたデータを CDS for Apps にアップロードする場合に使用します。 関連付けられたインポート (データ インポート) の一意の識別子は、要求の <xref:Microsoft.Crm.Sdk.Messages.ImportRecordsImportRequest.ImportId> プロパティで指定する必要があります。 バックグラウンドで実行され、CDS for Apps にデータをアップロードする非同期ジョブの一意の識別子が、メッセージ応答の <xref:Microsoft.Crm.Sdk.Messages.ImportRecordsImportResponse.AsyncOperationId> プロパティに返されます。 指定されたインポート (データ インポート) に関連付けられているすべてのインポート ファイルがインポートされます。  
  
 各インポート ジョブには、作成するレコードの `ImportSequenceNumber` 属性に格納される一意のシーケンス番号があります。 `Organization.CurrentImportSequenceNumber` 属性には、システムで最後に実行されたインポート ジョブの一意のシーケンス番号が含まれています。 これらの一意のシーケンス番号を使用して、インポート ジョブに属するレコードを追跡できます。  
  
<a name="log"></a>   
## <a name="log-failures"></a>エラー ログ  
 レコードのインポート エラーは、データの解析、変換、アップロード中などに発生します。 エラーの理由や、インポートに失敗したレコードに関するその他の詳細情報は、インポート ログ (ImportLog) エンティティに取り込まれます。  
  
 インポートに失敗したレコード数を確認するには、レコードの `ImportFile.FailureCount` 属性を取得します。 インポート時に部分的なエラーが発生したレコード数を確認するには、`ImportData.HasError` 属性を取得します。 `HasError` 属性が `true` の場合、部分的なエラーが発生しています。`false` の場合は、レコードのインポートが正常に行われています。  
  
<a name="import_audit"></a>   
## <a name="import-auditing-data"></a>監査データをインポートする  
 CDS for Apps のエンティティには、レコードが作成された日時と最後に変更された日時、および作成者と変更者の追跡に使用される既定の属性が 4 つあります。  
  
 `createdon` 属性は、レコードが作成された日時を指定します。 `createdon` 属性にデータをインポートするには、このデータを含むソース列を `overriddencreatedon` 属性にマップします。 インポートの際、レコードの `createdon` 属性は、`overriddencreatedon` 属性にマップされた値で更新され、`overriddencreatedon` 属性は、データがインポートされた日時に設定されます。 `overriddencreatedon` 属性にマップされているソース値がない場合、`createdon` 属性はデータがインポートされた日時に設定され、`overriddencreatedon` 属性には値が設定されません。  
  
> [!NOTE]
>  インポート中に `createdon` 属性の値を上書きするには、`prvOverrideCreatedOnCreatedBy` 権限が必要です。 この権限名は、インポート中に `createdby` 属性も上書きできることを意味します。 ただし、この機能は現在はサポートされていません。  
  
 `modifiedon` 属性、`createdby` 属性、および `modifiedby` 属性にデータをインポートすることはできません。 データを作成したユーザー、およびデータが変更された日時に関するデータを格納する必要がある場合は、CDS for Apps にユーザー定義属性を作成して、ソース列を新しいユーザー定義属性にマップします。  
  
### <a name="see-also"></a>関連項目

[データのインポート](import-data.md)<br />
[ソース ファイルのインポートを準備する](prepare-source-files-import.md)<br />
[インポート用データ マップの作成](create-data-maps-for-import.md)<br />
[インポート用の変換マッピングの追加](add-transformation-mappings-import.md)<br />
[データ インポートの構成](configure-data-import.md)<br />
[データ インポート エンティティ](data-import-entities.md)<br />
[サンプル: データ マップのエクスポートおよびインポート](org-service/samples/export-import-data-map.md)<br />
[サンプル: 複雑なデータ マップを使用してデータをインポートする](org-service/samples/import-data-complex-data-map.md)<br />
[ブログの投稿: 添付をプログラムでインポートする方法](http://blogs.msdn.com/b/crm/archive/2012/08/06/how-to-import-attachments-programmatically.aspx) 