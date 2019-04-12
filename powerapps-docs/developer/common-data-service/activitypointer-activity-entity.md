---
title: ActivityPointer (活動) エンティティ (Common Data Service) | Microsoft Docs
description: 活動ポインター (活動) エンティティは、ユーザーが実行した活動またはタスク、あるいはこれから実行する活動またはタスクを表します。 活動とは、エントリをカレンダー上に作成できる任意の操作です
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
# <a name="activitypointer-activity-entity"></a>ActivityPointer (活動) エンティティ

活動ポインター (活動) エンティティは、ユーザーが実行した活動またはタスク、あるいはこれから実行する活動またはタスクを表します。 活動は、カレンダーにエントリを作成できる任意のアクションです。  
  
 Common Data Service で活動レコードを作成すると、対応する活動ポインター レコードも作成されます。 この場合、活動レコードおよび対応する活動ポインター レコードの両方の `ActivityId` 属性は同じ値になります。 たとえば、`Email` レコードを作成すると、`Email.ActivityId` および対応する `ActivityPointer.ActivityId` の属性値は同じになります。  
  
 `ActivityPointer.ActivityTypeCode` 属性は、活動の種類を定義します。 `activitypointer_activitytypecode` グローバル オプション セットで、この属性に指定可能な値が定義されます。  
  
<a name="bkmk_sortdate"></a>   

## <a name="control-how-activities-are-sorted-by-date"></a>日付による活動の並べ替え方法を制御する  
  
 エンティティのリストを表示し、日付別にそれらを発注する時はいつでも、activitypointer エンティティで定義されている共通の日付の属性しか使用できません。 しかし、活動の種類によって異なる並べ替えの動作を必要とする場合があります。 例えば、電子メールのエンティティでは、modifiedon 属性値よりもむしろ、senton 属性値によって並べ替える場合があります。  
  
 sortdate 属性を使用して、日付によるアクティビティの並べ替え方法を制御します。 既定では、sortdate 属性値は null です。 ビジネス ロジックを含め、この属性に対して設定されるデータ値を設定し、ビューに対して定義されたクエリ内で sortdate 属性を使用する必要があります。 ワークフローまたはプラグインを使用して sortdate 属性値を設定できます。 一貫した結果を取得するために、あらゆるタイプのアクティビティおよびシステム内の既存のアクティビティ データに対してこの値を設定する必要があります。  
  
### <a name="see-also"></a>関連項目  
 [活動エンティティ](activity-entities.md)   
 [ActivityPointer エンティティ](reference/entities/activitypointer.md)