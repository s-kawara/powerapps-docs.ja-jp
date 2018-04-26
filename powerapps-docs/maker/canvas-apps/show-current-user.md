---
title: 現在のユーザーに関する詳細の表示 | Microsoft Docs
description: PowerApps にサインインしているユーザーの名前や電子メール アドレスを表示するには、User 関数を挿入します
documentationcenter: ''
author: lonu
manager: kfile
editor: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 10/16/2016
ms.author: lonu
ms.openlocfilehash: 11177ffa8913afe4d0245708dd8c9b2b0b50c8c2
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="show-information-about-a-powerapps-user"></a>PowerApps ユーザーに関する情報を表示する
サインイン ユーザーに関連付けられているフル ネーム、電子メール アドレス、写真は、User 関数で表示できます。 この情報を使用して自動的にフォームへの入力を行うことができます。

たとえば、この機能を使うと次のことができます。

* ユーザー用のサインアップ "シート" を作成する (トレーニング、イベントのボランティア、券売機での発券など)。
* 人事管理アプリでフル ネームを表示する。
* ヘルプデスクへの問い合わせ時に電子メール アドレスを自動的に入力する。

基本的にこの機能は、フォームやラベルの自動入力を活かすことができる部分であれば、どこにでも利用できます。

[!INCLUDE [app-customization-requirements](../../includes/app-customization-requirements.md)]

## <a name="show-user-details"></a>ユーザー情報を表示する
1. **[挿入]** タブの **[メディア]** をクリックまたはタップし、**[画像]** をクリックまたはタップします。
   
   ![][2]
2. **[Image](controls/properties-visual.md)** プロパティを次の数式に設定します。
   <br>**User().Image**
   
    ![][3]
3. **[挿入]** タブの **[テキスト]** をクリックまたはタップし、**[ラベル]** をクリックまたはタップします。  
   
    ![][4]
4. **[Text](controls/properties-core.md)** プロパティを次の数式に設定します。
   <br>**User().FullName**
   
   ![][6]
   
   これを実行すると、ラベルにフル ネームが自動的に設定されます。 次のように、ラベルをイメージ コントロールの下に移動します。
   
   ![][5]
5. 別のラベルを追加し、その **[Text](controls/properties-core.md)** プロパティを次の数式に設定します。
   <br>**User().Email**  
   
    ![][8]
   
    これを実行すると、ラベルに電子メール アドレスが自動的に設定されます。 このラベルを、次のように 1 つ目のラベルの下に移動します。  
   
    ![][7]

[2]: ./media/show-current-user/add-image.png
[3]: ./media/show-current-user/imageproperty.png
[4]: ./media/show-current-user/insertlabel.png
[5]: ./media/show-current-user/label.png
[6]: ./media/show-current-user/textproperty.png
[7]: ./media/show-current-user/secondlabel.png
[8]: ./media/show-current-user/email.png
[9]: ./media/show-current-user/preview.png
