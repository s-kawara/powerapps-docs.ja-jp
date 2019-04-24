---
title: Select 関数 | Microsoft Docs
description: 構文を含む PowerApps の Select 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 06/11/2018
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 74584e5855c6c72c619b4baefc2652f9ccc68997
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61520678"
---
# <a name="select-function-in-powerapps"></a>PowerApps の Select 関数
コントロールでの選択アクションをシミュレートし、**OnSelect** 式の評価を実行させます。

## <a name="description"></a>説明
**Select** 関数では、ユーザーがコントロールをクリックまたはタップしたかのように、コントロールでの選択アクションをシミュレートします。 その結果、対象のコントロールでの **OnSelect** 式が評価されます。

**Select** を使用して、選択アクションを親コントロールに伝達します。 この種類の伝達は、ギャラリーなどでの既定の動作です。 既定では、**[ギャラリー](../controls/control-gallery.md)** コントロールのすべてのコントロールの **OnSelect** プロパティは **Select( Parent )** に設定されています。 この方法では、ギャラリー コントロール自体の **OnSelect** プロパティの値を設定でき、ユーザーがギャラリーのどこをクリックまたはタップしたかにかかわらず、その式が評価されます。

ギャラリー内の 1 つまたは複数のコントロールでギャラリー自体とは異なるアクションを実行させる場合、そのコントロールの **OnSelect** プロパティを規定値以外に設定します。 ギャラリー自体と同じアクションを実行させる場合は、ギャラリー内のほとんどのコントロールの **OnSelect** プロパティを規定値のままにすることができます。

**Select** は、後の処理のために対象の **OnSelect** をキューに入れます。この動作は現在の式の評価が完了した後で行われる場合があります。 **Select** によって **OnSelect** がすぐに評価されたり、**Select** が **OnSelect** の評価の完了まで待機したりすることはありません。

**Select** は、ギャラリーやフォームなどのコンテナー コントロールの境界を超えることはできません。 コンテナー コントロール内のコントロールを対象にできるのは、同じコンテナー コントロール内にある式の **Select** 関数のみです。 画面をまたいで **Select** を使用することはできません。

**Select** は、**OnSelect** プロパティを持つコントロールと共にのみ使用できます。

**Select** は、[動作の数式](../working-with-formulas-in-depth.md)内でのみ使用できます。

コントロールが直接、または他のコントロールを通じて間接的に、自身を **Select** することはできません。

## <a name="syntax"></a>構文
**Select**( *Control* )

* *Control* – 必須。  ユーザーの代理として選択するコントロール。

## <a name="examples"></a>例

#### <a name="basic-usage"></a>基本的な使用方法

1. **[Button](../controls/control-button.md)** コントロールを追加し、別の名前になっている場合は **Button1** に名前を変更します。

1. **Button1** の **OnSelect** プロパティを次の数式に設定します。

    **Notify( "Hello World" )**

1. 同じ画面で、2 つ目の **Button** コントロールを追加し、その **OnSelect** プロパティを次の数式に設定します。

    **Select( Button1 )**

1. Alt キーを押しながら 2 つ目のボタンを選択します。

    通知がアプリケーションの上部に表示されます。 この通知を生成したのは、**Button1** の **OnSelect** プロパティです。

    ![2 つのボタンの OnSelect プロパティの設定と、2 つ目のボタンがクリックされたときの通知を示すアニメーション](media/function-select/basic-select.gif)

#### <a name="gallery-control"></a>ギャラリー コントロール

1. 他のコントロールを含む垂直方向の**[ギャラリー](../controls/control-gallery.md)** コントロールを追加します。

    ![コントロールを含む垂直方向のギャラリーを選択します](media/function-select/select-gallery.png)

2. ギャラリーの **OnSelect** プロパティを次の式に設定します。
 
    **Notify( "Gallery Selected" )**

3. Alt キーを押しながら、ギャラリーの背景かギャラリー内のコントロールをクリックまたはタップします。

    すべてのアクションで、アプリケーションの上部に **Gallery Selected** 通知が表示されます。

    ギャラリーの **OnSelect** プロパティを使用して、ユーザーがギャラリーの項目をクリックまたはタップしたときに実行する既定のアクションを指定します。

5. イメージ コントロールの **OnSelect** プロパティを次の式に設定します。

    **Notify( "Image Selected", Success )**

6. Alt キーを押しながら、ギャラリーのさまざまな要素をクリックまたはタップします。

    イメージ以外のギャラリーのコントロールをクリックまたはタップすると、前と同様に **Gallery Selected** が表示されます。 イメージをクリックまたはタップすると、**Image Selected** が表示されます。
 
    ギャラリーで個々のコントロールを使用して、ギャラリーの既定のアクションとは異なるアクションを実行させます。

    ![ギャラリー コントロールの OnSelect プロパティの規定値と、異なるアクションを実行するコントロールを示すアニメーション](media/function-select/gallery-select.gif)
