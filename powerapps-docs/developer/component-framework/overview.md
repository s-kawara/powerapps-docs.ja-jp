---
title: PowerApps コンポーネント フレームワーク | Microsoft Docs
description: PowerApps コンポーネント フレームワークを使用してカスタム コンポーネントを作成し、フォーム、ビュー、ダッシュボードでデータを表示して作業する高度なエクスペリエンスを提供します。
keywords: コンポーネント フレームワーク、カスタム コンポーネント、PowerApps コントロール
author: nkrb
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.custom:
  - dyn365-a11y
  - dyn365-developer
ms.topic: article
ms.assetid: 7923e36d-3640-49f7-9f2f-c97358a632db
ms.author: nabuthuk
---

# <a name="powerapps-component-framework"></a>PowerApps コンポーネント フレームワーク

[!INCLUDE[cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

PowerApps コンポーネント フレームワークを使用してモデル駆動型アプリにカスタム コンポーネントを作成し、フォーム、ビュー、ダッシュボードでデータを表示して作業するユーザーに高度なエクスペリエンスを提供します。 たとえば、次のようなものです。

- 数値テキスト値を表示するフィールドを `dial` や `slider` コンポーネントに置き換えます。
- リストを `Calendar` や `Map` のようにデータセットに結び付けられた全く異なる視覚的エクスペリエンスに変換します。

> [!IMPORTANT]
> - PowerApps コンポーネント フレームワークはプレビュー機能です。
> - [!INCLUDE[cc_preview_features_definition](../../includes/cc-preview-features-definition.md)] 
> - [!INCLUDE[cc_preview_features_no_MS_support](../../includes/cc-preview-features-no-ms-support.md)]

> [!NOTE]
> [モデル駆動型アプリ](/powerapps/maker/model-driven-apps/model-driven-app-overview) バージョン 9.1.0.3842 以上向けの統一インターフェイスでのみ、カスタム コンポーネントがサポートされます。

PowerApps コンポーネント フレームワークにより、専門的な開発者は幅広い PowerApps 機能で使用できるカスタム コンポーネントを作成できます。 コンポーネント ライフサイクル 管理、コンテキスト データおよびメタデータ アクセス、Web API を介したシームレスなサーバー アクセス、ユーティリティとデータの書式設定方法、カメラ、位置、マイクなどのデバイス機能と、ダイアログなどの UX 要素の簡単な呼び出し、検索、全画面表示などのような、機能を公開する豊富なフレームワーク API にカスタム コンポーネントはアクセスできます。  

コンポーネント開発者は最新の Web プラクティスを利用でき、また外部ライブラリの力を活用して高度なユーザー対話を作成できます。 フレームワークはコンポーネントのライフサイクルを自動的に処理し、アプリケーションのビジネス ロジックを保持し、パフォーマンスを最適化します (もう非同期 iframe は不要です)。 このフレームワークを使用して作成されたコンポーネントは完全な構成が可能で、フォーム、ダッシュボード、グリッドなどのモデル駆動型アプリの複数の外観に再利用できます。コンポーネントの定義、依存関係、および構成はすべて [ソリューション](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/customize/solutions-overview) にパッケージ化して環境間で移動し、[アプリ ソース](https://appsource.microsoft.com/en-us/marketplace/apps?page=1&product=dynamics-365) 経由で出荷できます。  

## <a name="related-topics"></a>関連トピック

[カスタム コンポーネントとは](custom-controls-overview.md)<br/>
[カスタム コンポーネントの作成](create-custom-controls-using-pcf.md)
