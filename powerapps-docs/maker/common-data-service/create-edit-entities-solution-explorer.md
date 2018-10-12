---
title: ソリューション エクスプローラーを使用したエンティティの作成と編集 | MicrosoftDocs
description: ソリューション エクスプローラーを使用してエンティティを作成する方法について説明します
ms.custom: ''
ms.date: 05/30/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
author: Mattp123
ms.author: matp
manager: kvivek
ms.openlocfilehash: 48025088da85bf0685ba1a46efa4f3a989a20a58
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39690293"
---
# <a name="create-and-edit-entities-using-solution-explorer"></a>ソリューション エクスプローラーを使用したエンティティの作成と編集

一般的なほとんどの状況で PowerApps ポータルを使用してエンティティを簡単に作成できますが、一部の機能が実装されないことがあります。 「[Common Data Service for Apps でのエンティティの作成と編集](create-edit-entities.md)」で説明されている要件を満たす必要があるとき、ソリューション エクスプローラーでエンティティを作成または編集することで要件を達成できます。

## <a name="open-solution-explorer"></a>ソリューション エクスプローラーを開く

作成するエンティティの名前には、カスタマイズのプレフィックスが含まれます。 これは、使用中のソリューションのソリューション発行元に基づいて設定されます。 カスタマイズのプレフィックスが重要であれば、カスタマイズのプレフィックスがこのエンティティに求めるプレフィックスになる、アンマネージド ソリューションを使用してください。 詳細: [既定の発行者のソリューション発行者の接頭辞を変更する](change-solution-publisher-prefix.md) 

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

## <a name="view-entities"></a>エンティティを表示する

ソリューション エクスプローラーの **[コンポーネント]** ノードで **[エンティティ]** ノードを選択します。

![ソリューション エクスプローラーでエンティティを表示する](media/view-entities-solution-explorer.png)

## <a name="create-an-entity"></a>エンティティを作成する

