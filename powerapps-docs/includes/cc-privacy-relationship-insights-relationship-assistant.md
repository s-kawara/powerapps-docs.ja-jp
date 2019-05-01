---
ms.openlocfilehash: 40dcde544894751da2696defc76819892659cb25
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61577528"
---
関係アシスタント機能を有効にすると、電子メールに含まれる関連分析情報を表示する目的で、送信者の名前、電子メール アドレス、電子メール本文からの抜粋を含む、限られた交換データが取得されます (ただし、[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] には保存されません)。 また、関係アシスタント機能は、([!INCLUDE[pn_ms_dyn_365](pn-ms-dyn-365.md)] Core Services とは見なされていない) MSN Money や Bing などの外部コンポーネントに要求を送信することでニュース、金融、フライトに関連する情報を取得するように構成できます。 管理者は関係アシスタント機能の有効/無効を切り替えることができます。**[設定]** > **[インテリジェンスの構成]** の順に移動し、**[関係アシスタント]** タブをクリックし、有効/無効を切り替えます。  
  
 関係アシスタント機能に付属する外部コンポーネントの詳細については後続のセクションで説明します。  
  
 **[!INCLUDE[pn_bing](pn-bing.md)]**  
  
 関係アシスタントでは、ユーザーに表示する関連ニュースの検索に [!INCLUDE[pn_bing](pn-bing.md)] が使用されます。その際、ユーザーの [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] データに含まれるアカウント名が利用されます。  
  
 **[!INCLUDE[pn_ms_MSN_Money](pn-ms-msn-money.md)]**  
  
 関係アシスタントでは、ユーザーに関連する株価情報を表示するために [!INCLUDE[pn_ms_MSN_Money](pn-ms-msn-money.md)] が使用されます。その際、ユーザーの [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] データに含まれるアカウント株式銘柄コードが利用されます。