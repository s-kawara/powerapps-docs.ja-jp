---
title: モデル駆動型アプリの getActivePath (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4916df68-b2d4-4a0b-b341-eb9f7032bc20
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getactivepath-client-api-reference"></a>getActivePath (クライアント API 参照)



[!INCLUDE[./includes/getActivePath-description.md](./includes/getActivePath-description.md)]

アクティブ パスは、分岐ルールとレコードの最新のデータに基づいてプロセス コントロールで現在表示されているステージを表します。

## <a name="syntax"></a>構文

`var stageCollection = formContext.data.process.getActivePath();`

## <a name="return-value"></a>戻り値

**種類:** コレクション。 

**説明**: すべての完了したステージ、現在アクティブなステージ、および分岐ルールの条件に基づいて予測される今後の一連のステージのコレクションです。 状況によっては、**formContext.data.process**.[getActiveProcess](../activeprocess/getActiveProcess.md) によって返されるステージのサブセットとなります。これは、プロセスで発生する分岐に基づき、現在のステージからの有効な遷移を表すステージのみを含むからです。

## <a name="example"></a>例

Sdk.formOnLoad 関数は、**formContext.data.process.getActivePath** メソッドを使用して、ステージのコレクションを取得します。 次に、このサンプル コードは、コレクションの [forEach](../../collections/forEach.md) メソッドを使用して、各ステージをループします。 次に、このコードは、このライブラリで定義されている **Sdk.writeToConsole**  関数を使用して、ステージの主要なプロパティをコンソールに書き込みます。 次にコードは、[getSteps](../stage/getSteps.md) メソッドを使用して、各ステージのステップのコレクションにアクセスします。 最後に、このサンプルは、ステップ コレクションの [forEach](../../collections/forEach.md) メソッドを使用して、各ステップにアクセスし、ステップの主要なプロパティをコンソールに書き込みます。

>[!NOTE]
>サンプルの JavaScript ライブラリに含まれる関数は **Sdk.formOnLoad** 関数を、フォームの **OnLoad** イベント ハンドラーとして設定し、**ハンドラーのプロパティ**ダイアログで、**実行コンテキストを最初のパラメーターとして渡す**チェック ボックスを選択する必要があります。<br/>また、このサンプルでは、**formContext.data.process** API のいくつかのメソッドの使用方法についても示しています。 その目的は、この API を使用してビジネス要件を満たす方法を説明することではなく、主なプロパティ値にコードでアクセスする方法を説明することです。

```JavaScript
// A namespace defined for SDK sample code
// You should define a unique namespace for your libraries
var Sdk = window.Sdk || {};
(function () {

    // A function to log messages while debugging only
    this.writeToConsole = function (message) {
        if (typeof console != 'undefined')
        { console.log(message); }
    };

    // Code to run in the OnLoad event 
    this.formOnLoad = function (executionContext) {
        // Retrieve the formContext
        var formContext = executionContext.getFormContext();

        // Enumerate the stages and steps in the active path
        var activePathCollection = formContext.data.process.getActivePath();
        activePathCollection.forEach(function (stage, n) {
            Sdk.writeToConsole("Stage Index: " + n);
            Sdk.writeToConsole("Entity: " + stage.getEntityName());
            Sdk.writeToConsole("StageId: " + stage.getId());
            Sdk.writeToConsole("Status: " + stage.getStatus());
            var stageSteps = stage.getSteps();
            stageSteps.forEach(function (step, i) {
                Sdk.writeToConsole("    Step Name: " + step.getName());
                Sdk.writeToConsole("    Step Attribute: " + step.getAttribute());
                Sdk.writeToConsole("    Step Required: " + step.isRequired());
                Sdk.writeToConsole("    ---------------------------------------")
            })
            Sdk.writeToConsole("---------------------------------------")
        });
    };
}).call(Sdk);
```

ブラウザーでサンプルを実行すると、ブラウザーの開発者ツールを使用して、コンソールに書き込まれるテキストを表示できます。 たとえば、このサンプルを、営業案件の営業プロセスを使用して、顧客エンティティ フォームで実行すると、コンソールには次のように書き込まれます。

```
Stage Index: 0
Entity: opportunity
StageId: 6b9ce798-221a-4260-90b2-2a95ed51a5bc
Status: active
    Step Name: Identify Contact
    Step Attribute: parentcontactid
    Step Required: false
    ---------------------------------------
    Step Name: Identify Account
    Step Attribute: parentaccountid
    Step Required: false
    ---------------------------------------
    Step Name: Purchase Timeframe
    Step Attribute: purchasetimeframe
    Step Required: false
    ---------------------------------------
    Step Name: Estimated Budget
    Step Attribute: budgetamount
    Step Required: false
    ---------------------------------------
    Step Name: Purchase Process
    Step Attribute: purchaseprocess
    Step Required: false
    ---------------------------------------
    Step Name: Identify Decision Maker
    Step Attribute: decisionmaker
    Step Required: false
    ---------------------------------------
    Step Name: Capture Summary
    Step Attribute: description
    Step Required: false
    ---------------------------------------
---------------------------------------
Stage Index: 1
Entity: opportunity
StageId: 650e06b4-789b-46c1-822b-0da76bedb1ed
Status: inactive
    Step Name: Customer Need
    Step Attribute: customerneed
    Step Required: false
    ---------------------------------------
    Step Name: Proposed Solution
    Step Attribute: proposedsolution
    Step Required: false
    ---------------------------------------
    Step Name: Identify Stakeholders
    Step Attribute: identifycustomercontacts
    Step Required: false
    ---------------------------------------
    Step Name: Identify Competitors
    Step Attribute: identifycompetitors
    Step Required: false
    ---------------------------------------
---------------------------------------
Stage Index: 2
Entity: opportunity
StageId: d3ca8878-8d7b-47b9-852d-fcd838790cfd
Status: inactive
    Step Name: Identify Sales Team
    Step Attribute: identifypursuitteam
    Step Required: false
    ---------------------------------------
    Step Name: Develop Proposal
    Step Attribute: developproposal
    Step Required: false
    ---------------------------------------
    Step Name: Complete Internal Review
    Step Attribute: completeinternalreview
    Step Required: false
    ---------------------------------------
    Step Name: Present Proposal
    Step Attribute: presentproposal
    Step Required: false
    ---------------------------------------
---------------------------------------
Stage Index: 3
Entity: opportunity
StageId: bb7e830a-61bd-441b-b1fd-6bb104ffa027
Status: inactive
    Step Name: Complete Final Proposal
    Step Attribute: completefinalproposal
    Step Required: false
    ---------------------------------------
    Step Name: Present Final Proposal
    Step Attribute: presentfinalproposal
    Step Required: false
    ---------------------------------------
    Step Name: Confirm Decision Date
    Step Attribute: finaldecisiondate
    Step Required: false
    ---------------------------------------
    Step Name: Send Thank You
    Step Attribute: sendthankyounote
    Step Required: false
    ---------------------------------------
    Step Name: File De-brief
    Step Attribute: filedebrief
    Step Required: false
    ---------------------------------------
---------------------------------------
```

### <a name="related-topics"></a>関連トピック

[formContext.data.process](../../formContext-data-process.md)
 


