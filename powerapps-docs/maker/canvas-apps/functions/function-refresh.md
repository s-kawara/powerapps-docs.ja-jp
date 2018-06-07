---
title: Refresh 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Refresh 関数の参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 10/21/2015
ms.author: gregli
ms.openlocfilehash: 9ec2711c4a38f26fec2d44681b2606b4a8ecba29
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31825374"
---
# <a name="refresh-function-in-powerapps"></a>PowerApps の Refresh 関数
[データ ソース](../working-with-data-sources.md)の[レコード](../working-with-tables.md#records)を更新します。

## <a name="description"></a>説明
**Refresh** 関数は、データ ソースの新しいコピーを取得します。  他のユーザーが加えた変更が表示されます。

**Refresh** には戻り値が存在せず、[動作の数式](../working-with-formulas-in-depth.md)内でのみ使用できます。

## <a name="syntax"></a>構文
**Refresh**( *DataSource* )

* *DataSource* – 必須。 更新するデータ ソース。

## <a name="example"></a>例
この例では、**IceCream** という名前のデータ ソースを更新します。このデータ ソースは次のデータから始まります。

![](media/function-refresh/icecream.png)

別のデバイスのユーザーが、**Strawberry** レコードの **Quantity** を **400** に変更します。  この数式が実行されるまで、この変更は表示されません。

**Refresh( IceCream )**

その数式が実行された後、**IceCream** データ ソースにバインドされたギャラリーに、**Strawberry** の更新後の値が表示されます。

![](media/function-refresh/icecream-after.png)

