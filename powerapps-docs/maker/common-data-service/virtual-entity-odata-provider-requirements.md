---
title: Common Data Service で仮想エンティティ OData v4 データ プロバイダーを使用する| MicrosoftDocs
ms.custom: ''
ms.date: 06/04/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
ms.assetid: null
caps.latest.revision: null
author: Mattp123
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="odata-v4-data-provider-configuration-requirements-and-best-practices"></a>OData v4 データ プロバイダーの構成、要件、ベスト プラクティス

このトピックでは、OData v4 プロバイダーの構成方法、および OData v4 データ プロバイダーを使用して OData v4 Webサービスに接続するための要件と推奨されるベスト プラクティスについて説明します。 

## <a name="odata-v4-data-provider-best-practices"></a>OData v4 データ プロバイダー ベスト プラクティス

- Common Data Service では、すべてのエンティティが ID 属性を持つことが必要になります。この ID は一意の識別子として知られ、値は GUID にする必要があります。  ID フィールドは、`Edm.Guid` データ型の外部フィールドにのみマップできます。  Common Data Service では、`Edm.Int32` データ型を一意の識別子データ型フィールドにマップすることはできません。
-  NULL 値が許容されるプロパティを使用する OData エンティティは、仮想エンティティにマップされたフィールドに一致するよう設定する必要があります。 たとえば、Nullable=False の OData エンティティ プロパティは、 Common Data Service**フィールド要求**属性がマップされたフィールドを**必須項目**に設定する必要があります。 
- グリッドにデータをロードするなど複数のクエリを取得する場合、クエリ パラメーターの選択とフィルターを使用して、外部データ ソースから返されるデータセットのサイズを制御します。
- システム管理者は、既に有効にされていない場合はプラグイン トレースを有効にしてください。 有効にすると、OData エンドポイントからのすべてのエラーがプラグイン トレース ログでキャプチャされます。 詳細情報: [管理者ガイド: [システムの設定] ダイアログ ボックス - [カスタマイズ] タブ](/dynamics365/customer-engagement/admin/system-settings-dialog-box-customization-tab) 

## <a name="data-type-mapping"></a>データの種類のマッピング

次の表は、Common Data Service データ型での OData エンティティ データ モデル (EDM) データ型マッピングの一覧を示しています。 

|OData データ型|Common Data Service データの種類  |
|---------|---------|
|`Edm.Boolean`|2 つのオプション|
|`Edm.DateTime`|日付と時間|
|`Edm.DateTimeOffset`|日付と時間|
|`Edm.Decimal`|少数または通貨|
|`Edm.Double`|浮動小数点数|
|`Edm.Guid`|一意識別子|
|`Edm.Int32`|整数|
|`Edm.Int64`|整数|
|`Edm.String`|単一行のテキストまたは複数行のテキスト|


### <a name="odata-edm-data-types-that-are-not-supported-for-mapping-with-virtual-entities"></a>仮想エンティティのマップをサポートしない OData EDM データ型 

- `Edm.Binary`
- `Edm.Time` 
- `Edm.Float`
- `Edm.Single` 
- `Edm.Int16` 
- `Edm.Byte` 
- `Edm.SByte`

 
## <a name="add-a-data-source-using-the-odata-v4-data-provider"></a>OData v4 データ プロバイダーを使用してデータ ソースを追加する

この手順では、仮想エンティティ データ ソースとして使用する標準の OData データ プロバイダーを使用する方法を示します。   
  
1. **[設定](../model-driven-apps/advanced-navigation.md#settings)** > **管理** > **仮想エンティティのデータ ソース**の順に移動します。  
1. [操作] ツール バーで、**新規**をクリックします。  
1. **データ プロバイダーの選択** ダイアログ ボックスで、次のデータ ソースから選択してから、**OK** をクリックします。  
  
    - **OData v4 データ プロバイダー**。 Common Data Service には、OData v4 オープン標準をサポートするデータ ソースへの接続に使用できる、Odata v4 データ プロバイダーが含まれています。  
    - *カスタム データ プロバイダー*。 データ プロバイダー プラグインをインポートした場合は、データ プロバイダーはここに表示されます。 詳細情報: [開発者ドキュメント: 仮想エンティティに関する入門情報](/dynamics365/customer-engagement/developer/virtual-entities/get-started-ve)  
    
1. **新規データ ソース** プロパティ ページで、以下のフィールドに入力してから、レコードを保存します。  
  
    - **名前**. データ ソースを説明する名前を入力します。  
    - **URI**。 OData データ プロバイダーを使用する場合、OData Web サービスの URI を入力します。 たとえば、OData プロバイダーを使用して Azure でホストされている Web サービスに接続する場合、URI は *`http://contosodataservice.azurewebsites.net/odata/`* のようになります。  
    - **タイムアウト (秒)**。 データ リクエストがタイムアウトする前に Web サービスからの応答を待機する時間を秒数で入力します。たとえば、タイムアウトが発生する前に最大 30 秒待つには、30 を入力します。  
    - **改ページ モード**。 クエリの結果のページングを制御するために、クライアント側またはサーバー側のページングを使用するかどうかを選択します。 既定値は、クライアント側のページングです。 サーバー側のページングでは、クエリ文字列に追加される $skiptoken パラメーターを使用して結果のページングを制御します。 詳細情報: [スキップ トークン システム クエリ オプション ($skiptoken)](https://msdn.microsoft.com/library/dd942121.aspx)  
        -  **インライン カウントを返す**。 結果セットの総レコード数を返します。 この設定は、グリッドにデータを返す際に次のページの機能を有効にするために使用します。 OData エンドポイントが OData $inclinecount パラメーターをサポートしない場合は false の値を使用します。 既定値は false です。
    - **要求パラメーター**。 必要に応じて、外部 Web サービスへの認証パラメーターなど、OData Web サービスへの接続に使用されるユーザー定義の見出しやクエリ文字列パラメーターを追加できます。 **クエリ文字列**をクリックすると、ヘッダーとクエリ文字列パラメーターおよび値との間で切り替わります。 最大 10 個のヘッダーまたはクエリ文字列を追加できます。 
        > [!div class="mx-imgBorder"] 
        > ![仮想エンティティ データ ソース レコード](media/virtual-entity-data-source.png) 


## <a name="see-also"></a>関連項目  

[外部データ ソースからのデータを格納する仮想エンティティの作成および編集](create-edit-virtual-entities.md) <br/>
[TechNet ブログ: 新しい仮想エンティティを使った外部システムからのデータとの対話](https://blogs.technet.microsoft.com/lystavlen/2017/09/08/virtual-entities/)
