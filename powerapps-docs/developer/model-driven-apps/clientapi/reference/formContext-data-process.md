---
title: モデル駆動型アプリの formContext.data.process (クライアント API 参照) | Microsoft Docs
description: クライアント API を使用したモデル駆動型アプリのプロセスの作業の詳細
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 32e8d1d0-4093-4588-a517-2930eec34dce
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="formcontextdataprocess-client-api-reference"></a>formContext.data.process (クライアント API 参照)



イベント、メソッド、およびオブジェクトを提供して、フォーム上の業務プロセス フローのデータを操作します。 フォーム上の業務プロセス フロー コントロールとやり取りする方法については、[formContext.ui.process (クライアント API 参照)](formContext-ui-process.md) を参照してください。

## <a name="process-events-and-event-handler-methods"></a>プロセス イベントとイベント ハンドラー メソッド

以下のイベントとイベント ハンドラー メソッドを使用して、業務プロセス フロー用のスクリプトを記述します。

|イベント | イベント ハンドラー メソッド|
|--|--|
|[OnProcessStatusChange](events/onprocessstatuschange.md)|[addOnProcessStatusChange](formContext-data-process/eventhandlers/addOnProcessStatusChange.md)<br/>[removeOnProcessStatusChange](formContext-data-process/eventhandlers/removeOnProcessStatusChange.md)|
|[OnStageChange](events/OnStageChange.md)|[addOnStageChange](formContext-data-process/eventhandlers/addOnStageChange.md)<br/>[removeOnStageChange](formContext-data-process/eventhandlers/removeOnStageChange.md)|
|[OnStageSelected](events/OnStageSelected.md)|[addOnStageSelected](formContext-data-process/eventhandlers/addOnStageSelected.md)<br/>[removeOnStageSelected](formContext-data-process/eventhandlers/removeOnStageSelected.md)|

## <a name="active-process-methods"></a>アクティブ プロセス メソッド

このメソッドを使用して、アクティブなプロセスに関する情報を取得し、 異なるプロセスをアクティブ プロセスとして設定します。

|Name | 内容 |
|--|--|
|[getActiveProcess](formcontext-data-process/activeprocess/getActiveProcess.md)|[!INCLUDE[formcontext-data-process/activeprocess/includes/getActiveProcess-description.md](formcontext-data-process/activeprocess/includes/getActiveProcess-description.md)]|
|[setActiveProcess](formcontext-data-process/activeprocess/setActiveProcess.md)|[!INCLUDE[formcontext-data-process/activeprocess/includes/setActiveProcess-description.md](formcontext-data-process/activeprocess/includes/setActiveProcess-description.md)]|

## <a name="process-methods"></a>プロセス メソッド 

プロセスには、業務プロセス フローのデータが含まれます。 これらのメソッドを使用して、プロセスのプロパティにアクセスします。

|Name | 内容 |
|--|--|
|[getId](formcontext-data-process/process/getId.md)|[!INCLUDE[formcontext-data-process/process/includes/getId-description.md](formcontext-data-process/process/includes/getId-description.md)]|
|[getName](formcontext-data-process/process/getName.md)|[!INCLUDE[formcontext-data-process/process/includes/getName-description.md](formcontext-data-process/process/includes/getName-description.md)]|
|[getStages](formcontext-data-process/process/getStages.md)|[!INCLUDE[formcontext-data-process/process/includes/getStages-description.md](formcontext-data-process/process/includes/getStages-description.md)]|
|[isRendered](formcontext-data-process/process/isRendered.md)|[!INCLUDE[formcontext-data-process/process/includes/isRendered-description.md](formcontext-data-process/process/includes/isRendered-description.md)]|


## <a name="processinstance-methods"></a>ProcessInstance メソッド

これらのメソッドを使用して、エンティティ レコードのすべてのプロセス インスタンスに関する情報を取得し、 プロセス インスタンスをアクティブなインスタンスとして設定します。

|Name | 内容 |
|--|--|
|[getProcessInstances](formContext-data-process/getProcessInstances.md)|[!INCLUDE[formcontext-data-process/includes/getProcessInstances-description.md](formcontext-data-process/includes/getProcessInstances-description.md)]|
|[setActiveProcessInstance](formContext-data-process/setActiveProcessInstance.md)|[!INCLUDE[formcontext-data-process/includes/setActiveProcessInstance-description.md](formcontext-data-process/includes/setActiveProcessInstance-description.md)]|


## <a name="instance-methods"></a>インスタンス メソッド 

プロセス インスタンスには業務プロセス フローのインスタンスのデータが含まれます。 これらのメソッドを使用して、プロセス インスタンスのプロパティにアクセスします。

|Name | 内容 |
|--|--|
|[getInstanceId](formcontext-data-process/instance/getInstanceId.md)|[!INCLUDE[formcontext-data-process/instance/includes/getInstanceId-description.md](formcontext-data-process/instance/includes/getInstanceId-description.md)]|
|[getInstanceName](formcontext-data-process/instance/getInstanceName.md)|[!INCLUDE[formcontext-data-process/instance/includes/getInstanceName-description.md](formcontext-data-process/instance/includes/getInstanceName-description.md)]|
|[getStatus](formcontext-data-process/instance/getStatus.md)|[!INCLUDE[formcontext-data-process/instance/includes/getStatus-description.md](formcontext-data-process/instance/includes/getStatus-description.md)]|
|[setStatus](formcontext-data-process/instance/setStatus.md)|[!INCLUDE[formcontext-data-process/instance/includes/setStatus-description.md](formcontext-data-process/instance/includes/setStatus-description.md)]|

## <a name="active-stage-methods"></a>アクティブ ステージ メソッド

