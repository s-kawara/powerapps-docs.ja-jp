---
title: Web API 基本操作のサンプル (Common Data Service) | Microsoft Docs
description: 'このサンプル グループは、 Web API を使用した、CRUD (作成、取得、更新、削除) 操作方法を説明します。 これらは、クライアント側の JavaScript と C# を使用して実装されます'
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: f006f88c-74cb-4fde-90e5-e1faf2051673
caps.latest.revision: 25
author: brandonsimons
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-basic-operations-sample"></a>Web API Operations 操作のサンプル

このサンプル グループは、Common Data Service Web API を使用した、基本的な CRUD (作成、取得、更新、削除) 操作方法や関連した操作方法を説明します。  
  
-   [Web API 基本操作のサンプル (C#)](samples/basic-operations-csharp.md)  
  
 このトピックでは、この各グループに対して実装される共通の一連の操作について説明します。 このトピックでは、このグループの各サンプルが言語固有の詳細な情報なしで実行する HTTP 要求と応答とテキスト出力について説明します。 これらの操作を実行する方法に関する詳細については、言語特有の説明および個別のサンプルを参照してください。  
  
<a name="bkmk_demonstrates"></a>  
 
## <a name="demonstrates"></a>説明  

このサンプルは次のセクションに分かれており、Common Data Service Web API の操作について、指定した関連する概念的なトピックでより詳しく説明されています。  
  
|コード セクション|関連する概念的なトピック|  
|------------------|----------------------------------|  
|[セクション 1: 基本的な操作の作成および更新](#bkmk_section1)|[基本的な作成](create-entity-web-api.md#bkmk_basicCreate) <br /> [返されるデータで作成する](create-entity-web-api.md#bkmk_createWithDataReturned) <br /> [基本的な更新](update-delete-entities-using-web-api.md#bkmk_update) <br /> [返されるデータでの更新](update-delete-entities-using-web-api.md#bkmk_updateWithDataReturned)|  
|[セクション 2: 関連付けを作成します](#bkmk_section2)|[作成時にエンティティを関連付ける](associate-disassociate-entities-using-web-api.md#bkmk_Associateentitiesoncreate)|  
|[セクション 3: 関連エンティティ (ディープ挿入) を作成します](#bkmk_section3)|[1 回の操作で関連するエンティティを作成する](create-entity-web-api.md#bkmk_CreateRelated)|  
|[セクション 4: 既存エンティティの関連付けおよび関連付け解除](#bkmk_section4)|[Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)|  
|[セクション 5: エンティティ (サンプル クリーンアップ) を削除します](#bkmk_section5)|[基本的な削除](update-delete-entities-using-web-api.md#bkmk_delete)|  
  
> [!NOTE]
>  簡潔にするために、関連の少ない HTTP ヘッダーは省略されています。 レコードの URL は、基本の組織アドレスおよび Common Data Service サーバーが割り当てるレコードの ID によって異なります。  
  
<a name="bkmk_section1"></a>
   
## <a name="section-1-basic-create-and-update-operations"></a>セクション 1: 基本的な操作の作成および更新 
 
このセクションでは、1 つの取引先担当者を作成して、そのインスタンスの一連の更新を実行します。 応答ヘッダーの [OData-EntityId](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793637) には、付加的にこのレコードの一意の ID を含む新しく作成されたレコード (エンティティ インスタンス) の URL が含まれることに注意してください。  
  
1.  Peter Cambel という名前の新しい取引先担当者を作成します。  
  
 **要求** 
  
    ```http
    POST http://[Organization URI]/api/data/v9.0/contacts HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    {  
      "firstname": "Peter",  
      "lastname": "Cambel"  
    }  
    ```  
  
 **応答**  
  
    ```http  
    HTTP/1.1 204 No Content  
    OData-Version: 4.0  
    OData-EntityId: http://[Organization URI]/api/data/v9.0/contacts(60f77a42-5f0e-e611-80e0-00155da84c03)  
    ```  
  
 **コンソール出力**  
  
    ```  
    Contact 'Peter Cambel' created.  
    ```  
  
     種類ごとに使用できるプロパティは、メタデータ ドキュメント内に定義され、<xref:Microsoft.Dynamics.CRM.EntityTypeIndex> セクションで種類ごとに文書化もされます。 そのほかの一般的な情報については、[Web API の種類と操作](web-api-types-operations.md) を参照してください。  
  
2.  取引担当者と年収の値 ($80,000) および役職 (Junior Developer) を更新します。  
  
 **要求** 
  
    ```http  
    PATCH http://[Organization URI]/api/data/v9.0/contacts(60f77a42-5f0e-e611-80e0-00155da84c03) HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    {  
      "annualincome": 80000,  
      "jobtitle": "Junior Developer"  
    }  
    ```  
  
 **応答**  
  
    ```http  
    HTTP/1.1 204 No Content  
    ```  
  
 **コンソール出力**  
  
    ```  
    Contact 'Peter Cambel' updated with job title and annual income.  
    ```  
  
3.  明示的に初期化されたプロパティ セットと取引先担当者を取得します。  `fullname` は、インスタンスを作成したときに明示的に初期化された`firstname` および `lastname` プロパティで計算された読み取り専用プロパティです。 一方、`description` プロパティは明示的に初期設定されないので、その既定値である `null` 文字列が保たれます。  
  
     要求された値と一般的なヘッダーに加えて、応答に注意してください。次の種類の追加情報も自動的に返されます。  
  
    -   現在のエンティティの種類の主な ID、`contactid` です。  
  
    -   *ETag* 値は、要求されたリソースの特定のバージョンを識別する `@odata.etag` キーによって示されます。 詳細については、[Web API を使用する条件付き演算を実行](perform-conditional-operations-using-web-api.md) を参照してください。  
  
    -   `@odata.context` キーによって示されるメタデータ コンテキストは、同じクエリから取得した場合、クエリ結果を比較する方法を提供します。  
  
    -   `_transactioncurrencyid_value` は、金銭取引の現地通貨を示します。  
  
 **要求** 
  
    ```http  
    GET http://[Organization URI]/api/data/v9.0/contacts(60f77a42-5f0e-e611-80e0-00155da84c03)?$select=fullname,annualincome,jobtitle,description HTTP/1.1  
    Accept: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    ```  
  
 **応答**  
  
    ```http
    HTTP/1.1 200 OK  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0  
    {   
       "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,annualincome,jobtitle,description)/$entity",  
       "@odata.etag":"W/\"628883\"",  
       "fullname":"Peter Cambel",  
       "annualincome":80000.0000,  
       "jobtitle":"Junior Developer",  
       "description":null,  
       "_transactioncurrencyid_value":"0d4ed62e-95f7-e511-80d1-00155da84c03",  
       "contactid":"60f77a42-5f0e-e611-80e0-00155da84c03"  
    }  
    ```  
  
 **コンソール出力**  
  
    ```http    
    Contact 'Peter Cambel' retrieved:  
            Income: 80000  
            Job title: Junior Developer  
            Description: .    
    ```  
  
    > [!IMPORTANT]
    >  検索操作のパフォーマンスを最適化するには、常に選択とフィルターを使用する必要があります。 詳細については、[Web API を使用するクエリ データ](query-data-web-api.md)」 を参照してください。  
  
4.  これらの同じプロパティで、新しい値を指定して取引先担当者エンティティ インスタンスを更新します。  
  
 **要求** 
  
    ```http
    PATCH http://[Organization URI]/api/data/v9.0/contacts(60f77a42-5f0e-e611-80e0-00155da84c03) HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    {  
      "jobtitle": "Senior Developer",  
      "annualincome": 95000,  
      "description": "Assignment to-be-determined"  
    }    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 204 No Content    
    ```  
  
 **コンソール出力**  
  
    ```http    
    Contact 'Peter Cambel' updated:  
            Job title: Senior Developer  
            Annual income: 95000  
            Description: Assignment to-be-determined    
    ```  
  
    > [!IMPORTANT]
    >  更新要求で変更されたプロパティのみを送信します。 詳細については、[基本更新](update-delete-entities-using-web-api.md#bkmk_update) を参照してください。  
  
5.  単一のプロパティと既定電話番号を明示的に指定します。 これは `PUT` 要求で、個々のプロパティの操作を実行する場合に `value` という名前の JSON キーが使用されるので注意してください。  
  
 **要求** 
  
    ```http  
    PUT http://[Organization URI]/api/data/v9.0/contacts(60f77a42-5f0e-e611-80e0-00155da84c03)/telephone1 HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    {  
      "value": "555-0105"  
    }  
    ```  
  
 **応答**  
  
    ```http  
    HTTP/1.1 204 No Content  
    ```  
  
 **コンソール出力**  
  
    ```  
    Contact 'Peter Cambel' phone number updated.  
    ```  
  
6.  同じ単一のプロパティと既定電話番号を取得します。 もう一度、`value`という名前のキーを使用します。  
  
 **要求** 
  
    ```http  
    GET http://[Organization URI]/api/data/v9.0/contacts(60f77a42-5f0e-e611-80e0-00155da84c03)/telephone1 HTTP/1.1  
    Accept: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 200 OK  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0  
    {   
       "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(60f77a42-5f0e-e611-80e0-00155da84c03)/telephone1",  
       "value":"555-0105"  
    }    
    ```  
  
 **コンソール出力**  
  
    ```  
    Contact's telephone# is: 555-0105.  
    ```  
  
7.  類似している取引先担当者を作成しますが、同じ操作でインスタンス情報も返します。 この後の機能は `Prefer: return=representation` ヘッダーにより有効になります。  
  
 **要求** 
  
    ```http    
    POST http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,annualincome,jobtitle,contactid HTTP/1.1  
    OData-Version: 4.0  
    Content-Type: application/json; charset=utf-8  
    Prefer: return=representation  
    {  
      "firstname": "Peter_Alt",  
      "lastname": "Cambel",  
      "jobtitle": "Junior Developer",  
      "annualincome": 80000,  
      "telephone1": "555-0110"  
    }    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 201 Created  
    Content-Type: application/json; odata.metadata=minimal  
    Preference-Applied: return=representation  
    OData-Version: 4.0  
    {  
      "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts/$entity","@odata.etag":"W/\"758870\"","_transactioncurrencyid_value":"0d4ed62e-95f7-e511-80d1-00155da84c03","annualincome":80000.0000,"contactid":"199250b7-6cbe-e611-80f7-00155da84c08","jobtitle":"Junior Developer","fullname":"Peter_Alt Cambel"  
    }    
    ```  
  
 **コンソール出力**  
  
    ```    
    Contact 'Peter_Alt Cambel' created:  
            Annual income: 80000  
            Job title: Junior Developer  
    Contact URI: http://[Organization URI]/api/data/v9.0/contacts(199250b7-6cbe-e611-80f7-00155da84c08)  
    ```  
  
8.  類似しているこの取引先担当者を更新し、同じ操作でインスタンス情報も返します。 また、この機能は `Prefer: return=representation` ヘッダーにより有効になります。
  
 **要求** 
  
    ```http    
    POST http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,annualincome,jobtitle,contactid HTTP/1.1  
    OData-Version: 4.0  
    Content-Type: application/json; charset=utf-8  
    Prefer: return=representation  
    {  
      "firstname": "Peter_Alt",  
      "lastname": "Cambel",  
      "jobtitle": "Junior Developer",  
      "annualincome": 80000,  
      "telephone1": "555-0110"  
    }    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 201 Created  
    Content-Type: application/json; odata.metadata=minimal  
    Preference-Applied: return=representation  
    OData-Version: 4.0  
    {  
      "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts/$entity","@odata.etag":"W/\"758870\"","_transactioncurrencyid_value":"0d4ed62e-95f7-e511-80d1-00155da84c03","annualincome":80000.0000,"contactid":"199250b7-6cbe-e611-80f7-00155da84c08","jobtitle":"Junior Developer","fullname":"Peter_Alt Cambel"  
    }    
    ```  
  
 **コンソール出力**  
  
    ```    
    Contact 'Peter_Alt Cambel' updated:  
            Annual income: 95000  
            Job title: Senior Developer   
    ```  
  
<a name="bkmk_section2"></a>  
 
## <a name="section-2-create-with-association"></a>セクション 2: 関連付けを作成します 
 
このセクションでは、[`Contoso, Ltd.`] という名の新しい取引先企業インスタンスを作成して、それを [セクション 1](#bkmk_section1) で作成された既存の取引先担当者である [`Peter Cambel`] に関連付けます。  この作成および関連付けは、1 つの POST 操作で実行されます。  
  
1.  Contoso, Ltd のアカウントを作成し、取引先責任者の属性を既存の取引先担当者である Peter Cambel に設定します。  `@odata.bind` コメントは、関連付けが作成され、ここに `primarycontactid` 単一値ナビゲーション プロパティを既存の取引先担当者である Peter Cambel にバインディングしたことを示します。  
  
 **要求** 
  
    ```http  
    POST http://[Organization URI]/api/data/v9.0/accounts HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    {  
      "name": "Contoso Inc",  
      "telephone1": "555-5555",  
      "primarycontactid@odata.bind": "http://[Organization URI]/api/data/v9.0/contacts(60f77a42-5f0e-e611-80e0-00155da84c03)"  
    }    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 204 No Content  
    OData-Version: 4.0  
    OData-EntityId: http://[Organization URI]/api/data/v9.0/accounts(65f77a42-5f0e-e611-80e0-00155da84c03)    
    ```  
  
 **コンソール出力**  
  
    ```  
    Account 'Contoso Inc' created.  
    ```  
  
2.  もう一度 `$expand` と `primarycontactid` 単一値ナビゲーション プロパティを使って、関連する <xref href="Microsoft.Dynamics.CRM.contact?text=contact EntityType" /> レコードにアクセスするために、取引先企業である Contoso, Ltd. の取引先責任者を取得します。  
  
 **要求** 
  
    ```http    
    GET http://[Organization URI]/api/data/v9.0/accounts(65f77a42-5f0e-e611-80e0-00155da84c03)?$select=name,&$expand=primarycontactid($select=fullname,jobtitle,annualincome) HTTP/1.1  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0   
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 200 OK  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0  
    {   
       "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,primarycontactid,primarycontactid(fullname,jobtitle,annualincome))/$entity",  
       "@odata.etag":"W/\"628886\"",  
       "name":"Contoso Inc",  
       "accountid":"65f77a42-5f0e-e611-80e0-00155da84c03",  
       "primarycontactid":{   
          "@odata.etag":"W/\"628885\"",  
          "fullname":"Peter Cambel",  
          "jobtitle":"Senior Developer",  
          "annualincome":95000.0000,  
          "_transactioncurrencyid_value":"0d4ed62e-95f7-e511-80d1-00155da84c03",  
          "contactid":"60f77a42-5f0e-e611-80e0-00155da84c03"  
       }  
    }    
    ```  
  
 **コンソール出力**  
  
    ```    
    Account 'Contoso Inc' has primary contact 'Peter Cambel':  
         Job title: Senior Developer  
         Income: 95000    
    ```  
  
<a name="bkmk_section3"></a>  
 
## <a name="section-3-create-related-entities-deep-insert"></a>セクション 3: 関連エンティティ (ディープ挿入) を作成します  

このセクションでは、1 つの POST 要求でエンティティ インスタンスと関連するエンティティ インスタンスを作成する方法を示します。 このメソッドを使用して、すべてのインスタンスが新しく作成されます。関連付ける既存のインスタンスはありません。 この方法には、2 つの利点があります。 より効率的に複数の簡単な作成および関連付け操作を 1 つの結合した操作に置き換えられます。 またこれは、[アトミック](https://msdn.microsoft.com/library/aa719484\(v=vs.71\).aspx)で、操作全体が成功しすべての関連オブジェクトが作成される場合、または操作が失敗し何も作成されない場合に表示されます。  
  
このセクションでは、取引先責任者である取引先企業および 1 つの要求でその取引先担当者の一連のタスクを作成します。  
  
1.  取引先企業である `Fourth Coffee` と、その取引先責任者である `Susie Curtis` および 1 回の操作で関連する 3 つのタスクを作成します。  単一値 `primarycontactid` ナビゲーション プロパティとコレクション値ナビゲーション プロパティ `Contact_Tasks` を使って、これらの関係をそれぞれ定義することに注意してください。  単一値ナビゲーション プロパティは、オブジェクト値を取得しますが、コレクション値のナビゲーション プロパティは配列値を取得します。  
  
 **要求** 
  
    ```http    
    POST http://[Organization URI]/api/data/v9.0/accounts HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    {  
      "name": "Fourth Coffee",  
      "primarycontactid": {  
        "firstname": "Susie",  
        "lastname": "Curtis",  
        "jobtitle": "Coffee Master",  
        "annualincome": 48000,  
        "Contact_Tasks": [  
          {  
            "subject": "Sign invoice",  
            "description": "Invoice #12321",  
            "scheduledend": "2016-04-19T00:00:00-07:00"  
          },  
          {  
            "subject": "Setup new display",  
            "description": "Theme is - Spring is in the air",  
            "scheduledstart": "2016-04-20T00:00:00-07:00"  
          },  
          {  
            "subject": "Conduct training",  
            "description": "Train team on making our new blended coffee",  
            "scheduledstart": "2016-06-01T00:00:00-07:00"  
          }  
        ]  
      }  
    }    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 204 No Content  
    OData-Version: 4.0  
    OData-EntityId: http://[Organization URI]/api/data/v9.0/accounts(6af77a42-5f0e-e611-80e0-00155da84c03)    
    ```  
  
 **コンソール出力**  
  
    ```  
    Account 'Fourth Coffee' created.  
    ```  
  
2.  選択的に、新しく作成された取引先企業 Fourth Coffee およびその取引先責任者を取得します。  拡張は、単一値ナビゲーション プロパティ `primarycontactid` で行なわれます。  
  
 **要求** 
  
    ```http    
    GET http://[Organization URI]/api/data/v9.0/accounts(6af77a42-5f0e-e611-80e0-00155da84c03)?$select=name,&$expand=primarycontactid($select=fullname,jobtitle,annualincome) HTTP/1.1  
    Accept: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 200 OK  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0   
    {   
       "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,primarycontactid,primarycontactid(fullname,jobtitle,annualincome))/$entity",  
       "@odata.etag":"W/\"628902\"",  
       "name":"Fourth Coffee",  
       "accountid":"6af77a42-5f0e-e611-80e0-00155da84c03",  
       "primarycontactid":{   
          "@odata.etag":"W/\"628892\"",  
          "fullname":"Susie Curtis",  
          "jobtitle":"Coffee Master",  
          "annualincome":48000.0000,  
          "_transactioncurrencyid_value":"0d4ed62e-95f7-e511-80d1-00155da84c03",  
          "contactid":"6bf77a42-5f0e-e611-80e0-00155da84c03"  
       }  
    }    
    ```  
  
 **コンソール出力**  
  
    ```    
    Account 'Fourth Coffee' has primary contact 'Susie Curtis':  
            Job title: Coffee Master  
            Income: 48000    
    ```  
  
3.  選択的に、上記の操作で取得した取引先責任者に関連付けられているタスクを取得します。  拡張は、コレクション値ナビゲーション プロパティ `Contact_Tasks` で行なわれます。  
  
 **要求** 
  
    ```http    
    GET http://[Organization URI]/api/data/v9.0/contacts(6bf77a42-5f0e-e611-80e0-00155da84c03)?$select=fullname,&$expand=Contact_Tasks($select=subject,description,scheduledstart,scheduledend) HTTP/1.1  
    Accept: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 200 OK  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0   
    {   
       "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,Contact_Tasks,Contact_Tasks(subject,description,scheduledstart,scheduledend))/$entity",  
       "@odata.etag":"W/\"628892\"",  
       "fullname":"Susie Curtis",  
       "contactid":"6bf77a42-5f0e-e611-80e0-00155da84c03",  
       "Contact_Tasks":[   
          {   
             "@odata.etag":"W/\"628903\"",  
             "subject":"Sign invoice",  
             "description":"Invoice #12321",  
             "scheduledstart":"2016-04-19T00:00:00Z",  
             "scheduledend":"2016-04-19T00:00:00Z",  
             "activityid":"6cf77a42-5f0e-e611-80e0-00155da84c03"  
          },  
          {   
             "@odata.etag":"W/\"628905\"",  
             "subject":"Setup new display",  
             "description":"Theme is - Spring is in the air",  
             "scheduledstart":"2016-04-20T00:00:00Z",  
             "scheduledend":"2016-04-20T00:00:00Z",  
             "activityid":"6df77a42-5f0e-e611-80e0-00155da84c03"  
          },  
          {   
             "@odata.etag":"W/\"628907\"",  
             "subject":"Conduct training",  
             "description":"Train team on making our new blended coffee",  
             "scheduledstart":"2016-06-01T00:00:00Z",  
             "scheduledend":"2016-06-01T00:00:00Z",  
             "activityid":"6ef77a42-5f0e-e611-80e0-00155da84c03"  
          }  
       ]  
    }    
    ```  
  
 **コンソール出力**  
  
    ```    
    Contact 'Susie Curtis' has the following assigned tasks:  
    Subject: Sign invoice,  
            Description: Invoice #12321  
            Start: 4/19/2016  
            End: 4/19/2016  
  
    Subject: Setup new display,  
            Description: Theme is - Spring is in the air  
            Start: 4/20/2016  
            End: 4/20/2016  
  
    Subject: Conduct training  
            Description: Train team on making our new blended coffee,  
            Start: 6/1/2016  
            End: 6/1/2016    
    ```  
  
<a name="bkmk_section4"></a>
   
## <a name="section-4-associate-and-disassociate-existing-entities"></a>セクション 4: 既存エンティティの関連付けおよび関連付け解除  

このセクションでは、既存のエンティティ インスタンスを関連付けたり関連付けを解除したりする方法を表示します。 関連付けを作成するときは、参照 URI と関係オブジェクトの使用が必要になり、POST 要求に送られます。 関連付け解除には、その関連付けの参照 URI に DELETE 要求を送信する必要があります。  まず、一対多の関連付けが取引先担当者と取引先企業の間で作成されます。  次に、多対多の関連付けが競合企業と 1 つ以上の営業案件との間で作成されます。  
  
1.  `contact_customer_accounts` コレクション値ナビゲーション プロパティを使って、取引先担当者として Peter Cambel を取引先企業 Fourth Coffee に追加します。 特別キー `@odata.id` を使用して、関連レコードを指定します。  
  
 **要求** 
  
    ```http    
    POST http://[Organization URI]/api/data/v9.0/accounts(6af77a42-5f0e-e611-80e0-00155da84c03)/contact_customer_accounts/$ref HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    {  
      "@odata.id": "http://[Organization URI]/api/data/v9.0/contacts(60f77a42-5f0e-e611-80e0-00155da84c03)"  
    }    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 204 No Content    
    ```  
  
 **コンソール出力**  
  
    ```  
    Contact 'Peter Cambel' associated to account 'Fourth Coffee'.  
    ```  
  
2.  取引先企業 Fourth Coffee の取引先担当者のコレクションを取得し、上記の操作を確認します。 応答には、最近割り当てられた取引先担当者 Peter Cambel の単一要素の配列が含まれます。  
  
 **要求** 
  
    ```http    
    GET http://[Organization URI]/api/data/v9.0/accounts(6af77a42-5f0e-e611-80e0-00155da84c03)/contact_customer_accounts?$select=fullname,jobtitle HTTP/1.1  
    Accept: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 200 OK  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0   
    {  
      "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle)","value":[  
        {  
          "@odata.etag":"W/\"632481\"","fullname":"Peter Cambel","jobtitle":"Senior Developer","contactid":"00b6e0e2-b010-e611-80e1-00155da84c03"  
        }  
      ]  
    }    
    ```  
  
 **コンソール出力**  
  
    ```    
    Contact list for account 'Fourth Coffee':  
            Name: Peter Cambel, Job title: Senior Developer    
    ```  
  
3.  取引先企業 Fourth Coffee と取引先担当者 Peter Cambelとの間に作成された関連付けを削除します。  
  
 **要求** 
  
    ```http    
    DELETE http://[Organization URI]/api/data/v9.0/accounts(6af77a42-5f0e-e611-80e0-00155da84c03)/contact_customer_accounts/$ref?$id=http://[Organization URI]/api/data/v9.0/contacts(60f77a42-5f0e-e611-80e0-00155da84c03) HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 204 No Content    
    ```  
  
 **コンソール出力**  
  
    ```  
    Contact 'Peter Cambel' dissociated from account 'Fourth Coffee'.  
    ```  
  
4.  `Adventure Works` という名前の競合企業を作成します。  
  
 **要求** 
  
    ```http    
    POST http://[Organization URI]/api/data/v9.0/competitors HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    {  
      "name": "Adventure Works",  
      "strengths": "Strong promoter of private tours for multi-day outdoor adventures"  
    }    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 204 No Content  
    OData-Version: 4.0  
    OData-EntityId: http://[Organization URI]/api/data/v9.0/accounts(77f77a42-5f0e-e611-80e0-00155da84c03)    
    ```  
  
 **コンソール出力**  
  
    ```  
    Competitor 'Adventure Works' created.  
    ```  
  
5.  `River rafting adventure` という名前の営業案件を作成します。  
  
 **要求** 
  
    ```http    
    POST http://[Organization URI]/api/data/v9.0/opportunities HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    {  
      "name": "River rafting adventure",  
      "description": "Sales team on a river-rafting offsite and team building"  
    }    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 204 No Content  
    OData-Version: 4.0  
    OData-EntityId: http://[Organization URI]/api/data/v9.0/opportunities(7cf77a42-5f0e-e611-80e0-00155da84c03)    
    ```  
  
 **コンソール出力**  
  
    ```  
    Opportunity 'River rafting adventure' created.  
    ```  
  
6.  この新しい営業案内をこの新しい競合企業に関連付けます。 前述の一対多の関連付けで使用できるように、この多対多の関連付けで同じ全般構文が使用されることに注意してください。  
  
 **要求** 
  
    ```http    
    POST http://[Organization URI]/api/data/v9.0/opportunities(7cf77a42-5f0e-e611-80e0-00155da84c03)/opportunitycompetitors_association/$ref HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    {  
      "@odata.id": "http://[Organization URI]/api/data/v9.0/competitors(77f77a42-5f0e-e611-80e0-00155da84c03)"  
    }    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 204 No Content    
    ```  
  
 **コンソール出力**  
  
    ```  
    Opportunity 'River rafting adventure' associated with competitor 'Adventure Works'.  
    ```  
  
7.  選択的に、競合企業 Adventure Works と関連付けられたすべての営業案件を取得します。  配列が、単一の営業案件を含んで返されます。  
  
 **要求** 
  
    ```http    
    GET http://[Organization URI]/api/data/v9.0/competitors(77f77a42-5f0e-e611-80e0-00155da84c03)?$select=name,&$expand=opportunitycompetitors_association($select=name,description) HTTP/1.1  
    Accept: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 200 OK  
    {   
       "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#competitors(name,opportunitycompetitors_association,opportunitycompetitors_association(name,description))/$entity",  
       "@odata.etag":"W/\"628913\"",  
       "name":"Adventure Works",  
       "competitorid":"77f77a42-5f0e-e611-80e0-00155da84c03",  
       "opportunitycompetitors_association":[   
          {   
             "@odata.etag":"W/\"628917\"",  
             "name":"River rafting adventure",  
             "description":"Sales team on a river-rafting offsite and team building",  
             "opportunityid":"7cf77a42-5f0e-e611-80e0-00155da84c03"  
          }  
       ]  
    }    
    ```  
  
 **コンソール出力**  
  
    ```    
    Competitor 'Adventure Works' has the following opportunities:  
            Name: River rafting adventure,  
            Description: Sales team on a river-rafting offsite and team building    
    ```  
  
8.  営業案件の競合企業との関連付けを解除します。  この場合、一対多の関連付けを削除するのに、全般構文が使用されることに再度注意してください。  
  
 **要求** 
  
    ```http    
    DELETE http://[Organization URI]/api/data/v9.0/opportunities(7cf77a42-5f0e-e611-80e0-00155da84c03)/opportunitycompetitors_association/$ref?$id=http://[Token-CRM-Org-Name]/Contoso/api/data/v8.1/competitors(77f77a42-5f0e-e611-80e0-00155da84c03) HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 204 No Content    
    ```  
  
 **コンソール出力**  
  
    ```  
    Opportunity 'River rafting adventure' disassociated from competitor 'Adventure Works'.  
    ```  
  
<a name="bkmk_section5"></a> 
  
## <a name="section-5-delete-entities-sample-cleanup"></a>セクション 5: エンティティ (サンプル クリーンアップ) を削除します 
 
<!-- TODO:
This section demonstrates how to delete entity instances. The corresponding message is a straightforward DELETE request that uses the URI of the entity instance to be deleted.  If the target entity has a parent-child relationship with other entities, then deleting the parent will, by default, automatically cascade delete child instances. For example, in this sample, tasks have contact as their parent. For more information, see [Entity relationship behavior](../entity-relationship-behavior.md).   -->
  
1.  各要素のエンティティ URL のコレクションは削除されます。  最初の取引先担当者レコードは Peter Cambel です。  
  
 **要求** 
  
    ```http
    DELETE http://[Organization URI]/api/data/v9.0/contacts(60f77a42-5f0e-e611-80e0-00155da84c03) HTTP/1.1  
    Content-Type: application/json  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 204 No Content    
    ```  
  
2.  それ以降のコレクションを介した繰り返しによって、残りのレコードが削除されます。  
  
 **要求** 
  
    ```http    
    DELETE http://[Organization URI]/api/data/v9.0/accounts(65f77a42-5f0e-e611-80e0-00155da84c03) HTTP/1.1  
    . . .  
  
    DELETE http://[Organization URI]/api/data/v9.0/accounts(6af77a42-5f0e-e611-80e0-00155da84c03) HTTP/1.1  
    . . .  
  
    DELETE http://[Organization URI]/api/data/v9.0/contacts(6bf77a42-5f0e-e611-80e0-00155da84c03) HTTP/1.1  
    . . .  
  
    DELETE http://[Organization URI]/api/data/v9.0/competitors(77f77a42-5f0e-e611-80e0-00155da84c03) HTTP/1.1  
    . . .  
  
    DELETE http://[Organization URI]/api/data/v9.0/opportunities(7cf77a42-5f0e-e611-80e0-00155da84c03) HTTP/1.1  
    . . .    
    ```  
  
### <a name="see-also"></a>関連項目  

[Common Data Service Web API の使用](overview.md)<br />
[Web API を使用してエンティティを作成する](create-entity-web-api.md)<br />
[Web API を使用してエンティティを取得する](retrieve-entity-using-web-api.md)<br />
[Web API を使用したエンティティの更新と削除](update-delete-entities-using-web-api.md)<br />
[Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)<br />
[Web API 基本操作のサンプル (C#)](samples/basic-operations-csharp.md)<br />

