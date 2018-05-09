---
title: データ主体の権利 (DSR) による PowerApps 顧客データに対する要求への対応 | Microsoft Docs
description: データ主体の権利 (DSR) による PowerApps 顧客データの要求に対応する方法を説明します
services: powerapps
suite: powerapps
documentationcenter: na
author: jamesol-msft
manager: kfile
editor: ''
tags: ''
ms-topic: article
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/23/2018
ms.author: jamesol
ms.openlocfilehash: 567a1e5d93d21fc315fe61b965ffb9005111172c
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="responding-to-data-subject-rights-dsr-requests-for-powerapps-customer-data"></a>データ主体の権利 (DSR) による PowerApps 顧客データに対する要求への対応

## <a name="introduction-to-dsr-requests"></a>DSR 要求の概要
欧州連合 (EU) の一般データ保護規則 (GDPR) は、規制において "*データ主体*" と呼ばれる人に、雇用主または他の種類の機関や組織 ("*データ コントローラー*" または単に "*コントローラー*" と呼ばれます) によって収集された個人データを管理する権限を与えます。 GDPR での個人データは、識別された自然人または識別可能な自然人に関連するすべてのデータと、非常に幅広く定義されています。 GDPR では、データ主体には個人データに関して次のことを行う権利が与えられています。

* コピーを取得する
* 修正を要求する
* 処理を制限する
* 削除する
* 別のコントローラーに移動できるように電子的な形式で受け取る

データ主体がコントローラーに対して個人データへの操作を実行するよう正式に要求することを、データ主体の権利 (DSR) 要求と呼びます。

この記事では、Microsoft が GDPR のために準備していることの説明、PowerApps、Microsoft Flow、Common Data Service (CDS) for Apps の使用時に GDPR コンプライアンスをサポートするためにお客様が実行できる手順の例を示します。 コントローラーのお客様が DSR 要求に対応して Microsoft クラウド内の個人データを検索、アクセス、操作するときに役立つ、Microsoft の製品、サービス、管理ツールの使用方法について説明します。

この記事では次の操作について説明されています。

* **検出** — 検索および検出ツールを使用して、DSR 要求の対象である可能性がある顧客データを簡単に検索します。 可能性のある応答ドキュメントが収集されると、以下の 1 つ以上の DSR アクションを実行して、要求に応答できます。 または、DSR 要求への応答に関する組織のガイドラインを要求が満たしていないと判断する場合もあります。

* **アクセス** — Microsoft のクラウドに存在する個人データを取得し、要求された場合は、データ主体が使用可能なそのデータのコピーを作成します。

* **修正** — 必要に応じて、個人データを変更するか、個人データに対して他の要求されたアクションを実施します。

* **制限** — さまざまなオンライン サービスに対するライセンスを削除するか、または可能な場合は目的のサービスをオフにすることで、個人データの処理を制限します。 また、Microsoft のクラウドからデータを削除して、オンプレミスの場所や別の場所にデータを保持することもできます。

* **削除** — Microsoft のクラウドに存在する個人データを完全に削除します。

* **エクスポート** — 個人データの (コンピューターが判読できる形式の) 電子コピーを、データ主体に提供します。

## <a name="discover"></a>Discover
DSR 要求に応答する最初のステップは、要求の対象である個人データを見つけることです。 対象の個人データを探して確認するこの最初のステップは、DSR 要求に応えるか断るかを決める組織の要件を DSR 要求が満たしているかどうかを判断するのに役立ちます。 たとえば、対象の個人データを探して確認した後で、要求に応えると、他のユーザーの権利や自由が損なわれる可能性があるため、要求は組織の要件を満たしていないものと判断する場合があります。

### <a name="step-1-find-personal-data-for-the-user-in-powerapps"></a>ステップ 1: PowerApps でユーザーの個人データを検索する
特定ユーザーの個人データを含む PowerApps リソースの種類の概要を次に示します。

