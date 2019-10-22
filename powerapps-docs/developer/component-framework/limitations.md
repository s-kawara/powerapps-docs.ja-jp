---
title: PowerApps component framework | の制限事項MicrosoftDocs
description: PowerApps component framework を使用した制限事項
author: nkrb
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.topic: index-page
ms.assetid: 18e88d702-3349-4022-a7d8-a9adf52cd34f
ms.author: nabuthuk
ms.openlocfilehash: aabcf4518e71648797c795a006c2d842f3e5ff01
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346741"
---
# <a name="limitations"></a>事項 

PowerApps component framework のリリースにより、独自のコードコンポーネントを作成して、モデル駆動型アプリとキャンバスアプリのユーザーエクスペリエンスを向上させることができるようになりました。 独自のコンポーネントを作成することもできますが、コードコンポーネントの一部の機能を実装する開発者を制限する制限がいくつかあります。 制限事項の一部を次に示します。

1. *データセット*型のコンポーネントではなく、キャンバスアプリの実験用プレビューでサポートされているのは、コンポーネントの*フィールド*の種類のみです。 
2. WebAPI を含む、他のいくつかの Api と共に Common Data Service 依存 Api は、この実験的なプレビューでは使用できません。 この実験的なプレビューリリースでの API の個別の可用性については、「 [PowerApps component FRAMEWORK api reference](reference/index.md)」を参照してください。
3. コードコンポーネントは、外部ライブラリコンテンツを含むすべてのコードをプライマリコードバンドルにバンドルする必要があります。 PowerApps コマンドラインインターフェイスを使用して外部ライブラリコンテンツをコンポーネント固有のバンドルにバンドルする方法の例については、「[角度フリップコンポーネント](sample-controls/angular-flip-control.md)の例」を参照してください。

   > [!NOTE]
   > コンポーネントマニフェストのライブラリノードを使用したコンポーネント間での共有ライブラリのサポートは、まだサポートされていません。 このことを確認しており、今後のリリースでこの機能が追加される予定です。
4. 1つのマニフェストファイルに複数のコンポーネントを定義することは、まだサポートされていません。
5. プロセスとアクションの呼び出しは、まだサポートされていません。 ダイアログボックスを呼び出すことができるのは、[ナビゲーション](reference/navigation.md)メソッドを使用した場合だけです。
6. 別のコードコンポーネントからのコンポーネントの呼び出しは、まだサポートされていません。
7. 現在、フォントリソース (tff) はサポートされていません。

## <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](overview.md)
