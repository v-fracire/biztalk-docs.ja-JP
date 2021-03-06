---
title: WCF Web サービスのパフォーマンスの最適化 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 93947cef-469c-4126-85a5-06456fa37443
caps.latest.revision: 10
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1b0dc200135d65f179d565ba0fe03cc8df897eeb
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36999379"
---
# <a name="optimizing-wcf-web-service-performance"></a>WCF Web サービスのパフォーマンスの最適化
WCF サービスは、パフォーマンスに影響する多数の構成パラメーターを公開します。 このトピックでは、WCF サービスのパフォーマンスを向上させるためにこれらの構成パラメーターの最適な値の設定に関する一般的なガイダンスを提供します。  
  
## <a name="implement-servicethrottling-behavior-for-backend-wcf-services"></a>バックエンド WCF サービスの serviceThrottling 動作を実装します。  
 バックエンド WCF サービスの serviceThrottling 動作を実装します。 調整サービスでは、リソースの割り当てを適用して、バックエンド WCF サーバーの負荷を均等にできます。 値を変更することによってバックエンド WCF サービスの serviceThrottling 動作が構成されている、 **maxConcurrentCalls**、 **maxConcurrentSessions**、および**maxConcurrentInstances** WCF サービスの構成ファイル内のパラメーター。 設定**maxConcurrentCalls**、 **maxConcurrentSessions**、および**maxConcurrentInstances** 16 より大きい値に * Cpu または CPU の数のコア。 たとえば、8 CPU コアを持つコンピューターは、次のように設定します**maxConcurrentCalls**、 **maxConcurrentSessions**、および**maxConcurrentInstances** 128 (16 * 8 = 128) より大きい値を。次のようにします。  
  
```  
<serviceThrottling  
maxConcurrentCalls="200"  
maxConcurrentSessions="200"  
maxConcurrentInstances="200" />  
```  
  
## <a name="increase-the-default-values-for-the-nettcpbindinglistenbacklog-and-nettcpbindingmaxconnections-properties-in-the-backend-wcf-service-webconfig-file"></a>バックエンド WCF サービスの web.config ファイルで NetTcpBinding.ListenBacklog と NetTcpBinding.MaxConnections プロパティの既定値を大きく  
 **NetTcpBinding.ListenBacklog**保留可能なキュー内の接続要求の最大数を制御するプロパティの Web サービス。 **NetTcpBinding.MaxConnections**プロパティは、クライアント上の後続の再利用するためにプールできる接続の最大数と、サーバー上でディスパッチを保留できる接続の最大数を制御します。 これらの各プロパティには、特に高スループットを必要とするシナリオを処理するドキュメント用の準最適な可能性のある 10 の既定値が使用されます。  
  
 これらのプロパティを実装している WCF サービスを使用する高スループット、ドキュメント処理のシナリオの既定値を増やすことを検討、 **netTcpBinding**クラスをバインドします。  
  
 次の例では、両方の**listenBacklog**と**maxConnections**パラメーターは、「200」の値に設定されます。  
  
