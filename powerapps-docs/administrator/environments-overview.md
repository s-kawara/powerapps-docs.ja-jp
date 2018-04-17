---
title: 環境の概要 | Microsoft Docs
description: 環境とその使用方法
services: powerapps
suite: powerapps
documentationcenter: na
author: manasmams
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2018
ms.author: manasma
ms.openlocfilehash: 4b71f931aa3e8263166d52b68ba375917405c2b8
ms.sourcegitcommit: 078ba325480147e6e4da61e319ed53219f1c5cfc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2018
---
# <a name="environments-overview"></a>環境の概要
環境とは、組織のビジネス データ、アプリ、フローを保管、管理、共有するためのスペースです。 ロール、セキュリティ要件または対象ユーザーが異なるアプリを分離するコンテナーとしても機能します。 環境を活用する方法は、組織や構築するアプリによって変わります。 例:

* 単一の環境でのみアプリを構築することもできます。
* アプリのテスト バージョンと製品バージョンをグループ化する個別の環境を作成できます。
* 会社の特定のチームや部門に対応する個別の環境を作成し、それぞれのユーザーに関連するデータとアプリを、それぞれの環境に配置できます。
* 会社のグローバルに展開する支店ごとに、個別の環境を作成することもできます。  

## <a name="environment-scope"></a>環境のスコープ
それぞれの環境は Azure AD テナントに作成され、そのリソースには、そのテナント内のユーザーのみがアクセスできます。 環境は、米国などの地理的な場所にも結び付けられています。 環境でアプリを作成すると、アプリはその地理的な場所にあるデータセンターにのみルーティングされます。 その環境で作成するすべての項目 (接続、ゲートウェイ、Microsoft Flow を使用するフローなど) は、それぞれの環境の場所にも結び付けられます。

それぞれの環境には、アプリのストレージを提供する Common Data Service データベースを配置できる場合と、1 つ配置できる場合があります。 環境にデータベースを作成できるかどうかは、購入する PowerApps のライセンスとその環境内のアクセス許可によります。 詳細については、[料金の情報](pricing-billing-skus.md)に関するページを参照してください。

アプリを環境に作成する場合、そのアプリは、接続、ゲートウェイ、フロー、Common Data Service データベースなど、同じ環境にもデプロイされているデータ ソースへの接続のみ許可されます。  たとえば、'Test' および 'Dev' という名前の 2 つの環境を作成し、それぞれの環境に Common Data Service データベースを作成したシナリオについて考えてみましょう。 'Test' 環境でアプリを作成する場合は、そのアプリは 'Test' データベースへの接続のみ許可され、'Dev' データベースに接続することはできません。

環境間でリソースを移動するプロセスもあります。 詳細については、[リソースの移行](environment-and-tenant-migration.md)に関するページを参照してください。

![](./media/environments-overview/Environments.png)

## <a name="environment-permissions"></a>環境のアクセス許可
環境には、環境内でのアクセス許可を提供する 2 つの組み込みの役割があります。

* Environment Admin ロールは、環境に対して、次を含むすべての管理操作を実行できます。

    * Environment Admin ロールまたは Environment Maker ロールのいずれかからユーザーまたはグループを追加または削除する

    * 環境に Common Data Service データベースをプロビジョニングする

    * 環境内で作成されたすべてのリソースを表示し、管理する

    * データ損失防止ポリシーを設定する。 詳細については、[データ損失防止ポリシー](prevent-data-loss.md)に関するページを参照してください。

    環境でデータベースを作成したら、環境管理者ロールではなく、システム管理者ロールを使用できます。

* Environment Maker ロールは、アプリ、接続、カスタム コネクタ、ゲートウェイ、および Microsoft Flow を使用するフローなど、環境内のリソースを作成できます。

Environment Maker は、組織内の個々のユーザー、セキュリティ グループ、またはすべてのユーザーとアプリを共有することにより、環境に構築するアプリを組織の他のユーザーに配布することもできます。 詳細については、[PowerApps でのアプリの共有](../maker/canvas-apps/share-app.md)に関するページを参照してください。

これらの環境のロールに割り当てられているユーザーまたはグループには、環境のデータベース (存在する場合) へのアクセス権が自動的に付与されるわけではありません。データベース所有者が個別にアクセス権を付与する必要があります。 詳細については、「[Configure database security (データベース セキュリティの構成)](database-security.md)」を参照してください。

環境管理者は、[PowerApps 管理センター][1]から、ユーザーまたはセキュリティ グループに、これらの 2 つのロールのいずれかを割り当てることができます。 詳細については、「[PowerApps での環境の管理](environments-administration.md)」を参照してください。

![](./media/environments-overview/EnvironmentRoles.png)

