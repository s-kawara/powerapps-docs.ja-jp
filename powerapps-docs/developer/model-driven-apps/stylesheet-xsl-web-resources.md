---
title: スタイルシート (XSL) の Web リソース (モデル駆動型アプリ) | MicrosoftDocs
description: スタイルシート (XSL) Webリソースを使用して XML データを変換する方法についてについて説明します。
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
# <a name="stylesheet-xsl-web-resources"></a>スタイルシート (XSL) Web リソース

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/stylesheet-xsl-web-resources -->


XML データを変換するには、スタイルシート (XSL) Web リソースを使用します。  
  
## <a name="capabilities-of-xsl-web-resources"></a>XSL Web リソースの機能  
 ソリューションで使用されている XML データを変換するには、XSL Web リソースを使用します。  
  
 以下の Web リソースが連動することで、XML Web リソースのデータを使用してテーブルを表示するページがレンダリングされます。 これらの Web リソースのソース ファイルは、**filestoimport** フォルダーの下の  Import Web Resources サンプルの一部です。 [Web リソースとしてのファイルのインポート](https://code.msdn.microsoft.com/Import-files-as-web-f84ad8dc) のサンプルをダウンロードします。  
  
 **HTML Web リソース:** sample_/ImportWebResources/Content/ShowData.htm  
 ```html  
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
<html>  
<head>  
 <title></title>  
 <script src="Script/Script.js" type="text/javascript"></script>  
 <link href="CSS/Styles.css" rel="stylesheet" type="text/css" />  
</head>  
<body onload="SDK.ImportWebResources.showData()">  
 <div id="results" />  
</body>  
</html>  
```  
  
 **XSL Web リソース:** sample_/ImportWebResources/XSL/Transform.xslt  
 ```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xsl:stylesheet version="1.0"  
                xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
                exclude-result-prefixes="msxsl"  
>  
 <xsl:output method="xml"  
             indent="yes"/>  
  
 <xsl:template match="@* | node()">  
  <xsl:copy>  
   <xsl:apply-templates select="@* | node()"/>  
  </xsl:copy>  
 </xsl:template>  
  
 <xsl:template match="people">  
  <xsl:element name="table">  
   <xsl:element name="thead">  
    <xsl:element name="tr">  
     <xsl:element name="th">  
      <xsl:text>First Name</xsl:text>  
     </xsl:element>  
     <xsl:element name="th">  
      <xsl:text>Last Name</xsl:text>  
     </xsl:element>  
    </xsl:element>  
   </xsl:element>  
   <xsl:element name="tbody">  
    <xsl:apply-templates />  
   </xsl:element>  
  </xsl:element>  
  
 </xsl:template>  
  
 <xsl:template match="person">  
  <xsl:element name="tr">  
   <xsl:element name="td">  
    <xsl:value-of select="@firstName"/>  
   </xsl:element>  
   <xsl:element name="td">  
    <xsl:value-of select="@lastName"/>  
   </xsl:element>  
  </xsl:element>  
  
 </xsl:template>  
  
</xsl:stylesheet>  
  
```  
  
 **XML Web リソース:** sample_/ImportWebResources/Data/Data.xml  
 ```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<people>  
 <person firstName="Apurva"  
         lastName="Dalia" />  
 <person firstName="Ofer"  
         lastName="Daliot" />  
 <person firstName="Jim"  
         lastName="Daly" />  
 <person firstName="Ryan"  
         lastName="Danner" />  
 <person firstName="Mike"  
         lastName="Danseglio" />  
 <person firstName="Alex"  
         lastName="Darrow" />  
</people>  
```  
  
 **スクリプト Web リソース:** sample_/ImportWebResources/Script/Script.js  
 ```javascript  
//If the SDK namespace object is not defined, create it.  
if (typeof (SDK) == "undefined")  
{ SDK = {}; }  
// Create Namespace container for functions in this library;  
SDK.ImportWebResources = {  
 dataFile: "Data/Data.xml",  
 transformFile: "XSL/Transform.xslt",  
 showData: function () {  
  
  //Create an XML document from the Data.xml file  
  var dataXml = new ActiveXObject("Msxml2.DOMDocument.6.0");  
  dataXml.async = false;  
  dataXml.load(this.dataFile);  
  
  //Create an XML document from the Transform.xslt file  
  var transformXSLT = new ActiveXObject("Msxml2.DOMDocument.6.0");  
  transformXSLT.async = false;  
  transformXSLT.load(this.transformFile);  
  
  // Set the innerHTML of the results area to the output of the transformation.  
  var resultsArea = document.getElementById("results");  
  resultsArea.innerHTML = dataXml.transformNode(transformXSLT);  
 }  
  
}  
```  
  
 **CSS Web リソース:** sample_/ImportWebResources/CSS/Styles.css  
 ```css
body  
{  
    font-family: Calibri;  
}  
table  
{  
    border: 1px solid gray;  
    border-collapse: collapse;  
}  
th  
{  
    text-align: left;  
    border: 1px solid gray;  
}  
td  
{  
    border: 1px solid gray;  
}  
```  
  
### <a name="see-also"></a>関連項目  
 [Web リソース](web-resources.md)   
 [Web ページ (HTML) の Web リソースの使用](webpage-html-web-resources.md)   
 [スタイル シート (CSS) Web リソースの使用](css-web-resources.md)   
 [スクリプト (JScript) Web リソースの使用](script-jscript-web-resources.md)   
 [データ (XML) Web リソースの使用](data-xml-web-resources.md)   
 [画像 (JPG、PNG、GIF、ICO) Web リソースの使用](image-web-resources.md)   
