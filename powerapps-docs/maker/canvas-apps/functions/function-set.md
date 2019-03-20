---
title: Set 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Set 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 06/29/2017
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 3292d03a55fe6296b8efdf2377efde5f2b4ad36e
ms.sourcegitcommit: 676cfa415f67e2e8fcfcf30fab83fc118a6f3210
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2019
ms.locfileid: "57800493"
---
# <a name="set-function-in-powerapps"></a>PowerApps の Set 関数
グローバル変数の値を設定します。

## <a name="overview"></a>概要
**Set** 関数を使用すると、グローバル変数の値を設定できます。グローバル変数とは、ユーザーがボタンを押した回数やデータ操作の結果など、一定の情報を一時的に格納する際に使用する変数です。  

グローバル変数はお使いのアプリ全体で、どの画面でも利用できます。 グローバル変数は最も単純な種類の変数であり、たいていの状況でニーズを満たせます。 単一の画面でのみスコープをもつコンテキスト変数や行レベルでテーブルを変更できるコレクションもあります。 これらのオプションの詳細については、確認[変数について](../working-with-variables.md)します。

PowerApps では基本的に、ユーザーがアプリを操作すると、数式が自動的に再計算されます。 変更時に、変数に依存するすべての数式が自動的に更新します。 ただし、変数で、数式の値が使用されている場合に自動的に更新するしません、**設定**関数の変更。 これには、変数は、エラーが発生しやすいと他のユーザーが理解が困難にすることができますを手動で更新するアプリ メーカーが必要です。 変数を使用する前に確認して[変数について](../working-with-variables.md)します。

## <a name="description"></a>説明
グローバル変数は **Set** 関数を使用して暗黙的に作成されます。 明示的に宣言する必要はありません。 すべて削除した場合、**設定**グローバル変数の関数は、そのグローバル変数は存在しなくなります。 変数をクリアするには、結果にその値を設定、 [**空白**関数](function-isblank-isempty.md)します。

変数の値、定義、および 変数の表示を使用して確認できます、**ファイル**PowerApps Studio のメニュー。

具体例はこのトピックで後ほど紹介しますが、グローバル変数には以下をはじめとするさまざまな情報を格納できます。

* 単一の値
* レコード
* テーブル
* オブジェクト参照
* 数式の結果

アプリが終了するまで、グローバル変数の値は保持されます。  アプリを終了すると、グローバル変数の値は失われ、アプリが再び読み込みされたときに再作成されます。

グローバル変数には既存のコレクションやコントロールと同じ名前は使用できません。  同じ名前がコンテキスト変数として使用されることがあります。  この 2 つの間の曖昧さを解消するには、[曖昧性除去演算子](operators.md#disambiguation-operator)を使用します。

**Set** には戻り値がないため、[動作の数式](../working-with-formulas-in-depth.md) の中でのみ使用できます。

## <a name="syntax"></a>構文
**Set**( *VariableName*, *Value* )

* *VariableName* - 必須。  作成または更新するグローバル変数の名前。
* *Value* - 必須。  コンテキスト変数に割り当てる値。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Set(&nbsp;Counter,&nbsp;1&nbsp;)** |グローバル変数 **Counter** を作成または変更し、その値を **1** に設定します。 |**Counter** に値 **1** が設定されます。 この変数は、数式に **Counter** という名前を使用することで、どの画面からでも参照できます。 |
| **Set(&nbsp;Counter,&nbsp;2&nbsp;)** |前の例のグローバル変数 **Counter** の値を **2** に設定します。 |**Counter** に値 **2** が設定されます。 |
| **Set(&nbsp;Counter,&nbsp;Counter + 1&nbsp;)** |前の例のグローバル変数 **Counter** の値を **3** に増やします。 |**Counter** に値 **3** が設定されます。 |
| **Set(&nbsp;Name,&nbsp;"Lily" )** |グローバル変数 **Counter** を作成または変更し、その値を **Lily** に設定します。 |**Name** に値 **Lily** が設定されます。 |
| **Set(&nbsp;Person,&nbsp;{&nbsp;Name:&nbsp;"Milton", Address:&nbsp;"1&nbsp;Main&nbsp;St"&nbsp;} )** |グローバル変数 **Person** を作成または変更し、その値をレコードに設定します。 このレコードには、**Name** と **Address** の 2 つの列が存在します。 **Name** 列の値は **Milton**、**Address** 列の値は **1 Main St** です。 |**Person** にレコード **{&nbsp;Name:&nbsp;"Milton", Address:&nbsp;"1&nbsp;Main&nbsp;St"&nbsp;}** の値が設定されます。<br><br>このレコード全体を参照する場合には、名前 **Person** を使用します。このレコードの個別の列を参照する場合には、**Person.Name** または **Person.Address** を使用します。 |
| **Set(&nbsp;Person, Patch(&nbsp;Person,&nbsp;{Address:&nbsp;"2&nbsp;Main&nbsp;St"&nbsp;}&nbsp;)&nbsp;)** |**[Patch](function-patch.md)** 関数を操作してグローバル変数 **Person** の **Address** 列の値を **2 Main St** に更新します。 |**Person** にレコード **{&nbsp;Name:&nbsp;"Milton", Address:&nbsp;"2&nbsp;Main&nbsp;St"&nbsp;}** の値が設定されます。 |