[エンティティを表示している](#view-entities)とき、**[新規]** を選択して新しいエンティティ フォームを開きます。

![ソリューション エクスプローラーの新しいエンティティ フォーム](media/new-entity-form-solution-explorer.png)

新しいエンティティ フォームには 2 つのタブがあります。 **[全般]** タブには、エンティティ オプションがあります。 **[プライマリ フィールド]** タブには、各エンティティに与えられているテキスト フィールドの特別な単一行に関するオプションがあります。この行によって、ルックアップ フィールドでエンティティを開くためのリンクがあるときに表示されるテキストが定義されます。

各セクションの詳細については、次をご覧ください。
- [プライマリ フィールドを構成する](#configure-the-primary-field)
- [必須フィールドを構成する](#configure-required-fields)

> [!NOTE]
> エンティティをカスタム活動にすることもできます。 この選択肢では、既定のオプション値の一部が変更されます。 詳細: [カスタム活動エンティティの作成](#create-custom-activity-entity)

エンティティに必須のオプションを設定したら、 ![[コマンドの保存]](media/save-entity-icon-solution-explorer.png) をクリックしてカスタム エンティティを作成します。

### <a name="configure-the-primary-field"></a>プライマリ フィールドを構成する

**[プライマリ フィールド]** タブでは、通常、プライマリ フィールドの既定値をそのまま使用できますが、次のオプションがあります。

|フィールド   |説明  |
|---------|---------|
|**表示名**|フォームとリストでこのフィールドに表示されるローカライズ可能なラベルを入力します。 既定値は **[名前]** です。|
|**Name**|このフィールドに対してシステムで使用される名前を設定します。 既定値は `<customization prefix>_name` です。|
|**最大長**|フィールド値の最大長を入力します。 既定値は 100 です。|

> [!NOTE]
> エンティティが活動エンティティの場合、これらのオプションは適用されません。 詳細: [カスタム活動エンティティの作成](#create-custom-activity-entity)

### <a name="configure-required-fields"></a>必須フィールドを構成する

**[全般]** タブではいくつかのオプションが必須となっており、それを指定しないとエンティティを保存できません。

|フィールド   |説明  |
|---------|---------|
|**表示名**|これは、アプリに表示されるエンティティの単数形の名前です。<br />これは後で変更できます。|
|**複数形の名前**|これは、アプリに表示されるエンティティの複数形の名前です。<br />これは後で変更できます。|
|**Name**|このフィールドは、入力した表示名に基づいて事前入力されます。 ソリューション発行元のカスタマイズ プレフィックスが含まれます。|
|**所有権**|ユーザー (またはチーム) による所有か組織による所有を選択できます。 詳細: [Entity ownership](types-of-entities.md#entity-ownership) (エンティティ所有権)|

## <a name="edit-an-entity"></a>エンティティを編集する

[エンティティを表示している](#view-entities)とき、編集するエンティティを選択するか、保存したばかりの新しいエンティティの編集を続行します。

> [!NOTE]
> マネージド ソリューションに含まれる標準エンティティまたはカスタム エンティティには、変更回数に関する上限が与えられている場合があります。 オプションが利用できないか、無効になっている場合、変更は許可されません。

#### <a name="set-once-options"></a>1 回だけ設定するオプション

次のオプションは 1 回だけ設定できます。設定後は変更できません。 これらのオプションは必要なときだけ設定するように心がけてください。

<!-- 
Same data is presented in edit-entities.md
Both should point to this include
 -->
[!INCLUDE [cc_entity-set-once-options-table](../../includes/cc_entity-set-once-options-table.md)]

#### <a name="options-that-you-can-change"></a>変更可能なオプション

次のプロパティはいつでも変更できます。

<!-- 
Same data is presented in edit-entities.md
Both should point to this include
 -->
[!INCLUDE [cc_entity-changeable-options-table](../../includes/cc_entity-changeable-options-table.md)]

次の変更も行うことができます。
- [Common Data Service for Apps でのフィールドの作成と編集](create-edit-fields.md)
- [エンティティ間のリレーションシップの作成と編集](create-edit-entity-relationships.md)
- [フォームの作成および設計](../model-driven-apps/create-design-forms.md)
- [プロセスを標準化するビジネス プロセス フローの作成](/flow/create-business-process-flow)

## <a name="delete-an-entity"></a>エンティティを削除する

システム管理者ロールが与えられているユーザーは、マネージド ソリューションに含まれないカスタム エンティティを削除できます。  
  
> [!IMPORTANT]
>  カスタム エンティティを削除すると、そのエンティティのデータを保存しているデータベース テーブルが削除され、それに含まれるすべてのデータが失われます。 カスタム エンティティに対して親のリレーションシップを持つ関連レコードも削除されます。 親のリレーションシップに関する詳細は、「[エンティティ間のリレーションシップの作成と編集](create-edit-entity-relationships.md)」でご覧ください。  
  
> [!NOTE]
> 削除されたエンティティからデータを復元する唯一の方法は、エンティティが削除される前のポイントからデータベースを復元することです。 詳細: [インスタンスのバックアップと復元](/dynamics365/customer-engagement/admin/backup-restore-instances)

[エンティティを表示している](#view-entities)とき、ツール バーの ![[削除コマンド]](media/delete.gif) コマンドをクリックします。

エンティティを表示しているとき、メニュー バーの削除コマンドを使用します。

![削除コマンド](media/delete-custom-entity-solution-explorer.png)

> [!WARNING]
> データが含まれるエンティティを削除すると、データがすべて削除されます。 削除されたデータは、データベースのバックアップでのみ復旧できます。

> [!NOTE]
> エンティティ依存関係がある場合、**[コンポーネントを削除できません]** エラーと **[詳細]** リンクが表示されます。このリンクから、エンティティを削除できない理由に関する情報を見つけることができます。 ほとんどの場合、依存関係も削除しなければならないことに起因します。 
>
> 複数の依存関係が 1 つのエンティティの削除を阻止していることもあります。 このエラー メッセージには、最初の依存関係のみが示されていることがあります。 依存関係を見つける代替手法については、「[エンティティ依存関係を特定する](#identify-entity-dependencies)」を参照してください。



### <a name="identify-entity-dependencies"></a>エンティティ依存関係を特定する

エンティティを削除する前に削除を阻止する依存関係を特定できます。 

1. ソリューション エクスプローラーでエンティティを選択し、コマンド バーで **[依存関係の表示]** をクリックします。

![[依存関係の表示] コマンド](media/entity-show-dependencies.png)

2. ダイアログ ウィンドウが開いたら、一覧を右にスクロールし、**[依存関係の種類]** 列を表示します。

![依存関係の種類が発行済み](media/published-entity-dependency.png)

依存関係が**発行済み**の場合、エンティティの削除が阻止されます。 依存関係が**内部**の場合、自動的に解決されるはずです。  

3. このような発行済みの依存関係を削除すれば、エンティティを削除できるようになるはずです。

 > [!NOTE]
 > よくある依存関係は、削除しようとしているエンティティの参照フィールドが別のエンティティ フォームに含まれているというものです。 ルックアップ フィールドをフォームから削除すると、依存関係が解決されます。

## <a name="create-custom-activity-entity"></a>カスタム活動エンティティを作成する

活動エンティティとしてエンティティを作成するには、このトピックで説明した同じ手順を使用しますが、**[Define as an activity entity]\(活動エンティティとして定義する\)** を選択します。

![活動エンティティとして定義する](media/create-activity-entity-solution-explorer.png)

活動エンティティは、暦に入力できるアクションを追跡する特別な種類のエンティティです。 詳細: [活動エンティティ](types-of-entities.md#activity-entities)。

このオプションを設定すると、一部のエンティティ プロパティで互換性がなくなります。 活動エンティティは、すべての活動エンティティで使用される標準の動作に従う必要があります。

プライマリ フィールドの **[名前]** と **[表示名]** は **[件名]** に設定されます。これは変更できません。

次のオプションは既定で設定されており、変更できません。

 - **フィードバック**
 - **メモ (添付ファイルを含む)**
 - **接続**
 - **キュー**
 - **Dynamics 365 for Outlook のオフライン機能**

次のオプションは設定できません。

- **このエンティティが表示される領域**
- **活動**
- **電子メールの送信**
- **差し込み印刷**
- **単一レコード監査**
- **複数レコード監査**

## <a name="create-a-virtual-entity"></a>仮想エンティティを作成する

一部のオプションは、仮想エンティティの作成時にのみ使用されます。

|オプション   |説明  |
|---------|---------|
|**仮想エンティティ**|エンティティが仮想エンティティであるかどうか。|
|**データ ソース**|エンティティのデータ ソース。|

詳細: [Create and edit virtual entities that contain data from an external data source](create-edit-virtual-entities.md) (外部データ ソースからのデータを含むエンティティの作成と編集)

### <a name="see-also"></a>関連項目
[Common Data Service for Apps でのエンティティの作成と編集](create-edit-entities.md)<br />
[チュートリアル: PowerApps でコンポーネントがあるカスタム エンティティを作成する](/powerapps/maker/common-data-service/create-custom-entity)<br />
[ソリューションを作成する](create-solution.md)