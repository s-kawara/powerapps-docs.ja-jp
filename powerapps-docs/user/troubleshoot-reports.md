---
title: レポートに表示されていないデータに関する問題のトラブルシューティング |Microsoft Docs
description: レポートに表示されていないデータに関する問題のトラブルシューティング
author: mduelae
manager: kvivek
ms.service: powerapps
ms.component: pa-user
ms.topic: conceptual
ms.date: 06/27/2019
ms.author: mkaur
ms.custom: ''
ms.reviewer: ''
ms.assetid: ''
search.audienceType:
- enduser
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 1156aa8fb5fbc3ae51c21b8aa41606df6dbc2e86
ms.sourcegitcommit: e9671e018c1ee4b640528915350a367758991b6a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67420768"
---
# <a name="troubleshoot-problems-with-data-not-displaying-in-a-report"></a>レポートに表示されていないデータに関する問題のトラブルシューティング

レポートに含まれるはずのデータが表示されない理由はいくつか考えられます。  
  
- **セキュリティのアクセス許可が不十分**です。 レコードを表示するためのアクセス許可が Common Data Service にない場合は、レポートに表示されません。  
  
- **データが入力されていません。** データを入力するユーザーは、左側のフィールドを空にすることができます。  
  
- **データがレポートの条件と一致しません。** 多くのレポートには、アクティブなレコードのみを表示する既定のフィルターが含まれています。または、一致するレコードがない条件を選択している可能性があります。 レポートフィルターを変更してみてください。 詳細については、「[レポートの既定のフィルターを編集](edit-report-filter.md)する」を参照してください。  
  
- **キャッシュされたレポートのコピーを表示している可能性があります。** 既定では、レポートを実行するたびに、Common Data Service レポート内のデータがデータベースからプルされます。 ただし、システム管理者が、キャッシュから実行するようにレポートを変更した可能性があります。 最近入力したデータがレポートに含まれていない場合は、古いバージョンのレポートがキャッシュから取得されている可能性があります。 レポートを更新するには、レポート ツールバーの **更新** ボタンをクリックします。  
  
- **サブレポートのレコードを読み取るためのアクセス許可がない可能性があります。** サブレポートに含まれているレコードの種類を読み取るアクセス許可がない場合は、サブレポートを表示できなかったというエラーメッセージが表示されます。  
  
- **Microsoft Internet Explorer のプライバシー設定によって、必要な cookie がブロックされる可能性があります。** グラフレポートの場合、グラフが表示されるのではなく、赤い文字の X が表示されていると、プライバシー設定によって、グラフコントロールに必要な cookie がブロックされている可能性があります。 この問題を解決するには、ブラウザーで Reporting Services を実行しているサーバーの cookie を有効にします。  
  

### <a name="see-also"></a>関連項目
[レポートの操作](work-with-reports.md) 

[レポートウィザードを使用してレポートを作成する](create-report-with-wizard.md)

[既存のレポートを追加する](add-existing-report.md)

[レポートフィルターの編集](edit-report-filter.md)

