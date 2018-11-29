---
title: クエリ階層型データ (アプリ用 Common Data Service) | Microsoft Docs
description: 明示的な階層型の関連付けを持つエンティティを照会するために、新しいクエリ条件演算子を利用する方法を説明します。
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
# <a name="query-hierarchical-data"></a>クエリ階層型データ

特定のエンティティの自己参照型1対多関連付けを階層として定義できます。 これらの階層に関連データを返すクエリを作成できます。  
  
明示的な階層型の関連付けを持つエンティティを照会するために、新しいクエリ条件演算子を利用できます。 これらの演算子は、特に階層型の関連付けとして定義されるエンティティ関係に対してのみ適用されます。 <xref:Microsoft.Xrm.Sdk.Query.QueryExpression> または <xref:Microsoft.Xrm.Sdk.Query.FetchExpression>を使用して照会する際にこの階層データを取得する場合、新しい条件演算子を使用できます。  
  
<a name="BKMK_ConditionOperators"></a>   
## <a name="condition-operators-for-hierarchical-data"></a>階層データの条件演算子  
 階層データを照会する際に条件を設定するには、次の演算子を使用します。  
  
|FetchXML|ConditionOperator|説明|  
|--------------|-----------------------|-----------------|  
|`above`|`Above`|参照されているレコードの階層の親子ラインにあるすべてレコードを返します。|  
|`eq-or-above`|`AboveOrEqual`|参照されているレコードと階層でそれより上にあるすべてのレコードを返します。|  
|`under`|`Under`|階層で参照されているレコードの下にあるすべての子レコードを返します。|  
|`eq-or-under`|`UnderOrEqual`|参照されているレコードと階層でそれより下にあるすべての子レコードを返します。|  
|`not-under`|`NotUnder`|階層で参照されているレコードの下にないすべてのレコードを返します。|  
|`eq-owneduseroruserhierarchy`|`OwnedByMeOrMyReports`|階層セキュリティ モデルが使用されている場合、現在のユーザーまたはユーザーのレポート階層を等しくします。|  
|`eq-useroruserhierarchyandteams`|`OwnedByMeOrMyReportsAndTeams`|階層セキュリティ モデルが使用されている場合、現在のユーザーとそのチームまたはユーザーのレポート階層とそのチームを等しくします。|  
  
### <a name="recursion-limits-when-querying-hierarchical-data"></a>再帰は階層データを照会する時を制限する  
 階層データを照会するとリソースを大量に消費するので、`Above`、`AboveOrEqual`、`Under`、`UnderOrEqual`、および `NotUnder`条件演算子を使用して階層を照会できる再帰を、既定で 100 に限定しています。  
  
 `OwnedByMeOrMyReports` と `OwnedByMeOrMyReportsAndTeams` は、階層セキュリティの条件演算子で、**設定** > **セキュリティ** > **階層セキュリティ**にある**階層の深さ**設定によって異なります。 この設定の値は `Organization.MaxDepthForHierarchicalSecurityModel` 属性に格納されます。  
  
<a name="BKMK_ChildCountAggregate"></a>   
## <a name="retrieve-the-number-of-hierarchically-related-child-records"></a>階層的に関連する子レコードの数を取得する  
 FetchXML ベースのクエリの `rowaggregate` 属性を使用して、階層的に関連する子レコードの数を取得します。 この値が `CountChildren` に設定されている場合、レコードの子レコードの合計数を含む値は、<xref:Microsoft.Xrm.Sdk.EntityCollection>に含まれます。 たとえば、次のクエリは、階層的な関係にある子取引先企業レコードの数を表す `AccountChildren` 合計値を含みます。ここで、 `{0}`パラメータは、親レコードの`AccountId`を表します。  
  
```xml  
<fetch distinct='false' no-lock='false' mapping='logical'>  
  <entity name='account'>  
    <attribute name='name' />  
    <attribute name='accountid' />  
    <attribute name='accountid' rowaggregate='CountChildren' alias='AccountChildren'/>  
    <filter type='and'>  
      <condition attribute='accountid' operator='under' value='{0}' />  
    </filter>  
  </entity>  
</fetch>  
  
```  
  
> [!NOTE]
>  戻された合計値はすべての子レコードを表します。それには、ユーザーが読み取ることのできないレコードも含まれます。  
  
 