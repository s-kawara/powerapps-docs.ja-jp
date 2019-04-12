---
title: Download、Launch、および Param 関数 | Microsoft Docs
description: 構文と例については、の Download、Launch、および Param 関数のキャンバス アプリを含む参照情報
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
ms.openlocfilehash: 4a53d8c20bd4b7784cb94daa574682c041f104ea
ms.sourcegitcommit: b316e0eee9946ef09e0512577ce2d11cd27aa864
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2019
ms.locfileid: "59508311"
---
# <a name="download-launch-and-param-functions-in-canvas-apps"></a>キャンバス アプリでの download、Launch、および Param 関数
パラメーターを使用して、Web ページまたはアプリをダウンロードまたは起動します。  

## <a name="description"></a>説明
**Download** 関数は、Web からローカル デバイスにファイルをダウンロードします。 ユーザーは、ファイルを保存する場所の入力を求められます。  **Download** は、ファイルが格納されているローカルの場所を文字列として返します。  

**Launch** 関数は、Web ページまたはアプリを起動します。  この関数では、必要に応じて、アプリにパラメーターを渡すことができます。

Internet Explorer と Microsoft Edge、**起動**関数は、web サイトまたはそのセキュリティ設定が同じ場合にのみ、または関数を含むアプリのものよりもアプリが表示されます。 たとえば、追加する場合は、**起動**関数で実行されるアプリを**信頼済みサイト**セキュリティ ゾーン、web サイトまたはアプリを開く関数がであることを確認、**信頼済みサイト**または**ローカル イントラネット**ゾーン (ではなく**制限付きサイト**)。 詳細情報:[Internet Explorer 11 のセキュリティとプライバシーの設定を変更](https://support.microsoft.com/en-us/help/17479/windows-internet-explorer-11-change-security-privacy-settings)します。  

**Param** 関数は、アプリに渡されたパラメーターをアプリの起動時に取得します。 名前付きパラメーターが渡されていなかった場合、**Param** は "*空白*" を返します。

## <a name="syntax"></a>構文
**Download**( *Address* )

* *Address* - 必須。  ダウンロードする Web リソースのアドレス。

**Launch**( *Address* [, *ParameterName1*, *ParameterValue1*, ... ] )

* *Address* - 必須。  起動する Web ページのアドレスまたはアプリの ID。
* *ParameterName(s)* - 省略可能。  パラメーター名。
* *ParameterValue(s)* - 省略可能。  アプリまたは Web ページに渡す、対応するパラメーター値。

**Param**( *ParameterName* )

* *ParameterName* - 必須。  アプリに渡されるパラメーターの名前。

