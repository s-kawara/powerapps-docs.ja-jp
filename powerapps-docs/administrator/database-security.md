---
title: 環境セキュリティの構成 | Microsoft Docs
description: このトピックでは、環境セキュリティを構成する方法について説明します。
author: manasmams
manager: kfile
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.date: 03/21/2018
ms.author: manasma
ms.openlocfilehash: d9bd70acaacbbeda98c14337035a233b7c70c181
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34168161"
---
# <a name="configure-environment-security"></a>環境セキュリティの構成
Common Data Service (CDS) for Apps では、ロールベースのセキュリティ モデルを使用して、データベースへのアクセスをセキュリティで保護します。 このトピックでは、アプリのセキュリティ保護に必要なセキュリティ アーティファクトを作成する方法を説明します。 これらのユーザー ロールは、データへの実行時アクセスを制御するもので、環境管理者や環境作成者を管理する環境ロールとは別のものです。 環境の概要については、「[Environments overview (環境の概要)](environments-overview.md)」を参照してください。

## <a name="assign-security-roles-to-users"></a>ユーザーにセキュリティ ロールを割り当てる
セキュリティ ロールは、一連のアクセス レベルとアクセス許可を使用してデータへのユーザーのアクセスを制御します。 アクセス レベルと、特定のセキュリティ ロールに含まれているアクセス許可を組み合わせて、ユーザーのデータの閲覧とそのデータのユーザー操作に対して制限を設定します。

環境ロールにユーザーまたはセキュリティ グループを割り当てるために、環境管理者は次の手順を [PowerApps 管理センター][1]で実行できます。

1. 環境一覧から環境を選択します。

    ![](./media/environment-admin/environment-list-new.png)

2. **[セキュリティ]** タブを選択します。

3. **環境内のユーザー一覧の表示**を選択することで、環境にユーザーが既に存在するかどうかを確認します。
    
    ![](./media/database-security/security-viewuser.png)

4. ユーザーが存在しない場合、PowerApps 管理センターからユーザーを追加できます。追加するには、組織内のユーザーのメール アドレスを指定して **[ユーザーの追加]** を選びます。

    ![](./media/database-security/security-adduser.png)

    数分待ってから、環境内のユーザーの一覧でユーザーが使用可能かどうかを確認します。
  
5. 環境内のユーザーの一覧からユーザーを選択します。

    ![](./media/environment-admin/D365-Select-User.png)

6. ロールをユーザーに割り当てます。

    ![](./media/environment-admin/D365-Assign-Role.png)

    > [!NOTE]
    > 現在のところ、ロールはユーザーにのみ割り当てることができます。 セキュリティ グループへのロールの割り当ては、実装予定の機能です。

7. **[OK]** を選択して環境ロールへの割り当てを更新します。

## <a name="predefined-security-roles"></a>定義済みのセキュリティ ロール
PowerApps 環境には、アプリの使用に必要な最小限のビジネス データへのアクセスを提供するというセキュリティのベスト プラクティス目標に一致するようにアクセス レベルが定義されている一般的なユーザー タスクを反映する定義済みのセキュリティ ロールが含まれます。

