---
title: XRM ツール用トレースの構成 (アプリ用 Common Data Service) | Microsoft Docs
description: オペレーションコール、警告、例外およびXRMツールの他の重要なイベントなどのコンポーネントのトレースを構成する方法について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: d7586a5a-40da-427e-bbeb-4f8a371a8dcf
caps.latest.revision: 8
author: MattB-msft
ms.author: kvivek
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="configure-tracing-for-xrm-tooling"></a>XRM ツール用トレースの構成

オペレーション コール、警告、例外、および他の重要なイベントなどの、XRM ツールのすべてのコンポーネントにおいて、プロセスのマイルストーンに関連するレコード データのトレースを有効にできます。 この情報では、Windows クライアント アプリケーションにおける、操作上およびパフォーマンス上の問題のトラブルシュートに使用できます。 XRM ツールのトレースは、[System.Diagnostics.Tracing](/dotnet/api/system.diagnostics.tracing) の最上部に構築されます。 アセンブリまたはコンポーネント、たとえば Microsoft.Xrm.Tooling.Connector のトレースを有効にするには、コードまたはアプリケーション構成ファイル (*\<AppName>*) 内の各コンポーネントに、次の 3 つを定義する必要があります。  
  
- トレースのソース  
- トレースのリスナー  
- **オフ**以外のトレース レベル。 **エラー**、**警告**、**情報**、**詳細**は指定できる他の値です。  
  
 XRM ツールのコンポーネントのトレースを有効にするための構成を以下に示します。 たとえば、次の構成は、Microsoft.Xrm.Tooling.CrmConnectControl コンポーネントのトレースのみを有効にできます。  
  
```xml  
</configuration>  
  <system.diagnostics>  
    <trace autoflush="true" />  
    <sources>  
      <source name="DynamicsCrm.CrmConnectControl"  
        switchName="DynamicsCrm.CrmConnectControl"  
        switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console" type="System.Diagnostics.DefaultTraceListener" />  
          <remove name="Default"/>  
          <add name ="fileListener"/>  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <!--   
            Possible values for switches: Off, Error, Warning, Info, Verbose  
                Verbose:    includes Error, Warning, Info, Trace levels  
                Info:       includes Error, Warning, Info levels  
                Warning:    includes Error, Warning levels  
                Error:      includes Error level  
        -->  
      <add name="DynamicsCrm.CrmConnectControl" value="Verbose"/>  
    </switches>  
    <sharedListeners>  
      <add name="fileListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="XRMLoginControl.log"/>  
      <add name="eventLogListener" type="System.Diagnostics.EventLogTraceListener" initializeData="XRMLogin"/>  
    </sharedListeners>  
  </system.diagnostics>  
</configuration>  
```  
  
XRM ツールのすべてのコンポーネントに対してトレースを有効にしたい場合、それも可能です。 以下の構成は、XRM ツールの 3 つすべてのコンポーネントの組み合わせトレースです。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="true" />  
    <sources>  
      <source name="Microsoft.Xrm.Tooling.Connector.CrmServiceClient"  
              switchName="Microsoft.Xrm.Tooling.Connector.CrmServiceClient"  
              switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console" type="System.Diagnostics.DefaultTraceListener" />  
          <remove name="Default"/>  
          <add name ="fileListener"/>  
        </listeners>  
      </source>  
  
      <source name="Microsoft.Xrm.Tooling.CrmConnectControl"  
              switchName="Microsoft.Xrm.Tooling.CrmConnectControl"  
              switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console" type="System.Diagnostics.DefaultTraceListener" />  
          <remove name="Default"/>  
          <add name ="fileListener"/>  
        </listeners>  
      </source>  
  
      <source name="Microsoft.Xrm.Tooling.WebResourceUtility"  
        switchName="Microsoft.Xrm.Tooling.WebResourceUtility"  
        switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console" type="System.Diagnostics.DefaultTraceListener" />  
          <remove name="Default"/>  
          <add name ="fileListener"/>  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <!--   
            Possible values for switches: Off, Error, Warning, Info, Verbose  
                Verbose:    includes Error, Warning, Info, Trace levels  
                Info:       includes Error, Warning, Info levels  
                Warning:    includes Error, Warning levels  
                Error:      includes Error level  
        -->  
      <add name="Microsoft.Xrm.Tooling.Connector.CrmServiceClient" value="Verbose" />  
      <add name="Microsoft.Xrm.Tooling.CrmConnectControl" value="Verbose"/>  
      <add name="Microsoft.Xrm.Tooling.WebResourceUtility" value="Verbose" />  
  
    </switches>  
    <sharedListeners>  
      <add name="fileListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="XRMToolingLogs.log"/>        
      <add name="eventLogListener" type="System.Diagnostics.EventLogTraceListener" initializeData="XRMTooling" />  
    </sharedListeners>  
  
  </system.diagnostics>  
</configuration>  
```  
  
### <a name="see-also"></a>関連項目

[XRM ツールを使用して Windows のクライアント アプリケーションを作成する](build-windows-client-applications-xrm-tools.md)
