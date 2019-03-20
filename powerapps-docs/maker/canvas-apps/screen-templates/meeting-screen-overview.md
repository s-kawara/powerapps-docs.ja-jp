---
title: 会議画面テンプレート |Microsoft Docs
description: キャンバス アプリの会議画面テンプレートのしくみを理解し、ユース ケースの画面の拡張
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 12/30/2018
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 24f04ff9ce95f603f5f7d4dc7d217146b9eebef8
ms.sourcegitcommit: 5e15a1033a68289781f8092fb65c57432501f911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54459412"
---
# <a name="overview-of-the-meeting-screen-template-for-canvas-apps"></a>キャンバス アプリの会議画面テンプレートの概要

キャンバス アプリでは、ユーザーを作成し、Office 365 Outlook アカウントから、会議出席依頼を送信できるようにする会議画面を追加します。 ユーザーは、組織内の参加者を検索し、外部の電子メール アドレスを追加できます。 テナントの会議室を Outlook に組み込まれている場合は、ユーザーは、同様の場所を選択できます。

など、Office 365 から別のデータを表示する他のテンプレートに基づく画面を追加することもできます。[電子メール](email-screen-overview.md)、[人](people-screen-overview.md)組織、およびユーザーの[カレンダー](calendar-screen-overview.md)します。

この概要では、画面の高度な機能について説明します。

この画面の既定の機能について詳しくを参照してください、[ミーティング画面参照](meeting-screen-reference.md)します。

## <a name="prerequisite"></a>前提条件

追加しても画面とその他のコントロールを構成する方法に関する知識[PowerApps でアプリを作成](../data-platform-create-app-scratch.md)です。

## <a name="default-functionality"></a>既定の機能

テンプレートから会議画面を追加します。

1. [サインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)PowerApps にアプリを作成するか、PowerApps Studio で既存のアプリを開きます。

    このトピックでは、phone アプリが、タブレット アプリを同じ概念が適用されます。

1. **ホーム**、リボンのタブ**新しい画面** > **会議**します。

  会議の画面の両方のタブをいっぱいになるには、次のようになります。

  ![会議 画面で、両方のタブ](media/meeting-screen/meeting-screen-full-both.png)

いくつかの役に立つ注記:

* 会議の画面により、アプリ ユーザーが Outlook で会議を作成します。
  ユーザーが検索のと参加者を追加したり、必要に応じて、会議室を会議に追加します。
* 組織内のユーザーを検索するには、テキスト入力ボックスで「出席者」チーム名を入力を開始します。
* ユーザーを検索するときは、上位 15 の結果のみが返されます。
* 組織外の出席者のメール アドレスを追加するには、完全な有効な電子メール アドレスを入力し、電子メール アドレスの右側に表示される '+' アイコンを選択します。
* 会議を作成する必要があります参加者として、少なくとも 1 人のユーザーを追加、指定、件名、しの会議の時間を選択、**スケジュール**タブ。
* 会議出席依頼を送信した後、その会議のすべての情報がクリアされます。
* **OnSelect**ステートメント送信 アイコン (右上隅) にはには、次の数式が含まれています。
    ```powerapps-dot
    Set( _myCalendarName, 
        LookUp( 'Office365'.CalendarGetTables().value, DisplayName = "Calendar" ).Name 
    );
    ```
* "Calendar"は、ほとんどの Office ユーザーの予定表の既定の表示名が、組織が異なる場合があります。 そうである場合、組織の適切な用語を"Calendar"を変更することができます。
* 過去に発生するミーティングをスケジュールしようとする場合にエラーが発生または会議に 20 個を超えるユーザーを追加するとします。

## <a name="next-steps"></a>次の手順

* [この画面のリファレンス ドキュメントを表示](./meeting-screen-reference.md)します。
* [詳細については、Office 365 Outlook コネクタは](../connections/connection-office365-outlook.md)します。
* [詳細については、Office 365 ユーザー コネクタは](../connections/connection-office365-users.md)します。
