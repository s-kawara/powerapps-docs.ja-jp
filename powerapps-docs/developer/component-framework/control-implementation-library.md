---
title: コンポーネント実装ライブラリ |Microsoft Docs
description: JavaScript または TypeScript を使用してコードコンポーネントを作成する
keywords: ''
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5d100dc3-bd82-4b45-964c-d90eaebc0735
ms.openlocfilehash: 31b7d2b30a1ef83ca4400011d50854713cb260f6
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72347247"
---
# <a name="component-implementation-library"></a>コンポーネント実装ライブラリ

コンポーネントライブラリの実装は、PowerApps コンポーネントフレームワークを使用してコードコンポーネントを開発する際の重要な手順の1つです。 開発者は、TypeScript を使用してコンポーネントライブラリを実装できます。 各コードコンポーネントには、コードコンポーネントインターフェイスに記述されているメソッドを実装するオブジェクトを返す関数の定義を含むライブラリが必要です。 

オブジェクトは、次のメソッドを実装します。

- [init](reference/control/init.md) (必須)
- [Updateview](reference/control/updateview.md) (必須)
- [Getoutputs](reference/control/getoutputs.md) (省略可能)
- [破棄](reference/control/destroy.md)(必須)

これらのメソッドは、コードコンポーネントのライフサイクルを制御します。

