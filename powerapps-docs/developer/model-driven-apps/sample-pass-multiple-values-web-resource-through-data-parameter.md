---
title: 'サンプル: データ パラメーターを使用した Web リソースへの複数の値の引き渡し (モデル駆動型アプリ) | Microsoft Docs'
description: このサンプルは、単一のパラメーターで追加の値を渡し、Web リソースでそれらを処理する手法を表します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-pass-multiple-values-to-a--web-resource-through-the-data-parameter"></a>サンプル: データ パラメーターを使用した Web リソースへの複数の値の引き渡し

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-pass-multiple-values-web-resource-through-data-parameter -->

(HTML) Web リソース ページは、`data` という単一のカスタム パラメーターのみを受け取ることができます。 data パラメーターで複数の値を渡すには、パラメーターをエンコードし、ページ内でパラメーターをデコードする必要があります。  
  
 ここに示すページは、単一のパラメーターで追加の値を渡し、Web リソースでそれらを処理する手法を表します。 
  
## <a name="sample-html-web-resource"></a>HTML Web リソースの例  
 以下の HTML コードは、次の 3 つの関数を定義するスクリプトを含む webpage (HTML) Web リソースを表します。  
  
- **getDataParam**: `body.onload` イベントから呼び出され、ページに渡されたクエリ文字列パラメーターを取得し、`data` という名前のパラメーターを探します。  
  
