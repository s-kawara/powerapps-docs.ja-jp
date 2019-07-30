---
title: 活動とタイムライン ウォールに関してよく寄せられる質問 | MicrosoftDocs
ms.custom: ''
author: mduelae
manager: kvivek
ms.service: powerapps
ms.component: pa-user
ms.topic: conceptual
ms.date: 01/29/2019
ms.author: mduelae
ms.reviewer: ''
ms.assetid: ''
search.audienceType:
- enduser
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 08859f70e047d1c53379e8a79f56997d6beedc58
ms.sourcegitcommit: 982cab99d84663656a8f73d48c6fae03e7517321
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67456987"
---
# <a name="frequently-asked-questions-about-activities-and-the-timeline-wall"></a>活動とタイムライン ウォールに関してよく寄せられる質問  

## <a name="is-a-title-required-when-adding-a-new-note"></a>新しいメモを追加するときにタイトルは必要ですか?

No. 活動にメモを追加するときにタイトル フィールドが必須フィールドとしてマークされますが、必要ありません。 これは従来の Web クライアントにおける既知の問題です。

## <a name="for-an-appointment-when-i-choose-the-option-to-save-as-draft-it-doesnt-show-that-the-appointment-has-been-saved-as-a-draft"></a>予定に対して "*下書きとして保存*" オプションを選択しても、予定が下書きとして保存されたことが表示されません。

従来の Web クライアントで予定を下書きとして保存しても、予定が下書きとして保存されたことを示す **[下書き]** はタイトルに表示されません。

## <a name="can-i-add-activities-to-read-only-records"></a>読み取り専用レコードに活動を追加できますか?

はい。 メモ、通話、タスクなどを始めとする読み取り専用のエンティティには、活動を追加できます。 

## <a name="are-html-tags-supported-in-notes"></a>**[メモ]** 内で HTML タグはサポートされていますか?

No. レコードやエンティティに対してメモのアクティビティを作成する場合、HTML タグはサポートされません。 たとえば、メモフィールドにを`<TAG> </TAG>`追加すると、として`<TAG_XXX="XX"> </TAG>`表示されます。

## <a name="how-can-i-improve-performance-on-timeline-wall"></a>タイムライン ウォール上のパフォーマンスを向上させる方法を教えてください

特定のエンティティ レコードによって返されるデータの量を最適化することによって、タイムライン ウォールのパフォーマンスを向上させることができます。 

1.  使用中の活動のみを表示するようにエンティティ フォームを構成します。  有用な活動のみを表示するように、これをフォーム レベルで実行できます。  たとえば、ケース用のタスクを使わない場合は、タスクを表示しないようにケースのフォーム上のタイムライン ウォールを構成できます。
2.  タイムライン ウォールによって表示される既定のレコードの数を減らします。  これは既定で 10 を返すように設定されていて、10 を超えるとパフォーマンスの問題が発生する場合があります。  既定値を超えないようにすることをお勧めします。 

## <a name="activity-wall-is-not-supported-in-print-preview"></a>印刷プレビューで活動ウォールがサポートされていません。

Dynamics 365 で **[印刷プレビュー]** オプションを選択した場合、利用可能なリスト内に **[Timeline Wall]\(タイムライン ウォール\)** は表示されません。 **[メモ]** は表示されますが、タスクやメールは表示されません。