個人データが含まれるリソース |    目的
--- | ---
環境 |   環境とは、組織のビジネス データ、アプリ、フローを保管、管理、共有するためのスペースです。 [詳細情報](https://go.microsoft.com/fwlink/?linkid=872239)
環境のアクセス許可 | ユーザーは、環境ロールを割り当てられることで、環境内での作成者権限および管理者権限を許可されます。 [詳細情報](https://go.microsoft.com/fwlink/?linkid=872240)
キャンバス アプリ  | 空のキャンバスから構築して、200 を超えるデータ ソースに接続することができる、クロスプラットフォームのビジネス アプリです。 [詳細情報](https://go.microsoft.com/fwlink/?linkid=872241)
キャンバス アプリのアクセス許可  | キャンバス アプリは、組織内のユーザーと共有することができます。 [詳細情報](https://go.microsoft.com/fwlink/?linkid=872242)
接続  | コネクタによって使用され、API、システム、データベースなどへの接続に対応します。 [詳細情報](https://go.microsoft.com/fwlink/?linkid=872243)
接続のアクセス許可  | 特定の種類の接続は、組織内のユーザーと共有することができます。 [詳細情報](https://go.microsoft.com/fwlink/?linkid=872244)
カスタム コネクタ    | PowerApps の標準コネクタのいずれでも提供されていないデータ ソースへのアクセスを提供する、ユーザーが作成したカスタム コネクタです。 [詳細情報](https://go.microsoft.com/fwlink/?linkid=872245)
カスタム コネクタのアクセス許可    | カスタム コネクタは、組織内のユーザーと共有することができます。 [詳細情報](https://go.microsoft.com/fwlink/?linkid=872246)
PowerApps のユーザーおよびユーザー アプリの設定    | PowerApps では、PowerApps ランタイムとポータル エクスペリエンスを提供するために使われる、複数のユーザー設定と設定が格納されます。
PowerApps の通知 | PowerApps は、アプリがユーザーと共有されたときや、CDS for Apps のエクスポート操作が完了したときなど、複数の種類の通知をユーザーに送信します。
ゲートウェイ | ゲートウェイはオンプレミスのデータ ゲートウェイであり、ユーザーはそれをインストールすることで、PowerApps とクラウド内に存在しないデータ ソースの間でデータをすばやく安全に転送できます。 [詳細情報](https://go.microsoft.com/fwlink/?linkid=872247)
ゲートウェイのアクセス許可 | ゲートウェイは、組織内のユーザーと共有することができます。 [詳細情報](https://go.microsoft.com/fwlink/?linkid=872249)
モデル駆動型アプリとモデル駆動型アプリのアクセス許可  | モデル駆動型アプリの設計は、コンポーネントに焦点を当てたアプリ開発の手法です。 モデル駆動型アプリおよびそのユーザー アクセスのアクセス許可は、CDS for Apps データベース内のデータとして格納されます。  [詳細情報](https://go.microsoft.com/fwlink/?linkid=872248)

PowerApps では、特定のユーザーの個人データを検索するために以下のエクスペリエンスが用意されています。

- **Web サイト アクセス**: [PowerApps サイト](https://web.powerapps.com)、[PowerApps 管理センター](https://admin.powerapps.com/)、[Office 365 Service Trust Portal](https://servicetrust.microsoft.com/)
- **PowerShell アクセス**: PowerApps コマンドレット ([アプリ作成者](https://go.microsoft.com/fwlink/?linkid=871448)用と[管理者](https://go.microsoft.com/fwlink/?linkid=871804)用) および[オンプレミス ゲートウェイ コマンドレット](https://go.microsoft.com/fwlink/?linkid=872238)

これらのエクスペリエンスを使ってリソースの種類ごとに特定ユーザーの個人データを検索する方法の詳細な手順については、「[データ主体の権利 (DSR) による PowerApps 顧客データ エクスポート要求への対応](powerapps-gdpr-export-dsr.md)」をご覧ください。

データが見つかったら、特定のアクションを実行してデータ主体による要求を満たすことができます。

### <a name="step-2-find-personal-data-for-the-user-in-microsoft-flow"></a>ステップ 2: Microsoft Flow でユーザーの個人データを検索する
PowerApps ライセンスには、常に Microsoft Flow の機能が含まれています。 PowerApps ライセンスに含まれるだけでなく、Microsoft Flow はスタンドアロン サービスとして利用することもできます。

Microsoft Flow サービスによって格納される個人データを発見する方法のガイダンスについては、「[Microsoft Flow に対する GDPR データ主体の要求への応答](https://go.microsoft.com/fwlink/?linkid=872250)」をご覧ください。

> [!IMPORTANT]
> 管理者には、PowerApps ユーザーに対してこの手順を完了することをお勧めします

### <a name="step-3-find-personal-data-for-the-user-in-instances-of-cds-for-apps"></a>ステップ 3: CDS for Apps のインスタンスでユーザーの個人データを検索する
PowerApps Community Plan などの特定の PowerApps ライセンスを持つ組織内のユーザーは、CDS for Apps のインスタンスを作成し、CDS for Apps 上でアプリを作成して構築できます。 PowerApps Community Plan は無料のライセンスであり、ユーザーは個々の環境で CDS for Apps を試すことができます。 各 PowerApps ライセンスに含まれる機能については、[PowerApps の価格](https://powerapps.microsoft.com/pricing/)に関するページをご覧ください。

CDS for Apps によって格納される個人データを発見する方法のガイダンスについては、「[Common Data Service for Apps での顧客データのデータ主体の権利 (DSR) 要求に対する対応](common-data-service-gdpr-dsr-guide.md)」をご覧ください。

> [!IMPORTANT]
> 管理者には、PowerApps ユーザーに対してこの手順を完了することをお勧めします。

## <a name="rectify"></a>修正
データ主体から組織のデータに存在する個人データの修正を要求された場合、管理者と組織は要求に応えるのが適切かどうかを判断する必要があります。 データの修正には、ドキュメントまたは他の種類のアイテムに含まれる個人データの編集、改訂、削除が含まれる場合があります。

Azure Active Directory を使って、PowerApps 内のユーザーの ID (個人データ) を管理することができます。 企業の顧客は、特定の Microsoft サービ内の限られた編集機能を使って、DSR 修正要求を管理することができます。 データ プロセッサとしての Microsoft は、システムによって生成されたログを修正する機能を提供していません。ログは実際のアクティビティを反映しており、Microsoft のサービス内でのイベントの履歴レコードを構成しているためです。 詳細については、「[GDPR: Data Subject Requests (DSRs)](https://servicetrust.microsoft.com/ViewPage/GDPRDSR)」(GDPR: データ主体の要求 (DSR)) をご覧ください。

## <a name="restrict"></a>制限
データ主体が、自分の個人データの処理を制限することを要求する場合があります。  それに対し、既存のアプリケーション プログラミング インターフェイス (API) と、ユーザー インターフェイス (UI) の両方が提供されています。  これらのエクスペリエンスにより、企業顧客のテナント管理者は、データ エクスポートとデータ削除を組み合わせて、このような DSR を管理できます。 顧客は次のことを要求する場合があります。

* ユーザーの次のような個人データの電子コピーをエクスポートする。

    - アカウント
    - システムで生成されたログ
    - 関連付けられているログ

* Microsoft システム内に存在するアカウントおよび関連データを削除する。

## <a name="export"></a>エクスポート
"データ ポータビリティの権利" では、データ主体は別のデータのコントローラーに送信できる電子形式 (つまり、構造化された、一般的に使用される、マシンが読み取り可能で相互運用可能な形式) で、個人データのコピーを要求できます。

詳細については、「[データ主体の権利 (DSR) による PowerApps 顧客データ エクスポート要求への対応](powerapps-gdpr-export-dsr.md)」をご覧ください。

## <a name="delete"></a>削除
組織の顧客データから個人データを削除することによる "忘れられる権利" は、GDPR での重要な保護です。 個人データの削除には、システムによって生成されたログは含まれますが、監査ログ情報は含まれません。

PowerApps では、組織の日常業務の重要な一部である基幹業務アプリケーションを構築できます。 ユーザーが組織を離れるときは、手作業で確認し、ユーザーが作成した特定のデータとリソースを削除するかどうかを判断する必要があります。 その他の顧客データは、Azure Active Directory からユーザーのアカウントが削除されるとき常に自動的に削除されます。

詳細については、[データ主体の権利 (DSR) による PowerApps 顧客データ削除要求への対応](powerapps-gdpr-delete-dsr.md)に関するページをご覧ください。