## <a name="the-default-environment"></a>既定の環境
既定の環境は、PowerApps によって各テナントに対して自動的に 1 つ作成され、そのテナント内のすべてのユーザーが共有します。 新しいユーザーは、PowerApps にサインアップすると、既定の環境の Maker ロールに自動的に追加されます。 既定の環境は、AAD テナントの既定のリージョンに最も近いリージョンに作成されます。

> [!NOTE]
> 既定の環境の Environment Admin ロールに自動的に追加されるユーザーはいません。 詳細については、「[PowerApps での環境の管理](environments-administration.md)」を参照してください。
>
>

既定の環境の名前は、"{Azure AD テナント名} (既定)" となります。

![](./media/environments-overview/DefaultEnvironment.png)

## <a name="production-and-trial-environments"></a>運用環境とテスト環境
目的に応じて環境を作成することができます。 試用環境は、Common Data Service エクスペリエンスで環境とデータベースを試すためのものです。 一定期間が経過すると有効期限が切れます。 詳細については、「[PowerApps での環境の管理](environments-administration.md)」を参照してください。

## <a name="choosing-an-environment"></a>環境の選択
環境の導入に伴い、[https://web.powerapps.com](https://web.powerapps.com) では、新しいエクスペリエンスを実現しています。このサイトに表示されるアプリ、接続、およびその他の項目は、選択している現在の環境に基づいて、フィルターされるようになりました。  現在の環境は、ヘッダーの右端近くにある環境選択リストで指定します。 別の環境を選択するには、選択リストをクリックまたはタップして、使用可能な環境のリストを表示します。 使用する環境をクリックまたはタップします。

次の条件のいずれかを満たしている場合、環境が選択リストに表示されます。

* 環境の Environment Admin ロールのメンバーである。
* 環境の Environment Maker ロールのメンバーである。
* 環境の Environment Admin または Environment Maker ではないが、環境内で少なくとも 1 つのアプリに対する '共同作業者’ アクセスが付与されている。 詳細については、「[share an app (アプリの共有)](../maker/canvas-apps/share-app.md)」を参照してください。 この場合は、この環境にアプリを作成できません。 自分と共有している既存のアプリの変更だけが可能です。

![](./media/environments-overview/EnvironmentPicker.png)

## <a name="creating-an-environment"></a>環境の作成
### <a name="who-can-create-environments"></a>環境を作成できるユーザー
環境を作成できるかどうかは、ライセンスによって決まります。

| ライセンス | 環境の作成が可能 |
| --- | --- |
| PowerApps P2 |○ (2 つの運用環境と 2 つのテスト環境)|
| PowerApps P2 試用版 |○ (2 つの試用版環境)|
| PowerApps P1 |x |
| PowerApps P1 試用版 |x |
| Dynamics 365 プラン |x |
| Office 365 プラン |x |
| Dynamics 365 アプリおよびチーム プラン |x |


### <a name="where-can-environments-be-created"></a>環境を作成できる場所
新しい環境は、[PowerApps.com][2] および [PowerApps 管理センター][1]で作成できます。 環境を作成すると、その環境の環境管理者ロールに自動的に追加されます。 環境管理者ロールまたは環境作成者ロールのメンバーとして参加できる環境の数に制限はありません。 環境の詳細については、「[PowerApps での環境の管理](environments-administration.md)」を参照してください。 環境を作成する方法については、「[環境を作成する](create-environment.md)」を参照してください。

![](./media/environments-overview/CreateEnvironmentDialog-New.png)


## <a name="managing-environments-for-your-organization"></a>組織の環境の管理
PowerApps 管理センターでは、作成した環境、または環境管理者ロールが付与されている環境をすべて管理できます。 管理センターでは、環境に対して、次を含むすべての管理操作を実行できます。

* Environment Admin ロールまたは Environment Maker ロールのいずれかからユーザーまたはグループを追加または削除する。  詳細については、「[PowerApps での環境の管理](environments-administration.md)」を参照してください。
* 環境に Common Data Service データベースをプロビジョニングする。 詳細については、「[Create a Common Data Service database (Common Data Service サービスの作成)](create-database.md)」を参照してください。
* データ損失防止ポリシーを設定する。 詳細については、[データ損失防止ポリシー](prevent-data-loss.md)に関するページを参照してください。
* データベースのセキュリティ ポリシーを設定する (オープン ポリシーまたは制限付きポリシー)。 詳細については、「[Configure database security (データベース セキュリティの構成)](database-security.md)」を参照してください。
* Azure AD テナントのグローバル管理者ロールのメンバー (Office 365 のグローバル管理者を含む) も、PowerApps 管理センターで、テナントに作成したすべての環境を管理し、テナント全体のポリシーを設定できます。

<!--Reference links in article-->
[1]: https://admin.powerapps.com
[2]: https://web.powerapps.com
[3]: https://aka.ms/cdspreviewtoga
