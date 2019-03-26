---
title: クエリと共に関連エンティティを取得する (アプリ用 Common Data Service)| Microsoft Docs
description: ead ナビゲーション プロパティの拡張による関連エンティティの取得方法。
ms.custom: ''
ms.date: 02/06/2019
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 3D8FB9AF-3663-437A-988E-CBAE9579F167
caps.latest.revision: 78
author: susikka
ms.author: susikka
manager: shujoshi
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# クエリに関連エンティティを取得します。

ナビゲーション プロパティの `$expand` システム クエリ オプションを使用して、関連エンティティからどのデータが返されるかをコントロールします。 ナビゲーション プロパティには次の 2 種類があります。  
  
- *単一値* ナビゲーション プロパティは、多対 1 関係をサポートし、別のエンティティに対する参照が設定できるような検索属性に対応します。  
  
- *コレクション値* ナビゲーション プロパティは 1 対多または多対多の関連付けに対応します。  
  
ナビゲーション プロパティ名のみを含める場合、関連レコードのすべてのプロパティが表示されます。 ナビゲーション プロパティ名の後にかっこで示される、`$select` システム クエリ オプションを使用して、関連レコードに対して返されるプロパティを制限できます。 これは、単一値とコレクション値のナビゲーション プロパティの両方で使用します。  

