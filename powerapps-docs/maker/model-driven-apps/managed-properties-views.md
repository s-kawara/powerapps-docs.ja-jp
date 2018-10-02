---
title: PowerApps を使用したビューのモデル駆動型管理プロパティ | MicrosoftDocs
description: ビューの管理プロパティの設定方法について学習
ms.custom: ''
ms.date: 06/12/2018
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
ms.assetid: a9014576-8fb2-4f28-b8bb-5d2d49d76e12
caps.latest.revision: 25
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="model-driven-app-managed-properties-for-views"></a>ビューのモデル駆動型管理プロパティ

<a name="BKMK_ManagedProperties"></a>   
 
 配布する管理ソリューションに含めるユーザー定義の共有ビューを PowerApps で作成する場合、ビューのカスタマイズからソリューションをインストールするユーザーの機能を制限することができます。  
  
 既定では、ほとんどのビューでは、ユーザーがカスタマイズできるように、**カスタマイズ可能**な管理プロパティが true に設定されています。 これを変更するもっともな理由がない場合は、ユーザーのアプリでビューをカスタマイズできるようにすることをお勧めします。  
  
## <a name="set-managed-properties-for-a-view"></a>ビューの管理プロパティの設定  
  
1.  [ソリューション エクスプローラー](advanced-navigation.md#solution-explorer)を開いて、**エンティティ** を展開し、目的のエンティティを選択して **ビュー** を選択します。  
  
2.  ユーザー定義共有ビューを選択します。  
  
3.  メニュー バーで、**その他の操作** > **管理プロパティ**を選択します。  

    > [!div class="mx-imgBorder"] 
    > ![管理プロパティ メニュー](media/managed-properties.png)
  
4.  **カスタマイズ可能** または **削除可能** オプションを **True** または **False** に設定できます。  

    > [!div class="mx-imgBorder"] 
    > ![管理プロパティの設定](media/set-managed-properties.png)
  
> [!NOTE]
> この設定は、ビューを管理ソリューションとして含むソリューションをエクスポートし、それを別の環境にインストールするまで有効にはなりません。  

## <a name="next-steps"></a>次のステップ
[ビューについて](create-edit-views.md)
