---
title: Azure DevOps 構築ツールの概要| Microsoft Docs
description: PowerApps 構築ツールは、PowerApps固有の Azure DevOps 構築タスクの集合です。これにより PowerApps の開発管理において、スクリプトを手動でダウンロードする必要がなくなります。
ms.custom: ''
ms.date: 07/21/2019
ms.reviewer: Dean-Haas
ms.service: powerapps
ms.topic: article
author: mikkelsen2000
ms.author: pemikkel
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="powerapps-build-tools-for-azure-devops-overview"></a>Azure DevOps の PowerApps 構築ツールの概要


[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

PowerApps の構築ツールを使用することで、PowerApps に関連する一般的な構築作業および導入タスクを自動化することができます。 これには、以下の処理が含まれています。 開発環境とソースコントロール間でのソリューション メタデータ (ソリューション) の同期、構築アーティファクトの生成、ダウンストリーム環境への展開、環境のプロビジョニングとデプロビジョニング、ソリューションに対するPowerApps チェッカー サービスを使用した静的解析チェック。

> [!IMPORTANT]
>
> - PowerApps 構築ツールはプレビュー機能です。
> - [!INCLUDE [cc-preview-features-definition](../../includes/cc-preview-features-definition.md)]

  
## <a name="what-are-powerapps-build-tools"></a>PowerApps 構築ツールはプレビューとは

PowerApps 構築 ツールは、一連のPowerApps 固有の Azure DevOps 構築タスクです。これを使用することで PowerApps のアプリケーション ライフサイクルの管理にあたって、カスタム ツールやスクリプトを手動でダウンロードする必要がなくなります。 タスクは、ダウンストリーム環境へのソリューションのインポートなどの簡単なタスクの実行に個別使用することもできますが、「構築アーティファクトの生成」や「テストの展開」、「メーカー変更の取り込み」などのパイプラインでシナリオをまとめるのことに使用することもできます。 構築タスクは大きく分けて以下の4つの種類に分類できます:

- ヘルパー 
- 品質のチェック 
- ソリューション 
- 環境の管理 

## <a name="get-the-powerapps-build-tools"></a>PowerApps構築ツールの入手 
PowerApps の構成ツールは、 [Azure Marketplace](https://marketplace.visualstudio.com/items?itemName=microsoft-IsvExpTools.PowerApps-BuildTools) から Azure DevOps へとインストールできます。 インストールが完了すると、PowerApps構築ツールに含まれるすべてのタスクが、新規または既存のパイプラインに追加できるようになり、 **PowerApps** を検索することで容易に見つけることができます。

![構築ツールを入手する](media/build-tools-download.png)
 
## <a name="next-step"></a>次の手順

[ツール構成タスク](build-tools-tasks.md)
