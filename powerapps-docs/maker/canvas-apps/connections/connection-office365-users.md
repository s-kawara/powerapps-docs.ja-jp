---
title: Office 365 Users 接続の概要 | Microsoft Docs
description: いくつかの例が付いた Office 365 Users への接続方法の段階的説明とすべての機能の紹介
author: lancedMicrosoft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 06/07/2016
ms.author: lanced
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 507bac0b57cdc1e348bd384d5544d7b664a3e0f5
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61557388"
---
# <a name="connect-to-office-365-users-connection-from-powerapps"></a>PowerApps から Office 365 ユーザーの接続に接続する
![Office 365 Users](./media/connection-office365-users/office365icon.png)

Office 365 Users を使用すると、自分の Office 365 アカウントを使用して組織内のユーザー プロファイルにアクセスできます。 自分のプロファイル、別のユーザーのプロファイル、ユーザーの上司または直属の部下を確認するなど、さまざまな操作を行うことができます。

こうした情報を、アプリのラベルに表示できます。 1 つまたは複数の機能を表示したり、異なる機能を組みわせたりすることも可能です。 たとえば、ユーザー名と電話番号を組み合わせる式を作成し、組み合わせた情報をアプリに表示できます。

このトピックでは、Office 365 Users を接続として追加する方法、アプリに Office 365 Users をデータ ソースとして追加する方法、およびギャラリー コントロールでテーブル データを使用する方法について説明します。

[!INCLUDE [connection-requirements](../../../includes/connection-requirements.md)]

## <a name="add-a-connection"></a>接続を追加する
1. [データ接続を追加](../add-data-connection.md)して、**[Office 365 ユーザー]** を選択します。  

    ![Office 365 への接続](./media/connection-office365-users/add-office.png)
2. **[接続]** を選択します。サインインが求められた場合は、職場アカウントを入力します。

Office 365 ユーザー 接続が作成され、アプリに追加されます。 これで、この接続を使用できるようになりました。

## <a name="use-the-connection-in-your-app"></a>アプリでこの接続を使用する
### <a name="show-information-about-the-current-user"></a>現在のユーザーに関する情報を表示する
1. **[挿入]** メニューで **[ラベル]** を選択します。
2. 関数バーで、**[Text](../controls/properties-core.md)** プロパティに次のいずれかの式を設定します。

    `Office365ユーザー.MyProfile().City`  
    `Office365ユーザー.MyProfile().CompanyName`  
    `Office365ユーザー.MyProfile().Country`  
    `Office365ユーザー.MyProfile().Department`  
    `Office365ユーザー.MyProfile().DisplayName`  
    `Office365ユーザー.MyProfile().GivenName`  
    `Office365ユーザー.MyProfile().Id`  
    `Office365ユーザー.MyProfile().JobTitle`  
    `Office365ユーザー.MyProfile().Mail`  
    `Office365ユーザー.MyProfile().MailNickname`  
    `Office365ユーザー.MyProfile().mobilePhone`  
    `Office365ユーザー.MyProfile().OfficeLocation`  
    `Office365ユーザー.MyProfile().PostalCode`  
    `Office365ユーザー.MyProfile().Surname`  
    `Office365ユーザー.MyProfile().TelephoneNumber`  
    `Office365ユーザー.MyProfile().UserPrincipalName`  
    `Office365ユーザー.MyProfile().AccountEnabled`  
    `Office365ユーザー.MyProfile().BusinessPhones`  

ラベルに、現在のユーザーに関する入力した情報が表示されます。

### <a name="show-information-about-another-user"></a>別のユーザーに関する情報を表示する
1. **[挿入]** メニューで、**[テキスト]**、**[Text input]** (テキスト入力) の順に選択します。 名前を **InfoAbout** に変更します。  

    ![コントロール名の変更](./media/connection-office365-users/renameinfoabout.png)