これらのメソッドを使用して、アクティブ ステージに関する情報を取得し、 異なるステージをアクティブ ステージとして設定します。

|Name | 内容 |
|--|--|
|[getActiveStage](formcontext-data-process/activestage/getActiveStage.md)|[!INCLUDE[formcontext-data-process/activestage/includes/getActiveStage-description.md](formcontext-data-process/activestage/includes/getActiveStage-description.md)]|
|[setActiveStage](formcontext-data-process/activestage/setActiveStage.md)|[!INCLUDE[formcontext-data-process/activestage/includes/setActiveStage-description.md](formcontext-data-process/activestage/includes/setActiveStage-description.md)]|

## <a name="stage-methods"></a>ステージ メソッド 

ステージには、業務プロセス フローのステージのデータが含まれます。 これらのメソッドを使用して、ステージのプロパティにアクセスします。
|Name | 内容|
|--|--|
|[getCategory](formcontext-data-process/stage/getCategory.md)|[!INCLUDE[formcontext-data-process/stage/includes/getCategory-description.md](formcontext-data-process/stage/includes/getCategory-description.md)]|
|[getEntityName](formcontext-data-process/stage/getEntityName.md)|[!INCLUDE[formcontext-data-process/stage/includes/getEntityName-description.md](formcontext-data-process/stage/includes/getEntityName-description.md)]|
|[getId](formcontext-data-process/stage/getId.md)|[!INCLUDE[formcontext-data-process/stage/includes/getId-description.md](formcontext-data-process/stage/includes/getId-description.md)]|
|[getName](formcontext-data-process/stage/getName.md)|[!INCLUDE[formcontext-data-process/stage/includes/getName-description.md](formcontext-data-process/stage/includes/getName-description.md)]|
|[getNavigationBehavior](formcontext-data-process/stage/getNavigationBehavior.md)|[!INCLUDE[formcontext-data-process/stage/includes/getNavigationBehavior-description.md](formcontext-data-process/stage/includes/getNavigationBehavior-description.md)]|
|[getStatus](formcontext-data-process/stage/getStatus.md)|[!INCLUDE[formcontext-data-process/stage/includes/getStatus-description.md](formcontext-data-process/stage/includes/getStatus-description.md)]|
|[getSteps](formcontext-data-process/stage/getSteps.md)|[!INCLUDE[formcontext-data-process/stage/includes/getSteps-description.md](formcontext-data-process/stage/includes/getSteps-description.md)]|

## <a name="step-methods"></a>ステップ メソッド

ステップには、業務プロセス フローのステージに含まれるステップのデータが含まれます。 これらのメソッドを使用して、ステップのプロパティにアクセスします。

|Name | 内容|
|--|--|
|[getAttribute](formcontext-data-process/step/getAttribute.md)|[!INCLUDE[formcontext-data-process/step/includes/getAttribute-description.md](formcontext-data-process/step/includes/getAttribute-description.md)]|
|[getName](formcontext-data-process/step/getName.md)|[!INCLUDE[formcontext-data-process/step/includes/getName-description.md](formcontext-data-process/step/includes/getName-description.md)]|
|[getProgress](formcontext-data-process/step/getProgress.md)|[!INCLUDE[formcontext-data-process/step/includes/getProgress-description.md](formcontext-data-process/step/includes/getProgress-description.md)]|
|[isRequired](formcontext-data-process/step/isRequired.md)|[!INCLUDE[formcontext-data-process/step/includes/isRequired-description.md](formcontext-data-process/step/includes/isRequired-description.md)]|
|[setProgress](formcontext-data-process/step/setProgress.md)|[!INCLUDE[formcontext-data-process/step/includes/setProgress-description.md](formcontext-data-process/step/includes/setProgress-description.md)]|

## <a name="navigation-methods"></a>ナビゲーション メソッド

これらのメソッドを使用して、次のステージや前のステージに移動します。 これらの両方のメソッドは、OnStageChange イベントが発生します。

|Name | 内容|
|--|--|
|[moveNext](formContext-data-process/navigation/moveNext.md)|[!INCLUDE[formcontext-data-process/navigation/includes/moveNext-description.md](formcontext-data-process/navigation/includes/moveNext-description.md)]|
|[movePrevious](formContext-data-process/navigation/movePrevious.md)|[!INCLUDE[formcontext-data-process/navigation/includes/movePrevious-description.md](formcontext-data-process/navigation/includes/movePrevious-description.md)]|

## <a name="other-useful-methods"></a>他の有用なメソッド

これらのメソッドを使用して、アクティブなパスにあるステージ、有効化されたプロセス、選択したステージに関する情報を見つけます。

|Name | 内容|
|--|--|
|[getActivePath](formContext-data-process/activepath/getActivePath.md)|[!INCLUDE[formcontext-data-process/activepath/includes/getActivePath-description.md](formcontext-data-process/activepath/includes/getActivePath-description.md)]|
|[getEnabledProcesses](formContext-data-process/getEnabledProcesses.md)|[!INCLUDE[formcontext-data-process/includes/getEnabledProcesses-description.md](formcontext-data-process/includes/getEnabledProcesses-description.md)]|
|[getSelectedStage](formContext-data-process/getSelectedStage.md)|[!INCLUDE[formcontext-data-process/includes/getSelectedStage-description.md](formcontext-data-process/includes/getSelectedStage-description.md)]|

### <a name="related-topics"></a>関連トピック

[formContext.ui.process (クライアント API 参照)](formContext-ui-process.md)

[Xrm オブジェクト モデルの理解](../understand-clientapi-object-model.md)

[コントロール (クライアント API 参照)](controls.md)




