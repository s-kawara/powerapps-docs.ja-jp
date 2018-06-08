---
title: Excel の接続の概要 | Microsoft Docs
description: ブックをクラウド ストレージ アカウントに保存し、アプリからデータに接続することによって、Excel でデータを表示および更新します。
author: lancedMicrosoft
ms.service: powerapps
ms.topic: reference
ms.component: canvas
ms.date: 10/02/2016
ms.author: lanced
ms.openlocfilehash: feb2d17400c2f1ddc9670e3bd840322dc1edfc10
ms.sourcegitcommit: 7354a0c61578fcc0b9965bf557b9d7c553c73e96
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2018
ms.locfileid: "34803100"
---
# <a name="connect-to-excel-from-powerapps"></a>PowerApps から Excel に接続する
![Excel](./media/connection-excel/excelicon.png)

Excel は接続*のようなもの*です。 アプリで Excel データを表示するには:

1. [Excel データをテーブルとして書式設定](https://support.office.com/article/Create-an-Excel-table-in-a-worksheet-E81AA349-B006-4F8A-9806-5AF9DF0AC664)します。
2. Excel ファイルをクラウド ストレージ アカウント (Box、Dropbox、Google Drive、OneDrive、OneDrive for Business など) に保存します。
3. [クラウド ストレージ アカウントに接続](../add-manage-connections.md)し、データ ソースとして Excel テーブルを追加します。
4. [アプリを自動的に生成する](../get-started-create-from-data.md)か、または**ギャラリー** コントロールのようなものを追加して構成することで、この情報を表示します。

> [!NOTE]
> PowerApps から Excel テーブルに接続すると、PowerApps は **\_* PowerAppsId_*** という新しい列を作成します。Excel テーブルの各行には一意の ID が付けられます。

「[クラウド ストレージ接続の概要](cloud-storage-blob-connections.md)」では、接続を追加し、データ ソースとして Excel テーブルを追加して、アプリで Excel のデータを使う方法が示されています。

他の種類のデータに接続する方法については、[PowerApps の接続の一覧](../connections-list.md)をご覧ください。

### <a name="known-limitations"></a>既知の制限
お客様の組織内の Excel データを共有する方法の詳細については、[これらの制限をご確認ください](cloud-storage-blob-connections.md#sharing-excel-tables)。

