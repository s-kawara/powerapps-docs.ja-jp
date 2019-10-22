---
ms.openlocfilehash: 29226cfe8ab5c0ad01b785cfdaeec2e12a230dd7
ms.sourcegitcommit: ad203331ee9737e82ef70206ac04eeb72a5f9c7f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2019
ms.locfileid: "67225342"
---
[Azure Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-overview/) に接続するために Social Engagement を有効にすると、オートメーション ルールを使用してソーシャル データをイベント ハブにストリーミングできます。 Azure Event Hubs には、Social Engagement からストリーミングされたソーシャル データが[事前構成された期間](https://azure.microsoft.com/documentation/articles/event-hubs-availability-and-support-faq/)格納されます。イベント ハブをリッスンできるすべてのアプリケーションがこのデータにアクセスしたり、格納および処理することができるようになります。  
  
 なお、Social Engagement から送信されるデータとは、ソーシャル投稿 (作成者とテキスト) や、言語、場所、センチメント、タグなどの付加情報などです。イベント ハブに送信されるソーシャル投稿のコンテンツの詳細については、[JSON スキーマの定義](http://go.microsoft.com/fwlink/p/?LinkId=786643)に関する記事を参照してください。