---
title: "BAM ポータルの構成をカスタマイズする |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- BAM portal, alerts
- BAM portal, timeout setting
- queries [BAM], timeout setting
- BAM portal, retry interval
- alerts, configuration options
- BAM portal, configuring
- BAM portal, portal banner
- clustering, NLB [BAM portal]
- BAM portal, Web.config file
- Kerberos protocol, BAM portal
- BAM portal, culture setting
- BAM portal, IIS
- IIS, BAM portal
- BAM portal, NLB cluster
- Web.config file
- BAM portal, 64-bit environments
- BAM portal, Kerberos protocol
- BAM portal, clustering
- 64-bit environments, BAM portal
- IIS, 64-bit support
- NLB system, BAM portal
- BAM portal, customizing
- configuring, BAM portal banner
- 64-bit support, IIS
- BAM portal, distributed environment
ms.assetid: 507bd5f0-b2a0-4d52-85f8-9d984138ca79
caps.latest.revision: "47"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: bad22e9bf2ecddcc50983078b21672f2c755c8a8
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="customizing-the-bam-portal-configuration"></a>BAM ポータルの構成のカスタマイズ
BAM ポータルには、構成可能なオプションが多数あります。 次の手順では、最適なユーザー エクスペリエンスを取得する BAM ポータルを変更する方法を示します。  
  
> [!NOTE]
>  権限を借用した管理者以外のユーザーとしてポータルを構成するときに、資格情報の入力を求められることなく BAM ポータルの機能にアクセスするには、ログオフしてログオンし直すことが必要になる場合があります。 たとえば、次のシナリオを考えてみます。  
>   
>  管理者以外の権限を借用したユーザーの Web サービスまたは BAM ポータルを構成するとします。 その後、Everyone グループがポータルにアクセスできないように、ポータルに対するアクセス許可を設定します。 PortalUsersGroup というローカル グループを作成して、そのグループをポータル ユーザー グループとして割り当てます。 つまり、そのグループのユーザーだけがポータルにアクセスできます。 BAM ポータルを構成した後、現在のユーザーをポータル ユーザー グループに追加します。 BAM ポータルを開くと、資格情報を求められます。 ただし、ログオフしてログオンし直すと、資格情報を求められることなく BAM ポータルを開くことができます。  
>   
>  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]ローカル グループとユーザー アカウントを 1 台のコンピューター構成でのみサポートします。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]単一および複数のコンピューター構成の両方では、ドメイン グループおよびユーザー アカウントをサポートしています。  
  
