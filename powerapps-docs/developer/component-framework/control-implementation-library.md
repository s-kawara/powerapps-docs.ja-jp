---
title: コンポーネント実装ライブラリ | Microsoft Docs
description: JavaScript や TypeScript を使用してカスタム コンポーネントを作成する
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5d100dc3-bd82-4b45-964c-d90eaebc0735
---

[!INCLUDE[cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

PowerApps コンポーネント フレームワークを使用してカスタム コンポーネントを開発する場合、コンポーネント ライブラリの実装は重要なステップのひとつです。 開発者は TypeScript を使用してコンポーネント ライブラリを実装できます。 各カスタム コンポーネントは、カスタム コンポーネント インタフェースに記述されたメソッドを実装したオブジェクトを返す、関数の定義を含むライブラリが必要です 

> [!IMPORTANT]
> - PowerApps コンポーネント フレームワークはプレビュー機能です。
> - [!INCLUDE[cc_preview_features_definition](../../includes/cc-preview-features-definition.md)] 
> - [!INCLUDE[cc_preview_features_no_MS_support](../../includes/cc-preview-features-no-ms-support.md)]

オブジェクトは次のメソッドを実装します:

- [init](reference/control/init.md) (必須)
- [updateView](reference/control/updateview.md) (必須)
- [getOutputs](reference/control/getoutputs.md) (オプション)
- [destroy](reference/control/destroy.md) (必須)

これらのメソッドはカスタム コンポーネントのライフサイクルを制御します。

