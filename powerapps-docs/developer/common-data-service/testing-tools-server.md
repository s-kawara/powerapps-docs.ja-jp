---
title: サーバー側開発のテスト ツール (Common Data Service) | Microsoft Docs
description: サーバー側開発のテスト フレームワークについて説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="testing-tools-for-server-side-development"></a>サーバ側開発のためのテスト ツール

多くの開発者が、開発プロセスの一部にユニット テストを含めることを強く擁護しています。 確信していない開発者もいます。 Common Data Service は、テスト フレームワーク ツールを提供していませんが、使用可能なコミュニティ ツールがある点に留意してください。 サーバー側開発の一般的なフレームワークは、[Fake Xrm Easy](https://dynamicsvalue.com/home) です。 このフレームワークは、.NET Framework テスト フレームワークの選択と組み合わせて使用できます。 [FakeItEasy](https://fakeiteasy.github.io/) は、共通の選択です。

> [!NOTE]
> Microsoft は、コミュニティにより作成されたツールをサポートしていません。 コミュニティ ツールに問題がある場合は、発行元にお問い合わせください。

## <a name="benefits-of-unit-testing"></a>ユニット テストのメリット

ユニット テストは強くお勧めしますが必須ではありません。 使い始めたばかりの場合や、ソリューション内のコードの量が比較的小さい場合、ソリューションに含まれる機能よりテストの記述により多くの時間を費やすことができます。

ユニット テストの利点は、ソリューションが大きく、より複雑になったときに現れ始めます。 特にサーバー側開発では、[プラグインのデバッグ](debug-plug-in.md)で説明されている手順をすべて実行してデバッグするプロファイルを生成しなくても、テスト フレームワークを持つモック データまたはフェイク データを使用してローカルでデバッグすることに大きなメリットがあります。

ユニット テストを使用してソリューションが開発されるとき、開発者は、生産性が向上して製品の品質が向上すると報告しています。

### <a name="see-also"></a>関連項目

[クライアント側開発のためのテスト ツール](../model-driven-apps/testing-tools-client.md)<br />
[ビデオ: DevOps と Dynamics 365 の概要](https://youtu.be/AorM792M8nY)