|セキュリティ ロール  |*データベースの特権  |説明 |
|---------|---------|---------|
|システム管理者     |  作成、読み取り、書き込み、削除、カスタマイズ、セキュリティ ロール       | セキュリティ ロールの作成、変更、割り当てなど、環境のカスタマイズまたは管理の完全なアクセス許可を持っています。 環境内のすべてのデータを表示できます。 詳細情報: [カスタマイズに必要な特権](https://docs.microsoft.com/dynamics365/customer-engagement/customize/privileges-required-customization)        |
|システム カスタマイザー     | 作成 (自己)、読み取り (自己)、書き込み (自己)、削除 (自己)、カスタマイズ         | 環境をカスタマイズする完全なアクセス許可を持っています。 ただし、自身が作成した環境エンティティのレコードのみを表示できます。 詳細情報: [カスタマイズに必要な特権](https://docs.microsoft.com/dynamics365/customer-engagement/customize/privileges-required-customization)        |
|環境作成者     |  なし       | アプリ、接続、カスタム API、ゲートウェイ、および Microsoft Flow を使用するフローなど、環境に関連付けられた新しいリソースを作成できます。 ただし、環境内のデータにアクセスする権限はありません。 詳細については、「[Environments overview](https://powerapps.microsoft.com/blog/powerapps-environments/)」(環境の概要) を参照してください。        |
|Common Data Service ユーザー     |  読み取り、作成 (自己)、書き込み (自己)、削除 (自己)       | 環境内でアプリを実行し、自分が所有するレコードについて共通タスクを実行できます。        |
|デリゲート     | 別のユーザーの代理で実行する        | 別のユーザーとしてコードを実行したり、偽装したりすることができます。  通常、別のセキュリティ ロールと併用してレコードへのアクセスを許可します。 詳細情報: [もう一方のユーザーの偽装](https://docs.microsoft.com/dynamics365/customer-engagement/developer/org-service/impersonate-another-user)        |

* 特権は、特記されていない限り、グローバル スコープです。

- 環境作成者ロールは、環境内にリソースを作成するだけでなく、環境内で自分が構築したアプリを組織内の他のユーザーに配布することもできます。 個々のユーザーとアプリを共有することができます。 詳細については、[PowerApps でのアプリの共有](../maker/canvas-apps/share-app.md)に関するページを参照してください。

- データベースに接続し、エンティティとセキュリティ ロールを作成または更新する必要のあるアプリを作成するユーザーには、環境作成者ロールとしての環境作成者だけでなく、システム カスタマイザー ロールを割り当て、データベースには特権を持たせないようにします。

## <a name="create-or-configure-a-custom-security-role"></a>ユーザー定義セキュリティ ロールを作成または構成する
自分のアプリがユーザー定義エンティティに基づいている場合、ユーザーがアプリを操作する前に、特権を明示的に指定する必要があります。 この場合、次のいずれかの方法を実行できます。
- 既存の定義済みセキュリティ ロールを拡張し、ユーザー定義エンティティに基づくレコードに対する権限が含まれるようにします。
- アプリのユーザーに対する権限を管理するためのユーザー定義セキュリティ ロールを作成します。

複数のアプリから使用できるレコードを保持する可能性がある環境の場合、異なる特権でデータにアクセスできるように複数のセキュリティ ロールが必要になることがあります。 例:
- 一部のユーザー (タイプ A) は読むこと、更新すること、他のレコードを添付することだけが必要なので、そのセキュリティ ロールは読み取り、書き込み、追加の特権を持っています。
- 他のユーザーは、タイプ A のユーザーが持つすべての特権に加えて、作成、追加、削除、共有を行うことができる必要があるので、そのセキュリティ ロールは、作成、読み取り、書き込み、追加、削除、割り当て、共有の特権を持っています。

アクセスとスコープの特権の詳細については、「[セキュリティ ロール](https://docs.microsoft.com/dynamics365/customer-engagement/admin/security-roles-privileges#security-roles)」を参照してください。

1. [PowerApps 管理センター][1]で、セキュリティ ロールを更新する環境を選択します。

    ![](./media/environment-admin/choose-environment-updated.png)

2. **[詳細]** タブのリンクをクリックし、Dynamics 365 管理センターの環境を管理します。

3. (環境と同じ名前の) インスタンスを選択し、[開く] をクリックします

    ![](./media/database-security/glados-instance-list.png)

4. ヘッダーにある **[設定]** をクリックし、**[セキュリティ]** を選択します

    ![](./media/database-security/dyn365-settings-security.png)

5. **[セキュリティ ロール]** を選択します

    ![](./media/database-security/dyn365-securityroles.png)

6. **[新規]** をクリックします

7. セキュリティ ロール デザイナーから、読み取り、書き込み、削除などのアクションと、そのアクションを実行するスコープを選択します。

8. タブを選択してエンティティを検索します。たとえば、ユーザー定義エンティティのアクセス許可を設定する場合は、**[ユーザー定義エンティティ]** タブを選択します。

9. **読み取り、書き込み、追加**特権を選択します。

10. **[保存して閉じる]** を選択します。



<!--Reference links in article-->
[1]: https://admin.powerapps.com
