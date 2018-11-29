---
title: 'ステップ 3: アプリのマネージド ソリューションを作成 (アプリ用 Common Data Service) | Microsoft Docs'
description: すべてのコンポーネントを含めるアプリの管理ソリューションを作成する方法を学習します。 これは Appsource にアプリを公開するために必要です。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: shmcarth
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="step-3-create-a-managed-solution-for-your-app"></a>手順3: アプリの管理ソリューションを作成する

アプリのためにすべてのコンポーネントを含める管理ソリューションを作成します。 アプリ コンポーネントをパッケージする管理ソリューションを計画して作成するときに、これらのトピックが役立つことに気付くことでしょう。
- [ソリューションの概要](introduction-solutions.md)
- [ソリューション開発の計画](/dynamics365/customer-engagement/developer/plan-solution-development) 
- [マネージド ソリューションのインストール、および更新](create-install-update-managed-solution.md)

## <a name="display-name-and-description-of-your-solution"></a>ソリューションの表示名および説明

アプリ コンポーネントをパッケージ化するためのソリューションを作成する場合は、顧客のために表示する新しいソリューションの**表示名**フィールドおよび**説明**フィールドに適切な値を指定してください。

![ソリューションの作成](media/appsource-new-solution.png)

顧客に対してソリューションの**表示名**および**説明**値が **Dynamics 365 管理センター**ポータルに表示されます。

![ソリューション](media/appsource-solution-names.png)

## <a name="supporting-data-for-your-solution"></a>ソリューションでサポートするデータ

ソリューションがサポートまたはデモ データを必要とする場合:
1. テスト環境でサポート/デモ データを作成します。
2. サポート/デモ データを含むスキーマを作成するには、[Configuration Migration ツール](/dynamics365/customer-engagement/admin/manage-configuration-data) を使用します。 
3. デモ データが変更される場合にデータを更新するためにスキーマ ファイルを後から再利用するため、スキーマ ファイルを保存します。
4. データをエクスポートするためにスキーマを使用します。 エクスポート ファイルには意味のある名前を指定してください。 データは .zip ファイルとしてエクスポートされます。

Configuration Migration ツールを使用してスキーマを作成してデータをエクスポートすることに関する詳細は、[構成データをエクスポートするスキーマの作成](/dynamics365/customer-engagement/admin/create-schema-export-configuration-data)を参照してください

## <a name="at-the-end-of-this-step"></a>この手順の最後に

アプリのためにソリューション ファイル (例: *SampleSolution.zip*) およびオプションとしてデモ データ フォイル (例: *SampleData.zip*) が作成されます。


> [!div class="nextstepaction"]
> [手順4: アプリの AppSource パッケージを作成する](create-package-app-appsource.md) 
  