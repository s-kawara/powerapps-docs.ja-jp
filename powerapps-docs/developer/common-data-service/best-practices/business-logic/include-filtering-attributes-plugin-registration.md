---
title: プラグイン登録にフィルター属性を含める | MicrosoftDocs
description: フィルター属性がプラグイン登録ステップで設定されていないと、そのイベントに更新メッセージが発生するたびにプラグインが実行します。
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
# <a name="include-filtering-attributes-with-plug-in-registration"></a>プラグイン登録にフィルター属性を含める

**カテゴリ**: パフォーマンス

**影響の可能性**: 中程度

<a name='symptoms'></a>

## <a name="symptoms"></a>現象

フィルター属性がプラグイン登録ステップで設定されていないと、そのイベントに更新メッセージが発生するたびにプラグインが実行します。  フィルタ属性なしと自動保存機能の組み合わせは、不必要なプラグインの実行を招き、望ましくない動作を引き起こしパフォーマンスを低下させる可能性があります。

<a name='guidance'></a>

## <a name="guidance"></a>ガイダンス

エンティティの更新メッセージに登録されたプラグインのほとんどは、すべての更新で実行する必要はありません。 通常は、特定の属性または属性が変更されたときに、特定のロジックを処理するだけで済みます。 環境内での余分な処理を防ぎ、プラグインおよびすべての更新ができるだけ早く完了するよう必要なロジックを最小限に抑えるためには、プラグイン ステップの登録に更新メッセージのフィルター属性も含めることを強く推奨します。

![フィルター属性のプラグイン登録ステップ](../media/plugin-registration-step-with-filtering-attributes.png)

<a name='additional'></a>

## <a name="additional-information"></a>追加情報

フィルター属性は、変更時にプラグインを実行させるエンティティ属性のリストです。  これらの属性は、プラグイン登録ツールを使用してプラグインを登録するときに設定できます。 属性が設定されていない場合、プラグインは更新メッセージが発生するたびに実行します。 更新は、さまざまな理由で発生します。 自動保存が環境でオンになっていると、エンティティ フォームでオンのときユーザーのセッション中に複数回発生する可能性があります。 フィルター属性が指定されていない場合、プラグインは設計されているエンティティのあらゆる属性の変更に対して実行されます。

<a name='seealso'></a>

### <a name="see-also"></a>関連項目

[プラグインの登録](../../register-plug-in.md)
[モデル駆動型のアプリで自動保存を無効にする](/powerapps/maker/model-driven-apps/manage-auto-save)