> [!NOTE]
>  エンティティ インスタンスの関連エンティティを取得するには、「[ナビゲーション プロパティの拡張による関連エンティティの取得](retrieve-entity-using-web-api.md#bkmk_expandRelated)」を参照してください。  

<a bkmk="bkmk_retrieverelatedentityexpandsinglenavprop"></a>

## 単一値のナビゲーション プロパティの拡張による関連エンティティの取得。

以下の例は、すべての取引先企業レコードの取引先担当者を取得する方法を示します。 関連する取引先担当者レコードの場合、取引先担当者 ID およびフルネームのみを取得します。  
  
****要求****  

```http 
GET [Organization URI]/api/data/v9.0/accounts?$select=name&$expand=primarycontactid($select=contactid,fullname) HTTP/1.1  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```  
  
****応答**** 
 
```http 
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
  
{  
   "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(name,primarycontactid,primarycontactid(contactid,fullname))",
   "value":[  
      {  
         "@odata.etag":"W/\"513475\"",
         "name":"Fourth Coffee (sample)",
         "accountid":"36dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "contactid":"9cdbf27c-8efb-e511-80d2-00155db07c77",
            "fullname":"Yvonne McKay (sample)"
         }
      },
      {  
         "@odata.etag":"W/\"513477\"",
         "name":"Litware, Inc. (sample)",
         "accountid":"38dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "contactid":"9edbf27c-8efb-e511-80d2-00155db07c77",
            "fullname":"Susanna Stubberod (sample)"
         }
      },
      {  
         "@odata.etag":"W/\"513479\"",
         "name":"Adventure Works (sample)",
         "accountid":"3adbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "contactid":"a0dbf27c-8efb-e511-80d2-00155db07c77",
            "fullname":"Nancy Anderson (sample)"
         }
      },
      {  
         "@odata.etag":"W/\"513481\"",
         "name":"Fabrikam, Inc. (sample)",
         "accountid":"3cdbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "contactid":"a2dbf27c-8efb-e511-80d2-00155db07c77",
            "fullname":"Maria Campbell (sample)"
         }
      },
      {  
         "@odata.etag":"W/\"514057\"",
         "name":"Blue Yonder Airlines (sample)",
         "accountid":"3edbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "contactid":"a0dbf27c-8efb-e511-80d2-00155db07c77",
            "fullname":"Nancy Anderson (sample)"
         }
      },
      {  
         "@odata.etag":"W/\"513485\"",
         "name":"City Power & Light (sample)",
         "accountid":"40dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "contactid":"a6dbf27c-8efb-e511-80d2-00155db07c77",
            "fullname":"Scott Konersmann (sample)"
         }
      },
      {  
         "@odata.etag":"W/\"513487\"",
         "name":"Contoso Pharmaceuticals (sample)",
         "accountid":"42dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "contactid":"a8dbf27c-8efb-e511-80d2-00155db07c77",
            "fullname":"Robert Lyon (sample)"
         }
      },
      {  
         "@odata.etag":"W/\"513489\"",
         "name":"Alpine Ski House (sample)",
         "accountid":"44dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "contactid":"aadbf27c-8efb-e511-80d2-00155db07c77",
            "fullname":"Paul Cannon (sample)"
         }
      },
      {  
         "@odata.etag":"W/\"513491\"",
         "name":"A. Datum Corporation (sample)",
         "accountid":"46dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "contactid":"acdbf27c-8efb-e511-80d2-00155db07c77",
            "fullname":"Rene Valdes (sample)"
         }
      },
      {  
         "@odata.etag":"W/\"513493\"",
         "name":"Coho Winery (sample)",
         "accountid":"48dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "contactid":"aedbf27c-8efb-e511-80d2-00155db07c77",
            "fullname":"Jim Glynn (sample)"
         }
      }
   ]
}    
```  

エンティティ セットの関連エンティティを返す代わりに、`$ref` オプションを使用して単一値ナビゲーション プロパティを展開することにより、関連エンティティへの参照 (リンク) を返すこともできます。 次の例では、すべての取引先企業の取引先担当者レコードに対するリンクを返します。  
  
 ****要求****

```http  
GET [Organization URI]/api/data/v9.0/accounts?$select=name&$expand=primarycontactid/$ref HTTP/1.1  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```  
  
 ****応答****
 
```http 
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
  
{  
   "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(name,primarycontactid)",
   "value":[  
      {  
         "@odata.etag":"W/\"513475\"",
         "name":"Fourth Coffee (sample)",
         "_primarycontactid_value":"9cdbf27c-8efb-e511-80d2-00155db07c77",
         "accountid":"36dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "@odata.id":"[Organization URI]/api/data/v9.0/contacts(9cdbf27c-8efb-e511-80d2-00155db07c77)"
         }
      },
      {  
         "@odata.etag":"W/\"513477\"",
         "name":"Litware, Inc. (sample)",
         "_primarycontactid_value":"9edbf27c-8efb-e511-80d2-00155db07c77",
         "accountid":"38dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "@odata.id":"[Organization URI]/api/data/v9.0/contacts(9edbf27c-8efb-e511-80d2-00155db07c77)"
         }
      },
      {  
         "@odata.etag":"W/\"513479\"",
         "name":"Adventure Works (sample)",
         "_primarycontactid_value":"a0dbf27c-8efb-e511-80d2-00155db07c77",
         "accountid":"3adbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "@odata.id":"[Organization URI]/api/data/v9.0/contacts(a0dbf27c-8efb-e511-80d2-00155db07c77)"
         }
      },
      {  
         "@odata.etag":"W/\"513481\"",
         "name":"Fabrikam, Inc. (sample)",
         "_primarycontactid_value":"a2dbf27c-8efb-e511-80d2-00155db07c77",
         "accountid":"3cdbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "@odata.id":"[Organization URI]/api/data/v9.0/contacts(a2dbf27c-8efb-e511-80d2-00155db07c77)"
         }
      },
      {  
         "@odata.etag":"W/\"514057\"",
         "name":"Blue Yonder Airlines (sample)",
         "_primarycontactid_value":"a0dbf27c-8efb-e511-80d2-00155db07c77",
         "accountid":"3edbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "@odata.id":"[Organization URI]/api/data/v9.0/contacts(a0dbf27c-8efb-e511-80d2-00155db07c77)"
         }
      },
      {  
         "@odata.etag":"W/\"513485\"",
         "name":"City Power & Light (sample)",
         "_primarycontactid_value":"a6dbf27c-8efb-e511-80d2-00155db07c77",
         "accountid":"40dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "@odata.id":"[Organization URI]/api/data/v9.0/contacts(a6dbf27c-8efb-e511-80d2-00155db07c77)"
         }
      },
      {  
         "@odata.etag":"W/\"513487\"",
         "name":"Contoso Pharmaceuticals (sample)",
         "_primarycontactid_value":"a8dbf27c-8efb-e511-80d2-00155db07c77",
         "accountid":"42dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "@odata.id":"[Organization URI]/api/data/v9.0/contacts(a8dbf27c-8efb-e511-80d2-00155db07c77)"
         }
      },
      {  
         "@odata.etag":"W/\"513489\"",
         "name":"Alpine Ski House (sample)",
         "_primarycontactid_value":"aadbf27c-8efb-e511-80d2-00155db07c77",
         "accountid":"44dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "@odata.id":"[Organization URI]/api/data/v9.0/contacts(aadbf27c-8efb-e511-80d2-00155db07c77)"
         }
      },
      {  
         "@odata.etag":"W/\"513491\"",
         "name":"A. Datum Corporation (sample)",
         "_primarycontactid_value":"acdbf27c-8efb-e511-80d2-00155db07c77",
         "accountid":"46dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "@odata.id":"[Organization URI]/api/data/v9.0/contacts(acdbf27c-8efb-e511-80d2-00155db07c77)"
         }
      },
      {  
         "@odata.etag":"W/\"513493\"",
         "name":"Coho Winery (sample)",
         "_primarycontactid_value":"aedbf27c-8efb-e511-80d2-00155db07c77",
         "accountid":"48dbf27c-8efb-e511-80d2-00155db07c77",
         "primarycontactid":{  
            "@odata.id":"[Organization URI]/api/data/v9.0/contacts(aedbf27c-8efb-e511-80d2-00155db07c77)"
         }
      }
   ]
}  
```  

<a bkmk="bkmk_retrieverelatedentityexpandcollectionnavprop"></a>

## コレクション値ナビゲーション プロパティの拡張による関連エンティティの取得

コレクション値ナビゲーション パラメーターを拡張してエンティティ セットの関連エンティティを取得すると、`@odata.nextLink` プロパティが関連エンティティに返されます。 `@odata.nextLink` プロパティの値を新しい `GET` 要求と共に使用して、必要なデータを返す必要があります。  

次の例は、上位 5 件の取引先企業レコードに割り当てられたタスクを取得します。  
  
****要求****

```http 
GET [Organization URI]/api/data/v9.0/accounts?$top=5&$select=name&$expand=Account_Tasks($select%20=%20subject,%20scheduledstart) HTTP/1.1  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```  
  
****応答**** 
 
```http 
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
  
{  
   "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(name,Account_Tasks,Account_Tasks(subject,scheduledstart))",
   "value":[  
      {  
         "@odata.etag":"W/\"513475\"",
         "name":"Fourth Coffee (sample)",
         "accountid":"36dbf27c-8efb-e511-80d2-00155db07c77",
         "Account_Tasks":[  

         ],
         "Account_Tasks@odata.nextLink":"[Organization URI]/api/data/v9.0/accounts(36dbf27c-8efb-e511-80d2-00155db07c77)/Account_Tasks?$select%20=%20subject,%20scheduledstart"
      },
      {  
         "@odata.etag":"W/\"513477\"",
         "name":"Litware, Inc. (sample)",
         "accountid":"38dbf27c-8efb-e511-80d2-00155db07c77",
         "Account_Tasks":[  

         ],
         "Account_Tasks@odata.nextLink":"[Organization URI]/api/data/v9.0/accounts(38dbf27c-8efb-e511-80d2-00155db07c77)/Account_Tasks?$select%20=%20subject,%20scheduledstart"
      },
      {  
         "@odata.etag":"W/\"514074\"",
         "name":"Adventure Works (sample)",
         "accountid":"3adbf27c-8efb-e511-80d2-00155db07c77",
         "Account_Tasks":[  

         ],
         "Account_Tasks@odata.nextLink":"[Organization URI]/api/data/v9.0/accounts(3adbf27c-8efb-e511-80d2-00155db07c77)/Account_Tasks?$select%20=%20subject,%20scheduledstart"
      },
      {  
         "@odata.etag":"W/\"513481\"",
         "name":"Fabrikam, Inc. (sample)",
         "accountid":"3cdbf27c-8efb-e511-80d2-00155db07c77",
         "Account_Tasks":[  

         ],
         "Account_Tasks@odata.nextLink":"[Organization URI]/api/data/v9.0/accounts(3cdbf27c-8efb-e511-80d2-00155db07c77)/Account_Tasks?$select%20=%20subject,%20scheduledstart"
      },
      {  
         "@odata.etag":"W/\"514057\"",
         "name":"Blue Yonder Airlines (sample)",
         "accountid":"3edbf27c-8efb-e511-80d2-00155db07c77",
         "Account_Tasks":[  

         ],
         "Account_Tasks@odata.nextLink":"[Organization URI]/api/data/v9.0/accounts(3edbf27c-8efb-e511-80d2-00155db07c77)/Account_Tasks?$select%20=%20subject,%20scheduledstart"
          }
       ]
    }
 
```  

<a bkmk="bkmk_retrieverelatedentitysingleandcollectionnavprop"></a>
  
## 単一値とコレクション値の両方のナビゲーション プロパティを拡張して、関連するエンティティを取得します

次の例では、単一値とコレクション値の両方のナビゲーション プロパティを使用して、エンティティセットの関連エンティティを拡張する方法を示します。 既に説明しているように、コレクション値ナビゲーション プロパティを拡張してエンティティ セットの関連エンティティを取得すると、関連エンティティの `@odata.nextLink` プロパティが返されます。 `@odata.nextLink` プロパティの値を新しい `GET` 要求と共に使用して、必要なデータを返す必要があります。  
  
この例では、上位 3 件の取引先企業に割り当てられた取引先担当者およびタスクを取得します。  
  
****要求****

```http 
GET [Organization URI]/api/data/v9.0/accounts?$top=3&$select=name&$expand=primarycontactid($select=contactid,fullname),Account_Tasks($select=subject,scheduledstart)  HTTP/1.1  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```  
  
****応答****  

```http 
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
  
{  
   "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(name,primarycontactid,Account_Tasks,primarycontactid(contactid,fullname),Account_Tasks(subject,scheduledstart))",
   "value":[  
      {  
         "@odata.etag":"W/\"550614\"",
         "name":"Fourth Coffee (sample)",
         "accountid":"5b9648c3-68f7-e511-80d3-00155db53318",
         "primarycontactid":{  
            "contactid":"c19648c3-68f7-e511-80d3-00155db53318",
            "fullname":"Yvonne McKay (sample)"
         },
         "Account_Tasks":[  

         ],
         "Account_Tasks@odata.nextLink":"[Organization URI]/api/data/v9.0/accounts(5b9648c3-68f7-e511-80d3-00155db53318)/Account_Tasks?$select=subject,scheduledstart"
      },
      {  
         "@odata.etag":"W/\"550615\"",
         "name":"Litware, Inc. (sample)",
         "accountid":"5d9648c3-68f7-e511-80d3-00155db53318",
         "primarycontactid":{  
            "contactid":"c39648c3-68f7-e511-80d3-00155db53318",
            "fullname":"Susanna Stubberod (sample)"
         },
         "Account_Tasks":[  

         ],
         "Account_Tasks@odata.nextLink":"[Organization URI]/api/data/v9.0/accounts(5d9648c3-68f7-e511-80d3-00155db53318)/Account_Tasks?$select=subject,scheduledstart"
      },
      {  
         "@odata.etag":"W/\"550616\"",
         "name":"Adventure Works (sample)",
         "accountid":"5f9648c3-68f7-e511-80d3-00155db53318",
         "primarycontactid":{  
            "contactid":"c59648c3-68f7-e511-80d3-00155db53318",
            "fullname":"Nancy Anderson (sample)"
         },
         "Account_Tasks":[  

         ],
         "Account_Tasks@odata.nextLink":"[Organization URI]/api/data/v9.0/accounts(5f9648c3-68f7-e511-80d3-00155db53318)/Account_Tasks?$select=subject,scheduledstart"
      }
   ]
}
  
```

## 関連項目

[[Web API を使用したクエリ データ](query-data-web-api.md)](query-data-web-api.md)<br />
[[Web API を使用して演算を実行する](perform-operations-web-api.md)](perform-operations-web-api.md)<br />
[[HTTP 要求の作成とエラーの処理](compose-http-requests-handle-errors.md)](compose-http-requests-handle-errors.md)<br />
[[Web API を使用してエンティティを作成する](create-entity-web-api.md)](create-entity-web-api.md)<br />
[[Web API を使用してエンティティを取得する](retrieve-entity-using-web-api.md)](retrieve-entity-using-web-api.md)<br />
[[Web API を使用したエンティティの更新と削除](update-delete-entities-using-web-api.md)](update-delete-entities-using-web-api.md)<br />
[[Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)](associate-disassociate-entities-using-web-api.md)