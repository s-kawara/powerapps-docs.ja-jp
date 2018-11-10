---
title: 環境とテナント間での PowerApps の移行 | Microsoft Docs
description: 環境とテナント間で PowerApps アプリを移行する方法のチュートリアル
author: jamesol-msft
manager: kvivek
ms-topic: conceptual
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.author: jamesol
search.audienceType:
- admin
search.app:
- D365CE
- PowerApps
- Powerplatform
ms.openlocfilehash: 651301dafa17c6ec159d462f018d6ec1984485ba
ms.sourcegitcommit: 7403ea7f103564fa7d1ae73a08a7dbdfeba7d999
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43263446"
---
# <a name="environment-and-tenant-app-migration-through-packaging"></a>パッケージによる環境とテナントのアプリ移行
ある環境から別の環境に、パッケージでリソースを移行する方法について説明します。 移行は、同じテナント内の環境間、またはテナントの異なる環境間で行うことができます。

## <a name="the-scenario"></a>シナリオ
リソースを移行する必要のある 1 つの一般的な状況として、テストまたは開発用の環境と運用環境とを利用している場合があります。 開発者やテスト担当者には、環境内にあるアプリへの幅広いアクセス権があります。 実稼働環境に新しいアプリを移行する際には、環境は更新と変更のアクセス権を厳密に制御します。

別の状況として、各顧客が独自の環境とデータを持っているという場合があります。 新しい顧客が追加されたときに、新しい環境が顧客に対して作成され、それらの環境にアプリを移行します。

## <a name="which-resources-can-i-migrate-through-packaging"></a>どのリソースがパッケージで移行できるか
アプリをエクスポートするときに、アプリに依存するリソースもパッケージにエクスポートされます。  最初は、次の表に記載したように、可能性のある全てのリソース タイプのサブセットのみがサポートされます。

| リソースの種類 | サポート対象 | インポート オプション |
| --- | --- | --- |
| アプリ |はい |アプリを環境にインポートするのに 2 つのオプションがあります。 <ol><li><b>新規作成</b> – アプリは、パッケージがインポートされる環境で新しいアプリとして作成されます。</li> <li><b>更新</b> - このパッケージがインポートされるときに、アプリは既に環境に存在するため、更新を行います。</li></ol> |
| フロー |はい |フローを環境にインポートするのに 2 つのオプションがあります。 <ol><li><b>新規作成</b> – フローは、パッケージがインポートされる環境で新しいフローとして作成されます。</li> <li><b>更新</b> - このパッケージがインポートされるときに、フローは既に環境に存在するため、更新を行います。</li></ol> <b>注: </b>フローが依存するすべてのリソースは、エクスポートされるアプリ パッケージの中にも含まれますが、インポートされるパッケージと共に構成する必要があります。 |
| カスタム コネクタ |いいえ |アプリがカスタム コネクタに依存している場合、パッケージの一部としてコネクタをエクスポートすることは、現時点ではサポート<b>していません</b>。 <p></p> 独自のコネクタに依存しているアプリがあれば、現時点での唯一のオプションは、対象となる環境でコネクタを手動で再作成または更新し、パッケージをインポートするときに、そのコネクタを選択することです。 |
| 接続 |いいえ |アプリが接続 (資格情報を使用した SQL 接続など) に依存している場合は、パッケージの一部として接続や資格情報をエクスポートすることは、現在はサポートしていません。 <p></p> 共有の接続 (SQL など) に依存しているアプリがあれば、現時点での唯一のオプションは、対象となる環境で適切な資格情報を持った接続を手動で作成しなおして、パッケージをインポートするときにその接続を選択することです。 |
| CDS のカスタマイズ |いいえ |CDS のカスタマイズのエクスポートは、パッケージ化の一部としてサポートされなくなりました。 現在、この機能は、以下の記事で説明されているように、環境の既定ソリューションをエクスポートおよびインポートする方法でサポートされています。 |
| ゲートウェイ |いいえ |ゲートウェイは、既定 (および {テナント名} (プレビューから) ) の環境でのみサポートされるため、エクスポート/移行はサポートされません。 |

## <a name="how-do-i-get-access-to-packaging-for-my-app"></a>自分のアプリのパッケージングにはどのようにアクセスできますか?
アプリのエクスポート機能は、アプリの ”編集が可能” なアクセス許可を持つユーザーであれば使用できます。

アプリのインポート機能は、インポート先の環境で ”Environment Maker” のアクセス許可を持つユーザーであれば使用できます。

アプリをエクスポートまたはインポートするには、PowerApps Plan 2 または PowerApps Plan 2 の試用版ライセンスが必要です。

> [!NOTE]
> パッケージングがプレビューで提供されている間は、有効な PowerApps ライセンスを持つユーザーであれば誰でも、アプリと環境のパッケージングをお試しいただけます。

