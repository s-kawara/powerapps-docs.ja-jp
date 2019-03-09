---
title: Outlook 用 Dynamics 365 アプリを展開する | MicrosoftDocs
ms.custom: ''
ms.date: 2017-04-20
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- Dynamics 365 (online)
ms.assetid: 09736e14-e744-48ca-a755-1b05bb55340e
caps.latest.revision: 39
author: jimholtz
ms.author: jimholtz
manager: brycho
ms.openlocfilehash: 98a5ec78b0edf607b954d794b3eef95403926a64
ms.sourcegitcommit: baadb67f5cc962b7c3393f9763959eae3a7649dd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57346949"
---
# <a name="deploy-dynamics-365-app-for-outlook"></a>Outlook 用 Dynamics 365 アプリを展開する
ユーザーは [!INCLUDE[pn_ms_dyn_crm_app_for_outlook](../includes/pn-ms-dyn-crm-app-for-outlook.md)] を使用することで、デスクトップ、Web、またはタブレット上で [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] を使用している間に、[!INCLUDE[pn_microsoftcrm](../includes/pn-microsoftcrm.md)] の機能を活用できます。 たとえば、電子メールまたは予定の受信者に関する情報を表示したり、営業案件、取引先企業、またはサポート案件などの [!INCLUDE[pn_microsoftcrm](../includes/pn-microsoftcrm.md)] レコードに対して [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] 電子メールまたは予定をリンクしたりできます。 [!INCLUDE[pn_ms_dyn_crm_app_for_outlook](../includes/pn-ms-dyn-crm-app-for-outlook.md)] の機能の詳細については、「[Outlook 用 Dynamics 365 アプリのユーザー ガイド](http://go.microsoft.com/fwlink/p/?LinkID=613099)」を参照してください。  
  
> [!IMPORTANT]
>  [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)] は、[!INCLUDE[pn_crm_for_outlook_short](../includes/pn-crm-for-outlook-short.md)] と同じものではありません。 [!INCLUDE[pn_crm_8_2_0_both](../includes/pn-crm-8-2-0-both.md)] では、[!INCLUDE[pn_ms_dyn_crm_app_for_outlook](../includes/pn-ms-dyn-crm-app-for-outlook.md)]と [!INCLUDE[cc_server_side_synch](../includes/cc-server-side-synch.md)] を組み合わせることが、[!INCLUDE[pn_microsoftcrm](../includes/pn-microsoftcrm.md)] と [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] を統合するための推奨された方法です。 **同じユーザーが [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)] と [!INCLUDE[pn_crm_for_outlook_short](../includes/pn-crm-for-outlook-short.md)] を一緒に使用する場合、追跡アクティビティはサポートされないので注意してください。** [!INCLUDE[pn_crm_for_outlook_short](../includes/pn-crm-for-outlook-short.md)]の詳細については、[Outlook 用 Dynamics 365 のユーザー ガイド](http://go.microsoft.com/fwlink/p/?LinkID=524751)を参照してください。  
>   
>  [委任されたユーザー](https://support.office.com/article/Allow-someone-else-to-manage-your-mail-and-calendar-9684B670-7588-4EEA-8717-9E5799047540)が、[!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)]を使用して電子メールを追跡することはできません。 委任されたユーザーには、[フォルダー レベルの追跡、または自動追跡](https://www.microsoft.com/en-us/dynamics/crm-customer-center/overview-of-tracking-records-in-dynamics-365-for-outlook.aspx)を使用することをお勧めします。  
  
<a name="BKMK_Compare"></a>   
## <a name="comparing-dynamics-365-app-for-outlook-with-dynamics-365-for-outlook"></a>Outlook 用 Dynamics 365 アプリを Outlook 用 Dynamics 365 と比較する  
 次の表では、[!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)] の機能を [!INCLUDE[pn_crm_8_2_0_both](../includes/pn-crm-8-2-0-both.md)] の時点での [!INCLUDE[pn_crm_for_outlook_short](../includes/pn-crm-for-outlook-short.md)] ([!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] クライアントまたはアドインとも呼ばれる) と比較します。  
  
||||  
|-|-|-|  
|**機能**|**[!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)]**|**[!INCLUDE[pn_crm_for_outlook_short](../includes/pn-crm-for-outlook-short.md)]**|  
|電子メールの追跡および関連の設定|はい|はい|  
|予定の追跡および関連の設定|はい|はい|  
|連絡先の追跡および関連の設定|はい|はい|  
|タスクの追跡および関連の設定|いいえ|はい|  
|ワンクリック関連の設定|はい|いいえ|  
|受信者の概要を表示|はい|いいえ|  
|電子メール/予定の関連レコード概要を表示|はい|いいえ|  
|[!INCLUDE[pn_outlook_web_app](../includes/pn-outlook-web-app.md)] に対応|はい|いいえ|  
|[!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] デスクトップに対応|はい|はい|  
|Mac 用 [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] に対応|はい|いいえ|  
|携帯電話に対応|はい|いいえ|  
|[!INCLUDE[pn_microsoftcrm](../includes/pn-microsoftcrm.md)] レコードを直接開く、および作成する|はい|はい|  
|カスタム フォームとビジネス ロジックを適用|はい|はい|  
|オフライン作業|いいえ|はい|  
|電子メール テンプレートを適用|はい|はい|  
|販売資料を適用|はい|はい|  
|ナレッジ記事を適用|はい|はい|  
|送信後に電子メールを監視する機能|はい|いいえ|  
|ビューの並べ替え、フィルター処理、フォーマット、グループ化、および分類|いいえ|はい|  
|Word 差し込み文書の作成|いいえ|はい|  
|コントロール フィールドの同期|いいえ|はい|  
  
