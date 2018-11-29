---
title: 重複データ検出を実行する (Common Data Service for Apps) | Microsoft Docs
description: 特定のレコードやエンティティの種類に対して、あるいは作成または更新の操作中に重複データ検出を実行します。
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
# <a name="run-duplicate-detection"></a>重複データ検出を実行する

重複データ検出を有効にして重複データ検出ルールを公開した後、いくつかの方法で重複データ検出を実行することができます。  

<a name="BKMK_RetDupwebapi"></a>

## <a name="retrieve-and-detect-duplicates-for-a-specified-record"></a>指定されたレコードの重複を検出し、取得する

以下のように重複を検出し、取得します。

- エンティティを作成する前に
- 既存のエンティティに対して
- 複数のエンティティにわたる重複ルールに対応するその他のエンティティに対して。 たとえば、取引先担当者エンティティに一致する潜在顧客エンティティ。

### <a name="options"></a>オプション:

- Web API: <xref href="Microsoft.Dynamics.CRM.RetrieveDuplicates?text=RetrieveDuplicates Function" />
- 組織のサービス: <xref:Microsoft.Crm.Sdk.Messages.RetrieveDuplicatesRequest>


### <a name="example-detect-duplicates-for-a-specified-record-using-web-api"></a>例: Web APIを使用して、指定されたレコードの重複を検出する

次の例は、`RetrieveDuplicates` 関数を使用して、指定されたレコードの重複を検出する方法を示しています。

**要求**
```http
GET [Organization URI]/api/data/v9.0/RetrieveDuplicates(BusinessEntity=@p1,MatchingEntityName=@p2,PagingInfo=@p3)?@p1={'@odata.type':'Microsoft.Dynamics.CRM.account','accountid':'0d1156d2-1598-e711-80e8-00155db64062'}&@p2='account'&@p3={'PageNumber':1,'Count':50} HTTP/1.1
If-None-Match: null
OData-Version: 4.0
OData-MaxVersion: 4.0
Content-Type: application/json
Accept: application/json
```
**応答**
```json
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0

{
    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#accounts",
    "value": [
        <Omitted for brevity: JSON data for any matching accounts including all properties>
    ]
}
```

<a name="BKMK_DupEntwebapi"></a>

## <a name="detect-duplicates-for-an-entity-type"></a>エンティティの種類の重複を検出する

バックグラウンドで実行される非同期の重複データ検出ジョブを実行します。 重複データは、このエンティティの種類に対する公開済みの重複データ ルールに従って検出されます。 検出された重複データは、`DuplicateRecord` レコードとして Dynamics 365 に格納されます。 

重複データ検出ジョブからは最大 5000 件の重複が返されます。

### <a name="options"></a>オプション​​

- Web API: <xref href="Microsoft.Dynamics.CRM.BulkDetectDuplicates?text=BulkDetectDuplicates Action" />
- 組織のサービス: <xref:Microsoft.Crm.Sdk.Messages.BulkDetectDuplicatesRequest>

### <a name="example-detect-duplicates-for-an-entity-type-using-the-web-api"></a>例: Web APIを使用して、エンティティの種類の重複データを検出する 

次の例は、`BulkDetectDuplicates` アクションを使用して非同期ジョブを作成し、1 つのエンティティの種類の重複データを検出する方法を示しています。

**要求**
```http
POST [Organization URI]/api/data/v9.0/BulkDetectDuplicates HTTP/1.1
If-None-Match: null
OData-Version: 4.0
Content-Type: application/json
Accept: application/json
OData-MaxVersion: 4.0

{
    "Query": {
        "@odata.type": "#Microsoft.Dynamics.CRM.QueryExpression",
        "EntityName": "lead"
    },
    "JobName": "jobname1",
    "SendEmailNotification": false,
    "TemplateId": "07B94C1D-C85F-492F-B120-F0A743C540E6",
    "ToRecipients": [],
    "CCRecipients": [],
    "RecurrencePattern": "",
    "RecurrenceStartTime": "2015-07-15T05:30:00Z"
}  
```
**応答**
```json
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0

{
    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.BulkDetectDuplicatesResponse",
    "JobId": "efaff068-7598-e711-80e8-00155db64062"
}
```
上記の要求により、応答で JobID が返される非同期の重複データ検出ジョブが作成されます。 上記の要求から返される JobID を使用して、以下の例に示すように、エンティティの種類の重複レコードをフェッチできます。

