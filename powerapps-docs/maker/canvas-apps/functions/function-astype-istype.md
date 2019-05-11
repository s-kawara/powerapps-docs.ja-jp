---
title: AsType および IsType 関数のキャンバス アプリ |Microsoft Docs
description: キャンバス アプリを含む構文と例を AsType と IsType 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 05/06/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: dafffcc148329be81f7544bdc2f0730f307ae4eb
ms.sourcegitcommit: f6c9e525130a03b8c76f0a4b4e90419604c5823c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2019
ms.locfileid: "65526056"
---
# <a name="astype-and-istype-functions-in-canvas-apps"></a>AsType および IsType 関数のキャンバス アプリ

特定のエンティティ型のレコードの参照を確認し、参照を特定の種類として扱われます。

## <a name="description"></a>説明

読み取り[レコードの参照とポリモーフィックな参照を理解する](../working-with-references.md)より広範な概要と詳細。

ルックアップ フィールドは、通常、特定のエンティティ内のレコードを参照します。 エンティティ型は、準備されていますが、単純なドット表記を使用して検索のフィールドを表示できます。 たとえば、**最初 (アカウント).'主要連絡先 '.'完全名 '** からについて説明します、**アカウント**エンティティを**主要連絡先**レコード、**連絡先**エンティティと抽出、**完全な名前**フィールド。

Common Data Service には、これらの例のように、エンティティのセットからレコードを参照できるポリモーフィックなルックアップ フィールドもサポートしています。

| ルックアップ フィールド | を参照できます。 |
|--------------|--------------|
| **所有者** | **ユーザー**または**チーム** |
| **顧客** | **アカウント**または**連絡先** |
| **に関する** | **アカウント**、**連絡先**、**ナレッジ**など。 |

キャンバス アプリの数式では、ポリモーフィックな参照を使用するレコードの参照を使用できます。 レコードの参照は、さまざまなエンティティを参照できる、ため、数式を記述するときに、どのフィールドが使用できますがわかりません。 *します。フィールド*表記は使用できません。 これらの数式は、実行時に、アプリで発生したレコードに対応する必要があります。

**IsType**関数は、レコードの参照が特定のエンティティ型を表しているかどうかをテストします。 ブール値を返します*true*または*false*します。

**AsType**関数はレコードの参照とも呼ば、特定のエンティティ型として扱います*キャスト*します。 エンティティのレコードの場合と同様の結果を使用して、使用して、もう一度*します。フィールド*そのレコードのフィールドのすべてにアクセスする表記法。 エラーは、特定の種類の参照がない場合に発生します。

これらの関数を使用して、まとめて最初のレコードのエンティティ型をテストし、として扱い、他人タイプのレコードのフィールドが使用できるようにします。

```powerapps-dot
If( IsType( First( Accounts ).Owner, Users ),
    AsType( First( Accounts ).Owner, Users ).'Full Name',
    AsType( First( Accounts ).Owner, Teams ).'Team Name'
)
```

レコードの参照のフィールドにアクセスしている場合にのみは、これらの関数を作成する必要があります。 たとえば、内のレコードの参照を使用することができます、 [**フィルター** ](function-filter-lookup.md)せずに機能させる**IsType**または**AsType**:

```powerapps-dot
Filter( Accounts, Owner = First( Users ) )
```

同様でのレコードの参照を使用することができます、 [**パッチ**](function-patch.md)関数。

```powerapps-dot
Patch( Accounts, First( Accounts ), { Owner: First( Teams ) } )
```  

