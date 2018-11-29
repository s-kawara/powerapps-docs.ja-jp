---
title: クライアント側開発のテスト ツール (Common Data Service for Apps) | Microsoft Docs
description: クライアント側開発のテスト フレームワークについて説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: aengusheaney
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="testing-tools-for-client-side-development"></a>クライアント側開発のためのテスト ツール

Microsoft では、[Easy Repro](https://github.com/Microsoft/EasyRepro) と呼ばれるモデル駆動型アプリ専用の自動化 UI テスト フレームワークを提供しています。 このフレームワークは、[SeleniumHQ](https://www.seleniumhq.org/) ブラウザー自動化オープンソース プロジェクトを使用してビルドされます。

Easy Repro は、モデル駆動型アプリの各種ページを操作する一連のクラスとメソッドを提供するため、テスト ケースを記述するときにアプリケーションの HTML 要素を解析する必要はありません。 これにより、アプリケーション ページを構成する HTML 要素での変更に対してテストが弾力性を持つようになります。

## <a name="benefits-of-unit-testing"></a>ユニット テストのメリット

ユニット テストは強くお勧めしますが必須ではありません。 使い始めたばかりの場合や、ソリューション内のコードの量が比較的小さい場合、ソリューションに含まれる機能よりテストの記述により多くの時間を費やすことができます。

ユニット テストの利点は、ソリューションが大きく、より複雑になったときに現れ始めます。 クライアント側の開発では、テスト用の自動化 UI フレームワークによって、ユーザー アクションによって開始された問題を検出できます。  

ユニット テストを使用してソリューションが開発されるとき、開発者は、生産性が向上して製品の品質が向上すると報告しています。

### <a name="see-also"></a>関連項目

[サーバ側開発のためのテスト ツール](../common-data-service/testing-tools-server.md)<br />
[ビデオ: UI テストの作成および実行](https://youtu.be/ryWgK34Akt0)<br />
[ブログの投稿: Easy Repro とは](http://www.itaintboring.com/dynamics-crm/easy-repro-what-is-it/)<br />
[ビデオ: DevOps の概要](https://youtu.be/AorM792M8nY)
