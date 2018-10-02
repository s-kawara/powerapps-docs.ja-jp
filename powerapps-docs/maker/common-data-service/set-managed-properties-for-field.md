---
title: PowerApps のフィールドに対する管理プロパティの設定 | MicrosoftDocs
description: フィールドに対する管理プロパティの設定方法について学習
ms.custom: ''
ms.date: 06/19/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: 4ddcfcf3-5604-4b93-a5ee-589d4fb97fa4
caps.latest.revision: 33
ms.author: matp
manager: kvivek
tags: null
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="set-managed-properties-for-fields"></a>フィールドに管理プロパティを設定する

<a name="BKMK_SettingManagedProperties"></a>   

 管理プロパティは、管理ソリューションにフィールドを含め、そのソリューションを別の環境にインポートするときにのみ適用されます。 これらの設定により、ソリューション作成者は、管理ソリューションをインストールしているユーザーがそのフィールドをカスタマイズする際に許可されるカスタマイズのレベルを制御することができます。 フィールドの管理プロパティを設定するには、メニュー バーの**管理プロパティ**を選択します。  
  
 **カスタマイズ可能**オプションは、そのほかのすべてのオプションを制御します。 このオプションが `False` の場合、そのほかの設定は一切適用されません。 これが `True` の場合、そのほかのカスタマイズ オプションを指定できます。  
  
 フィールドがカスタマイズ可能な場合、`True`または`False`へ以下のオプションを設定できます。  
  
- **修正可能な表示名**  
  
- **入力要求レベルを変更可能**  
  
- **追加プロパティを変更可能**  
  
 これらのオプションは、一目瞭然です。 すべての個別のオプションを `False`に設定した場合、**カスタマイズ可能**も`False` に設定できます。  

 ## <a name="next-steps"></a>次のステップ

 [フィールドの作成および編集](create-edit-fields.md)