内では、ように、レコードのコンテキストで使用される場合、 [**ギャラリー** ](../controls/control-gallery.md)または[**編集フォーム**](../controls/control-form-detail.md)コントロールを使用する必要があります、[グローバル曖昧性除去演算子](operators.md#disambiguation-operator)エンティティ型を参照します。 たとえば、次の数式が連絡先の一覧が表示されているギャラリーを有効に、**会社名**は、**顧客**参照。

```powerapps-dot
If( IsType( ThisItem.'Company Name', [@Accounts] ),
    AsType( ThisItem.'Company Name', [@Accounts] ).'Account Name',
    AsType( ThisItem.'Company Name', [@Contacts] ).'Full Name'
)
```

どちらの関数の名前を使って、エンティティに接続されているデータ ソースの種類を指定します。 操作する数式をテストまたはキャストする型の場合、アプリにデータ ソースを追加することも必要があります。 たとえば、追加する必要があります、**ユーザー**エンティティを使用する場合は、データ ソースとして**IsType**と**AsType**で、**所有者**参照とレコードそのエンティティ。 実際には、アプリで使用するデータ ソースのみを追加します。参照が参照するすべてのエンティティを追加する必要はありません。

レコードの参照がある場合*空白*、 **IsType**返します*false*と**AsType**返します*空白*します。 すべてのフィールドを*空白*レコードになります*空白*します。

## <a name="syntax"></a>構文

**AsType**( *RecordReference*, *EntityType* )

- *RecordReference* - 必須。 レコードの参照、多くの場合、複数のエンティティのいずれかのレコードを参照できますルックアップ フィールド。
- *EntityType* - 必須。 テスト対象の特定のエンティティ。

**IsType**( *RecordReference*, *EntityType* )

- *RecordReference* - 必須。 レコードの参照、多くの場合、複数のエンティティのいずれかのレコードを参照できますルックアップ フィールド。
- *EntityType* - 必須。 特定のどれにキャストするエンティティ。

## <a name="example"></a>例

[レコードの参照とポリモーフィックな参照を理解する](../working-with-references.md)詳細な使用例が含まれています。

1. タブレット用の空白のキャンバス アプリを作成します。

1. **ビュー** ] タブで [**データ ソース**、し、追加、**連絡先**と**アカウント**データ ソースとしてのエンティティ。
    > [!div class="mx-imgBorder"]
    > ![2 つのデータ ソースを空のアプリ: アカウントと連絡先](media/function-astype-istype/contacts-add-datasources.png)

1. 挿入、**ギャラリー**コントロールを**空白垂直**向き。

    > [!div class="mx-imgBorder"]
    > ![空の垂直レイアウトのギャラリー コントロールを挿入します。](media/function-astype-istype/contacts-customer-gallery.png)

1. **プロパティ** タブの右側のペインで、設定ギャラリーの**項目**プロパティを**連絡先**します。

    > [!div class="mx-imgBorder"]
    > ![プロパティ ペインで、連絡先フォルダーに項目を設定します。](media/function-astype-istype/contacts-customer-datasource.png)

1. ギャラリーのレイアウトを設定します**タイトルとサブタイトル**します。

    > [!div class="mx-imgBorder"]
    > ![プロパティ ペインからレイアウトの選択を開く](media/function-astype-istype/contacts-customer-layout.png)

    > [!div class="mx-imgBorder"]
    > ![タイトルとサブタイトルのレイアウトを設定します](media/function-astype-istype/contacts-customer-flyout.png)

1. **データ**ウィンドウで、開いている、 **Title1** 、一覧表示し、**フル_ネーム**:

    > [!div class="mx-imgBorder"]
    > ![タイトルの値の設定](media/function-astype-istype/contacts-customer-title.png)

1. 選択、 **Subtitle1**ラベル コントロール。

    > [!div class="mx-imgBorder"]
    > ![サブタイトルの値の設定](media/function-astype-istype/contacts-customer-subtitle.png)

1. 設定、**テキスト**プロパティの**Subtitle1**に次の式。

    ```powerapps-dot
    If( IsBlank( ThisItem.'Company Name' ), "--",
        IsType( ThisItem.'Company Name', [@Accounts] ),
            "Account: " & AsType( ThisItem.'Company Name', [@Accounts] ).'Account Name',
        "Contact: " & AsType( ThisItem.'Company Name', [@Contacts] ).'Full Name'
    )
    ```

    > [!div class="mx-imgBorder"]
    > ![画面になって完了が表示されたアカウントと、ギャラリー内に混在して連絡先](media/function-astype-istype/contacts-customer-complete.png)

    ギャラリーのサブタイトルは、これらの値を示しています。
    - "-"場合、 **' Company Name'** は*空白*します。
    - "アカウント:"をクリックし、**アカウント名**フィールドを**アカウント**エンティティ場合、**会社名**フィールドは、アカウントを参照します。
    - "にお問い合わせください:"をクリックし、**フル_ネーム**フィールドを**連絡先**エンティティ場合、**会社名**フィールドは、連絡先を参照します。

    変更された結果の他の種類を表示するサンプル データを使用しているために、このトピックで、結果が異なる場合があります。