---
title: データのインポート エンティティ (Common Data Service) | Microsoft Docs
description: データ マップを作成し、データのインポートを構成して実行し、エラー情報を記録するために使用するデータ インポート エンティティをリスト表示します。
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
# <a name="data-import-entities"></a>データ インポート エンティティ

Common Data Service データ インポート エンティティを使用して、データ マップを作成し、データのインポートを構成して実行し、エラー情報を記録します。  

 以下の表には、インポート操作の構成、実行、およびエラーの記録を行うために使用されるエンティティが一覧表示されます。  

|エンティティ名 (表示名)|説明|  
|----------------------------------|-----------------|  
|インポート (データ インポート)|インポート ジョブの状態と所有者情報。|  
|importfile (インポート ソース ファイル)|論理ソース ファイル。|  
|importlog (インポート ログ)|インポートに失敗したレコードの失敗原因とその他の詳細情報です。|  

 次の表には、データ マップの作成に使用されるエンティティが一覧表示されます。  


|                    エンティティ名 (表示名)                     |                                                                                                                      説明                                                                                                                       |
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                       importmap (データ マップ)                        |                                                                                                           インポートに使用されるデータ マップ。                                                                                                            |
|                  columnmapping (列マッピング)                   |                                                           ソース ファイル内の列と Common Data Service 内のターゲット属性間のマッピング。                                                           |
|                  lookupmapping (検索マッピング)                   |       ソース ファイル内の列 (または複雑な変換の出力) と <xref:Microsoft.Xrm.Sdk.EntityReference> 型のターゲット属性間のマッピング。 列マッピングまたは複雑な変換マッピングと組み合わせて使用されます。        |
|                   ownermapping (所有者マッピング)                    |                                                             ソース ファイルに指定されたユーザーと Common Data Service 内のユーザー間のマッピング。                                                             |
|                picklistmapping (候補リスト マッピング)                 | ソース ファイル内の列と Common Data Service 内の <xref:Microsoft.Xrm.Sdk.OptionSetValue>、ブール値、状態、または状態の種類のターゲット属性間のマッピング。 列マッピングと組み合わせて使用されます。 |
|          transformationmapping (変換マッピング)           |                                                                                                            複雑な変換のマッピング。                                                                                                             |
| transformationparametermapping (変換パラメーター マッピング) |                                                                                           複雑な変換マッピングで使用されるパラメーター マッピング                                                                                            |

### <a name="see-also"></a>関連項目  
 [Dynamics 365 でのデータのインポート](import-data.md)   
 [エンティティのインポート](reference/entities/import.md)   
 [ImportFile エンティティ](reference/entities/importfile.md)   
 [ImportLog エンティティ](reference/entities/importlog.md)   
 [ImportMap エンティティ](reference/entities/importmap.md)   
 <!-- jdaly These links will have content when we re-gen docs after bug 689487 is checked in. START -->
 [ColumnMapping エンティティ](reference/entities/columnmapping.md)   
 [LookupMapping エンティティ](reference/entities/lookupmapping.md)   
 [OwnerMapping エンティティ](reference/entities/ownermapping.md)   
 [PicklistMapping エンティティ](reference/entities/picklistmapping.md)   
 [TransformationMapping エンティティ](reference/entities/transformationmapping.md)    
 [TransformationParameterMapping エンティティ](reference/entities/transformationparametermapping.md)   
 <!-- jdaly These links will have content  when we re-gen docs after bug 689487 is checked in. END -->
 [サンプル: データ マップのエクスポートおよびインポート](/dynamics365/customer-engagement/developer/sample-export-import-data-map)   
 [インポート用データ マップの作成](create-data-maps-for-import.md)<br />
 [インポート用の変換マッピングの追加](add-transformation-mappings-import.md)<br />
 [データ インポートの構成](configure-data-import.md)<br />
 [データ インポートの実行](run-data-import.md)<br />
 [サンプル: データ マップのエクスポートおよびインポート](/dynamics365/customer-engagement/developer/org-service/samples/export-import-data-map)<br />
 [サンプル: 複雑なデータ マップを使用してデータをインポートする](/dynamics365/customer-engagement/developer/org-service/samples/import-data-complex-data-map)<br />