<a name="BKMK_Requirements"></a>   
## <a name="requirements"></a>要件  
 [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)] を使用するには、以下が必要です。  
  
-   [!INCLUDE[pn_crm_online_2016_update](../includes/pn-crm-online-2016-update.md)]、または [!INCLUDE[pn_crm_8_2_0_both](../includes/pn-crm-8-2-0-both.md)]  
  
-   サーバー側の同期を介した着信電子メールの同期。 [!INCLUDE[proc_more_information](../includes/proc-more-information.md)][電子メール、予定、連絡先、およびタスクのサーバー側の同期を設定する](../Topic/Set%20up%20server-side%20synchronization%20of%20email,%20appointments,%20contacts,%20and%20tasks.md)  
  
-   以下の説明した必須の特権  
  
> [!NOTE]
>  [!INCLUDE[pn_dyn_365](../includes/pn-dyn-365.md)] 機能のサポートされている構成と要件は、ドキュメントのいたるところに一覧表示されています。 ドキュメントに記載されていない特定の構成は、サポートされていないと見なしてください。  
  
### <a name="required-privileges"></a>必須の特権  
 [!INCLUDE[pn_microsoftcrm](../includes/pn-microsoftcrm.md)] では、**[Outlook 用 Dynamics 365 アプリの使用]** 特権によって [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)]にアクセスすることができます。 ユーザーにこの特権がない場合、そのユーザーには次のエラー メッセージが表示されます。  
  
> "このアプリを使用するよう許可されていません。 設定を更新する場合は、システム管理者にお問い合わせください。"  
  
 ユーザーはさらに、以下のエンティティに対する読み取り/書き込み特権が必要です。  
  
 [事業部管理] タブ:  
  
-   **メールボックス**  
  
 [カスタマイズ] タブ:  
  
-   **エンティティ**  
  
-   **フィールド**  
  
-   **リレーションシップ**  
  
-   **システム アプリケーション メタデータ**  
  
-   **システム フォーム**  
  
-   **ユーザーのアプリケーション メタデータ**  
  
-   **ビュー**  
  