```  
<netTcpBinding>  
   <binding name="netTcpBinding"  
      closeTimeout="00:10:00"  
      openTimeout="00:10:00"  
      receiveTimeout="00:10:00"  
      sendTimeout="00:10:00"  
      transactionFlow="false"  
      transferMode="Buffered"  
      transactionProtocol="OleTransactions"  
      hostNameComparisonMode="StrongWildcard"  
      listenBacklog="200"  
      maxBufferPoolSize="1048576"  
      maxBufferSize="10485760"  
      maxConnections="200"  
      maxReceivedMessageSize="10485760">  
      <readerQuotas  
         maxDepth="32"  
         maxStringContentLength="8192"  
         maxArrayLength="16384"  
         maxBytesPerRead="4096"  
         maxNameTableCharCount="16384" />  
      <reliableSession  
         ordered="true"  
         inactivityTimeout="00:10:00"  
         enabled="false" />  
      <security mode="None">  
         <transport clientCredentialType="Windows" protectionLevel="EncryptAndSign" />  
         <message clientCredentialType="Windows" />  
      </security>  
   </binding>  
</netTcpBinding>  
```  
  
 NetTcpBinding.ListenBacklog プロパティの詳細については、次を参照してください。 [NetTcpBinding.ListenBacklog プロパティ](http://go.microsoft.com/fwlink/?LinkId=157752)(http://go.microsoft.com/fwlink/?LinkId=157752) msdn です。  
  
 NetTcpBinding.MaxConnections プロパティの詳細については、次を参照してください。 [NetTcpBinding.MaxConnections プロパティ](http://go.microsoft.com/fwlink/?LinkID=157751)(http://go.microsoft.com/fwlink/?LinkID=157751) msdn です。  
  
## <a name="eliminate-aspnet-httpmodules-that-are-not-required-to-run-wcf-web-services"></a>WCF Web サービスを実行する必要のない ASP.NET httpModules を排除します。  
 既定では、いくつかの ASP.NET httpModules は、IIS 6.0 では、クラシックまたは IIS 7.5 または 7.0 の Integrated パイプラインで要求パイプラインで定義されます。 これらのコンポーネントがインターセプトし、すべての受信要求を処理します。 既定のモジュールは、64 ビットの ASP の %windir%\Microsoft.NET\Framework64\v2.0.50727\CONFIG フォルダーと 32 ビット ASP.NET アプリケーションの %windir%\Microsoft.NET\Framework\v2.0.50727\CONFIG フォルダーに含まれる、web.config ファイルで定義されます。次のスニペットで示すように .NET アプリケーション。  
  
```  
<httpModules>  
<add name="OutputCache" type="System.Web.Caching.OutputCacheModule"/>  
<add name="Session" type="System.Web.SessionState.SessionStateModule"/>  
<add name="WindowsAuthentication" type="System.Web.Security.WindowsAuthenticationModule"/>  
<add name="FormsAuthentication" type="System.Web.Security.FormsAuthenticationModule"/>  
<add name="PassportAuthentication" type="System.Web.Security.PassportAuthenticationModule"/>  
<add name="RoleManager" type="System.Web.Security.RoleManagerModule"/>  
<add name="UrlAuthorization" type="System.Web.Security.UrlAuthorizationModule"/>  
<add name="FileAuthorization" type="System.Web.Security.FileAuthorizationModule"/>  
<add name="AnonymousIdentification" type="System.Web.Security.AnonymousIdentificationModule"/>  
<add name="Profile" type="System.Web.Profile.ProfileModule"/>  
<add name="ErrorHandlerModule" type="System.Web.Mobile.ErrorHandlerModule, System.Web.Mobile, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"/>  
<add name="ServiceModel" type="System.ServiceModel.Activation.HttpModule, System.ServiceModel, Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
</httpModules>  
```  
  
 ほとんどのシナリオでは、これらのモジュールのすべてを読み込む必要はありません。 したがって、WCF Web サービスを実行するときに、次の httpModules を排除することによってパフォーマンスが向上することは。  
  
-   Session  
  
-   Windows 認証  
  
-   FormsAuthentication  
  
-   PassportAuthentication  
  
-   RoleManager  
  
-   AnonymousIdentification  
  
-   プロファイル  
  
## <a name="use-the-wcf-modulehandler-registration-tool-to-configure-wcf-moduleshandlers-and-improve-scalability-of-iis-7570-hosted-wcf-services"></a>WCF のモジュールを使用して、WCF のモジュール/ハンドラーを構成して、IIS 7.5 または 7.0 のスケーラビリティが向上するハンドラーの登録ツールには、WCF サービスがホストされている/  
 WCF のモジュール/ハンドラーの登録ツールがダウンロードできる[ http://go.microsoft.com/fwlink/?LinkId=157593 ](http://go.microsoft.com/fwlink/?LinkId=157593) (http://go.microsoft.com/fwlink/?LinkId=157593)します。 このユーティリティを使用して、一覧をインストールします。 または、次の WCF モジュールを構成することができます。  
  
- WCF 同期 HTTP モジュールとハンドラー  
  
- WCF の非同期 HTTP モジュールとハンドラー  
  
- WCF の HTTP モジュールとハンドラー  
  
  非同期の WCF の HTTP モジュール/ハンドラーを使用して、IIS 7.5 または 7.0 のスケーラビリティを向上させる方法については、WCF サービスをホストされている、Wenlong ドンのブログを参照してください[Orcas SP1 の改善: 非同期 WCF HTTP モジュール/ハンドラー良く IIS7 用。サーバーのスケーラビリティ](http://go.microsoft.com/fwlink/?LinkId=157428)(http://go.microsoft.com/fwlink/?LinkId=157428)します。  
  
## <a name="see-also"></a>参照  
 [BizTalk Server WCF Adapter パフォーマンスの最適化](../technical-guides/optimizing-biztalk-server-wcf-adapter-performance.md)