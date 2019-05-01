---
ms.openlocfilehash: 252f09737dbf55309a64ef5d02d479fde0e61c0e
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61577512"
---
埋め込みインテリジェンス機能である電子メール エンゲージメントを有効にして、**[フォローする]** の設定でマークされたメールを [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] から送信すると、受信者のアクティビティの KPI および "フォローされた" メールでの相互作用を計算するため、受信者によるメールとの対話に関する情報が収集されて、[!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] に格納されます。  
  
 システム管理者は、埋め込みインテリジェンス内の **[電子メール エンゲージメント]** タブから機能をプロビジョニングすることによって、電子メール エンゲージメントを有効にします。 後で、**[設定]** の **[インテリジェンスの構成]** ノードから、組織の電子メール エンゲージメントを無効にできます。  
  
 機能を無効にすると、[!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] から送信されたメールを、ユーザー インターフェイスまたはプログラムからフォローすることはできません。 また、**[フォローする]** の設定でマークされたメールが送信されても、受信者の対話データは収集されなくなります。 以前に収集されたデータは [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] に残っており、組織でこの機能を再び有効にすると利用できます。 データは、お客様が Microsoft のサブスクリプションを終了してから 90 日間保持されます。 [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] ユーザーは、**[優先する連絡方法]** で **[電子メールのフォロー]** の設定を変更することにより、取引先担当者またはリードごとに埋め込みインテリジェンスの電子メール エンゲージメント機能を無効にすることもできます。  
  
 電子メール エンゲージメント機能と関係する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] のコンポーネントやサービスについては、以下で詳しく説明します。  
  
 [!INCLUDE[cc_privacy_note_azure_trust_center](cc-privacy-note-azure-trust-center.md)]  
  
 **[!INCLUDE[pn_azure_storage_account](pn-azure-storage-account.md)]**  
  
 電子メール エンゲージメント機能では、[!INCLUDE[pn_azure_storage_account](pn-azure-storage-account.md)]を使用してメール対話 BLOB を一時的に格納します。