---
ms.openlocfilehash: 7b0f9ce710887c870d22a6362f9cd28245d72519
ms.sourcegitcommit: d87b2068a63e416e2814791328a3a47bbcb5bb48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "62090770"
---
## <a name="delegation"></a>委任
可能であれば、PowerApps ではフィルターおよび並べ替え操作をデータ ソースに委任し、必要に応じて結果をページ送りします。 たとえば、データが入力された **[ギャラリー](../maker/canvas-apps/controls/control-gallery.md)** コントロールが表示されるアプリを起動すると、最初に先頭のレコード セットだけがデバイスに取り込まれます。 ユーザーがスクロールすると、データ ソースから追加のデータが取得されます。 その結果、アプリの起動が速くなり、非常に大規模なデータ セットにすばやくアクセスできます。

ただし、常に委任できるとは限りません。 委任をサポートしている関数と演算子は、データ ソースによって異なります。 数式の完全委任が不可能な場合は、作成時に、委任できない部分に警告が表示されます。 可能であれば、数式を変更して、委任できない関数や演算子を使用しないようにすることを検討してください。  [委任の一覧](../maker/canvas-apps/delegation-list.md)には、委任できるデータ ソースと操作の詳細が記載されています。

委任できない場合、PowerApps では、少数のレコード セットのみを取り込んで、ローカルで処理します。 フィルター関数と並べ替え関数は、削減されたレコード セットを操作します。 **[ギャラリー](../maker/canvas-apps/controls/control-gallery.md)** で使用できるデータが完全でないため、ユーザーが混乱する可能性があります。 

詳細については、[委任の概要](../maker/canvas-apps/delegation-overview.md)に関する記事を参照してください。

