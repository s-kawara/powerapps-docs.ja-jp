---
title: 相互にレコードをリンクするための接続ロールを追加する |MicrosoftDocs
ms.custom: ''
author: mduelae
manager: kvivek
ms.service: powerapps
ms.component: pa-user
ms.topic: conceptual
ms.date: 8/01/2019
ms.author: mduelae
ms.reviewer: ''
ms.assetid: ''
search.audienceType:
- enduser
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: d824e76f6ffd5cc72f2f030f7009d3f4a140bf8a
ms.sourcegitcommit: d6b7f98b4ae011a753c1e72d7708f0f8dfbfb1fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69896260"
---
# <a name="add-a-connection-role-to-link-records-to-each-other"></a>相互にレコードをリンクするための接続ロールを追加する

[!INCLUDE [cc-beta-prerelease-disclaimer](../includes/cc-beta-prerelease-disclaimer.md)]

接続を使用すると、ユーザー、連絡先、見積もり、販売注文、およびその他の多くのエンティティレコードを相互に簡単に関連付けることができます。 関連付けのレコードには、リレーションシップの目的を定義するのに役立つ特定のロールを割り当てることができます。

これは、特定のレコードに対して複数の接続とロールを作成するための簡単な方法です。 たとえば、連絡先には、他の連絡先、アカウント、または契約との関係が多数存在する場合があります。 各リレーションシップにおいて、連絡先は異なるロールを持つ場合があります。

接続ロールは、接続に直接関連付けられます。 接続ロールを使用するには、まず、レコードに接続を追加する必要があります。

接続ロールを追加する前に、管理者が接続ロールを有効にする必要があります。詳細については、「[接続ロールを構成する](https://docs.microsoft.com/en-us/powerapps/maker/common-data-service/configure-connection-roles)」を参照してください。

1. 接続を追加または管理するには、営業案件のように管理するレコードを選択します。  
2. **[関連]** タブを選択し、 **[接続]** を選択します。 これにより、レコードの接続の一覧が表示された接続グリッドが開きます。

    > [!div class="mx-imgBorder"]
    > ![新しい接続ロールの追加](media/connection1.png "新しい接続ロールの追加") 

3. **[接続]** を選択し、**別**のまたは **[自分に]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![接続の種類の選択](media/connection2.png "接続の種類の選択") 
  
4. **[名前]** フィールドに、接続のレコードの名前を入力または検索します。

5. **[このロールフィールドとして]** 参照 アイコンを選択し、 **[新しい接続ロール]** を選択します。 または、検索を使用して、接続に関連付ける既存のロールを検索し、 **[保存]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![新しい接続ロールの選択](media/connection3.png "新しい接続ロールの選択")  

    > [!NOTE]
    > 新しい接続ロールを作成する前に情報を入力した場合は、キャンセルして接続を続行するかどうかを確認する警告ダイアログが表示されます。または、現在の作業中のレコードをそのまま使用することもできます。

6. 新しい接続ロールを作成するには、 **[新しい接続ロール]** 画面で名前を入力し、[**接続ロール] カテゴリ**を選択します。

    > [!div class="mx-imgBorder"]
    >  ![接続ロールカテゴリの追加](media/connection4.png "接続ロールカテゴリの追加") 

7. 終了したら、 **[保存 & 閉じる]** を選択します。

  
## <a name="manage-connection-roles"></a>接続ロールの管理

接続ロールを管理するには、接続エンティティから接続ロールを選択します。 これにより、接続ロールエンティティレコードが開きます。  名前を編集し、接続ロールカテゴリを選択して、説明を追加することができます。


   > [!div class="mx-imgBorder"]
   > ![接続ロールの編集](media/connection7.png "Editconnection ロール") 
  
接続ロールに関連付ける接続ロールの種類を管理することもできます。

1. 接続ロールを開き、コマンドの **[レコードの種類の管理]** を選択します。 

    > [!div class="mx-imgBorder"]
    > ![接続ロールの編集](media/connection5.png "Editconnection ロール") 
  

2. これにより、この接続ロールに追加または削除できる接続ロールの種類の一覧が表示されます。

    > [!div class="mx-imgBorder"]
    > ![レコードの種類の管理](media/connection6.png "レコードの種類の管理") 