##### <a name="set-the-privileges-for-a-security-role"></a>セキュリティ ロール用の権限を設定する  
  
1.  [!INCLUDE[proc_settings_security](../includes/proc-settings-security.md)]  
  
2.  **[セキュリティ ロール]** を開きます。  
  
3.  セキュリティ ロールを選択してから、**[事業部管理]** タブをクリックします。  
  
4.  **[エンティティ]** セクションで、**[メールボックス]** 特権設定を確認します。 セキュリティ ロールには、ユーザーまたはそれ以上の設定がある必要があります。  
  
5.  **[プライバシー関連の特権]** セクションで、**[Outlook 用の Dynamics 365 アプリの使用]** が **[組織]** に設定されていることを確認します。 設定されていない場合は、**[Outlook 用 Dynamics 365 アプリの使用]** をクリックします。  
  
### <a name="supported-configurations-with-microsoft-exchange"></a>Microsoft Exchange でサポートされている構成  
 [!INCLUDE[pn_crm_8_2_0_both](../includes/pn-crm-8-2-0-both.md)] については、ハイブリッド構成を含め、[!INCLUDE[pn_crm_online_shortest](../includes/pn-crm-online-shortest.md)] または [!INCLUDE[pn_crm_op_edition](../includes/pn-crm-op-edition.md)] と [!INCLUDE[pn_Exchange_Online](../includes/pn-exchange-online.md)] または [!INCLUDE[pn_Exchange_Server_short](../includes/pn-exchange-server-short.md)] (オンプレミス) との任意の組み合わせでアプリを使用できます。 これは次のいずれの構成でも [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)] を使用できることを意味します。  
  
|||  
|-|-|  
|[!INCLUDE[pn_crm_online_shortest](../includes/pn-crm-online-shortest.md)]|[!INCLUDE[pn_Exchange_Online](../includes/pn-exchange-online.md)]|  
|[!INCLUDE[pn_crm_online_shortest](../includes/pn-crm-online-shortest.md)]|[!INCLUDE[pn_Exchange_Server_short](../includes/pn-exchange-server-short.md)] (オンプレミス)|  
|[!INCLUDE[pn_crm_op_edition](../includes/pn-crm-op-edition.md)]|[!INCLUDE[pn_Exchange_Server_short](../includes/pn-exchange-server-short.md)] (オンプレミス)|  
|[!INCLUDE[pn_crm_op_edition](../includes/pn-crm-op-edition.md)]|[!INCLUDE[pn_Exchange_Online](../includes/pn-exchange-online.md)]|  
  
> [!NOTE]
>  [!INCLUDE[pn_crm_op_edition](../includes/pn-crm-op-edition.md)] を利用する場合は、以下の説明に従い IFD 認証を使用して認証する必要があります。  
  
### <a name="supported-browsers-for-outlook-on-the-web"></a>Outlook on the web 用にサポートされているブラウザー  
 以下のブラウザー上で [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)] を [!INCLUDE[pn_outlook_web_app](../includes/pn-outlook-web-app.md)] と共に使用できます。  
  
-   [!INCLUDE[pn_IE_10](../includes/pn-ie-10.md)]、[!INCLUDE[pn_ie_11](../includes/pn-ie-11.md)]、または [!INCLUDE[pn_microsoft_edge](../includes/pn-microsoft-edge.md)]  
  
     以下の構成がサポートされています。  
  
    -   保護モードは **[インターネット]** セキュリティ ゾーンで有効になっています。 保護モードを有効にするには: IE 10 または 11 で、**[ツール]** > **[インターネット オプション]** > **[セキュリティ] タブ** > **[インターネット]** の順に移動します。  
  
    -   保護モードは **[ローカル イントラネット]** セキュリティ ゾーンで有効になっています。 保護モードを有効にするには: IE 10 または 11 で、**[ツール]** > **[インターネット オプション]** > **[セキュリティ] タブ** > **[ローカル インターネット]** の順に移動します。  
  
    -   [!INCLUDE[pn_dyn_365](../includes/pn-dyn-365.md)] の URL は、信頼できる Web サイトの **[ローカル イントラネット]** セキュリティ ゾーン リストに含まれます。 IE 10 または 11 では、**[ツール]** > **[インターネット オプション]** > **[セキュリティ] タブ** > **[ローカル イントラネット]** > **[サイト]** > **[詳細設定]** の順に移動します。  
  
