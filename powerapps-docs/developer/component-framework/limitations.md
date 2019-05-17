---
title: PowerApps コンポーネント フレームワークの制限 | MicrosoftDocs
description: PowerApps コンポーネント フレームワークを使用する制限
author: nkrb
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.topic: index-page
ms.assetid: 18e88d702-3349-4022-a7d8-a9adf52cd34f
ms.author: nabuthuk
---

# <a name="limitations-of-powerapps-component-framework"></a>PowerApps コンポーネント フレームワークの制限

[!INCLUDE[cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

PowerApps コンポーネント フレームワークのリリースにより、モデル駆動型アプリのユーザー エクスペリエンスを向上させる独自のカスタム コンポーネントを作成できるようになりました。 独自のコンポーネントを作成することができますが、カスタム コンポーネントには機能を実装する時に開発者を制限するいくつかの制約があります。 以下にその制限をいくつか示します:

> [!IMPORTANT]
> - PowerApps コンポーネント フレームワークはプレビュー機能です。
> - [!INCLUDE[cc_preview_features_definition](../../includes/cc-preview-features-definition.md)] 
> - [!INCLUDE[cc_preview_features_no_MS_support](../../includes/cc-preview-features-no-ms-support.md)]

## <a name="support-for-external-libraries"></a>外部ライブラリのサポート

パブリック プレビューで、コンポーネントは外部ライブラリの内容を含むすべてのコードを、主要なコード バンドルにバンドルする必要があります。 PowerApps コマンド ライン インターフェースが、外部ライブラリーのコンテンツをコンポーネント固有のバンドルにバンドルするのに役立つ方法を確認するには、 [Angular フリップ コンポーネント](sample-controls/angular-flip-control.md) の例を参照してください。

> [!NOTE]
> コンポーネント マニフェストでライブラリ ノードを使用しているコンポーネント間での共有ライブラリのサポートは、パブリック プレビューでサポートされません。 これを見直してこの機能を今後のリリースで追加する予定です。

## <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](overview.md)