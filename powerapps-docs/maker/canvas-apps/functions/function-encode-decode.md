---
title: EncodeUrl および PlainText 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の EncodeUrl および PlainText 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 9956332c35b4df2773b2634cb7f66d2ea96469e4
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61551056"
---
# <a name="encodeurl-and-plaintext-functions-in-powerapps"></a>PowerApps の EncodeUrl および PlainText 関数
文字列をエンコードおよびデコードします。

## <a name="description"></a>説明
**EncodeUrl**関数 % と 16 進数を特定の英数字以外の文字に置き換えて、URL 文字列をエンコードします。  

**プレーン テキスト**関数は、特定のタグを適切な記号を次のように変換する、HTML および XML のタグを削除します。

* **&amp;nbsp;**
* **&amp;quot;**

これらの関数からの戻り値は、エンコードまたはデコードされた文字列です。 この関数は、すべての HTML および XML タグを削除しません。 

## <a name="syntax"></a>構文
**EncodeUrl**( *String* )

* *String* - 必須。  エンコードする URL。

**PlainText**( *String* )

* *String* - 必須。 HTML および XML タグが削除される文字列。

## <a name="examples"></a>例
テキスト ギャラリーに RSS フィードを表示し、そのギャラリーのラベルの **[Text](../controls/properties-core.md)** プロパティを **ThisItem.description** に設定した場合、ラベルには次の例のように未加工の HTML または XML コードが表示される可能性があります。

    <p>We have done an unusually&nbsp;&quot;deep&quot; globalization and localization.<p>

ラベルの **[Text](../controls/properties-core.md)** プロパティを **PlainText(ThisItem.description)** に設定すると、次の例のようなテキストが表示されます。

    We have done an unusually "deep" globalization and localization.