-   [!INCLUDE[pn_ms_Windows_short](../includes/pn-ms-windows-short.md)] での [!INCLUDE[tn_Google_Chrome](../includes/tn-google-chrome.md)] (最新バージョン)  
  
-   [!INCLUDE[pn_ms_Windows_short](../includes/pn-ms-windows-short.md)] での [!INCLUDE[tn_Firefox](../includes/tn-firefox.md)] (最新バージョン)  
  
-   Mac または OSX での [!INCLUDE[tn_apple](../includes/tn-apple.md)] [!INCLUDE[tn_Safari](../includes/tn-safari.md)] (バージョン 9 または 10)  
  
### <a name="supported-operating-systems-for-outlook-on-the-desktop"></a>デスクトップ上の Outlook でサポートされているオペレーティング システム  
 デスクトップ用の [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)] の次のバージョンでは [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] アプリを使用できます。  
  
-   [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] 2013 および [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] 2016。  
  
-   [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] for Mac*。  
  
     *[!INCLUDE[pn_Exchange_Server_short](../includes/pn-exchange-server-short.md)] バージョン 15.0.847.32 以降が必要です。  
  
### <a name="supported-mobile-devices"></a>サポートされているモバイル デバイス  
 次の電話およびオペレーティング システム上のモバイル ブラウザーでは、[!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)]と [!INCLUDE[pn_outlook_web_app](../includes/pn-outlook-web-app.md)] を一緒に使用できます。  
  
-   iOS バージョン 8、9、または 10 が稼働している [!INCLUDE[tn_apple](../includes/tn-apple.md)] [!INCLUDE[tn_iphone](../includes/tn-iphone.md)] デバイス。  
  
-   [!INCLUDE[tn_android](../includes/tn-android.md)] 4.4 (KitKat) または 5.0 (Lollipop)、6 (Marshmallow)、または 7 (Nougat) が稼働している [!INCLUDE[tn_android](../includes/tn-android.md)] 電話。  
  
-   [!INCLUDE[pn_windows_8_1](../includes/pn-windows-8-1.md)] または [!INCLUDE[pn_windows_10](../includes/pn-windows-10.md)] が稼働している [!INCLUDE[pn_windows_phone](../includes/pn-windows-phone.md)] デバイス。  
  
