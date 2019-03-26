---
title: 非アクティブ化または無効化されたカスタマイズを削除 | MicrosoftDocs
description: 非アクティブ化または無効化されたカスタマイズは、ソリューション管理を改善するため、および古いコンポーネントを使用または管理するリスクを減らすためにソリューションから削除されます。
services: ''
suite: powerapps
documentationcenter: na
author: jowells
manager: austinj
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 1/15/2019
ms.author: jowells
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="remove-deactivated-or-disabled-customizations"></a>非アクティブ化または無効化されたカスタマイズを削除

**カテゴリ**: 保守性、サポート

**影響の可能性**: 低い

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

非アクティブ化または無効化されたカスタマイズは、ソリューション管理を改善するため、および古いコンポーネントを使用または管理するリスクを減らすためにソリューションから削除されます。

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

非アクティブ化または無効化された各ソリューション コンポーネントが、意図してそのようにされたことを確認します。  意図して行われたもので、今後利用しない場合は、ユーザーおよびシステム カスタマイザーが混乱しないようにソリューションから削除することを検討してください。 これらのコンポーネントには、以下のものが含まれます:

- SDK メッセージ処理手順
- プロセス
- レコード作成および更新ルール
- SLA

以下のようなエンティティ コンポーネントも含まれます:

- フォーム
- [ビュー]
- 業務ルール

![非アクティブ化されたプロセス](../media/deactivated-processes.png)

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

[モデル駆動型アプリの業務ルールおよびフローによるカスタム ビジネス ロジックの適用](/powerapps/maker/model-driven-apps/guide-staff-through-common-tasks-processes)<br />
[モデル駆動型アプリのフォームとグリッド内のイベント](/powerapps/developer/model-driven-apps/clientapi/events-forms-grids)<br/>