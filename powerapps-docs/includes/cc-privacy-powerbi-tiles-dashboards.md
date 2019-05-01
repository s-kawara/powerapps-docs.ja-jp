---
ms.openlocfilehash: 41ec7aed42a950e5adf0b87783fc568dbe9d02af
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61581195"
---
Power BI のタイルとダッシュボードの埋め込みを有効にすることで、ユーザーが Power BI のタイルとダッシュボードを埋め込んだとき、そのユーザーの [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 用の [!INCLUDE[pn_azure_active_directory](pn-azure-active-directory.md)] 認証トークンが暗黙的な付与で Power BI サービスの認証に使用されます。エンド ユーザーにとってシームレスな “シングルサインオン“ 体験となります。  
  
 管理者は Power BI のタイルとダッシュボードの埋め込みをいつでも無効にし、Power BI サービスの認証手段として [!INCLUDE[pn_dynamics_crm](pn-dynamics-crm.md)] 認証トークンが使用されるのを停止できます。 既存のタイルまたはダッシュボードでは、エンド ユーザーのためのレンダリングが停止します。  
  
 Power BI タイルの埋め込みに関係する [!INCLUDE[pn_azure_shortest](pn-azure-shortest.md)] コンポーネントまたはサービスについては次のセクションで説明されています。  
  
 [!INCLUDE[cc_privacy_note_azure_trust_center](cc-privacy-note-azure-trust-center.md)]  
  
 [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)  
  
 このサービスによって、API と UI の認証に対して、Power BI サービスとの間で認証トークンが交換されます。