### <a name="supported-clients-per-feature"></a>機能ごとにサポートされているクライアント  
 サポートされている [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)] 機能は、実行しているクライアントによって異なります。 次の表では、[!INCLUDE[pn_crm_shortest](../includes/pn-crm-shortest.md)] および [!INCLUDE[pn_Exchange](../includes/pn-exchange.md)] のクライアント/構成ごとに、サポートされている機能がまとめられています。  
  
 ![Outlook 用 Dynamics 365 アプリの機能ごとにサポートされているクライアント](media/clients-supported-for-each-dynamics-365-app-for-outlook-feature.png "Outlook 用 Dynamics 365 アプリの機能ごとにサポートされているクライアント")  
  
 (1)  [!INCLUDE[pn_outlook_web_app](../includes/pn-outlook-web-app.md)] では [!INCLUDE[pn_IE_10](../includes/pn-ie-10.md)]、[!INCLUDE[pn_ie_11](../includes/pn-ie-11.md)]、[!INCLUDE[pn_microsoft_edge](../includes/pn-microsoft-edge.md)]、[!INCLUDE[tn_Safari](../includes/tn-safari.md)] 9、[!INCLUDE[tn_Safari](../includes/tn-safari.md)] 10、[!INCLUDE[tn_Firefox](../includes/tn-firefox.md)]、および [!INCLUDE[tn_chrome](../includes/tn-chrome.md)] がサポートされています。  
  
 (2)  モバイル [!INCLUDE[pn_outlook_web_app](../includes/pn-outlook-web-app.md)] では、[!INCLUDE[pn_windows_8_1](../includes/pn-windows-8-1.md)]、[!INCLUDE[pn_windows_10](../includes/pn-windows-10.md)]、[!INCLUDE[tn_ios](../includes/tn-ios.md)] 8、[!INCLUDE[tn_ios](../includes/tn-ios.md)] 9、[!INCLUDE[tn_ios](../includes/tn-ios.md)] 10、[!INCLUDE[tn_android](../includes/tn-android.md)] KitKat (4.4)、[!INCLUDE[tn_android](../includes/tn-android.md)] Lollipop、[!INCLUDE[tn_android](../includes/tn-android.md)] Marshmallow、および [!INCLUDE[tn_android](../includes/tn-android.md)] Nougat がサポートされています。  
  
 (3)  作成モードでの電子メールの追跡および予定の追跡には、[!INCLUDE[pn_Exchange_Server_short](../includes/pn-exchange-server-short.md)] 2013 CU14 または [!INCLUDE[pn_Exchange_Server_short](../includes/pn-exchange-server-short.md)] 2016 が必要です。  
  
 (4)  連絡先の追跡は、[!INCLUDE[pn_Exchange_Server_short](../includes/pn-exchange-server-short.md)] 2016 CU3 および [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] 2016 16.0.6741.1000 以降のみでサポートされています。  
  
 (5)  電子メール テンプレート、ナレッジ マネージメント記事、および営業資料はモバイル [!INCLUDE[pn_outlook_web_app](../includes/pn-outlook-web-app.md)] でサポートされていません。  
  
 (6)  [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] 2016 16.0.7426.1049 以降でのみサポートされています。  
  
 (7)  16.0.6741.1000 以降でのみサポートされています。  
  
> [!NOTE]
>  タブレットは現時点 (2017 年度) ではサポートされていません。  
  
 [サポートされているクライアントの詳細については次のブログ記事を参照してください: Outlook 用 Dynamics 365 アプリのサポート マトリックス](https://blogs.msdn.microsoft.com/crm/2016/12/13/dynamics-365-app-for-outlook-support-matrix/)  
  
### <a name="supported-servers"></a>サポートされているサーバー  
 [Office アドインを使用するためのサーバー要件](https://dev.office.com/docs/add-ins/overview/requirements-for-running-office-add-ins)は、[!INCLUDE[pn_Exchange_Server_2013_short](../includes/pn-exchange-server-2013-short.md)]、[!INCLUDE[pn_exchange_server_2016_short](../includes/pn-exchange-server-2016-short.md)]、または [!INCLUDE[pn_Exchange_Online](../includes/pn-exchange-online.md)] です。  
  
### <a name="supported-languages"></a>サポートされている言語  
 [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)] では、次の言語がサポートされています。  
  
||||  
|-|-|-|  
|ブルガリア語 (ブルガリア) - 1026|ヒンディー語 (インド) - 1081|ポルトガル語 (ポルトガル) - 2070|  
|中国語 (中華人民共和国) - 2052|ハンガリー語 - 1038|ルーマニア語 - 1048|  
|中国語 (台湾) - 1028|インドネシア語 - 1057|ロシア語 - 1049|  
|クロアチア語 (クロアチア) - 1050|イタリア語 - 1040|セルビア語 - 2074|  
|チェコ語 (チェコ共和国) - 1029|日本語 - 1041|スロバキア語 - 1051|  
|デンマーク語 - 1030|カザフ語 - 1087|スロベニア語 - 1060|  
|オランダ語 - 1043|韓国語 - 1042|スペイン語 - 3082|  
|英語 - 1033|ラトビア語 - 1062|スウェーデン語 - 1053|  
|エストニア語 - 1061|リトアニア語 - 1063|タイ語 - 1054|  
|フィンランド語 - 1035|マレー語 - 1086|トルコ語 - 1055|  
|フランス語 - 1036|ノルウェー語 - 1044|ウクライナ語 - 1058|  
|ドイツ語 - 1031|ポーランド語 - 1045|ベトナム語 - 1066|  
|ギリシャ語 - 1032|ポルトガル語 (ブラジル) - 1046||  
  
<a name="BKMK_Deploy"></a>   
## <a name="deploy-dynamics-365-app-for-outlook"></a>Outlook 用 Dynamics 365 アプリを展開する  
 [!INCLUDE[cc_server_side_synch](../includes/cc-server-side-synch.md)]と必要な特権の設定後、[!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)] を一部またはすべてのユーザーにプッシュするか、またはユーザーに必要に応じて自分自身でインストールしてもらうことができます。  
  
