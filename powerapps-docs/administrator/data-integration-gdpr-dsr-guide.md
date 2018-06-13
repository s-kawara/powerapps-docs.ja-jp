---
title: Data Integration for Admins の顧客データ
description: CDS for Apps の Data Integration for Admins での個人データの特定、エクスポート、削除
author: sabinn-msft
ms.service: powerapps
ms.topic: how-to
ms.component: cds
ms.date: 05/20/2018
ms.author: sabinn
ms.openlocfilehash: 01dafceacff89cb9b3a400caad5dde07a0995f1c
ms.sourcegitcommit: e59c849a88c6fc0ed333ef4ce2d982a5b8623c97
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34754227"
---
# <a name="responding-to-data-subject-rights-dsr-requests-for-data-integration-for-common-data-service-for-apps-customer-data"></a>Common Data Service for Apps 顧客データの Data Integration に対するデータ主体の権利 (DSR) 要求への対応

## <a name="introduction-to-dsr-requests"></a>DSR 要求の概要

欧州連合 (EU) の一般データ保護規則 (GDPR) は、規制において "データ主体" と呼ばれる人に、雇用主または他の種類の機関や組織 ("データ コントローラー" または単に "コントローラー" と呼ばれます) によって収集された個人データを管理する権限を与えます。 GDPR での個人データは、識別された自然人または識別可能な自然人に関連するすべてのデータと、非常に幅広く定義されています。 GDPR では、データ主体には個人データに関して次のことを行う権利が与えられています。

- コピーを取得する
- 修正を要求する
- 処理を制限する
- 削除する
- 別のコントローラーに移動できるように電子的な形式で受け取る

データ主体がコントローラーに対して個人データへの操作を実行するよう正式に要求することを、データ主体の権利 (DSR) 要求と呼びます。

この記事では、Microsoft が GDPR に対してどのように備えているかを説明します。また、CDS for Apps の管理ポータルで Data Integration for Admins を使用するときに GDPR のコンプライアンスをサポートするためにお客様が実行できる手順の例を示します。 コントローラーのお客様が DSR 要求に対応して Microsoft クラウド内の個人データを検索、アクセス、操作するときに役立つ、Microsoft の製品、サービス、管理ツールの使用方法について説明します。

### <a name="searching-for-and-identifying-personal-data"></a>個人データの検索と特定

CDS for Apps の Data Integration for Admins を使用すると、統合アプリケーションの任意のユーザーがデータ統合タブを使用してデータを表示できるようになります。

[https://admin.powerapps.com/dataintegration](https://admin.powerapps.com/dataintegration)

ユーザーの格納データは、ポータルに表示されます。 すべてのプロジェクトはプロジェクト タブに表示されます。

![プロジェクト タブでプロジェクトを表示する](./media/data-integration-gdpr-dsr/projects-tab.png)

すべての接続セットは接続セット タブに表示されます。

![接続セット タブの接続セットを表示する](./media/data-integration-gdpr-dsr/connections-tab.png)

すべてのテンプレートは、テンプレート タブに表示されます。

![テンプレート タブのテンプレートを表示する](./media/data-integration-gdpr-dsr/templates-tab.png)

## <a name="securing-and-controlling-access-to-personal-information"></a>個人情報へのアクセスのセキュリティ保護と管理

CDS for Apps の Data Integration for Admins でデータ統合アプリケーションによって格納されたデータにアクセスするには、管理者ポータルを使用する必要があります。

## <a name="deleting-personal-data"></a>個人データの削除

CDS for Apps の Data Integration for Admins では、ユーザーが作成したデータ、プロジェクト、および接続セットは、そのデータが関連付けられているユーザーが削除できます。 個人データを削除するには、管理者ポータルにログオンします。[https://admin.powerapps.com](https://admin.powerapps.com)

プロジェクトを削除するには、プロジェクト タブに移動し、プロジェクトの横にある省略記号をクリックし、削除オプションを選択します。

![省略記号をクリックしてプロジェクトを削除する](./media/data-integration-gdpr-dsr/projects-del.png)

テンプレートを削除するには、テンプレート タブに移動し、テンプレートの横にある省略記号をクリックし、削除オプションを選択します。

![省略記号をクリックしてテンプレートを削除する](./media/data-integration-gdpr-dsr/templates-del.png)

接続セットを削除するには、接続セット タブに移動し、接続セットの横にある省略記号をクリックし、削除オプションを選択します。

![省略記号をクリックして接続セットを削除する](./media/data-integration-gdpr-dsr/connsets-del.png)

## <a name="exporting-personal-data"></a>個人データのエクスポート

CDS for Apps の Data Integration for Admins では、ユーザーが作成したデータは、そのデータが関連付けられているユーザーがエクスポートできます。 個人データをエクスポートするには、管理者ポータルにログオンします。

[https://admin.powerapps.com](https://admin.powerapps.com)

プロジェクト、またはプロジェクトと実行履歴をエクスポートするには、プロジェクト タブに移動し、プロジェクトの横にある省略記号をクリックし、目的のエクスポート オプションを選択します。

![省略記号をクリックしてプロジェクトをエクスポートする](./media/data-integration-gdpr-dsr/projects-exp.png)

テンプレートをエクスポートするには、テンプレート タブに移動し、テンプレートの横にある省略記号をクリックし、エクスポート オプションを選択します。

![省略記号をクリックしてテンプレートをエクスポートする](./media/data-integration-gdpr-dsr/templates-exp.png)

接続セットをエクスポートするには、接続セット タブに移動し、接続セットの横にある省略記号をクリックし、エクスポート オプションを選択します。

![省略記号をクリックして接続セットをエクスポートする](./media/data-integration-gdpr-dsr/connsets-exp.png)
