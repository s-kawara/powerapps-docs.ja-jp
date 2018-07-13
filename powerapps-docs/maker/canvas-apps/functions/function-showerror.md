---
title: ShowError 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の ShowError 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 06/05/2018
ms.author: gregli
ms.openlocfilehash: e9c0d85525ee8a067c903d59f459541a08a22d39
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39014790"
---
# <a name="notify-function-in-powerapps"></a>PowerApps の Notify 関数
バナー メッセージをユーザーに表示します。

## <a name="description"></a>説明
**Notify** 関数を使用すると、画面の上部に現在表示されている内容の上に重ねて、バナー メッセージがユーザーに表示されます。  

メッセージの種類に応じて適切な色とアイコンが使用されます。   種類は、関数の 2 つ目の引数で指定します。

| NotificationType 引数 | 説明 |
| --- | --- |
| **NotificationType.Error** | メッセージをエラーとして表示します。 |
| **NotificationType.Information** (既定) | メッセージを情報提供として表示します。  |
| **NotificationType.Success** | メッセージを成功として表示します。 |
| **NotificationType.Warning** | メッセージを警告として表示します。 |

アプリの作成中と、エンド ユーザーがアプリを使用しているときの両方でメッセージが表示されます。

**Notify** は、[動作の数式](../working-with-formulas-in-depth.md)内でのみ使用できます。

**Notify** は [**IfError**](function-iferror.md) 関数と組み合わせて、エラーを検出し、カスタム エラー メッセージを使って報告することができます。

PowerApps では、**Notify** と全く異なるメカニズムを使用してプッシュ通知を送信することもできます。  詳細については、「[PowerApps でプッシュ通知を送信する](../add-notifications.md)」を参照してください。

**Notify** は、常に *true* を返します。

注: この関数は、以前は **ShowError** という名前で、エラー メッセージのみを表示できました。

## <a name="syntax"></a>構文
**Notify**( *Message*, [ *NotificationType* ] )

* *Message* – 必須。  ユーザーに表示するメッセージです。
* *NotificationType* – 省略可能。  前述の表の表示できるメッセージの種類。  既定は **NotificationType.Information** です。  

## <a name="examples"></a>例

### <a name="step-by-step"></a>ステップ バイ ステップ

1. 画面に**ボタン** コントロールを追加します。

2. **Button** の **OnSelect** プロパティを次のように設定します。

    **Notify( "Hello, World" )**

3. ボタンをクリックするか、押します。  

    ボタンがクリックされるたびに、**Hello, World** というメッセージが情報提供としてユーザーに表示されます。

    ![作成環境で、Button.OnSelect により Notify が呼び出され、その結果ユーザーに対して青色のバナー メッセージで "Hello, World" のメッセージが表示されている図](media/function-showerror/hello-world.png)

4. エラーを示すようにメッセージの種類を変更します。  次の式に 2 つ目の引数を追加します。

    **Notify( "Hello, World", NotificationType.Error )**

5. ボタンをクリックするか、押します。

    これで、ボタンがクリックされるたびに、**Hello, World** というメッセージがエラーとしてユーザーに表示されます。

    ![作成環境で、Button.OnSelect により Notify が呼び出され、その結果ユーザーに対して赤色のバナー メッセージで "Hello, World" のメッセージが表示されている図](media/function-showerror/hello-world-error.png)

4. 警告を示すようにメッセージの種類を変更します。  次の式の 2 つ目の引数を変更します。

    **Notify( "Hello, World", NotificationType.Warning )**

5. ボタンをクリックするか、押します。

    これで、ボタンがクリックされるたびに、**Hello, World** というメッセージが警告としてユーザーに表示されます。

    ![作成環境で、Button.OnSelect により Notify が呼び出され、その結果ユーザーに対してオレンジ色のバナー メッセージで "Hello, World" のメッセージが表示されている図](media/function-showerror/hello-world-warning.png)

4. 成功を示すようにメッセージの種類を変更します。  次の式の 2 つ目の引数を変更します。

    **Notify( "Hello, World", NotificationType.Success )**

5. ボタンをクリックするか、押します。

    これで、ボタンがクリックされるたびに、**Hello, World** というメッセージが成功としてユーザーに表示されます。

    ![作成環境で、Button.OnSelect により Notify が呼び出され、その結果ユーザーに対して緑色のバナー メッセージで "Hello, World" のメッセージが表示されている図](media/function-showerror/hello-world-success.png)
