---
title: FetchXML における会計日演算子と older than 日付/時刻クエリ演算子 (アプリ用 Common Data Service) | Microsoft Docs
description: 日付と時刻の値に、FetchXML の会計日付条件演算子および &quot;older than&quot; 句を使用する方法の説明
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
# <a name="fiscal-date-and-older-than-datetime-query-operators-in-fetchxml"></a>FetchXML の会計日クエリ演算子および older than 日付/時刻クエリ演算子

アプリ用 Common Data Service の FetchXML クエリは、クエリの日付と時刻の値に、特別な会計日の値と *older than* 句を使用できます。 たとえば、FetchXML クエリは、前の会計月に履行したすべての注文や、15 分経過した重大度の高い緊急のサポート案件を検索できます。  
  
> [!NOTE]
>  すべての会計日付クエリに対して、FetchXML クエリは組織の会計年度設定を使用します。  
  
<a name="FiscalDate"></a>   
## <a name="using-fetchxml-fiscal-date-conditional-operators"></a>FetchXML の会計日付条件演算子の使用  
 以下は、組織の会計年度設定に基づいて、前の会計期間の処理済みのすべての注文を検索する FetchXML 式の例です。 このクエリは、たとえば、組織の会計期間単位が歴月なら、前の会計月の処理済みの注文を返します。 組織の会計期間単位が四半期制なら、前の四半期の処理済みの注文を返します。 組織の会計期間単位が上半期/下半期制なら、前の半期の処理済みの注文を返します。  
  
```xml  
<fetch>  
 <entity name="order">  
  <attribute name="name"/>  
  <filter type="and">  
   <condition attribute="datefulfilled" operator="last-fiscal-period"/>  
  </filter>  
 </entity>  
</fetch>  
```  
  
 以下は、2013 会計年度に作成されたすべてのアカウントを検索する FetchXML 式の例です。  
  
```xml  
<fetch>  
 <entity name="account">  
  <attribute name="name"/>  
  <filter type="and">  
   <condition attribute="createdon" operator="in-fiscal-year" value="2013"/>  
  </filter>  
 </entity>  
</fetch>  
```  
  
 以下は、組織の会計年度に基づいて次の 3 年間の間に推定クローズ日を迎えるすべての営業案件を検索する FetchXML 式の例です。 condition タグの value 属性で `x` の値が指定されています。  
  
```xml  
<fetch>  
 <entity name="opportunity">  
  <attribute name="name"/>  
  <filter type="and">  
   <condition attribute="estimatedclosedate" operator="next-x-fiscal-years" value="3"/>  
  </filter>  
 </entity>  
</fetch>  
```  
  
 以下は、組織の会計年度設定に基づいて、任意の会計年度の第 3 期のすべての処理済みの注文を検索する FetchXML 式の例です。 condition タグの value 属性で会計期間値が指定されています。 組織の会計期間単位が歴月なら、このクエリは第 3 月の結果を返します。 組織の会計期間単位が四半期制なら、第 3 四半期の結果を返します。 組織の会計期間単位が上半期/下半期制の場合、結果は返されません。この場合、期間が 2 つしか存在せず、指定した値が範囲を越えるからです。  
  
```xml  
<fetch>  
 <entity name="order">  
  <attribute name="name"/>  
  <filter type="and">  
   <condition attribute="datefulfilled" operator="in-fiscal-period" value="3"/>  
  </filter>  
 </entity>  
</fetch>  
```  
  
 以下は、組織の会計年度設定に基づいて、2013 会計年度の第 3 期の処理済みのすべての注文を検索する FetchXML 式の例です。 組織の会計期間単位が歴月なら、このクエリは第 3 月の結果を返します。 組織の会計期間単位が四半期制なら、第 3 四半期の結果を返します。 組織の会計期間単位が上半期/下半期制の場合、結果は返されません。この場合、期間が 2 つしか存在せず、指定した値が範囲を越えるからです。  
  
```xml  
<fetch>  
 <entity name="order">  
  <attribute name="name"/>  
  <filter type="and">  
   <condition attribute="datefulfilled" operator="in-fiscal-period-and-year">  
    <value>3</value>  
    <value>2013</value>  
   </condition>  
  </filter>  
 </entity>  
</fetch>  
```  
  
 以下は、処理済みの注文の総額を計算して結果を上半期/下半期ごとと会計年度ごとにまとめる FetchXML 集計式の例です。  
  
```xml  
<fetch aggregate="true">  
 <entity name="order">  
  <attribute name="totalamount" aggregate="sum" alias="total"/>  
  <attribute name="datefulfilled" groupby="true" dategrouping="fiscal-period"/>  
 </entity>  
</fetch>  
```  
  
<a name="OlderThan"></a>   
## <a name="using-older-than-clauses-for-date-and-time-values"></a>日付と時刻の値への "よりも古い" 句の使用  
 次の例は、30 分経過したインシデントを検索する FetchXML を示しています。  
  
```xml  
<fetch>  
  <entity name="incident">  
    <attribute name="title" />  
    <attribute name="ticketnumber" />  
    <attribute name="createdon" />  
    <attribute name="incidentid" />  
    <filter type="and">  
      <condition attribute="createdon" operator="olderthan-x-minutes" value="30" />  
    </filter>  
  </entity>  
</fetch>  
```  
  
 次の構文を使用して、FetchXML 式でさまざまな *older than* 句を指定します。  
  
 が X 分よりも古い  
 ```xml  
<condition attribute="<AttributeName>" operator="olderthan-x-minutes" value="<VALUE>" />  
```  
  
> [!NOTE]
>  この句は、`DateOnly` 動作の日付属性と時間属性に対してはサポートされません。 詳細: [DateOnly の動作でサポートされない日付および時刻のクエリ演算子](/dynamics365/customer-engagement/developer/behavior-format-date-time-attribute#date-and-time-query-operators-not-supported-for-dateonly-behavior)
  
 が X 時間よりも古い  
 ```xml  
<condition attribute="<AttributeName>" operator="olderthan-x-hours" value="<VALUE>" />  
```  
  
> [!NOTE]
>  この句は、`DateOnly` 動作の日付属性と時間属性に対してはサポートされません。 詳細: [DateOnly の動作でサポートされない日付および時刻のクエリ演算子](/dynamics365/customer-engagement/developer/behavior-format-date-time-attribute#date-and-time-query-operators-not-supported-for-dateonly-behavior)  
  
 が X 日よりも古い  
 ```xml  
<condition attribute="<AttributeName>" operator="olderthan-x-days" value="<VALUE>" />  
```  
  
 が X 週間よりも古い  
 ```xml  
<condition attribute="<AttributeName>" operator="olderthan-x-weeks" value="<VALUE>" />  
```  
  
 が X か月よりも古い  
 ```xml  
<condition attribute="<AttributeName>" operator="olderthan-x-months" value="<VALUE>" />  
```  
  
 が X 年間よりも古い  
 ```xml  
<condition attribute="<AttributeName>" operator="olderthan-x-years" value="<VALUE>" />  
```

### <a name="see-also"></a>関連項目  
 [データを取得するクエリの作成](/dynamics365/customer-engagement/developer/org-service/retrieve-data-queries-sdk-assemblies)   
 [FetchXML を使用したクエリの構築](/dynamics365/customer-engagement/developer/org-service/build-queries-fetchxml)   
 [左外部結合を FetchXML で使用して "存在しない" 記録をクエリする](/dynamics365/customer-engagement/developer/use-left-outer-join-fetchxml-query-records-not-in)