> [!NOTE]
>  [!INCLUDE[pn_dyn_365_op](../includes/pn-dyn-365-op.md)] を使用している場合は、次のセクションを参照してください: [オンプレミスの Dynamics 365 ユーザーに展開するには](#BKMK_DeployOnprem)  
  
#### <a name="to-push-the-app-to-users"></a>ユーザーにアプリをプッシュするには  
  
1.  **[設定]** >  **[Outlook 用 Dynamics 365 アプリ]** の順に移動します。  
  
2.  ユーザーが自動的にアプリを取得できるようにする場合は、**[Getting Started with Dynamics 365 App for Outlook]\(Outlook 用 Dynamics 365 アプリで開始する\)** 画面の **[利用資格があるユーザー用に追加]** (2 回目またはそれ以降にこの画面を開く場合には **[設定]** をクリックすることが必要な場合があります) の下で **[Automatically add the app to [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)]]\(Outlook へのアプリの自動的な追加\)** チェック ボックスを選択します。 必要な特権がユーザーにあり、電子メールが[!INCLUDE[cc_server_side_synch](../includes/cc-server-side-synch.md)]によって同期されている場合、アプリはそれらにプッシュするために行わなければならないことは何もありません。 たとえば、必要な特権を営業担当者ロールに追加してから、このロールを新しいユーザーに割り当てた場合、アプリは自動的に取得されます。  
  
3.  次のいずれかを実行します。  
  
    -   すべての利用資格を持つユーザーにアプリをプッシュするには、**[利用資格があるすべてのユーザー用のアプリの追加]** をクリックします。  
  
    -   特定のユーザーにアプリをプッシュするには、リストでそれらのユーザーを選択してから、**[Outlook へのアプリの追加]** をクリックします。  
  
    > [!TIP]
    >  ユーザーが保留中または追加されていないことがリストから分かった場合は、ユーザーの横にある **[詳細]** リンクをクリックして、状態に関する詳細を検索します。  
  
4.  完了したら、**[保存]** をクリックします。  
  
#### <a name="to-have-users-install-the-app-themselves"></a>ユーザーに自分でアプリをインストールしてもらうには  
  
1.  ユーザーは **[設定]** ボタン ![[設定]] ボタン (media/mp-ua-r16-settings.png "[設定]") ボタンをクリックしてから、**[Dynamics 365 用アプリ]** をクリックします。  
  
2.  **[Dynamics 365 用アプリ]** 画面の **[!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)]** の下で、ユーザーは **[[!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] へのアプリの追加]** をクリックします。  
  