2. **InfoAbout** に、組織内のユーザーの電子メール アドレスを入力するか貼り付けます。 たとえば、「*ユーザー名*@*yourCompany.com*」と入力します。
3. **[挿入]** メニューで **[ラベル]** を追加し、**[Text](../controls/properties-core.md)** プロパティに次のいずれかの式を設定します。

   * 別のユーザーに関する情報を表示する場合:  

       `Office365ユーザー.UserProfile(InfoAbout.Text).City`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).CompanyName`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).Country`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).Department`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).DisplayName`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).GivenName`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).Id`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).JobTitle`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).Mail`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).MailNickname`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).mobilePhone`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).OfficeLocation`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).PostalCode`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).Surname`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).TelephoneNumber`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).UserPrincipalName`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).AccountEnabled`  
       `Office365ユーザー.UserProfile(InfoAbout.Text).BusinessPhone`  
   * 別のユーザーの上司に関する情報を表示する場合:  

       `Office365ユーザー.Manager(InfoAbout.Text).City`  
       `Office365ユーザー.Manager(InfoAbout.Text).CompanyName`  
       `Office365ユーザー.Manager(InfoAbout.Text).Country`  
       `Office365ユーザー.Manager(InfoAbout.Text).Department`  
       `Office365ユーザー.Manager(InfoAbout.Text).DisplayName`  
       `Office365ユーザー.Manager(InfoAbout.Text).GivenName`  
       `Office365ユーザー.Manager(InfoAbout.Text).Id`  
       `Office365ユーザー.Manager(InfoAbout.Text).JobTitle`  
       `Office365ユーザー.Manager(InfoAbout.Text).Mail`  
       `Office365ユーザー.Manager(InfoAbout.Text).MailNickname`  
       `Office365ユーザー.Manager(InfoAbout.Text).mobilePhone`  
       `Office365ユーザー.Manager(InfoAbout.Text).OfficeLocation`  
       `Office365ユーザー.Manager(InfoAbout.Text).PostalCode`  
       `Office365ユーザー.Manager(InfoAbout.Text).Surname`  
       `Office365ユーザー.Manager(InfoAbout.Text).TelephoneNumber`  
       `Office365ユーザー.Manager(InfoAbout.Text).UserPrincipalName`  
       `Office365ユーザー.Manager(InfoAbout.Text).AccountEnabled`  
       `Office365ユーザー.Manager(InfoAbout.Text).BusinessPhones`  

ラベルに、指定したユーザーまたはそのユーザーの上司に関する入力した情報が表示されます。

> [!NOTE]
> Common Data Service のエンティティに基づくアプリを開発する場合は、メール アドレスではなく ID でユーザーを指定できます。

たとえば、[アプリを自動で作成し](../data-platform-create-app.md)、**[ラベル]** コントロールが含まれる画面を追加してから、このコントロールの **Text** プロパティを次の式に設定します。
<br>**Office365ユーザー.UserProfile(BrowseGallery1.Selected.CreatedByUser).DisplayName**

連絡先を作成しアプリのブラウズ画面でその連絡先を選択すると、**[ラベル]** コントロールに連絡先の表示名が表示されます。

### <a name="show-the-direct-reports-of-another-user"></a>別のユーザーの直属の部下を表示する
1. **[挿入]** メニューの **[テキスト]** から **[Text input]** (テキスト入力) を追加し、名前を **InfoAbout** に変更します。
2. **InfoAbout** に、組織内のユーザーの電子メール アドレスを入力します。 たとえば、「*上司の名前*@*yourCompany.com*」と入力します。
3. **[挿入]** メニューの **[ギャラリー]** から **[テキスト付き]** ギャラリーを追加し、**[Items](../controls/properties-core.md)** プロパティに次の式を設定します。

    `Office365ユーザー.DirectReports(InfoAbout.Text)`

    ギャラリーに、入力したユーザーの直属の部下に関する情報が表示されます。

    ギャラリーを選択すると、右側のペインにそのギャラリーのオプションが表示されます。
4. 2 番目のリストで、**[JobTitle]** (役職) を選択します。 3 番目のリストで、**[DisplayName]** (表示名) を選択します。 ギャラリーが更新され、これらの値が表示されます。  

> [!NOTE]
> 実際には、1 番目のボックスはイメージ コントロールです。 イメージがない場合はこのイメージ コントロールを削除し、その場所にラベルを追加できます。 [コントロールの追加および構成](../add-configure-controls.md)に関する記事をご覧ください。

### <a name="search-for-users"></a>ユーザーを検索する
1. **[挿入]** メニューの **[テキスト]** から **[Text input]** (テキスト入力) を追加し、名前を **SearchTerm** に変更します。 検索対象の名前を入力します。 たとえば、姓を入力します。
2. **[挿入]** メニューの **[ギャラリー]** から **[テキスト付き]** ギャラリーを追加し、**[Items](../controls/properties-core.md)** プロパティに次の式を設定します。

    `Office365ユーザー.SearchUser({searchTerm: SearchTerm.Text})`

    ギャラリーに、入力した検索テキストを含む名前のユーザーが表示されます。

    ギャラリーを選択すると、右側のペインにそのギャラリーのオプションが表示されます。
