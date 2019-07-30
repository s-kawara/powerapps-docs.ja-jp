---
title: モデル駆動型アプリでのナビゲーションの基本 | MicrosoftDocs
author: mduelae
manager: kvivek
ms.service: powerapps
ms.component: pa-user
ms.topic: conceptual
ms.date: 11/16/2018
ms.author: mkaur
ms.reviewer: ''
ms.assetid: ''
search.audienceType:
- enduser
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: e563c1b17e7ef7628efcf51be2a312d3083bf187
ms.sourcegitcommit: 483c777a1537ccab6a2a2da6a5d1fe4470dd0e7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2019
ms.locfileid: "61530936"
---
#  <a name="basic-navigation-in-a-model-driven-app"></a>モデル駆動型アプリでのナビゲーションの基本 

モデル駆動型アプリで作業領域に移動したり、新しいレコードを作成したり、検索したり、他のタスクを実行したりするにはナビゲーション バーを使用します。

> [!div class="mx-imgBorder"]
> ![モデル駆動型アプリでのナビゲーション](media/nav.png "モデル駆動型アプリでのナビゲーション")

1. このサイト マップは、既定で拡大され維持されます。
2. 現在使用しているサブ領域は、アプリのどの部分に現在いるのかを示すために、強調表示されます。
3. **最近**のアイテムと**ピン留め**されたアイテムは、簡単にアクセスできるように上部にあります。 
4. アプリを切り替えるには、領域スイッチャーを使用します。
5. コマンド バー上のアイコンは、コマンド間の違いを表すために違う色になっています。
  
## <a name="get-back-to-recent-records-items-or-view"></a>最近のレコード、アイテムまたはビューに戻る
ユーザーは、大半の時間、同じレコードで作業します。 たとえば、常に同じ連絡先やアカウントにアクセスします。 また、同じデータの一覧 (ビュー) を何度も使用します。 サイト マップを使用すると、最近使用したレコードやビューにすぐに戻ることができます。 また、レコードやビューをピン留めして、探しやすくすることも可能です。 
  
1. **[サイト マップ]** から **[最近]** を選択します。
  
2. **[最近]** から再度使用するレコード、アイテム、ビューを選択します。 

## <a name="pin-records-items-or-view"></a>レコード、アイテムまたはビューをピン留めする

1. **[サイト マップ]** から **[最近]** を選択し、最近アクセスしたアイテムの一覧を展開します。
2. 最近の一覧でアイテムの横のピン留めアイコンを選択すると、それがピン留めされた一覧に追加されます。

   > [!div class="mx-imgBorder"]
   > ![ピン留めされたレコード](media/pinnedrecords.png "ピン留めされたレコード")

## <a name="unpin-records-items-or-view"></a>レコード、アイテム、またはビューのピン留めを解除する

1. **[サイト マップ]** から **[ピン留め]** を選択し、ピン留めされたアイテムの一覧を展開します。
2. アイテムの横のピン留め解除のアイコンを選択すと、一覧からそれが削除されます。  

   > [!div class="mx-imgBorder"]
   > ![レコードのピン留めの解除](media/unpinnedrecords.png "レコードのピン留めの解除")

## <a name="record-set-navigation"></a>レコードのセットのナビゲーション 
事前設定されたビューとクエリを使用して、複数のレコード間を移動できます。 レコードを使用したナビゲーションでは、作業一覧を失うことなく、一覧のレコード間を移動し、元に簡単に戻ることができるので、ユーザーの生産性が高まります。

> [!div class="mx-imgBorder"]
> ![レコード セットのナビゲーション](media/recordset.png "レコード セットのナビゲーション")

## <a name="reference-panel"></a>参照パネル
参照パネルは、使用している画面から移動せずに、作業を終えられる優れた方法です。 別の画面に移動せずに、参照しているレコードのコンテキスト内で、ケースやアカウントの機会など、その他の関連するものを参照できます。

> [!div class="mx-imgBorder"]
> ![参照パネル](media/reference-panel.png "参照パネル")

 [参照] パネルの詳細については、次のビデオをご覧ください。

<div class="embeddedvideo"><iframe src="https://www.microsoft.com/en-us/videoplayer/embed/d8224c3f-6e20-4b8e-9d0d-b0f5602c7708" frameborder="0" allowfullscreen=""></iframe></div>

## <a name="notifications"></a>通知 

フォームには、情報提供、警告およびエラーの 3 種類の通知が表示されます。 通知は常にヘッダーの真上のフォームの上部にあります。

以下に示す通知は、バージョン 9.1.9.3010 のものです。

![通知の例](media/notifications.png "通知の例")

通知が 1 つのみある場合は、行が 1 つ表示されます。

![通知が 1 つの場合の例](media/single_notification.png "通知が 1 つの場合の例")

通知が 2 つ以上ある場合は、通知の数が表示されます。 各メッセージを表示するには、シェブロンを選択します。

![通知が複数の場合の例](media/multiple_notification.png "通知が複数の場合の例")



