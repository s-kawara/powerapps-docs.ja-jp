---
title: モデル駆動型アプリの getEnabledProcesses (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 52f79803-2ce0-4ca7-8200-aec544545d62
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getenabledprocesses-client-api-reference"></a>getEnabledProcesses (クライアント API 参照)



[!INCLUDE[./includes/getEnabledProcesses-description.md](./includes/getEnabledProcesses-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.getEnabledProcesses(callbackFunction(enabledProcesses));`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|callbackFunction|関数|あり|このコールバック関数は、ディクショナリ プロパティを持つオブジェクトを含むパラメーターを受け入れる必要があります。プロパティの名前は業務プロセス フローの ID であり、プロパティの値は業務プロセス フローの名前です。<br/><br/>有効なプロセスは、ユーザーの特権に基づいてフィルター処理されます。 プロセスを手動で変更する場合、有効なプロセスのリストは、ユーザーが UI で表示できるものと同じです。|

## <a name="example"></a>例

例にある **Sdk.formOnLoad** 関数は、**formContext.data.process.getEnabledProcesses** メソッドを使用して、エンティティに対して有効になっている業務プロセス フローの情報を非同期に取得します。 このサンプルは、最初のパラメーターとして匿名関数を渡します。 この関数は、データが返され、パラメーターとして匿名関数に渡されると、非同期で実行されます。

有効な業務プロセス フローに関する情報は、ディクショナリ オブジェクトとして提供されます。このとき、プロセスの ID はプロパティの名前、業務プロセス フローの名前はプロパティの値になります。 サンプル コードは、この情報を処理し、後で実行されるロジックがアクセスするグローバル **Sdk.enabledProcesses** 配列に値を設定します。 また、このサンプルは、**Sdk.enabledProcesses** 配列の値をループして、取得した業務プロセス フローに関する情報を **Sdk.writeToConsole** 関数を使用してコンソールに書き込みます。

>[!NOTE]
>サンプルの JavaScript ライブラリに含まれる関数は **Sdk.formOnLoad** 関数を、フォームの **OnLoad** イベント ハンドラーとして設定し、**ハンドラーのプロパティ**ダイアログで、**実行コンテキストを最初のパラメーターとして渡す**チェック ボックスを選択する必要があります。<br/>また、このサンプルでは、**formContext.data.process** API のいくつかのメソッドの使用方法についても示しています。 その目的は、この API を使用してビジネス要件を満たす方法を説明することではなく、主なプロパティ値にコードでアクセスする方法を説明することです。

```JavaScript
//A namespace defined for SDK sample code
//You should define a unique namespace for your libraries
var Sdk = window.Sdk || {};
(function () {
    //A global variable to store information about enabled business processes after they are retrieved asynchronously
    this.enabledProcesses = [];

    // A function to log messages while debugging only
    this.writeToConsole = function (message) {
        if (typeof console != 'undefined')
        { console.log(message); }
    };

    // Code to run in the OnLoad event 
    this.formOnLoad = function (executionContext) {
        // Retrieve the formContext
        var formContext = executionContext.getFormContext();

        // Retrieve Enabled processes
        formContext.data.process.getEnabledProcesses(function (processes) {
            //Move processes to the global Sdk.enabledProcesses array;
            for (var processId in processes) {
                Sdk.enabledProcesses.push({ id: processId, name: processes[processId] })
            }
            Sdk.writeToConsole("Enabled business processes flows retrieved and added to Sdk.enabledProcesses array.");

            //Write the values of the Sdk.enabledProcesses array to the console
            if (Sdk.enabledProcesses.length < 0) {
                Sdk.writeToConsole("There are no enabled business process flows for this entity.");
            }
            else {
                Sdk.writeToConsole("These are the enabled business process flows for this entity:");
                for (var i = 0; i < Sdk.enabledProcesses.length; i++) {
                    var enabledProcess = Sdk.enabledProcesses[i];
                    Sdk.writeToConsole("id: " + enabledProcess.id + " name: " + enabledProcess.name)
                }
            }

            //Any code that depends on the Sdk.enabledProcesses array needs to be initiated here

        });
    };

}).call(Sdk);
```

ブラウザーの開発者ツールを開いてこのサンプルを実行する場合に、有効な複数の業務プロセス フローを持つエンティティに関してコンソールに書き込まれる出力の例を以下に示します。

```
Enabled business processes flows retrieved and added to Sdk.enabledProcesses array.
These are the enabled business process flows for this entity:
id: 7994be68-899e-4a40-8d18-f5c3b6940188 name: Sample Lead Process
id: 919e14d1-6489-4852-abd0-a63a6ecaac5d name: Lead to Opportunity Sales Process
```

### <a name="related-topics"></a>関連トピック

[setActiveProcessInstance](setActiveProcessInstance.md)

[formContext.data.process](../formContext-data-process.md)
 