## <a name="exporting-an-app"></a>アプリのエクスポート
1. [http://web.powerapps.com](http://web.powerapps.com) で、**[アプリ]** をクリックまたはタップし、移行するアプリの省略記号を選択してから、**[エクスポート (プレビュー)]** を選択します。

    ![エクスポートを選択](./media/environment-and-tenant-migration/select-export.png)
2. エクスポート パッケージ ページを開いて、パッケージの名前と説明を入力します。

    ![パッケージの詳細の確認](./media/environment-and-tenant-migration/package-details.png)
3. [パッケージ コンテンツの確認] セクション内で、必要に応じてコメントやメモを追加したり、パッケージのインポート時に各リソースをターゲット環境にインポートする方法に関して、設定を変更したりできます。

    ![パッケージの内容の構成](./media/environment-and-tenant-migration/export-package-content.png)

4. **[エクスポート]** を選択すると、数秒以内にパッケージ ファイルのダウンロードが開始されます。

## <a name="importing-an-app"></a>アプリのインポート
1. [http://web.powerapps.com](http://web.powerapps.com) で、**[アプリ]** をクリックまたはタップし、**[パッケージのインポート (プレビュー)]** を選択します。

    ![インポートの選択](./media/environment-and-tenant-migration/select-import.png)
2. **[アップロード]** を選択し、インポートするアプリ パッケージ ファイルを選択します。

    ![パッケージ ファイルの選択](./media/environment-and-tenant-migration/select-file.png)
3. パッケージがアップロードされたなら、パッケージの内容を確認し、赤いアイコンでマークされたすべての項目を追加で入力する必要があります。これを行うには、各項目のレンチ アイコンを選択して、必要な情報を入力してください。

    ![パッケージの内容の確認](./media/environment-and-tenant-migration/import-package-content.png)
4. 必要な情報をすべて入力し終わったら、**[インポート]** を選択します。

    ![パッケージ化された内容の更新](./media/environment-and-tenant-migration/import-package-content-dirty.png)
5. インポートが完了すると、(下記のような) ページに自動的にリダイレクトされ、インポート操作の結果について概要が表示されます。

    ![インポート結果の確認](./media/environment-and-tenant-migration/import-results.png)

> [!NOTE]
>  アプリをインポートするときに既存のアプリの **[更新]** を選択すると、新しい変更はアプリケーションのドラフトとして保存されます。  アプリケーションの全ユーザーが利用できるように、それらの変更を[公開](http://powerapps.microsoft.com/tutorials/save-publish-app/#publish-an-app)する必要があります。
>
>

## <a name="exporting-cds-customizations-and-model-driven-apps"></a>CDS のカスタマイズとモデル駆動型アプリのエクスポート
エンティティまたはオプション セットのカスタマイズまたは [http://web.powerapps.com](https://web.powerapps.com) で構築したモデル駆動型アプリのエクスポートは、次のように、既定の環境ソリューションをエクスポートする方法でサポートされます。
> [!NOTE]
>  PowerApps のソリューションの詳細については、「[Introduction to solutions](../developer/common-data-service/introduction-solutions.md)」(ソリューションの概要) を参照してください。
>
>

1. http://web.powerapps.com で、実際の環境の **[モデル駆動 (プレビュー)]** デザイン モードを選択します。

    ![モデル駆動デザイン モードの選択](./media/environment-and-tenant-migration/select-model-driven.png)

2. 左側のナビゲーション バーで **[詳細]** を選択して、この環境の既定ソリューションのソリューション エクスプローラーを起動します

    ![[詳細] の選択](./media/environment-and-tenant-migration/select-advanced.png)

3. **[ソリューションのエクスポート]** を選択して、必要な手順を実行します。  数秒後にソリューション パッケージ ファイルのダウンロードが開始されます。

    ![エクスポートを選択](./media/environment-and-tenant-migration/select-export-solution.png)

## <a name="importing-cds-customization-and-model-driven-apps"></a>CDS のカスタマイズとモデル駆動型アプリのインポート
残念ながら、CDS ソリューション パッケージをインポートするには、エクスペリエンスに手動の回避策が必要です。現在、Microsoft ではこの問題の解決に取り組んでいます。

1. [http://web.powerapps.com](http://web.powerapps.com) で、実際の環境の **[モデル駆動 (プレビュー)]** デザイン モードを選択します。

    ![モデル駆動デザイン モードの選択](./media/environment-and-tenant-migration/select-model-driven.png)

2. 左側のナビゲーション バーで **[詳細]** を選択して、この環境の既定ソリューションのソリューション エクスプローラーを起動します。

    ![[詳細] の選択](./media/environment-and-tenant-migration/select-advanced.png)

3. ブラウザーから URL をコピーし、次の変更を行い、ブラウザーで新しい URL に移動します。

    * 現在の URL 構造: `https://{orguniquename}.crm.dynamics.com/tools/solution/edit.aspx?id={solutionname}`

        ![URL の編集](./media/environment-and-tenant-migration/edit-url.png)

    * 新しい URL 構造: `https://{orguniquename}.crm.dynamics.com/tools/solution/SolutionImportWizard.aspx`

        ![パッケージの選択](./media/environment-and-tenant-migration/select-package.png)

4. インポートする CDS ソリューション パッケージ ファイルを選択し、ウィザードを完了します。

5. インポートが成功すると、次の確認ダイアログが表示されます。 ソリューションの変更を環境内の他のカスタマイザーも利用できるようにするには、**[すべてのカスタマイズの公開]** を選択します。

    ![インポートの成功](./media/environment-and-tenant-migration/successful-import.png)
