---
title: マニフェスト |Microsoft Docs
description: ''
keywords: ''
ms.author: nabuthuk
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
ms.assetid: 31af2963-b4ca-4347-98f6-4a3f6277f43a
ms.openlocfilehash: 22750956cea12e1ed17bbc1ee8d4f015cf0ce2c1
ms.sourcegitcommit: 63ea15e2f861d43333aacda19230cd8922d7bdfd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "72338921"
---
マニフェストは、コンポーネントを定義するメタデータ ファイルです。 これは、次のように記述された `XML` ファイルです。

- コンポーネントの名前空間。
- 構成できるデータの種類。フィールドまたはデータセットのいずれかです。
- コンポーネントを追加するときにアプリケーションで構成できるすべてのプロパティ。
- コンポーネントが必要とするリソースファイルの一覧。 
  - そのうちの1つは、JavaScript web リソースである必要があります。 この JavaScript には、オブジェクトをインスタンス化する関数を含める必要があります。 それにより、コンポーネントが動作するために必要なメソッドを公開するインターフェイスが実装されます。 これはコンポーネント実装ライブラリと呼ばれています。
- 必要なコンポーネントインターフェイスを適用するオブジェクトを返す、コンポーネント実装ライブラリ内の JavaScript 関数の名前。

ユーザーがキャンバスアプリまたはモデル駆動型アプリでカスタムコンポーネントを構成すると、マニフェスト内のデータによって使用可能なコンポーネントが除外され、そのコンテキストの有効なコンポーネントのみが構成に使用できるようになります。 コンポーネントのマニフェストで定義されているプロパティは構成フィールドとして表示されるため、コンポーネントを構成するユーザーは値を指定できます。 これらのプロパティ値は、実行時にコンポーネント関数で使用できます。