**要求**
```http
GET [Organization URI]/api/data/v9.0/asyncoperations(efaff068-7598-e711-80e8-00155db64062)/AsyncOperation_DuplicateBaseRecord
If-None-Match: null
OData-Version: 4.0
OData-MaxVersion: 4.0
Content-Type: application/json
Accept: application/json
```
上記の要求に相当する FetchXML を以下に示します。

```xml
<fetch>
    <entity name="duplicaterecord">
        <attribute name="owninguser" />
        <attribute name="ownerid" />
        <attribute name="baserecordid" />
        <attribute name="duplicateid" />
        <attribute name="owningbusinessunit" />
        <attribute name="createdon" />
        <attribute name="asyncoperationid" />
        <filter>
            <condition attribute="asyncoperationid" operator="eq" value="efaff068-7598-e711-80e8-00155db64062" />
        </filter>
    </entity>
</fetch>
```

**応答**
```json
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0

{  
   "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#duplicaterecords",
   "value":[  
      {  
         "owninguser":"b3ac4144-6d9a-e711-811c-000d3a75ce72",
         "_ownerid_value":"b3ac4144-6d9a-e711-811c-000d3a75ce72",
         "_baserecordid_value":"3a6fc65b-3f9c-e711-811c-000d3a75ce72",
         "duplicateid":"489a879c-019b-4c28-8539-51ebc850d18f",
         "createdon":"2017-09-19T03:34:25Z",
         "owningbusinessunit":"20a44144-6d9a-e711-811c-000d3a75ce72",
         "_asyncoperationid_value":"efaff068-7598-e711-80e8-00155db64062",
         "_duplicateruleid_value":null,
         "_duplicaterecordid_value":null
      },
      {  
         "owninguser":"b3ac4144-6d9a-e711-811c-000d3a75ce72",
         "_ownerid_value":"b3ac4144-6d9a-e711-811c-000d3a75ce72",
         "_baserecordid_value":"406fc65b-3f9c-e711-811c-000d3a75ce72",
         "duplicateid":"0a4a7dea-1488-4e05-b5eb-c2925ad2925a",
         "createdon":"2017-09-19T03:34:25Z",
         "owningbusinessunit":"20a44144-6d9a-e711-811c-000d3a75ce72",
         "_asyncoperationid_value":"efaff068-7598-e711-80e8-00155db64062",
         "_duplicateruleid_value":null,
         "_duplicaterecordid_value":null
      }
   ]
}
```
基本のレコードの GUID は、`baserecordid` として `DuplicateRecord` レコードに保存されます。 上記の応答の `duplicateid` は、重複レコードの一意の識別子です。 `asyncoperationid` は、このレコードを作成したシステム ジョブの一意の識別子です。 また、`ownerid` は、重複レコードを所有するユーザーまたはチームの一意の識別子です。 詳細については、「[DuplicateRecord エンティティ](reference/entities/duplicaterecord.md)」を参照してください。

> [!NOTE]
>  重複データ検出ジョブを作成して実行する前に、適切な重複データ検出ルールが設定されていることを確認します。 Dynamics 365 には、取引先企業、取引先担当者、および潜在顧客のための既定の重複データ検出ルールが組み込まれています。他のレコードの種類のための既定のルールは存在しません。 システムが他のレコードの種類の重複データを検出するようにするには、新しいルールを作成する必要があります。 重複データ検出ルールを作成する方法の詳細については、「[重複データ検出ルール](/dynamics365/customer-engagement/admin/set-up-duplicate-detection-rules-keep-data-clean)」を参照してください。

<a name="BKMK_CRwebapi"></a>

## <a name="detect-duplicates-during-create-and-update-operations"></a>作成および更新操作中の重複データ検出

レコードの作成または更新時の重複データ検出は、組織で重複データ検出が有効であり、エンティティが重複データ検出に対応しており、アクティブな重複データ検出ルールが適用されている場合にのみ適用されます。 既定では、Web API または組織サービスを使用したレコードの作成または更新時には重複データ検出が実行されません。 

レコードの作成および更新時に重複データを検出するには、以下を参照してください。

- WebAPI: [Web API を使用した重複データの検出](webapi/manage-duplicate-detection-create-update.md)
- 組織サービス: [組織サービスを使用した重複データ検出](org-service/detect-duplicate-data.md)

  
### <a name="see-also"></a>関連項目  
 [重複データ検出のメッセージ](duplicate-detection-messages.md)
