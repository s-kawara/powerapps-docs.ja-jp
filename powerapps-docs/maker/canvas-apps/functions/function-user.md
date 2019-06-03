---
title: User 関数 | Microsoft Docs
description: 構文を含む PowerApps の User 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2016
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: f452fedfbb26394bcaf4d490fa608f066469fb53
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61544573"
---
# <a name="user-function-in-powerapps"></a>PowerApps の User 関数
現在のユーザーに関する情報を返します。

## <a name="description"></a>説明
**User** 関数は現在のユーザーに関する情報の[レコード](../working-with-tables.md#records)を返します。

| プロパティ | 説明 |
| --- | --- |
| **User().Email** |現在のユーザーの電子メール アドレス。 |
| **User().FullName** |姓名を含む、現在のユーザーのフル ネーム。 |
| **User().Image** |現在のユーザーの画像。 これは、フォーム "blob:*identifier*" の画像の URL になります。 **[画像](../controls/control-image.md)** コントロールの **[Image](../controls/properties-visual.md)** プロパティをこの値に設定し、アプリで画像を表示します。 |

> [!NOTE]
> 返される情報は、現在の PowerApps ユーザーについての情報です。  この情報は、作成したアプリの外部にある PowerApps プレイヤーと PowerApps Studio に表示される "アカウント" 情報と一致します。  これは、Office 365 または他のサービスの現在のユーザーの情報とは一致しない場合があります。

## <a name="syntax"></a>構文
**User**()

## <a name="examples"></a>例
現在の PowerApps ユーザーには、次の情報があります。

* 完全名: **"John Doe"**
* メール アドレス: **"john.doe@contoso.com"**
* 画像: ![](media/function-user/john-doe-picture.png) 

|       数式       |                                                                    説明                                                                    |                                                 結果                                                  |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
|     **User()**      |                                             現在の PowerApps ユーザーについてのすべての情報のレコード。                                             |    { FullName:&nbsp;"John Doe", Email:&nbsp;"john.doe@contoso.com", Image:&nbsp;"blob:1234...5678" }    |
|  **User().Email**   |                                                 現在の PowerApps ユーザーの電子メール アドレス。                                                  |                                         "john.doe@contoso.com"                                          |
| **User().FullName** |                                                   現在の PowerApps ユーザーのフル ネーム。                                                    |                                               "John Doe"                                                |
|  **User().Image**   | 現在の PowerApps ユーザーの画像の URL。  **画像**コントロールの **Image** プロパティをこの値に設定し、アプリで画像を表示します。 | "blob: 1234... 5678"<br><br>**ImageControl.Image** を使用:<br>![](media/function-user/john-doe-picture.png) |

