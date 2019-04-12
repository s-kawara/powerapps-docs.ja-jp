---
title: インポート用データ マップの作成 (Common Data Service) | Microsoft Docs
description: データ マップはデータのインポートに必要で、ソース ファイルに含まれるデータとそれぞれのエンティティ属性間のマッピングが含まれます。
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
# <a name="create-data-maps-for-import"></a>インポート用データ マップの作成

Common Data Service にデータをインポートするには、適切なデータ マップを指定する必要があります。  
  
 データ マップの例を、 [Microsoft ダウンロード: DataImportMaps.zip](http://download.microsoft.com/download/D/5/F/D5F73E15-439B-4EBC-BFFB-C6837B146C76/DataImportMaps.zip)からダウンロードできます。
  
 データ マップを使用してソース ファイルに含まれるデータを Common Data Service のエンティティ属性にマップします。 ソース ファイルのすべての列を適切な属性にマップする必要があります。 マップされていない列のデータは、データ インポートの操作中にインポートされません。  
  
 データ マップは、インポート マップ (データ マップ) エンティティによって表されます。 <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> メッセージを使用して新しいマップを作成したり、<xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>  メソッドを使用して既存のマップを更新したりすることができます。 マップには一意の名前があります。この名前は、`ImportMap.Name` 属性に格納されています。 このデータ マップが作成されるインポート ソースの名前は、`ImportMap.Source` 属性を使用して指定できます。  
  
<a name="BKMK_Column"></a>   
## <a name="column-list-value-and-lookup-mappings"></a>列、リスト値、検索マッピング  
 ソース ファイルの列、リスト値、または検索値を Common Data Service の属性にマップするには、次のマッピングを使用します:  
  
 **列マッピング**  
  
 ソース ファイルの列を Common Data Service のエンティティ属性にマップします。 列マッピングの場合は、列マッピング (`ColumnMapping`) エンティティを使用します。 ソース属性とターゲット属性との間には、1:1 (1 対 1) または 1:N (1 対多) の関連付けを使用することができます。 たとえば、取引先企業の住所情報を、受注の請求先住所と送付先住所にマップできます。  
  
 **リスト値マッピング**  
  
 ソース ファイルのリスト値を、<xref:Microsoft.Xrm.Sdk.OptionSetValue> 型の Common Data Service 属性にマップします。 リスト値マッピングの場合は、候補リスト マッピング (`PicklistMapping`) エンティティを使用します。  
  
 ソース ファイルの列で指定された値が OptionSetValue、Status、State、Boolean などのリスト値である場合は、列マッピングの他に、リスト値マッピングを指定する必要があります。 たとえば、ソース ファイルに含まれている "請求先" および "送付先" のリスト値を、<xref:Microsoft.Xrm.Sdk.OptionSetValue> 型の送付先および請求先の値にマップします。  
  
 **検索マッピング**  
  
 ソース ファイルの検索値を、<xref:Microsoft.Xrm.Sdk.EntityReference> 型の Common Data Service 属性にマップします。 検索マッピングの場合は、検索マッピング (`LookupMapping`) エンティティを使用します。  
  
 ソース ファイルで指定された値がエンティティを参照している場合は、この値に対して検索マッピングを指定する必要があります。 参照されているエンティティをソース ファイル内または Common Data Service 内のどちらで検索するかを指定するには、`LookupMapping.LookupSourceCode` 属性を使用します。 事前バインド型を使用している場合は、`LookupSourceType` 列挙体を使用して検索値を設定できます。 ソース ファイル内を検索するには、値 `LookupSourceType.Source` を使用します。 Common Data Service 内を検索するには `LookupSourceType.System` 値を使用します。 LookupSourceCode値の一覧については、エンティティの候補リスト値を参照してください。 組織のエンティティ メタデータを表示するには、メタデータ ブラウザー ソリューションをインストールしてください。メタデータ ブラウザー ソリューションについては、「[組織のメタデータの参照](/dynamics365/customer-engagement/developer/browse-your-metadata)」を参照してください。 「[エンティティ参照](reference/about-entity-reference.md)」でエンティティの参照ドキュメントを参照することもできます。 複数の検索マッピングを指定できます。 非同期の変換ジョブでは、有効なすべてのマッピングが処理されます。 このジョブでは、参照されているレコードが検索されて、レコードの一意の識別子で解析テーブルが更新されます。 詳細については、「[データインポートの実行](run-data-import.md)」を参照してください。  
  
<a name="BKMK_Owner"></a>   
## <a name="owner-mapping"></a>所有者マッピング  
 ソース ファイルで指定されたユーザーを Common Data Service のユーザーにマップするには所有者マッピングを使用します。 ログ情報には Common Data Service ユーザーのログオン名を使用します。 所有者マッピングの場合は、所有者マッピング (`OwnerMapping`) エンティティを使用します。  
  
<a name="BKMK_Notes"></a>   
## <a name="notes-and-attachments"></a>メモおよび添付ファイル  
 メモおよび添付ファイルのマッピングは、他のエンティティとは異なる方法で処理されます。 メモおよび添付ファイルは、情報を Common Data Service のレコードに追加する場合に使用します。 メモはテキストとして、また添付ファイルはファイルとして、Common Data Service データベースに格納されます。  
  
 Common Data Service でメモを作成するには、コメント (メモ) エンティティの `Annotation.IsDocument` 属性を `false` に設定します。 添付ファイルを作成するには、`IsDocument` を `true` に設定します。  
  
 メモおよび添付ファイルをマップするには、次の設定を使用します。  
  
- `ColumnMapping.SourceAttributeName` 属性を “`true`” または “`false`” に設定します。 “`true`” 値 は添付ファイルを示します。 “`false`” 値はメモを示します。  
  
- `ColumnMapping.TargetAttributeName` 属性を `IsDocument` に設定します。  
  
- 事前バインド型を使用する場合は、`ColumnMapping.ProcessCode` 属性を `ImportProcessCode.Internal` 列挙体の `ImportProcessCode` 値に設定します。 ProcessCode値の一覧については、エンティティの候補リスト値を参照してください。  
  
  ソース データがメモを表す場合は、メモのテキストを `Annotation.NoteText` 属性にマップします。 Salesforce ファイルで作業している場合、これらのファイルは、通常、ディスクの一意の ID 番号の下に格納されます。 添付ファイルをインポートするには、ソース ファイルに含まれているファイルの ID 番号を `Annotation.DocumentBody` 属性にマップする必要があります。 `DocumentBody` 属性には、添付ファイルの内容が格納されます。  
  
  インポート非同期ジョブでは、ソース属性名が “`true`” および “`false`” に設定されているマッピングが確認され、メモと添付ファイルが検出されます。 添付ファイルのマッピングが見つかった場合、ディスク上の指定されたファイルが検索され、ファイルの内容が添付ファイルとして Common Data Service にアップロードされます。 ファイルが見つからない場合、エラーが返されます。  
  
  コメント (メモ) エンティティにマッピングを行わない場合は、インポート ジョブによってメモに既定のマッピングが生成されます。  
  
> [!NOTE]
> アップロードできる最大ファイル サイズは、**Organization.MaxUploadFileSize** プロパティによって決まります。 このプロパティは Common Data Service アプリケーションの **システム設定** の **電子メール** タブで設定します。 この設定で電子メール メッセージ、メモ、および Web リソースに添付できるファイルのサイズを制限します。 既定の設定は 5 MB です。 ただし、添付ファイルのサイズが、HTTP 要求サイズの最大値 (既定では 16MB) を超えてはいけません。 変更を有効にするには、インターネット インフォメーション サービスをリセットします。 この操作を行うには、**スタート**、**ファイル名を指定して実行**の順にクリックし、「`iisreset`」を入力して、**OK** をクリックします。  
  
<a name="BKMK_ImportExport"></a>   
## <a name="import-and-export-data-maps"></a>データ マップのインポートとエクスポート  
 既存のデータ マップを XML ファイルにエクスポートでき、XML のデータ マッピングを Common Data Service にインポートできます。 データ マップを Common Data Service からエクスポートするには <xref:Microsoft.Crm.Sdk.Messages.ExportMappingsImportMapRequest> メッセージを使用します。 XML のデータ マッピングをインポートして Common Data Service にデータ マップを作成するには、<xref:Microsoft.Crm.Sdk.Messages.ImportMappingsImportMapRequest> メッセージを使用します。  
  
### <a name="see-also"></a>関連項目

[データのインポート](import-data.md)<br />
[ソース ファイルのインポートを準備する](prepare-source-files-import.md)<br />
[インポート用の変換マッピングの追加](add-transformation-mappings-import.md)<br />
[データ インポートの構成](configure-data-import.md)<br />
[データ インポートの実行](run-data-import.md)<br />
[データ インポート エンティティ](data-import-entities.md)<br />
[サンプル: データ マップのエクスポートおよびインポート](org-service/samples/export-import-data-map.md)<br />
[サンプル: 複雑なデータ マップを使用してデータをインポートする](org-service/samples/import-data-complex-data-map.md)<br />