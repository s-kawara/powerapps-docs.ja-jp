---
title: ソリューション エクスプローラーを使用してエンティティを作成および編集する | MicrosoftDocs
description: ソリューション エクスプローラーを使用してエンティティを作成する方法について説明します
ms.custom: ''
ms.date: 05/30/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
author: Mattp123
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="create-and-edit-entities-using-solution-explorer"></a>ソリューション エクスプローラーを使用してエンティティを作成および編集する

最も一般的な状況で PowerApps ポータルを使用してエンティティを簡単に作成できますが、すべての機能が実装されているわけではありません。 [Common Data Service でのエンティティの作成および編集](create-edit-entities.md) に記載されている要件を満たす必要がある場合は、ソリューション エクスプローラーを使用してエンティティを作成または編集することでそれらを達成できます。

## <a name="open-solution-explorer"></a>ソリューション エクスプローラーを開きます

作成するエンティティの名前の一部はカスタマイズの接頭辞です。 これは、作業中のソリューションの発行者に基づいて設定されます。 カスタマイズの接頭辞に注意を払う場合は、カスタマイズの接頭辞がこのエンティティに対して必要な接頭辞であるアンマネージド ソリューションで作業するようにします。 詳細: [ソリューション発行者の接頭辞を変更する](change-solution-publisher-prefix.md) 

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

## <a name="view-entities"></a>エンティティの表示

ソリューション エクスプローラーで、**コンポーネント** ノードで、**エンティティ** ノードを選択します。

![ソリューション エクスプローラーでエンティティを表示する](media/view-entities-solution-explorer.png)

## <a name="create-an-entity"></a>エンティティの作成