> [!NOTE]
>  ユーザーは必要に応じてアドインを自分で無効にすることも削除することもできます。 詳細については、「[Outlook 用 Dynamics 365 アプリのユーザー ガイド](http://go.microsoft.com/fwlink/p/?LinkID=613099)」を参照してください。  
  
<a name="BKMK_DeployOnprem"></a>   
## <a name="to-deploy-to-dynamics-365-on-premises-users"></a>オンプレミスの Dynamics 365 ユーザーに展開するには  
 オンプレミスの Dynamics 365 を使用している場合は次の手順に従います。  
  
-   インターネットに接続する展開に合わせて、ご利用の Dynamics 365 Server を構成します。 「[Microsoft Dynamics 365 の IFD を構成する](https://technet.microsoft.com/library/dn609803.aspx)」を参照してください。  
  
-   オンプレミスの Exchange に接続している場合は、OAuth プロバイダーを構成してクライアント アプリケーションを登録します。 [OAuth を使用する Dynamics 365 アプリケーション用の Windows Server 2012 R2 の設定](https://technet.microsoft.com/library/hh699726.aspx)に関するページを参照してください。  
  
<a name="BKMK_Troubleshoot"></a>   
## <a name="troubleshooting-installation-problems"></a>インストールに関する問題のトラブルシューティング  
 ご自分が、またはユーザーが [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)]のインストールに関する問題を抱えている場合、[!INCLUDE[pn_Exchange](../includes/pn-exchange.md)] メールボックスが、現在、別の [!INCLUDE[pn_crm_shortest](../includes/pn-crm-shortest.md)] 組織にリンクされていることが原因である可能性があります。 1 つの [!INCLUDE[pn_Exchange](../includes/pn-exchange.md)] メールボックス (電子メール アドレス) では、予定、連絡先、タスクを 1 つの組織とのみ同期できます。また、その組織に属するユーザーは、予定、連絡先、タスクを 1 つの [!INCLUDE[pn_Exchange](../includes/pn-exchange.md)] メールボックスとのみ同期できます。  プライマリ同期組織を変更したい場合には、[!INCLUDE[pn_Exchange](../includes/pn-exchange.md)] に保存されている設定を上書きできます。 詳細については、[このサポート情報の記事](https://support.microsoft.com/en-gb/help/3211627/incomingemailrejected-error-when-attempting-to-install-dynamics-365-app-for-outlook)を参照してください。  
  
<a name="BKMK_Explore"></a>   
## <a name="explore-the-users-guide-and-train-your-users"></a>ユーザー ガイドの説明とユーザーのトレーニング  
 [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)]の使用方法については、「[Outlook 用 Dynamics 365 アプリのユーザー ガイド](http://go.microsoft.com/fwlink/p/?LinkID=613099)」を参照してください。  
  
 ![Outlook 用 Dynamics 365 アプリのユーザー ガイド ページ](media/dynamics-365-app-for-outlook-user-s-guide-page.png "Outlook 用 Dynamics 365 アプリのユーザー ガイド ページ")  
  
## <a name="see-also"></a>関連項目  
 [Outlook 用 Dynamics 365 アプリのユーザー ガイド](http://go.microsoft.com/fwlink/p/?LinkID=613099)   
 [サポートされているクライアントの詳細については次のブログ記事を参照してください: Outlook 用 Dynamics 365 アプリのサポート マトリックス](https://blogs.msdn.microsoft.com/crm/2016/12/13/dynamics-365-app-for-outlook-support-matrix/)   
 [電子メール、予定、連絡先、およびタスクのサーバー側の同期の設定](../Topic/Set%20up%20server-side%20synchronization%20of%20email,%20appointments,%20contacts,%20and%20tasks.md)   
 [ユーザー、ライセンス、セキュリティ ロールの追加](http://msdn.microsoft.com/en-us/23612155-f92d-4871-a109-186419d5c19d)   
 [相互運用の機能を Microsoft Dynamics 365 (オンライン) に追加する](../DocSets/CRMIGv9_Admin/Toc/Add%20interoperation%20features%20to%20Microsoft%20Dynamics%20365%20\(online\).md)