3. 2 番目のリストで、**[メール]** を選択します。 3 番目のリストで、**[DisplayName]** (表示名) を選択します。

    ギャラリーの 2 番目と 3 番目のラベルが更新されます。

## <a name="view-the-available-functions"></a>使用可能な関数の確認
この接続には、次の関数が含まれています。

| 関数名 | 説明 |
| --- | --- |
| [DirectReports](connection-office365-users.md#directreports) |指定したユーザーの直属の部下を返します |
| [Manager](connection-office365-users.md#manager) |指定したユーザーの上司のユーザー プロファイルを取得します |
| [MyProfile](connection-office365-users.md#myprofile) |現在のユーザーのプロファイルを取得します |
| [SearchUser](connection-office365-users.md#searchuser) |ユーザー プロファイルの検索結果を取得します |
| [UserProfile](connection-office365-users.md#userprofile) |特定のユーザー プロファイルを取得します |

### <a name="myprofile"></a>MyProfile
マイ プロフィールを取得します。現在のユーザーのプロファイルを取得します。

#### <a name="input-properties"></a>入力プロパティ
なし。

#### <a name="output-properties"></a>出力プロパティ

| プロパティ名 | 種類 | 説明 |
| --- | --- | --- |
| City | string |ユーザーの市です。|
| CompanyName | string |ユーザーの会社名です。 |
| Country | string |ユーザーの国です。 |
| Department |string |ユーザーの部署です。 |
| DisplayName |string |ユーザーの表示名です。 |
| GivenName |string |ユーザーの名です。 |
| Id |string |ユーザー ID です。|
| JobTitle |string |ユーザーの役職です。 |
| Mail |string |ユーザーの電子メール ID です。 |
| MailNickname |string |ユーザーのニックネームです。 |
| mobilePhone | string |ユーザーの携帯電話です。|
| OfficeLocation | string |ユーザーの会社場所です。|
| PostalCode | string |ユーザーの郵便番号です。|
| Surname |string |ユーザーの姓です。 |
| TelephoneNumber |string |ユーザーの電話番号です。 |
| UserPrincipalName |string |ユーザー プリンシパル名です。 |
| AccountEnabled |bool |アカウントの有効化フラグです。 |
| BusinessPhones | string |ユーザーの会社の電話番号です。|

### <a name="userprofile"></a>UserProfile
ユーザー プロファイルを取得します。特定のユーザー プロファイルを取得します。

#### <a name="input-properties"></a>入力プロパティ

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| Id |string |はい |ユーザー プリンシパル名または電子メール ID |

#### <a name="output-properties"></a>出力プロパティ

| プロパティ名 | 種類 | 説明 |
| --- | --- | --- |
| City | string |ユーザーの市です。|
| CompanyName | string |ユーザーの会社名です。 |
| Country | string |ユーザーの国です。 |
| Department |string |ユーザーの部署です。 |
| DisplayName |string |ユーザーの表示名です。 |
| GivenName |string |ユーザーの名です。 |
| Id |string |ユーザー ID です。|
| JobTitle |string |ユーザーの役職です。 |
| Mail |string |ユーザーの電子メール ID です。 |
| MailNickname |string |ユーザーのニックネームです。 |
| mobilePhone | string |ユーザーの携帯電話です。|
| OfficeLocation | string |ユーザーの会社場所です。|
| PostalCode | string |ユーザーの郵便番号です。|
| Surname |string |ユーザーの姓です。 |
| TelephoneNumber |string |ユーザーの電話番号です。 |
| UserPrincipalName |string |ユーザー プリンシパル名です。 |
| AccountEnabled |bool |アカウントの有効化フラグです。 |
| BusinessPhones | string |ユーザーの会社の電話番号です。|

### <a name="manager"></a>Manager
上司の取得。指定したユーザーの上司のユーザー プロファイルを取得します

#### <a name="input-properties"></a>入力プロパティ

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| Id |string |はい |ユーザー プリンシパル名または電子メール ID |

#### <a name="output-properties"></a>出力プロパティ

| プロパティ名 | 種類 | 説明 |
| --- | --- | --- |
| City | string |ユーザーの市です。|
| CompanyName | string |ユーザーの会社名です。 |
| Country | string |ユーザーの国です。 |
| Department |string |ユーザーの部署です。 |
| DisplayName |string |ユーザーの表示名です。 |
| GivenName |string |ユーザーの名です。 |
| Id |string |ユーザー ID です。|
| JobTitle |string |ユーザーの役職です。 |
| Mail |string |ユーザーの電子メール ID です。 |
| MailNickname |string |ユーザーのニックネームです。 |
| mobilePhone | string |ユーザーの携帯電話です。|
| OfficeLocation | string |ユーザーの会社場所です。|
| PostalCode | string |ユーザーの郵便番号です。|
| Surname |string |ユーザーの姓です。 |
| TelephoneNumber |string |ユーザーの電話番号です。 |
| UserPrincipalName |string |ユーザー プリンシパル名です。 |
| AccountEnabled |bool |アカウントの有効化フラグです。 |
| BusinessPhones | string |ユーザーの会社の電話番号です。|

### <a name="directreports"></a>DirectReports
直属の部下を取得します。直属の部下を取得します。

#### <a name="input-properties"></a>入力プロパティ

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| Id |string |はい |ユーザー プリンシパル名または電子メール ID |

#### <a name="output-properties"></a>出力プロパティ

| プロパティ名 | 種類 | 説明 |
| --- | --- | --- |
| City | string |ユーザーの市です。|
| CompanyName | string |ユーザーの会社名です。 |
| Country | string |ユーザーの国です。 |
| Department |string |ユーザーの部署です。 |
| DisplayName |string |ユーザーの表示名です。 |
| GivenName |string |ユーザーの名です。 |
| Id |string |ユーザー ID です。|
| JobTitle |string |ユーザーの役職です。 |
| Mail |string |ユーザーの電子メール ID です。 |
| MailNickname |string |ユーザーのニックネームです。 |
| mobilePhone | string |ユーザーの携帯電話です。|
| OfficeLocation | string |ユーザーの会社場所です。|
| PostalCode | string |ユーザーの郵便番号です。|
| Surname |string |ユーザーの姓です。 |
| TelephoneNumber |string |ユーザーの電話番号です。 |
| UserPrincipalName |string |ユーザー プリンシパル名です。 |
| AccountEnabled |bool |アカウントの有効化フラグです。 |
| BusinessPhones | string |ユーザーの会社の電話番号です。|

### <a name="searchuser"></a>SearchUser
ユーザーを検索します。ユーザー プロファイルの検索結果を取得します

#### <a name="input-properties"></a>入力プロパティ

| 名前 | データ型 | 必須 | 説明 |
| --- | --- | --- | --- |
| searchTerm |string |いいえ |文字列を検索します。 適用対象は、表示名、名、姓、メール、メールのニックネーム、およびユーザー プリンシパル名です。 |

#### <a name="output-properties"></a>出力プロパティ

| プロパティ名 | 種類 | 説明 |
| --- | --- | --- |
| City | string |ユーザーの市です。|
| CompanyName | string |ユーザーの会社名です。 |
| Country | string |ユーザーの国です。 |
| Department |string |ユーザーの部署です。 |
| DisplayName |string |ユーザーの表示名です。 |
| GivenName |string |ユーザーの名です。 |
| Id |string |ユーザー ID です。|
| JobTitle |string |ユーザーの役職です。 |
| Mail |string |ユーザーの電子メール ID です。 |
| MailNickname |string |ユーザーのニックネームです。 |
| mobilePhone | string |ユーザーの携帯電話です。|
| OfficeLocation | string |ユーザーの会社場所です。|
| PostalCode | string |ユーザーの郵便番号です。|
| Surname |string |ユーザーの姓です。 |
| TelephoneNumber |string |ユーザーの電話番号です。 |
| UserPrincipalName |string |ユーザー プリンシパル名です。 |
| AccountEnabled |bool |アカウントの有効化フラグです。 |
| BusinessPhones | string |ユーザーの会社の電話番号です。|

## <a name="helpful-links"></a>便利なリンク
* [利用可能な接続](../connections-list.md)をすべて表示する。
* アプリに[接続を追加する](../add-manage-connections.md)方法を確認する。