[エンティティを表示](#view-entities)しながら、**新規** を選択して新しいエンティティ フォームを開きます。

![ソリューション エクスプローラーの新しいエンティティ フォーム](media/new-entity-form-solution-explorer.png)

新しいエンティティ フォームには 2 つのタブがあります。 **概要** タブにはエンティティ オプションがあります。 **プライマリ フィールド** タブには、各エンティティが持つテキスト フィールドの特殊な 1 行に関するオプションがあり、検索フィールドにエンティティを開くリンクがあるときに表示されるテキストを定義します。

各セクションの詳細については、以下を参照してください。
- [プライマリ フィールドの構成](#configure-the-primary-field)
- [必須フィールドの構成](#configure-required-fields)

> [!NOTE]
> エンティティをユーザー定義の活動にすることもできます。 この選択により、一部の既定のオプション値が変更されます。 詳細: [ユーザー定義活動エンティティを作成する](#create-custom-activity-entity)

エンティティの必須オプションを設定したら、 ![コマンドの保存](media/save-entity-icon-solution-explorer.png) をクリックしてユーザー定義エンティティを作成します。

### <a name="configure-the-primary-field"></a>プライマリ フィールドの構成

**プライマリ フィールド** タブでは、通常プライマリ フィールドの既定値をそのまま使用することができますが、次のオプションがあります。

|フィールド   |説明  |
|---------|---------|
|**表示名**|フォームおよびリストのこのフィールドに表示されるローカライズ可能なラベルを入力します。 既定値は **名前** です。|
|**名前**|このフィールドのシステムで使用される名前を設定します。 既定値は `<customization prefix>_name` です|
|**最大長**|フィールド値の最大長を入力します。 既定値は 100 です。|

> [!NOTE]
> これらのオプションは、エンティティが活動エンティティである場合は適用されません。 詳細: [ユーザー定義活動エンティティを作成する](#create-custom-activity-entity)

### <a name="configure-required-fields"></a>必須フィールドの構成

**概要** タブでは、オプションの一部は、エンティティを保存する前に必要です。

|フィールド   |説明  |
|---------|---------|
|**表示名**|これは、アプリに表示されるエンティティの単数形の名前です。<br />これは後で変更できます。|
|**複数名**|これは、アプリに表示されるエンティティの複数形の名前です。<br />これは後で変更できます。|
|**名前**|このフィールドは、ユーザーが入力する表示名に基づいて事前設定されます。 これには、ソリューション発行者のカスタマイズ接頭辞が含まれます。|
|**企業形態**|ユーザーか、あるいはチーム所有または組織所有のいずれかを選択できます。 詳細情報: [エンティティの所有権](types-of-entities.md#entity-ownership)|

## <a name="edit-an-entity"></a>エンティティの編集

[エンティティを表示](#view-entities)しているとき、編集するエンティティを選択するか、前の手順で保存した新しいエンティティの編集を続行します。

> [!NOTE]
> 標準エンティティまたは管理ソリューションの一部であるユーザー定義エンティティには、適用できる変更の制限がある場合があります。 オプションを使用できない場合や有効でない場合は、変更を行うことができません。

#### <a name="set-once-options"></a>変更不可オプション

次のオプションは 1 回のみ設定でき、設定後に変更を行うことはできません。 必要なときにのみこれらのオプションを設定するように注意してください。

<!-- 
Same data is presented in edit-entities.md
Both should point to this include
 -->
[!INCLUDE [cc_entity-set-once-options-table](../../includes/cc_entity-set-once-options-table.md)]

#### <a name="options-that-you-can-change"></a>変更可能なオプション

以下のプロパティは、いつでも変更できます。

<!-- 
Same data is presented in edit-entities.md
Both should point to this include
 -->
[!INCLUDE [cc_entity-changeable-options-table](../../includes/cc_entity-changeable-options-table.md)]

次の変更を加えることもできます。
- [Common Data Service のフィールドの作成および編集](create-edit-fields.md)
- [エンティティ間の関連付けの作成および編集](create-edit-entity-relationships.md)
- [フォームの作成および設計](../model-driven-apps/create-design-forms.md)
- [プロセスを標準化する業務プロセス フローの作成](/flow/create-business-process-flow)

## <a name="delete-an-entity"></a>エンティティの削除

システム管理者のセキュリティ ロールを持つユーザーとして、管理ソリューションの一部でないユーザー定義エンティティを削除できます。  
  
> [!IMPORTANT]
>  ユーザー定義エンティティを削除すると、そのエンティティのデータを保存しているデータベース テーブルが削除され、それらのテーブルに含まれるすべてのデータが失われます。 ユーザー定義エンティティと上位下位の関連付けのある関連レコードも削除されます。 上位下位の関連付けの詳細については、「[エンティティ間の関連付けの作成と編集](create-edit-entity-relationships.md)」を参照してください。  
  
> [!NOTE]
> 削除されたエンティティからのデータを回復する唯一の方法は、エンティティが削除される前の時点からデータベースを復元します。 詳細については、「[インスタンスのバックアップと復元](/dynamics365/customer-engagement/admin/backup-restore-instances)」を参照してください。

[エンティティを表示](#view-entities)しているとき、ツール バーの ![削除コマンド](media/delete.gif) コマンドをクリックします。

エンティティを表示しているとき、メニュー バーで削除コマンドを使用します。

![削除コマンド](media/delete-custom-entity-solution-explorer.png)

> [!WARNING]
> データが含まれるエンティティを削除すると、すべてのデータが削除されます。 このデータは、データベースのバックアップによってのみ取得できます。

> [!NOTE]
> エンティティの依存関係がある場合、**詳細** リンクが記載された **コンポーネントは削除できません** エラーが表示されます。リンクを使用すると、エンティティを削除できない理由を調べることができます。 ほとんどの場合、これは削除が必要な依存関係のためです。 
>
> エンティティの削除を妨げる複数の依存関係がある場合があります。 このエラー メッセージには、最初の 1 つのみ表示される場合があります。 依存関係を検出する別の方法については、「[エンティティの依存関係の特定](#identify-entity-dependencies)」を参照してください



### <a name="identify-entity-dependencies"></a>エンティティの依存関係の特定

削除する前にエンティティが削除されないようにする依存関係を特定できます。 

1. 選択したエンティティを持つソリューション エクスプローラーで、コマンド バーで **依存関係を表示する** をクリックします。

![[依存関係を表示] コマンド](media/entity-show-dependencies.png)

2. 開いたダイアログ ウィンドウで、一覧を右にスクロールして、**依存関係の種類** 列を表示します。

![公開された依存関係の種類](media/published-entity-dependency.png)

**公開済み** 依存関係は、エンティティを削除する操作をブロックします。 **内部** 依存関係は、システムによって解決する必要があります。  

3. これらの公開済み依存関係を削除すると、エンティティを削除できるようになります。

 > [!NOTE]
 > 非常によくあるの依存関係は、別のエンティティ フォームに、削除するエンティティの検索フィールドがあることです。 フォームから検索フィールドを削除すると、依存関係が解決されます。

## <a name="create-custom-activity-entity"></a>カスタム活動エンティティの作成

活動エンティティとしてエンティティを作成するには、**活動エンティティとして定義** を選択する以外、このトピックに記載されているのと同じ手順を使用します。

![活動エンティティとして定義](media/create-activity-entity-solution-explorer.png)

活動エンティティは、カレンダーにエントリを作成できるアクションを追跡するエンティティに関する特別な種類です。 詳細: [活動エンティティ](types-of-entities.md#activity-entities)。

このオプションを設定すると、エンティティ プロパティとの互換性がなくなります。 活動エンティティは、すべての活動エンティティが使用する標準動作に準拠する必要があります。

プライマリ フィールド **名前** と **表示名** は、**情報カテゴリ** に設定され、これを変更することはできません。

次のオプションは既定で設定されており、変更できません。

 - **フィードバック**
 - **メモ (添付ファイルを含む)**
 - **接続**
 - **キュー**
 - **Outlook 用 Dynamics 365 のオフライン機能**

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
|**仮想エンティティ**|エンティティが仮想エンティティかどうか。|
|**データ ソース**|エンティティのデータ ソース。|

詳細情報: [外部データ ソースからのデータを格納する仮想エンティティの作成および編集](create-edit-virtual-entities.md)

### <a name="see-also"></a>関連項目
[Common Data Service でエンティティを作成および編集する](create-edit-entities.md)<br />
[チュートリアル: PowerApps でのコンポーネントがあるユーザー定義エンティティの作成](/powerapps/maker/common-data-service/create-custom-entity)<br />
[ソリューションの作成](create-solution.md)