## <a name="running-the-bam-portal-in-a-64-bit-environment"></a>64 ビット環境での BAM ポータルの実行  
 64 ビット環境でインターネット インフォメーション サービス (IIS) 6 を使用する場合、BAM ポータルを実行するには IIS を 32 ビット モードに設定する必要があります。 モードの設定に関する詳細についてで「32 ビット バージョンの ASP.NET 1.1 と Windows の 64 ビット バージョンの ASP.NET 2.0 の 64 ビット バージョンを切り替える方法」を参照してください。 [http://go.microsoft.com/fwlink/?LinkId=61991](http://go.microsoft.com/fwlink/?LinkId=61991)です。  
  
> [!IMPORTANT]
>  IIS 7 は 32 ビット モードに設定する必要はありません。  
  
#### <a name="to-set-a-64-bit-mode-iis-installation-to-32-bit-mode"></a>64 ビット モードの IIS を 32 ビット モードに設定するには  
  
1.  コマンド プロンプトを開き、実行、 **adsutil**コマンド。 これを行うには、をクリックして**開始**をクリックして**実行**、し、入力**cmd**です。  
  
2.  コマンド プロンプトで、次を入力:`cscript c:\inetpub\adminscripts\adsutil.vbs SET W3SVC/AppPools/Enable32bitAppOnWin64 1`です。  
  
3.  コマンド プロンプトを閉じます。  
  
## <a name="configuring-the-bam-portal-banner"></a>BAM ポータルのバナーを構成します。  
 BAM ポータル ページは、ユーザーのビジネスを表すテキストや画像を表示するように変更できます。  
  
-   Windows Server System のロゴ (BAM ポータル ページの右上隅に配置されます)。  
  
 次の手順では、カスケード スタイル シート ファイル (.css ファイル) を編集して、BAM ポータルの外観をカスタマイズします。 指定されたクラスへの変更のみを行ってください。 クラスに変更を加えている途中でエラーが発生しても BAM ポータルが稼働し続けるように、変更による影響が最小限に留まるようになっています。  
  
> [!CAUTION]
>  データおよびポータルの機能は非表示に styles.css ファイル内の他のクラスを変更して、ポータルを使用できないようにします。  
  
#### <a name="to-configure-the-banner"></a>バナーを構成するには  
  
1.  BAM ポータルの web.config ファイルを編集します。 これを行うには、をクリックして**開始**、 をクリックして**実行**、「notepad [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]bamportal \web.config」とクリック**ok**です。  
  
2.  メイン ページのクイック スタート コンテンツは、次の行を変更することで置き換え可能:\<キーを追加 ="MainPageContentUrl"value="~/MainPageContent.htm"/ >。 変更**MainPageContent.htm**を独自の HTML ファイルを指す値フィールドにします。 HTML ファイルは、web.config ファイルと同じディレクトリに存在する必要があります。  
  
3.  Web.config ファイルに次の行を追加することによってテキストを識別するページを変更する:\<キーを追加"PortalTitle"の値を = ="New Identifying text"/>。 value フィールドを変更して、ポータルを識別するテキストを含めます。  
  
4.  BAM ポータルの styles.css ファイルを編集します。 をクリックして**開始**、 をクリックして**実行**、「notepad [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]bamportal \styles.css」をクリックして**OK**です。  
  
5.  右上隅のロゴを変更します。この操作を行うには、.headerLogo div クラスを探して、background-image: url("../images/WSS_Logo.gif") という行を、作成した画像ファイルを指すように変更します。 .gif 形式の画像を使用することをお勧めします。  
  
6.  SharePoint アイコンを変更するには、次の行には、.headerPageIcon div クラスを探して: 背景イメージ: url("../images/btsSuiteProduction.gif") です。ファイルを指す、イメージを作成しました。  
  
7.  ファイルを保存します。  
  
8.  BAM ポータルを開いて、変更内容を表示します。  
  
## <a name="modifying-the-bam-portal-webconfig-file"></a>BAM ポータルの web.config ファイルを変更します。  
 SSL (Secure Sockets Layer) 用のエンタープライズ シングル サインオン (SSO) 証明書を使用するサーバー上に BAM ポータルが存在する場合、証明書の適切な URL を受け取るようにポータルを構成する必要があります。  
  
#### <a name="to-modify-the-bam-portal-to-support-ssl-sites"></a>SSL サイトをサポートするように BAM ポータルを変更するには  
  
1.  メモ帳を使用して web.config ファイルを開きます。 をクリックして**開始**、 をクリックして**実行**、「notepad [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]bamportal \web.config」とクリック**ok**です。  
  
2.  SSL 対応のポータルの場所を指すように、ファイル内の次の 2 行を変更します。  
  
    ```  
    <add key="BamQueryWSUrl" value="http://localhost/BAM/BamQueryService/BamQueryService.asmx"/>  
    <add key="BamManagementWSUrl" value="http://localhost/BAM/BamManagementService/BamManagementService.asmx"/>  
    ```  
  
3.  ファイルを保存します。  
  
 BAM ポータルでは、ポータルの構成に使用されているカルチャに従って書式設定されたデータが表示され受け取られます。 構成は、web.config ファイルで指定されています。 Web ポータルは、Internet Explorer から送信される「Accept Language」情報を無視します。 たとえば、日本語のカルチャ設定に設定されているし、米国を使用する BAM ポータルを構成する Internet Explorer を実行していること英語はカルチャ設定です。 ここではデータ項目などが日付や整数が表示されます、受理、および米国に該当するルールを使用して並べ替える英語のカルチャ設定ではなく、日本語のカルチャ設定に該当するルール。 日本語形式を使用して入力任意のカルチャに固有の情報が無効と見なされます、BAM ポータルで米国の書式設定されたデータを求めるため英語版です。  
  
 カルチャ設定によって変化するデータの表示および書式設定に対して一貫性のある処理を実現するには、すべての BAM ポータル クライアントに適した言語を 1 つ選択します。 このカルチャ用の BAM ポータルを構成します。 Multilingual User Interface Pack をインストールして、すべてのクライアントが、選択したカルチャに設定されるようにする必要があります。  
  
 英語 (米国) 以外のBAM の英語版のインストールを web.config ファイルのカルチャ パラメーターを設定するために必要な場合があります。 この設定が必要になるのは、次の場合です。  
  
-   日付と時刻の表示形式をローカライズする場合。  
  
-   通貨の表示形式をローカライズする場合。  
  
#### <a name="to-modify-the-culture-setting-of-the-portal"></a>ポータルのカルチャ設定を変更するには  
  
1.  メモ帳を使用して web.config ファイルを開きます。 をクリックして**開始**、 をクリックして**実行**、「notepad [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]bamportal \web.config」とクリック**ok**です。  
  
2.  次の行で、適切なグローバリゼーション設定を反映するように、ファイル内のカルチャ属性を変更します。  
  
    ```  
    <globalization requestEncoding="utf-8" responseEncoding="utf-8" culture="de-DE" uiCulture="en" />  
    ```  
  
3.  ファイルを保存します。  
  
 大量の SQL クエリの待機中にタイムアウトが発生する場合は、クエリ サービスのタイムアウト値を大きくすることが必要になることがあります。  
  
#### <a name="to-increase-the-query-service-time-out-value"></a>クエリ サービスのタイムアウト値を大きくには  
  
1.  メモ帳を使用して web.config ファイルを開きます。 をクリックして**開始**、 をクリックして**実行**、「notepad [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]BAMPortal\BAMManagementService\web.config、をクリックして**OK**です。  
  
2.  QueryServiceTimeout の既定値は 45 秒です。 タイムアウト間隔を増減するには、次の行の値を変更します。  
  
    ```  
    <add key="QueryServiceTimeout" value="45" />  
    ```  
  
3.  ファイルを保存します。  
  
 マルチサーバー環境では、サーバーがオフラインの場合もあります。 この場合、BAM ポータルが応答を停止する遅延時間が生じることがあります。 ユーザー エクスペリエンスを向上させるために、サーバーの再試行間隔を変更できます。 再試行間隔を適切な値に変更すると、いったん接続に失敗しても、BAM クエリ Web サービスでサーバーがオフラインであると見なされる時間が最短になります。  
  
 値は、ローカル データベースがリモート データベースに接続しているときにタイムアウトした場合、データが不完全としてマークし、ローカル コンピューターは、指定した時間が経過するまで、リモート データベースへの接続にしませんを示します。  
  
#### <a name="to-increase-the-retry-interval-for-distributed-activities-in-a-multiserver-environment"></a>マルチサーバー環境で分散アクティビティの再試行間隔を大きくするには  
  
1.  メモ帳を使用して web.config ファイルを開きます。 をクリックして**開始**、 をクリックして**実行**、「notepad [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]BAMPortal\BAMManagementService\web.config、をクリックして**OK**です。  
  
2.  ServerRetryInterval の既定値は 5 分です。 サーバーの再試行間隔を増加または減少するには、次の行の値を変更します。  
  
    ```  
    <add key="ServerRetryInterval" value="5"/>  
    ```  
  
3.  ファイルを保存します。  
  
#### <a name="to-configure-how-alert-notification-options-are-presented-in-the-bam-portal"></a>BAM ポータルに警告通知オプションを表示する方法を構成するには  
  
1.  メモ帳を使用して web.config ファイルを開きます。 をクリックして**開始**、 をクリックして**実行**、「notepad [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]bamportal \web.config」とクリック**ok**です。  
  
2.  値フィールドを変更する、\<キーを追加"AlertNotificationOptions"の値を = =""/> 次の値のいずれかの有効な通知のオプションを指定するコンマ区切りの一覧を含む web.config ファイルの行。 値が空の場合は、サーバーで使用可能なすべての通知オプションがサーバーから返される順に表示されます。 値が認識されない場合は、値が空の場合と同様に処理されます。  
  
    |値|Description|  
    |-----------|-----------------|  
    |ファイル, 電子メール|[ファイル] オプションと [電子メール] オプションが表示されます。 ドロップダウン リストでは、最初に [ファイル]、次に [電子メール] が表示されます。|  
    |電子メール, ファイル|[ファイル] オプションと [電子メール] オプションが表示されます。 ドロップダウン リストでは、最初に [電子メール]、次に [ファイル] が表示されます。|  
    |ファイル|ポータルに、[ファイル] 通知のみが表示されます。|  
    |Email|ポータルに、[電子メール] 通知のみが表示されます。|  
  
3.  ファイルを保存します。  
  
## <a name="distributed-server-environments"></a>分散型サーバー環境  
 BAM ポータルのインストールは、異なるサーバー上のアラートおよび BAM ポータルを配置する場合は、イベント ログに次のエラーが表示されます:"System.Reflection.TargetInvocationException: 呼び出しのターゲットが例外をスローしました。 ---> レジストリ エントリを指定した Notification Services のインスタンスが見つかりませんでした。"  
  
#### <a name="to-configure-the-portal-and-alerts-on-different-servers"></a>さまざまなサーバー上でポータルおよび警告を構成するには  
  
1.  コマンド プロンプトを開きます。  
  
2.  実行**C:\Program files \microsoft SQL Server\90\Notification Services\9.0.242\Bin\nscontrol register bamalerts という名前のサーバー***\<サーバー名 >*置換 *\<サーバー名 >*サーバーの名前に置き換えます。  
  
3.  <localizedText>F5</localizedText> キーを押して、ブラウザーを更新します。  
  
## <a name="configuring-iis-to-allow-the-bam-portal-to-use-the-kerberos-network-protocol"></a>BAM ポータルによる Kerberos ネットワーク プロトコルの使用を許可する IIS の構成  
 BAM ポータルで Kerberos ネットワーク プロトコルを使用する場合は、Web ポータルの ACL セキュリティを変更する必要があります。 IIS が正しく構成されていない場合、次のエラーが発生します。  
  
 HTTP エラー 401.1 - 権限がありません。 無効な資格情報により、アクセスが拒否されました。  
  
 IIS のセキュリティ設定を変更する方法の詳細については、サポート技術情報の記事を参照してください。 [http://go.microsoft.com/fwlink/?LinkId=57922](http://go.microsoft.com/fwlink/?LinkId=57922)です。  
  
## <a name="viewing-aggregate-bam-data-in-the-bam-portal-in-sql-server-2008--deployments"></a>SQL Server 2008 の展開で BAM ポータルの集計 BAM データの表示  
 [!INCLUDE[btsSQLServer2008](../includes/btssqlserver2008-md.md)] を使用する展開環境で、BAM ポータルに接続しているクライアント コンピューターから BAM ポータルの集計データを表示するには、クライアント コンピューターに Microsoft SQL Server 2008 Analysis Services 10.0 OLE DB Provider をインストールする必要があります。 Analysis Services がインストールされていない場合は、次のエラー メッセージが表示されます。  
  
 サーバー  *\<servername >*通信できないか、ビジー状態です。  
  
 Microsoft SQL Server 2008 用 Feature Pack をインストールするを参照してください。 [http://go.microsoft.com/fwlink/?LinkId=70728](http://go.microsoft.com/fwlink/?LinkId=70728)です。  
  
## <a name="see-also"></a>参照  
 [BAM ポータルの計画](../core/planning-for-the-bam-portal.md)