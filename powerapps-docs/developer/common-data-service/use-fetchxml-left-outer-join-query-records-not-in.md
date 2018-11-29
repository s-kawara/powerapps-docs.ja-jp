---
title: FetchXML の左外部結合を  &bdquo;not in&bdquo; レコードのクエリに使用する (アプリ用 Common Data Service) | Microsoft Docs
description: 左外部結合を FetchXML で使用して、結合の表をフィルタリングするクエリを実行して、セットに "存在しない" 記録を探すクエリを作成する方法について説明します
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-a-left-outer-join-in-fetchxml-to-query-for-records-not-in"></a>左外部結合を FetchXML で使用して "存在しない" 記録をクエリする

FetchXML の左外部結合を使用して、結合の表をフィルタリングするクエリを実行できます。たとえば、過去 2 か月間のキャンペーン活動がない取引先担当者をすべて検索できます。 このクエリタイプの別のよくある使用法では、次のような場合には存在しないといった、あるセットには存在しないレコードを検索するクエリです。  
  
- タスクのないすべての潜在顧客を検索する  
  
- 取引先担当者のないすべての取引先企業を検索する  
  
- 1つか、2つのタスクがあるすべての潜在顧客を検索する  
  
  左外部結合では、2 番め入力で最初の入力の結合を満たす各列を返します。 また、2 番目入力で一致する列がない最初の入力列を返します。 2 番めの一致しない列が null 値として返されます。  
  
  条件演算子として `entityname` 属性を使用して、FetchXML の左外部結合を実行できます。 `entityname` 属性は、条件、フィルターおよび入れ子フィルターで有効です。  
  
  プログラムで左外部結合を使用してクエリを作成し、 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMultipleRequest> を使用してクエリを実行し、`SavedQuery` レコードを作成してクエリを保存できます。 Web アプリケーションの高度な検索または保存済みクエリ エディターに左外部結合が含まれている保存済みクエリを開き、実行して結果を表示できますが、一部のエディタ機能は無効化されます。 これらのエディターでは、返される列を変更するなどのクエリの変更はできますが、エディタは左外部結合の変更はサポートしていません。  
  
## <a name="example-find-all-accounts-that-have-no-leads"></a>例: 潜在顧客のないすべての取引先企業を検索する  
 次に、FetchXML でのクエリの作成方法を示します。  
  
```xml  
<fetch mapping='logical'>  
 <entity name='account'>  
  <attribute name='name'/>  
  <link-entity name='lead'  
               from='leadid'  
               to='originatingleadid'  
               link-type='outer'/>  
  <filter type='and'>  
   <condition entityname='lead'  
              attribute='leadid'  
              operator='null'/>  
  </filter>  
 </entity>  
</fetch>  
  
```  
  
## <a name="example-find-all-leads-that-have-no-tasks-using-an-alias"></a>例: エイリアス名を使用して、タスクのないすべての潜在顧客を検索する  
 次に、FetchXML でのクエリの作成方法を示します。  
  
```xml  
<fetch version="1.0" output-format="xml-platform" mapping="logical" distinct="true">  
  <entity name="lead">  
    <attribute name="fullname" />  
    <link-entity name="task" from="regardingobjectid" to="leadid" alias="ab" link-type="outer">  
       <attribute name="regardingobjectid" />  
    </link-entity>  
    <filter type="and">  
        <condition entityname="ab" attribute="regardingobjectid" operator="null" />  
    </filter>  
  </entity>  
<fetch/>  
  
```  
  
 これは次のSQLと等価です。  
  
```sql  
SELECT lead.FullName  
FROM Leads as lead  
LEFT OUTER JOIN Tasks as ab  
ON (lead.leadId  =  ab.RegardingObjectId)  
WHERE ab.RegardingObjectId is null  
  
```  
  
### <a name="see-also"></a>関連項目  
 [FetchXML を使用したクエリの構築](/dynamics365/customer-engagement/developer/org-service/build-queries-fetchxml)   
 [サンプル: FetchXML での集計の使用](org-service/samples/use-aggregation-fetchxml.md)   
 [FetchXML の使用によるクエリの作成](use-fetchxml-construct-query.md)   
 [サンプル: 保存済みクエリの検証および実行](org-service/samples/validate-execute-saved-query.md)