- **parseDataValue**: `getDataParam` から data パラメーターを受け取り、`data` パラメーターで渡された値を表示するための DHTML テーブルを構築します。  
  
  > [!NOTE]
  >  クエリ文字列に含まれるすべての文字は、[encodeURIComponent メソッド](https://msdn.microsoft.com/library/xh9be5xc\(v=VS.85\).aspx)を使用してエンコードされます。 この関数は、JavaScript [decodeURIComponent メソッド](https://msdn.microsoft.com/library/91b80x6x\(VS.85\).aspx)を使用して、渡された値をデコードします。  
  
- **noParams**: ページにパラメーターが渡されていない場合にメッセージを表示します。  
  
```html  
<!DOCTYPE html >  
<html lang="en-us">  
<head>  
 <title>Show Data Parameters Page</title>  
 <style type="text/css">  
  body  
  {  
   font-family: Segoe UI, Tahoma, Arial;  
   background-color: #d6e8ff;  
  }  
  tbody  
  {  
   background-color: white;  
  }  
  th  
  {  
   background-color: black;  
   color: White;  
  }  
 </style>  
 <script type="text/javascript">  
  document.onreadystatechange = function () {  
   if (document.readyState == "complete") {  
    getDataParam();  
   }  
  }  
  
  function getDataParam() {  
   //Get the any query string parameters and load them  
   //into the vals array  
  
   var vals = new Array();  
   if (location.search != "") {  
    vals = location.search.substr(1).split("&");  
    for (var i in vals) {  
     vals[i] = vals[i].replace(/\+/g, " ").split("=");  
    }  
    //look for the parameter named 'data'  
    var found = false;  
    for (var i in vals) {  
     if (vals[i][0].toLowerCase() == "data") {  
      parseDataValue(vals[i][1]);  
      found = true;  
      break;  
     }  
    }  
    if (!found)  
    { noParams(); }  
   }  
   else {  
    noParams();  
   }  
  }  
  
  function parseDataValue(datavalue) {  
   if (datavalue != "") {  
    var vals = new Array();  
  
    var message = document.createElement("p");  
    setText(message, "These are the data parameters values that were passed to this page:");  
    document.body.appendChild(message);  
  
    vals = decodeURIComponent(datavalue).split("&");  
    for (var i in vals) {  
     vals[i] = vals[i].replace(/\+/g, " ").split("=");  
    }  
  
    //Create a table and header using the DOM  
    var oTable = document.createElement("table");  
    var oTHead = document.createElement("thead");  
    var oTHeadTR = document.createElement("tr");  
    var oTHeadTRTH1 = document.createElement("th");  
    setText(oTHeadTRTH1, "Parameter");  
    var oTHeadTRTH2 = document.createElement("th");  
    setText(oTHeadTRTH2, "Value");  
    oTHeadTR.appendChild(oTHeadTRTH1);  
    oTHeadTR.appendChild(oTHeadTRTH2);  
    oTHead.appendChild(oTHeadTR);  
    oTable.appendChild(oTHead);  
    var oTBody = document.createElement("tbody");  
    //Loop through vals and create rows for the table  
    for (var i in vals) {  
     var oTRow = document.createElement("tr");  
     var oTRowTD1 = document.createElement("td");  
     setText(oTRowTD1, vals[i][0]);  
     var oTRowTD2 = document.createElement("td");  
     setText(oTRowTD2, vals[i][1]);  
  
     oTRow.appendChild(oTRowTD1);  
     oTRow.appendChild(oTRowTD2);  
     oTBody.appendChild(oTRow);  
    }  
  
    oTable.appendChild(oTBody);  
    document.body.appendChild(oTable);  
   }  
   else {  
    noParams();  
   }  
  }  
  
  function noParams() {  
   var message = document.createElement("p");  
   setText(message, "No data parameter was passed to this page");  
  
   document.body.appendChild(message);  
  }  
  //Added for cross browser support.  
  function setText(element, text) {  
   if (typeof element.innerText != "undefined") {  
    element.innerText = text;  
   }  
   else {  
    element.textContent = text;  
   }  
  
  }  
 </script>  
</head>  
<body>  
</body>  
</html>  
  
```  
  
#### <a name="using-this-page"></a>このページの使用方法  
  
1.  サンプル コードを使用して、"new_/ShowDataParams.htm" という webpage Web リソースを作成します。  
  
     渡すパラメーターは `first=First Value&second=Second Value&third=Third Value` です。  
  
    > [!NOTE]
    >  フォーム エディターの [Web リソースのプロパティ] ダイアログ ボックスを使用して静的パラメーターを追加する場合は、パラメーターをエンコードせずに**カスタム パラメーター(data)** フィールドに貼り付けることができます。 これらの値は自動的にエンコードされますが、ページ内でデコードして値を抽出する必要はあります。  
  
2.  コードで生成される動的な値の場合は、パラメーターで `encodeURIComponent` メソッドを使用します。 エンコードされる値は次のようになります。  
  
     `first%3DFirst%20Value%26second%3DSecond%20Value%26third%3DThird%20Value`  
  
     ページを開き、エンコードされたパラメーターを data パラメーターの値として渡します。  
  
    ```  
    http://<server name>/WebResources/new_/ShowDataParams.htm?Data=first%3DFirst%20Value%26second%3DSecond%20Value%26third%3DThird%20Value  
    ```  
  
    > [!NOTE]
    >  Web リソースをフォームに追加し、エンコードされていないパラメーターを**カスタム パラメーター(data)** フィールドに貼り付けた場合は、フォームをプレビューできます。  
  
3.  `new_/ShowDataParams.htm` により、動的に生成されたテーブルが表示されます。  
  
    |パラメーター|値|  
    |---------------|-----------|  
    |第 1|First Value|  
    |第 2|Second Value|  
    |第 3|Third Value|  
  
### <a name="how-it-works"></a>動作  
 データ クエリ文字列パラメーター値に埋め込まれた値にアクセスするには、Web ページ Web リソースで、data パラメーターの値を抽出し、コードを使用して文字列を配列に分割して、名前と値の各ペアに個別にアクセスできます。  
  
 ページが読み込まれると、`getDataParam` 関数が呼び出されます。 この関数は、data パラメーターを識別し、値を `ParseDataValue` 関数に渡します。 data パラメーターが見つからない場合、`noParams` 関数はテーブルではなくページにメッセージを追加します。  
  
 `ParseDataValue` 関数は、`getDataParam` と同様のロジックを使用してカスタム パラメーター区切り文字を特定し、名前と値のペアの配列を作成します。 次に、テーブルを生成し、空の document.body に追加します。  
  
### <a name="see-also"></a>関連項目  
 [Web リソース](web-resources.md)   
 [サンプル: Web リソースとしてファイルをインポート](sample-import-files-web-resources.md)   
 [Web ページ (HTML) の Web リソース](webpage-html-web-resources.md)   
