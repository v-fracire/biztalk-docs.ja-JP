---
title: "指向ソリューションのインライン バージョンおよびアダプター バージョンのサービスをインストールする方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- certificate services
- service solution tutorial, affiliat applications [SSO]
- service solution tutorial, adapter version
- service solution tutorial, Web services
- service solution tutorial, definition files [BAM]
- service solution tutorial, COM+ applications
- service solution tutorial, virtual directories
- service solution tutorial, testing connectivity
- TI components
- MQSeries queues, creating
- service solution tutorial, deploying
- service solution tutorial, MQSeries adapters
- service solution tutorial, mainframe CICS applications
- service solution tutorial, certificate services
- service solution tutorial, back-end systems
- service solution tutorial, MQSeries queues
- service solution tutorial, remote environments
- certificates, creating requests
- service solution tutorial, starting service
- service solution tutorial, TI components
- service solution tutorial, inline version
- CICS application
- service solution tutorial, installing
- service solution tutorial, deleting stub version
- service solution tutorial, certificates
ms.assetid: 6050cfe9-4e94-4a55-8b24-fbcc74d9e8f4
caps.latest.revision: "97"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: cb7de8939037f9e7647c62c1164e3c3de3ab378c
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-install-the-inline-and-adapter-versions-of-the-service-oriented-solution"></a>サービス指向ソリューションのインライン バージョンおよびアダプター バージョンをインストールする方法
次の手順では、サービス指向ソリューションのインライン バージョンおよびアダプタ バージョンをコンピュータにインストールするための準備を行う方法、およびコンピュータにソリューションをインストールする方法について説明します。  
  
-   [サービス指向ソリューションのアダプターとインライン バージョンをインストールするコンピューターを準備します](#step1)  
  
-   [サービス指向ソリューションのスタブ バージョンを削除します。](#step3)  
  
-   [アクセスするサービス指向ソリューションのバックエンド システムを準備します。](#step5)  
  
-   [セキュリティで保護されたソケット レイヤー (SSL) の Web サーバーを構成します。](#step7)  
  
-   [バックエンド システム用の Web サービスを作成します。](#step9)  
  
-   [サービス指向ソリューションの TI コンポーネントを作成します。](#step11)  
  
-   [Web サービスのオーケストレーションの仮想ディレクトリを作成します。](#step13)  
  
-   [ビルド サービス指向ソリューション](#step15)  
  
-   [SSO 関連アプリケーションを作成します。](#step17)  
  
-   [サービス指向ソリューションの BAM 定義ファイルを配置します。](#step19)  
  
-   [配置サービス指向ソリューション](#step21)  
  
-   [メインフレームが利用できない場合は、スタブ Pending Transactions Web サービスを構成します。](#step23)  
  
-   [開始、サービス指向ソリューション](#step25)  
  
> [!NOTE]
>  サービス指向ソリューションはフォルダーにある\< *BizTalk Server のインストール フォルダー*> \SDK\Scenarios\SO です。  
  
> [!NOTE]
>  このソリューションに対応するメインフレームがない場合、ポートのバインドを変更して、Pending Transactions のスタブ Web サービスを使用できます。 メインフレームのトランザクションをエミュレートするため、Web サービスは、ローカルにトランザクションを生成します。  
  
##  <a name="step1"></a>サービス指向ソリューションのアダプターとインライン バージョンをインストールするコンピューターを準備します  
  
#### <a name="to-prepare-the-computer-for-installing-the-adapter-and-inline-versions-of-the-service-oriented-solution"></a>サービス指向ソリューションのアダプター バージョンおよびインライン バージョンをコンピューターにインストールするための準備を行うには  
  
1.  Windows SharePoint Services をインストールした場合 (ルートを除外)、既定の Web サイトの Windows SharePoint Services 管理パスから次のようにします  をクリック**開始**、 をポイント**すべてのプログラム**、 をポイント。**管理ツール**、クリックして**SharePoint サーバーの全体管理**です。  
  
    1.  **仮想サーバーの構成****仮想サーバーの設定を構成する**です。  
  
    2.  **仮想サーバーのリスト**] ページで [**既定の Web サイト**です。  
  
    3.  **仮想サーバーの設定**] ページで [**管理パスの定義**です。  
  
    4.  **インクルード パス**のセクションで、**管理パスの定義** ページで、**ルート** をクリックし、**選択したパスの削除**です。  
  
    5.  コマンド プロンプトで IISReset コマンドを実行します。  
  
2.  をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**管理ツール**、 をクリックして**コンピューターの管理**コンソール、および追加し、ローカルの Administrators グループに BizTalk サービス アカウント。  
  
3.  コンピュータからログオフして、BizTalk サービス アカウントを使用してコンピュータにログオンします。  
  
4.  コマンド プロンプトで、次のコマンドを入力し、&lt;localizedText&gt;Enter&lt;/localizedText&gt; キーを押して、%BTSSolutionsPath% 環境変数を設定します。 次に、コマンド プロンプトを終了します。  
  
    -   setx BTSSolutionsPath [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\Scenarios"  
  
        > [!NOTE]
        >  64 ビット コンピューターを使用する場合は、「%ProgramFiles%」の代わりに「%ProgramFiles%(x86)」と入力してください。  
  
        > [!NOTE]
        >  SETX コマンドの詳細については、Microsoft TechNet Web サイトを参照してください。 [http://go.microsoft.com/fwlink/?LinkId=67831](http://go.microsoft.com/fwlink/?LinkId=67831)です。  
  
##  <a name="step3"></a>サービス指向ソリューションのスタブ バージョンを削除します。  
  
#### <a name="to-remove-the-stub-version-of-the-service-oriented-solution"></a>サービス指向ソリューションのスタブ バージョンを削除するには  
  
1.  開く、 **BizTalk Server 管理コンソール**次のように: をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント[!INCLUDE[btsBizTalkServer2006r3ui](../includes/btsbiztalkserver2006r3ui-md.md)]、順にクリック**BizTalk Server 管理**です。  
  
2.  **BizTalk Server 管理コンソール**、展開**BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**を右クリックして**[btsscn.so.customerservice]**、クリックして**停止**です。 **アプリケーションの停止**ダイアログ ボックスで、**完全停止 - インスタンスを終了**、クリックして**停止**です。  
  
    > [!NOTE]
    >  インライン バージョンおよびアダプター バージョンをインストールするために、スタブ バージョンを削除する必要はありません。 すべてのバージョンを一緒に配置する場合は、この手順を省略できます。  
  
3.  コマンド プロンプトを開いて次のコマンドを入力し、&lt;localizedText&gt;Enter&lt;/localizedText&gt; キーを押します。 このコマンドは、既定のスクリプト ホストを CScript.exe に変更します。  
  
    -   `cscript /H:CScript`  
  
4.  コマンド プロンプトで、現在のディレクトリを %BTSSolutonsPath%\SO\BTSSoln\Scripts フォルダーに変更し、次のコマンドを入力して &lt;localizedText&gt;Enter&lt;/localizedText&gt; キーを押します。  
  
    -   `UnEnlistStub.vbs`  
  
5.  コマンド プロンプトで次のコマンドを入力し、ENTER キーを押します。  
  
    -   `UndeployStub.vbs`  
  
6.  コマンド プロンプトで、次のコマンドを実行します。  
  
     SET PATH=%PATH%;[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]Tracking"  
  
     これで、BAM ユーティリティを参照するためのパスが設定されます。  
  
    > [!NOTE]
    >  64 ビット コンピューターを使用している場合は、入力`%ProgramFiles(x86)%`の代わりに`%ProgramFiles%`です。  
  
7.  コマンド プロンプトで、ディレクトリを %BTSSolutionsPath%\SO\BTSSoln\BAM フォルダーに変更し、次のコマンドを実行します。  
  
    -   `bm remove-all -DefinitionFile:ServiceLevelTracking.xml`  
  
8.  コマンド プロンプトでのディレクトリに移動\<*エンタープライズ シングル サインオンをインストール ディレクトリ*>、および次のコマンドを実行します。  
  
    -   `ssomanage -tickets no no`  
  
9. コマンド プロンプトで次のコマンドを実行し、WoodgroveBank.CustomerService SSO 関連アプリケーションを削除します。  
  
    -   `ssomanage -deleteapp WoodgroveBank.CustomerService`  
  
10. コマンド プロンプトで次のコマンドを実行し、スタブ バージョンで使用される Web サイトを削除します。 Iisvdir.vbs の詳細については、Microsoft TechNet Web サイトを参照してください。 [http://go.microsoft.com/fwlink/?LinkId=67830](http://go.microsoft.com/fwlink/?LinkId=67830)です。  
  
    -   `iisvdir /delete W3SVC/1/ROOT/Microsoft.Samples.BizTalk.WoodgroveBank.OrchProxy.Stub`  
  
    -   `iisvdir /delete W3SVC/1/ROOT/Microsoft.Samples.BizTalk.WoodgroveBank.StubSAP`  
  
    -   `iisvdir /delete W3SVC/1/ROOT/Microsoft.Samples.BizTalk.WoodgroveBank.StubPendingTransactions`  
  
    -   `iisvdir /delete W3SVC/1/ROOT/Microsoft.Samples.BizTalk.WoodgroveBank.StubPaymentTracker`  
  
11. 次のようにインターネット インフォメーション サービス (IIS) マネージャーを開始: をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**管理ツール**をクリックして**インターネット インフォメーション サービス (IIS) マネージャー**です。  
  
    -   展開、**アプリケーション プール**の以前の Web アプリケーションを作成したアプリケーション プールを右クリックしをクリックして**削除**、順にクリック**[ok]**確認ダイアログでダイアログ ボックス。  
  
12. をクリックして**開始**、 をポイント**コントロール パネルの** 、 をクリックして**プログラム追加と削除**、IBM WebSphere MQ Client for Windows をアンインストールします。  
  
13. 開始**Visual Studio コマンド プロンプト**し、スタブ バージョン用にインストールした amqmdnet.dll を削除するのには、次のコマンドを実行します。  
  
    -   `gacutil /u amqmdnet`  
  
##  <a name="step5"></a>アクセスするサービス指向ソリューションのバックエンド システムを準備します。  
  
#### <a name="to-install-the-required-applications-for-the-back-end-systems-for-the-service-oriented-solution-to-access"></a>サービス指向ソリューションがアクセスするバックエンド システムに必要なアプリケーションをインストールするには  
  
1.  ローカル コンピューターに IBM WebSphere MQ for Windows のバージョン 5.3 サーバーをインストールします。  
  
    1.  すべての設定を既定のままにします。 セットアップ、**既定の構成**の最後に、 **WebSphere MQ ウィザードの準備**です。 キュー マネージャーは、qm _ という名前\<*コンピューター名*>。  
  
    2.  フィックス パック 10 (CSD10) をインストールします。 すべての設定を既定のままにします。  
  
2.  MQSeries エージェントをインストールします。  
  
    1.  [!INCLUDE[btsBizTalkServer2006r3](../includes/btsbiztalkserver2006r3-md.md)] セットアップ プログラムを再度実行します。  
  
    2.  **プログラムのメンテナンス**] ページで、[**変更**、順にクリック**次**です。  
  
    3.  **コンポーネントのインストール** ページで、展開、**追加のソフトウェア**ノードをクリックして**MQSeries エージェント**です。  
  
    4.  **完了**ことを確認] ページで、 **[BizTalk MQSeries エージェント構成ウィザードの**が選択されていません。  
  
    > [!NOTE]
    >  **MQSeries エージェント**for Windows がインストールされている チェック ボックスは、IBM WebSphere MQ の後にのみアクティブ化されています。  
  
3.  開く、 **Visual Studio コマンド プロンプト**、ディレクトリに移動、 \< *IBM MQSeries インストール ディレクトリ*> \bin フォルダーに、その後、次のコマンド。  
  
    -   `gacutil /i amqmdnet.dll`  
  
4.  メインフレームにアクセスするために Microsoft Host Integration Server 2004 をインストールする場合、Microsoft [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] をインストールします。 セットアップ プログラムでの**オプション**] ページで、[ **Visual c# .NET**、し、その他のコンポーネントのチェック ボックスをオフにします。 もその他のコンポーネントをインストールする必要はありません、 **Visual c# .NET**です。  
  
    > [!NOTE]
    >  Host Integration Server 2004 の TI デザイナーを使用する場合、[!INCLUDE[btsVStudioNet2003](../includes/btsvstudionet2003-md.md)] が必要です。  
  
5.  インストールし、メインフレームにアクセスした場合は、Microsoft Host Integration Server 2004 を構成します。 すべての設定を既定のままにします。  
  
#### <a name="to-create-the-mqseries-queues"></a>MQSeries キューを作成するには  
  
1.  WebSphere MQ エクスプ ローラーを開き、展開**キュー マネージャー**、キューを作成するキュー マネージャーを展開します。 通常、キュー マネージャーの名前 qm _ として\<*コンピューター名*>。  
  
2.  WebSphere MQ エクスプ ローラーを右クリックして**キュー**、 をポイント**新規**をクリックして**ローカル キュー**のアダプター バージョン用の次のローカル キューを作成し、解決方法:  
  
    -   AdapterSOAInputQueue  
  
    -   AdapterSOAOutputQueue  
  
    > [!NOTE]
    >  キューでは MQSeries クラスターを共有できますが、これは必須ではありません。  
  
    > [!NOTE]
    >  MQSeries キュー マネージャーの名前およびキューの名前では、大文字と小文字が区別されます。  
  
3.  前のステップを繰り返して、インライン バージョン用の次のローカル キューを作成します。  
  
    -   InlineSOAOutputQueue  
  
    -   InlineSOAInputQueue  
  
4.  前のステップを繰り返して、Payment Tracker シミュレーター用の次のローカル キューを作成します  (Payment Tracker シミュレーターはアダプター バージョンおよびインライン バージョンの両方で使用されます)。  
  
    -   LastPaymentsInputQueue  
  
    -   LastPaymentsOutputQueue  
  
#### <a name="to-complete-configuration-of-the-mqseries-adapter"></a>MQSeries アダプターの構成を完了するには  
  
1.  をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]、順にクリック**BizTalk MQSeries エージェント構成ウィザード**です。  
  
2.  **ようこそ** ページで、をクリックして**次**です。  
  
3.  **アプリケーション Id** ] ページで、[**このユーザー**、ユーザー名とパスワードを入力します。 MQSeries エージェントの COM+ アプリケーションは、このユーザー アカウントで実行されます。 このチュートリアルでは、BizTalk サービスが使用するユーザー アカウントとして同じものを使用します。 ない場合は、ユーザー アカウントに、MQSeries アダプターをホストする BizTalk サービスを追加する必要があります、 **CreatorOwner** COM + アプリケーションの役割です。  
  
4.  をクリックして**はい**上、 **MQSConfigWiz**ダイアログ ボックスで、前の手順で入力したユーザー アカウントが管理者特権を持っている場合。  
  
5.  **ロールの名前**] ページで [**次**です。  
  
6.  **MQSAgent COM + アプリケーションを作成する** ページで、をクリックして**次へ**、順にクリック**完了**上、**完了**ページ。  
  
#### <a name="to-configure-the-mainframe-cics-application"></a>メインフレームの CICS アプリケーションを構成するには  
  
1.  メモ帳を使用して %BTSSolutionsPath%\SO\MFAccess\HISTIComponent フォルダーの bizcbl.txt とその "コピー ブック" (MainFrameProgramVTCS2Description.txt) を開き、内容を確認します。  
  
    -   bizcbl.txt には、アカウント番号入力からランダム アカウント ステートメントを返す COBOL プロシージャが記述されています。  
  
    -   MainFrameProgramVTCS2Descriptoin.txt には、入出力データ情報を記述する COMMAREA が記述されています。 COMMAREA は、呼び出し元プログラムと呼び出し先プログラムの間でデータをやり取りするために使用する連続したメモリ ブロックです。  
  
    > [!NOTE]
    >  コピー ブックを使用してトランザクション インテグレーター (TI) メタデータ ファイルを生成し、[!INCLUDE[vs2010](../includes/vs2010-md.md)] で TI デザイナー プラグインを使用することもできます。  
  
    > [!NOTE]
    >  以降のステップは正常な配置を行うために非常に重要な操作ですが、一般的には BizTalk Server 開発者は行いません。 メインフレームの担当者に依頼して、メインフレーム環境を適切に構成する必要があります。 このチュートリアルで必要なソフトウェアは、一般的にほとんどのメインフレーム環境にインストールされています。 最小のメインフレーム オペレーティング システムの環境の詳細については、Host Integration Server のマニュアルを参照してください。  
  
2.  FTP などを使用して、ホストに COBOL コードをコピーします。  
  
3.  COBOL コードとコピー ブックをコンパイルします。 次のコードは、COBOL コンパイラ用のジョブ制御言語 (JCL) のサンプルです。  
  
    ```  
    //COB      EXEC PGM=IGYCRCTL,  
    //            PARM=&COBPARM,  
    //            REGION=&REG  
    //STEPLIB  DD DSN=&COMPINDX..SIGYCOMP,DISP=SHR  
    //SYSLIB   DD DSN=&INDEX..SDFHCOB,DISP=SHR  
    //         DD DSN=&INDEX..SDFHMAC,DISP=SHR  
    //         DD DSN=&HLQ..&COMP..COBCOPY,DISP=SHR  
    //SYSPRINT DD SYSOUT=&OUTC  
    //*SYSPRINT DD DSN=&&INPUT,DISP=(,PASS),UNIT=SYSDA,  
    //*         SPACE=(TRK,(100,50)),  
    //*         DCB=(DSORG=PS,LRECL=121,BLKSIZE=2420,RECFM=FBA)  
    //SYSIN    DD DSN=&&SYSCIN,DISP=(OLD,DELETE)  
    //SYSLIN   DD DSN=&&LOADSET,  
    //            DISP=(MOD,PASS),  
    //            UNIT=&WORK,  
    //            SPACE=(80,(250,100))  
    //SYSUT1   DD UNIT=&WORK,SPACE=(460,(350,150))  
    //SYSUT2   DD UNIT=&WORK,SPACE=(460,(350,150))  
    //SYSUT3   DD UNIT=&WORK,SPACE=(460,(350,150))  
    //SYSUT4   DD UNIT=&WORK,SPACE=(460,(350,150))  
    //SYSUT5   DD UNIT=&WORK,SPACE=(460,(350,150))  
    //SYSUT6   DD UNIT=&WORK,SPACE=(460,(350,150))  
    //SYSUT7   DD UNIT=&WORK,SPACE=(460,(350,150))  
    ```  
  
4.  コンパイルしたソースをリンク編集して、実行可能ファイルを作成します。 次のコードは、COBOL リンク編集用の JCL のサンプルです。  
  
    ```  
    //LKED     EXEC PGM=IEWL,REGION=&REG,  
    //            PARM=&LNKPARM,COND=(5,LT,COB)  
    //SYSLIB   DD DSN=&INDEX..SDFHLOAD,DISP=SHR  
    //         DD DSN=CEE.SCEELKED,DISP=SHR  
    //         DD DSN=&TCPINDX..SEZATCP,DISP=SHR  
    //SYSLMOD  DD DSN=&LMINDX..&COMP..LOADLIB,DISP=SHR  
    //SYSUT1   DD UNIT=&WORK,  
    //            DCB=BLKSIZE=1024,  
    //            SPACE=(1024,(200,20))  
    //SYSPRINT DD SYSOUT=&OUTC  
    //SYSLIN   DD DSN=&&LOADSET,DISP=(OLD,DELETE)  
    //         DD DSN=&&COPYLINK,DISP=(OLD,DELETE)  
    ```  
  
5.  CICS メインフレーム アプリケーションを構成します。  
  
    -   このステップでは、メインフレーム システム プログラマまたは CICS 開発者が TCPIPSERVICE、セッション、接続、トランザクション、およびプログラム リソース定義をインストールする必要があります。  
  
    -   メインフレーム管理者に、IP アドレス、ポート番号、およびアクセス可能なプログラムへのリンク名を問い合わせてください。  
  
        > [!NOTE]
        >  このチュートリアルは、メインフレームで CICS アプリケーションを使用し、トランザクション用のプログラミング モデルが TCP/IP (Enhanced Listener Mode (ELM) リンク) であることを前提としています。  
  
##  <a name="step7"></a>セキュリティで保護されたソケット レイヤー (SSL) の Web サーバーを構成します。  
  
#### <a name="to-install-certificate-services"></a>証明書サービスをインストールするには  
  
1.  をクリックして**開始**、] をポイント**コントロール パネルの [**、順にクリック**プログラム追加と削除**です。  
  
2.  **プログラム追加と削除**ダイアログ ボックスで、をクリックして**Windows コンポーネントの追加/削除**です。  
  
3.  **Windows コンポーネント ウィザード**を選択、**証明書サービス**、 をクリックして**次へ**、しに従って、画面に表示されるインストールを完了する指示します。  
  
#### <a name="to-create-a-certificate-request"></a>証明書要求を作成するには  
  
1.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Web サイト**を右クリックし、**既定の Web サイト**をクリックして**プロパティ**、をクリックして、**ディレクトリ セキュリティ** タブをクリックして**サーバー証明書**です。  
  
2.  **へようこそ**のページ、 **Web サーバー証明書ウィザード**、 をクリックして**次**です。  
  
3.  **サービス証明書**] ページで、[**新しい証明書を作成**、順にクリック**次**です。  
  
4.  **証明書の要求** ページで、をクリックして**ここで、要求を準備するが、後で送信**、クリックして**次へ**です。  
  
5.  **名とセキュリティ設定** ページで、すべての設定の既定では、保持して、をクリックして**次**です。  
  
6.  **組織情報**ページで、会社の組織と組織単位名を入力し、をクリックして**次**です。  
  
7.  **サイトの一般名** ページで、コンピューター名を入力、**共通名**ボックスし、をクリックして**次**です。  
  
8.  **地理情報** ページで、地理的な情報を入力してをクリックして**次**です。  
  
9. **証明書要求ファイル名** ページで、入力`c:\certreq.txt`で、**ファイル名**ボックスし、をクリックして**次**です。  
  
10. **要求ファイルの概要** ページで、をクリックして**次へ**、順にクリック**完了**上、**完了**ページ。  
  
#### <a name="to-submit-the-certificate-request-to-the-certification-authority"></a>証明機関に証明書の要求を送信するには  
  
1.  Internet Explorer で、[アドレス] ボックスで、次のように入力します。 `http://localhost/certsrvt`、ENTER キーを押します。  
  
2.  **へようこそ**  ページで、をクリックして**証明書を要求**、クリックして**高度な証明書の要求**上、**証明書を要求**ページです。  
  
3.  **証明書の要求の高度な**] ページで [ **PKCS #10 ファイルまたは base64 でエンコードされた PKCS #7 ファイルを使用して更新の要求にエンコードされた base64 を使用して、証明書要求を送信**です。  
  
4.  "証明書の要求を作成するには"貼り付けますの手順で作成した c:\certreq.txt からすべてのテキストをコピー、**保存されている要求**ボックスに、**証明書の要求または更新の要求を送信**クリックして、ページ、**送信**です。  
  
#### <a name="to-issue-a-certificate-using-certification-authority-management-tool"></a>証明機関管理ツールを使用して証明書を発行するには  
  
1.  をクリックして**開始**、 をポイント**管理ツール**、順にクリック**証明機関**です。  
  
2.  **証明機関**コンソールで、証明機関の名前を展開し、展開、**保留中の要求**、前の手順では、ポイントに送信した証明書の要求を右クリックして**すべてのタスク**、クリックして**問題**です。  
  
3.  閉じる、**証明機関**コンソールです。  
  
#### <a name="to-download-the-certificate-to-the-web-server"></a>証明書を Web サーバーにダウンロードするには  
  
1.  Internet Explorer で、[アドレス] ボックスで、次のように入力します。 `http://localhost/certsrvt`、ENTER キーを押します。  
  
2.  **ようこそ** ページで、をクリックして**保留中の証明書の要求の状態を表示**です。  
  
3.  **保留中の証明書要求の状態を表示** ページで、証明書をクリックして**要求**証明書の要求を作成するには」の手順で作成しました。  
  
4.  **証明書は発行** ページでのエンコード スキームのいずれかを選択してをクリックして**証明書のダウンロード**です。  
  
5.  **セキュリティ警告**ダイアログ ボックスで、をクリックして**保存**、し、証明書を c:\certnew.cer として保存します。  
  
#### <a name="to-install-the-certificate-to-the-web-server"></a>Web サーバーに証明書をインストールするには  
  
1.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**を右クリックし、**既定の Web サイト**証明書の要求を作成するし、をクリックして**プロパティ**です。  
  
2.  **プロパティ**ダイアログ ボックスで、をクリックして、**ディレクトリ セキュリティ** タブをクリックして**サーバー証明書**です。  
  
3.  **へようこそ**のページ、 **Web サーバー証明書ウィザード**、 をクリックして**次**です。  
  
4.  **保留中の証明書の要求**] ページで、[**保留中の要求を処理し、証明書をインストール**、順にクリック**次**です。  
  
5.  **保留中の要求を処理** ページで、入力`c:\certnew.cer`で、**パスとファイル名**テキスト ボックス、およびクリック**次へ**です。  
  
6.  をクリックして**次へ**上、 **SSL ポート** ページで、をクリックして**次へ**上、**証明書の概要** ページで、をクリックして**を完了**上、**確認**ページ。  
  
    > [!NOTE]
    >  このチュートリアルでは、証明書サービスと Web サーバーの両方を同じコンピューターにインストールするため、ローカル コンピューターの信頼されたルート証明機関のストアにサーバー証明書をインストールする必要はありません。  
  
##  <a name="step9"></a>バックエンド システム用の Web サービスを作成します。  
  
#### <a name="to-create-a-new-iis-application-pool-for-the-pending-transaction-web-services"></a>Pending Transaction Web サービス用に新しいアプリケーション プールを作成するには  
  
1.  **インターネット インフォメーション サービス (IIS) マネージャー**を右クリックして**アプリケーション プール****新規**、し、 **のアプリケーションプール**.  
  
    > [!NOTE]
    >  サービス指向ソリューションでは、この Web サービスを使用してメインフレームにアクセスします。  
  
2.  **新しいアプリケーション プールの追加** ダイアログ ボックスに、入力、**アプリケーション プール ID** (任意の値) をクリックし、 **ok**です。  
  
3.  **インターネット インフォメーション サービス (IIS) マネージャー**作成したアプリケーション プールを右クリックし、**プロパティ**です。  
  
4.  **プロパティ** ページで、をクリックして、 **Identity**  タブで **構成可能**、入力、**ユーザー名**と**パスワード**、クリックして**OK**です。 このチュートリアルでは、BizTalk サービスが使用するユーザー アカウントとして同じものを使用します。  
  
#### <a name="to-create-the-pendingtransactions-web-service-for-runtime"></a>ランタイム用の PendingTransactions Web サービスを作成するには  
  
1.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**を右クリックし、**既定の Web サイト**、 をポイント**新規**とをクリックして**仮想ディレクトリ**を実行する**仮想ディレクトリの作成ウィザード**です。  
  
     使用して、**仮想ディレクトリの作成ウィザード**、スタブ SAP Web サービスの次の仮想ディレクトリを作成します。  
  
     Alias = Microsoft.Samples.BizTalk.WoodgroveBank.PendingTransactions  
  
     パス = \< *BizTalk インストール ディレクトリ*> \SDK\Scenarios\SO\MFAccess\PendingTransactions  
  
     Access Permissions = Read, Run scripts  
  
2.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**、展開、**既定の Web サイト**を右クリックしてクリックして、Microsoft.Samples.BizTalk.WoodgroveBank.PendingTransactions**プロパティ**です。  
  
    1.  **ディレクトリ セキュリティ** タブで、をクリックして**編集**を変更する**認証とアクセス制御**です。 選択**基本認証 (パスワードはクリア テキストで送信)**、し、その他をオフに**認証アクセス**チェック ボックスをオンします。 をクリックして**OK**を閉じる、**認証方法** ダイアログ ボックス。  
  
    2.  **ディレクトリ セキュリティ** タブで、をクリックして**編集**下にある、**セキュリティで保護された通信**ボックスで、グループ化し、確認**セキュリティで保護されたチャネル (SSL)**で、**セキュリティ保護された通信** ダイアログ ボックス。  
  
    3.  **仮想ディレクトリ** タブで、設定、**アプリケーション プール**Pending Transaction Web サービスの新しい IIS アプリケーション プールの作成"するには」手順で作成したアプリケーション プールにします。  
  
#### <a name="to-create-the-pendingtransactions-web-service-for-development-environment"></a>開発環境用の PendingTransactions Web サービスを作成するには  
  
1.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**を右クリックし、**既定の Web サイト**、 をポイント**新規**とをクリックして**仮想ディレクトリ**を実行する**仮想ディレクトリの作成ウィザード**です。  
  
     使用して、**仮想ディレクトリの作成ウィザード**、スタブ SAP Web サービスの次の仮想ディレクトリを作成します。  
  
     Alias = PendingTransactions  
  
     パス = \< *BizTalk インストール ディレクトリ*> \SDK\Scenarios\SO\MFAccess\PendingTransactions  
  
     Access Permissions = Read, Run scripts  
  
2.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Web サイト**、展開、**既定の Web サイト**PendingTransactions を右クリックし、クリックして**プロパティ**です。  
  
    1.  **ディレクトリ セキュリティ** タブで、をクリックして**編集**を変更する**認証とアクセス制御**です。 選択**への匿名アクセスを有効にする**です。 をクリックして**OK**を終了します。  
  
        > [!NOTE]
        >  開発環境用の PendingTransactions Web アプリケーションは [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] で使用します。 この Web アプリケーションは実稼働環境では不要です。  
  
    2.  **仮想ディレクトリ** タブで、設定、**アプリケーション プール**Pending Transaction Web サービスの新しい IIS アプリケーション プールの作成"するには」手順で作成したアプリケーション プールにします。  
  
#### <a name="to-create-the-stub-sap-web-service"></a>スタブ SAP Web サービスを作成するには  
  
1.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**を右クリックし、**既定の Web サイト**、 をポイント**新規**とをクリックして**仮想ディレクトリ**を実行する**仮想ディレクトリの作成ウィザード**です。  
  
     使用して、**仮想ディレクトリの作成ウィザード**、スタブ SAP Web サービスの次の仮想ディレクトリを作成します。  
  
     Alias = Microsoft.Samples.BizTalk.WoodgroveBank.StubSAP  
  
     パス = \< *BizTalk インストール ディレクトリ*> \SDK\Scenarios\SO\BTSSoln\StubWebServices\SAP  
  
     Access Permissions = Read, Run scripts  
  
2.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**、展開、**既定の Web サイト**を右クリックしてMicrosoft.Samples.BizTalk.WoodgroveBank.StubSAP をクリックして**プロパティ**、し、次のように設定を変更します。  
  
    1.  **仮想ディレクトリ** タブで、設定、**アプリケーション プール**に\< *YourAppPool*> 新しい IIS アプリケーションを作成するには」の手順で作成します。プール Pending Transaction Web サービスの"です。  
  
    2.  **ディレクトリ セキュリティ**] タブで、をクリックして**編集**で、**認証とアクセス制御**ボックスで、グループ化し、[ **への匿名アクセスを有効にします。**. をクリックして**OK**を終了します。  
  
##  <a name="step11"></a>サービス指向ソリューションの TI コンポーネントを作成します。  
  
#### <a name="to-create-a-com-application-for-the-ti-component"></a>TI コンポーネント用の COM+ アプリケーションを作成するには  
  
1.  コマンド プロンプトで %systemroot%\system32\com\comexp.msc を実行します。  
  
2.  **コンポーネント サービス**コンソールで、**コンポーネント サービス**、展開**コンピューター**、展開**マイ コンピューター**を右クリックして**COM + アプリケーション**、指す**新規**、順にクリック**アプリケーション**です。  
  
    1.  **へようこそ**  ページで、をクリックして**次へ**、順にクリック**空のアプリケーションを作成**上、**のインストールまたは新しいアプリケーションを作成**ページ。  
  
    2.  型`BTSScn SO TI Component`で、**新しいアプリケーションの名前を入力**ボックスで、**サーバー アプリケーション**として**ライセンス認証の種類**、クリックして**次へ**.  
  
    3.  **アカウント**のグループ ボックス、**アプリケーション Id の設定**] ページで、[**このユーザー**、ユーザー名とパスワードを入力し、**ユーザー**と**パスワード**ボックス。 作成する COM+ アプリケーションは、このユーザー アカウントで実行されます。 このユーザー アカウントは、ローカルの HIS Runtime Users グループのメンバーである必要があります。 このチュートリアルでは、BizTalk サービスが使用するユーザー アカウントとして同じものを使用します。  
  
    4.  **アプリケーション ロールの追加**] ページで [**次**です。  
  
    5.  **にユーザー ロールを追加** ページで、展開**CreatorOwner**、 をクリックして**ユーザー**、クリックして**追加**です。  
  
    6.  **[ユーザーまたはグループ**] ダイアログ ボックスで、メインフレームにアクセスするために使用されるユーザー アカウントを選択します。 このチュートリアルでは、UserID ローカル アカウントを追加します。  
  
        > [!NOTE]
        >  TI コンポーネントを使用して CICS トランザクションにアクセスする場合、.NET リモート コンポーネントをホストしている COM+ アプリケーションまたは Web アプリケーションを使用できます。 このチュートリアルではメインフレームへのアクセスに TI コンポーネント用の COM+ アプリケーションおよび COM 相互運用を使用して、パフォーマンスを向上させます。  
  
    7.  **完了**] ページで [**完了**です。  
  
#### <a name="to-create-a-remote-environment-to-access-the-mainframe"></a>メインフレームにアクセスするためのリモート環境を作成するには  
  
1.  をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**Microsoft Host Integration Server 2004**、順にクリック**TI マネージャー**です。  
  
2.  **TI マネージャー**コンソールで **トランザクション インテグレーター (構成)**、展開**Windows Initiated Processing**を右クリックして**リモート環境**、指す**新規**、順にクリック**リモート環境**です。  
  
    1.  **ようこそ** ページで、をクリックして**次**です。  
  
    2.  **新しいリモート環境の構成** ページで、入力、**リモート アプリケーション名**、クリックして**次へ**です。 このチュートリアルでは、Mainframe_TCP という名前を使用します。  
  
    3.  **ホスト環境の構成とプログラミング モデル**] ページで、[ **CICS**の**ターゲット ホスト**と**ELM リンク**の**プログラミング モデル**、クリックして**次**です。  
  
    4.  **エンドポイント TCP/IP の構成** ページにメインフレームの IP アドレスを入力、 **IP/DNS アドレス**ボックスし、をクリックして**編集**ポート番号を追加します。 HIS COM は、このエンドポイント アドレスを使用してトランザクションにアクセスします。  
  
    5.  **完了**] ページで [**完了**です。  
  
#### <a name="to-create-the-ti-component-for-the-service-oriented-solution"></a>サービス指向ソリューション用の TI コンポーネントを作成するには  
  
1.  をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**Microsoft Host Integration Server 2004**、順にクリック**TI マネージャー**です。  
  
2.  **TI マネージャー**コンソールで、をクリックして**トランザクション インテグレーター (構成)**をクリックして**Windows Initiated Processing**、順にクリック**オブジェクト**. 右クリック**オブジェクト**をクリックして**新規**、順にクリック**オブジェクト**です。  
  
    1.  **ようこそ** ページで、をクリックして**次**です。  
  
    2.  **指定または検索オブジェクト** ページで **参照**、%BTSSolutionsPath%\SO\MFAccess\HISTIComponent フォルダーの SOHISTIUsingCOM.TLB を選択し、クリックして**次へ**.  
  
    3.  **COM オブジェクトの環境特性の定義**] ページで、[ **BTSScn SO TI Component**の**COM + アプリケーション**、クリックして**[次へ]**.  
  
    4.  **リモート環境の定義** ページで、前の手順で作成したリモート環境を選択して、**リモート環境では、し、次へ をクリックします。**  
  
    5.  **WIP オブジェクトの作成** ページで、をクリックして**次へ**、順にクリック**完了**上、**完了**ページ。  
  
#### <a name="to-test-the-connectivity-to-the-mainframe"></a>メインフレームへの接続をテストするには  
  
1.  Windows エクスプローラーで %BTSSolutionsPath%\SO\MFAccess\HISTISimpleTester フォルダーを開き、Interop.SOHISTIUsingCOM.dll.reg ファイルをダブルクリックします。 これにより、ランタイム呼び出し可能ラッパー (RCW) を経由して TI コンポーネントを呼び出す HISTISimpleTester アプリケーションのレジストリ値が追加されます。  
  
2.  Windows エクスプローラーで %BTSSolutionsPath%\SO\MFAccess\ フォルダーを開き、SetupMFAccess.bat を実行します。  
  
3.  Windows エクスプローラーで %BTSSolutionsPath%\SO\MFAccess\HISTISimpleTester\bin\Debug フォルダーに移動し、BTSScnSOHISTIComponentSimpleTester.exe を実行します。  
  
    -   HISTISimpleTester アプリケーションでクリックして**Call Mainframe Program - COM を使用して**です。 メインフレームで実行されている COBOL アプリケーションから、5 レコードが返されます。  
  
##  <a name="step13"></a>Web サービスのオーケストレーションの仮想ディレクトリを作成します。  
  
#### <a name="to-create-the-virtual-directories-for-the-orchestration-web-services"></a>オーケストレーション Web サービス用の仮想ディレクトリを作成するには  
  
1.  **インターネット インフォメーション サービス (IIS) マネージャー**を右クリックして**アプリケーション プール****新規**、し、 **のアプリケーションプール**.  
  
    1.  **新しいアプリケーション プールの追加** ダイアログ ボックスに、入力、**アプリケーション プール ID** (任意の値) をクリックし、 **ok**です。  
  
    2.  作成したアプリケーション プールを右クリックし、**プロパティ**です。  
  
    3.  **プロパティ** ページで、をクリックして、 **Identity**  タブで **構成可能**、入力、**ユーザー名**と**パスワード**、クリックして**OK**です。 このチュートリアルでは、BizTalk サービスが使用しているユーザー アカウントを使用します。  
  
    > [!NOTE]
    >  このユーザーには、オーケストレーション プロキシ Web サービスを実行する権限が必要です。また、BizTalk Server 管理者グループ、SSO 管理者グループ、または SSO 関連管理者グループのいずれかにこのユーザーを追加する必要があります。  
  
2.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**を右クリックし、**既定の Web サイト**、 をポイント**新規**とをクリックして**仮想ディレクトリ**を実行する**仮想ディレクトリの作成ウィザード**です。  
  
     使用して、**仮想ディレクトリの作成ウィザード**、アダプター バージョン用の Web サービス プロキシの次の仮想ディレクトリを作成します。  
  
     Alias = Microsoft.Samples.BizTalk.WoodgroveBank.OrchProxy.Adapter  
  
     パス = \< *BizTalk インストール ディレクトリ*> \SDK\Scenarios\SO\BTSSoln\OrchProxy\Adapter  
  
     Access Permissions = Read, Run scripts  
  
3.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Web サイト、**展開、 **Default Web Site**を右クリックしてMicrosoft.Samples.BizTalk.WoodgroveBank.OrchProxy.Adapter をクリックして**プロパティ**、し、次のように設定を変更します。  
  
    1.  **仮想ディレクトリ** タブで、設定、**アプリケーション プール**に\< *YourAppPool*> 前の手順で作成しました。  
  
    2.  **ディレクトリ セキュリティ** タブで、をクリックして**編集**で、**認証とアクセス制御**グループ ボックスで、**統合 Windows 認証のみ有効になっている**、し、その他のオフ**認証アクセス**チェック ボックスをオンします。 をクリックして**OK**を終了します。  
  
4.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**を右クリックし、**既定の Web サイト**、 をポイント**新規**とをクリックして**仮想ディレクトリ**を実行する**仮想ディレクトリの作成ウィザード**です。  
  
     使用して、**仮想ディレクトリの作成ウィザード**、インライン バージョン用の Web サービス プロキシの次の仮想ディレクトリを作成します。  
  
     Alias = Microsoft.Samples.BizTalk.WoodgroveBank.OrchProxy.Inline  
  
     パス = \< *BizTalk インストール ディレクトリ*> \SDK\Scenarios\SO\BTSSoln\OrchProxy\Inline  
  
     Access Permissions = Read, Run scripts  
  
5.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**、展開、**既定の Web サイト**を右クリックしてMicrosoft.Samples.BizTalk.WoodgroveBank.OrchProxy.Inline をクリックして**プロパティ**、し、次のように設定を変更します。  
  
    1.  **仮想ディレクトリ** タブで、設定、**アプリケーション プール**に\< *YourAppPool*> で作成しました。  
  
    2.  をクリックして**ディレクトリ セキュリティ** タブで、をクリックして**編集**で、**認証とアクセス制御**グループ ボックスで、**統合 Windows 認証のみ有効になっている**、し、その他のオフ**認証アクセス**チェック ボックスをオンします。 をクリックして**OK**を終了します。  
  
##  <a name="step15"></a>ビルド サービス指向ソリューション  
  
#### <a name="to-build-the-service-oriented-solution"></a>サービス指向ソリューションをビルドするには  
  
-   コマンド プロンプトでディレクトリを変更 BTSSolutionsPath%\SO\BTSSoln、型 % `SetupBTSSoln.bat`、ENTER キーを押します。 SetupBTSSoln.bat では、次のタスクが実行されます。  
  
    -   SO ソリューションのアセンブリに署名を一意の厳密な名前キー (SNK) を作成します。  
  
    -   SNK から公開キー トークンを抽出し、公開キー トークンを使用してバインド ファイルを更新します。  
  
    -   SO ソリューションをビルドします。  
  
    -   %BTSSolutionsPath%\Common フォルダーに SSOApplicationConfig を作成します。  
  
##  <a name="step17"></a>SSO 関連アプリケーションを作成します。  
  
#### <a name="to-create-the-sso-affiliate-applications"></a>SSO 関連アプリケーションを作成するには  
  
1.  コマンド プロンプトを開いて、ディレクトリを %BTSSolutionsPath%\SO\BTSSoln\Scripts フォルダーに変更します。  
  
2.  コマンド プロンプトで、メモ帳を使用して PendTransAffApp.xml を開き、内容を確認します。 このファイルへの変更は、不要です。  
  
    > [!NOTE]
    >  PendTransAffApp.xml では、Pending Transactions バックエンド システム用の SSO 関連アプリケーション WoodgroveBank.PendingTransactions が定義されています。 また、SSO 関連アプリケーションのユーザー グループと管理者グループも定義されています。 このチュートリアルでは、使用**BizTalk Application Users**と**BizTalk Server 管理者**です。  
    >   
    >  SSO 関連アプリケーションの別のグループを使用する場合は、Active Directory で (任意の名前) を持つ Windows グループを作成し、変更する必要があります、 **appAdminAccount**と**appUserAccount**PendTransAffApp.xml 内のノードです。 これを行う場合は、値を設定する必要があります**groupApp**の属性**フラグ**ノードを"yes"です。  
    >   
    >  SSO 関連アプリケーションの詳細については、次を参照してください。 [SSO 関連アプリケーション](../core/sso-affiliate-applications.md)です。  
  
3.  コマンド プロンプトで、メモ帳を使用して PendTransUserMap.xml ファイルを開き、次のように編集します。  
  
    ```  
    <mapping>  
      <windowsDomain><DomainName></windowsDomain>  
      <windowsUserId><UserID></windowsUserId>  
      <externalUserId><ExternalUserID></externalUserId>  
    </mapping>  
    ```  
  
    > [!NOTE]
    >  PendTransUserMap.xml ファイルには、Pending Transactions バックエンド システム用のユーザー マッピングが保存されています。  
  
    > [!NOTE]
    >  **ExternalUserId**ノード、Pending Transactions バックエンド システムの外部ユーザー ID を使用します。 このチュートリアルでは、外部 ID として UserID を使用します。  
  
    > [!NOTE]
    >  **WindowsUserId**ノード、ユーザー入力名に、 **externalUserId**にマップされます。 ドメイン グループとドメイン ユーザー アカウントの両方を使用できます。 このユーザーは、Pending Transactions バックエンド システムの使用が許可されたグループのメンバーである必要があります。 このチュートリアルでは、BizTalk サービスのユーザー名を使用します。  
  
    > [!NOTE]
    >  **WindowsDomain**  ノードのドメイン名を入力、 **windowsUserId**です。  
  
4.  コマンド プロンプトで、メモ帳を使用して PmntTrckAffApp.xml ファイルを開き、ファイルの内容を確認します。 このファイルへの変更は、不要です。  
  
    > [!NOTE]
    >  PmntTrckAffApp.xml では、Payment Tracker バックエンド システム用の SSO 関連アプリケーション WoodgroveBank.PaymentTracker が定義されています。  
  
5.  コマンド プロンプトで、メモ帳を使用して PmntTrckUserMap.xml ファイルを開き、次のように編集します。  
  
    ```  
    <mapping>  
      <windowsDomain><DomainName></windowsDomain>  
      <windowsUserId><UserID></windowsUserId>  
      <externalUserId><ExternalUserID></externalUserId>  
    </mapping>  
    ```  
  
    > [!NOTE]
    >  Payment Tracker SSO 関連アプリケーションは MQSeries アダプターによって使用され、マップされた外部ユーザー IDおよびパスワードが MQSeries ヘッダー プロパティを使用して送信されます。 MQSeries アダプターが実行されている場合、MQSeries サーバーは BizTalk サービス アカウントのみを検証します。 外部ユーザーの資格情報は検証しません。  
    >   
    >  SSO の詳細については、MQSeries アダプタのアプリケーションをそれ以後を参照してください[方法を構成する MQSeries アダプターの受信場所と送信ポートに](../core/how-to-configure-mqseries-adapter-receive-locations-and-send-ports.md)です。  
  
    > [!NOTE]
    >  PmntTrckUserMap.xml ファイルには、Payment Tracker バックエンド システム用の SSO ユーザー マッピングが保存されています。 Payment Tracker シミュレーター プログラムでは、ユーザー認証が成功する条件と失敗する条件の両方がシミュレートされます。  
    >   
    >  プログラム文字で始まるすべてのユーザー Id の認証に成功**PT** (たとえば、 **PTUserID**)、すべてのユーザーで始まっていない Id の認証に失敗したと**PT**. このため、テストする条件に応じて、適切なユーザー ID を選択できます。 全体を繰り返すことができますも**マッピング**各ユーザー ID のノードと同じファイル内の複数のマッピングを定義します。  
  
    > [!NOTE]
    >  **ExternalUserId**ノード、Payment Tracker バックエンド システムの外部ユーザー ID を入力します。 このチュートリアルでは、外部 ID として PTUserID を使用します。  
  
    > [!NOTE]
    >  **WindowsUserId**ノード、ユーザー入力名に、 **externalUserId**にマップされます。 このユーザーは、Payment Tracker バックエンド システムの使用が許可されたグループのメンバーである必要があります。 このチュートリアルでは、BizTalk サービスのユーザー名を使用します。  
  
    > [!NOTE]
    >  **WindowsDomain**  ノードのドメイン名を入力、 **windowsUserId**です。  
  
6.  コマンド プロンプトで、メモ帳を使用して ConfigStoreApp.xml ファイルを開き、ファイルの内容を確認します。  
  
     このファイルは、このシナリオで構成パラメータを保存するために使用する SSO の構成ストア アプリケーションを定義します。 一部の構成パラメーターには、アダプター バージョンとインライン バージョンの両方の SAP との通信時に使用されるタイムアウト値と、インライン バージョンの使用時に使用するキュー マネージャーの名前およびキューが含まれます。 このファイルへの変更は、不要です。  
  
7.  コマンド プロンプトで、メモ帳を使用して SetConfigValuesInSSO.cmd ファイルを開き、次の表に従ってファイルの内容を確認および変更します。  
  
    > [!NOTE]
    >  このコマンド ファイルは、SSO データベースの構成パラメーターの値を設定します。 コマンド ファイルの最初にローカル変数の値を割り当てる SET ステートメントがいくつか含まれます。  
    >   
    >  SAPAdapterTimeout、PendingTransactionsAdapterTimeout、および PaymentTrackingAdapterTimeout の値は、アダプター バージョンで使用されます。 他の値は、インライン バージョンで使用されます。  
  
    > [!NOTE]
    >  入力することができます""(2 つの二重引用符) マークされている既定値の\<ユーザー指定 > 次の表にします。  
  
    |パラメーター|既定値|Description|  
    |---------------|-------------------|-----------------|  
    |SAPAdapterTimeout|20000|SAP バックエンドに対する要求の最大タイムアウト (ミリ秒)。|  
    |SAPInlineTimeout|20000|SAP バックエンドに対する要求の最大タイムアウト (ミリ秒)。|  
    |SAPInlineHostName|\<指定されたユーザー >|SAP バックエンド識別子。|  
    |SAPInlineClientNumber|\<指定されたユーザー >|SAP クライアント番号。|  
    |SAPInlineSystemNumber|\<指定されたユーザー >|SAP システム番号。|  
    |SAPInlineUserName|\<指定されたユーザー >|SAP バックエンドへの接続に使用するユーザー名。|  
    |SAPInlinePassword|\<指定されたユーザー >|SAP バックエンドへの接続に使用するパスワード。|  
    |PendingTransactionsAdapterTimeout|20000|Pending Transactions サーバーに対する要求の最大タイムアウト (ミリ秒)。|  
    |PendingTransactionsInlineTimeout|20000|Pending Transactions サーバーに対する要求の最大タイムアウト (ミリ秒)。|  
    |PendingTransactionsInlineURL|https://\<*コンピューター名*>/Microsoft.Samples.BizTalk.WoodgroveBank.PendingTransactions/PendTransWS.asmx|Pending Transactions サービスの URL。 \<*コンピューター名*> と一致する必要があります、**共通名**証明書の要求を作成するには」の手順でします。 "Localhost"を使用する必要がありますいない\<*コンピューター名*>。|  
    |PendingTransactionsInlineSSOAffiliateApp|WoodgroveBank.PendingTransactions|Pending Transactions SSO アプリケーション名。|  
    |PaymentTrackingAdapterTimeout|20000|Payment Tracking システムに対する要求の最大タイムアウト (ミリ秒)。|  
    |PaymentTrackingInlineTimeout|20000|Payment Tracking システムに対する要求の最大タイムアウト (ミリ秒)。|  
    |PaymentTrackingInlineQManager|\<ユーザー指定 > (通常 qm _\<*コンピューター名*>)。|MQSeries キュー マネージャーの名前。|  
    |PaymentTrackingInlineMQChannelDefinition|" " (二重引用符を 2 つ入力してください)|ローカルの場合は空の文字列。または、リモート MQ サーバーのフォーマットされたチャネル名。 IBM WebSphere MQ を構成するすべての既定の設定を保持する場合、チャネル定義になる時\<*コンピューター名*>/tcp/\<*コンピューター名*> (1414) です。|  
    |PaymentTrackingInlineRequestQueue|LastPaymentsInputQueue|Payment Tracking 要求用の MQ キュー名。|  
    |PaymentTrackingInlineResponseQueue|LastPaymentsOutputQueue|Payment Tracking 応答用の MQ キュー名。|  
    |PaymentTrackingInlineSSOAffiliateApp|WoodgroveBank.PaymentTracker|Payment Tracking SSO アプリケーション名。|  
    |StubSAPWebServiceURL|http://localhost/Microsoft.Samples.BizTalk.WoodgroveBank.StubSAP/StubSAPWS.asmx|Credit Limit SAP システムのスタブ Web サービス URL。|  
  
8.  コマンド プロンプトで次のコマンドを実行して、PATH 環境変数を設定します。  
  
    -   `SET PATH=%PATH%;"%CommonProgramFiles%\Enterprise Single Sign-On"`  
  
9. コマンド プロンプトで CreateInitialConfigInSSO.cmd を実行します。 これは、SSO 関連アプリケーション、SSO 構成ストア アプリケーション、および関連アプリケーションのユーザー マッピングを作成します。 その後で、SetConfigValuesInSSO.cmd が実行され、SSO 構成ストア アプリケーションに構成値が格納されます。  
  
10. コマンド プロンプトで次のコマンドを実行して、Pending Transactions 関連アプリケーション用のユーザー資格情報を設定します。 使用して、 \< **DomainName**> と\< **UserID**> の PendTransUserMap.xml に定義されている、 \<WindowsDomain >\\<WindowsUserId\>です。 このコマンドでは、このチュートリアルで使用している外部ユーザー (UserID) のパスワードの入力が求められます。  
  
    -   `ssomanage -setcredentials <WindowsDomain>\<WindowsUserId> WoodgroveBank.PendingTransactions`  
  
11. コマンド プロンプトで次のコマンドを実行して、Payment Tracker 関連アプリケーション用のユーザー資格情報を設定します。 使用して、 \< **DomainName**> と\< **UserID**> の PmntTrckUserMap.xml に定義されている、 \<WindowsDomain >\\< WindowsUserId\>. このコマンドでは、このチュートリアルで使用している外部ユーザー (PTUserID) のパスワードの入力が求められます。  
  
    > [!NOTE]
    >  Payment Tracker シミュレーターは、外部ユーザー資格情報の検証を行いません。 PTUserID のパスワードとして任意の値を入力できます。  
  
    -   `ssomanage -setcredentials < WindowsDomain >\< WindowsUserId > WoodgroveBank.PaymentTracker`  
  
##  <a name="step19"></a>サービス指向ソリューションの BAM 定義ファイルを配置します。  
  
#### <a name="to-deploy-the-bam-definition-file-for-the-service-oriented-solution"></a>サービス指向ソリューションの BAM 定義ファイルを展開するには  
  
1.  コマンド プロンプトを開いて、次のコマンドを入力し、&lt;localizedText&gt;Enter&lt;/localizedText&gt; キーを押して、BAM ユーティリティを参照するためのパスを設定します。  
  
    -   SET PATH=%PATH%;[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]Tracking"  
  
2.  コマンド プロンプトで、ディレクトリを %BTSSolutionsPath%\SO\BTSSoln\BAM に変更し、次のコマンドを入力して &lt;localizedText&gt;Enter&lt;/localizedText&gt; キーを押します。  
  
    -   `bm deploy-all -DefinitionFile:ServiceLevelTracking.xml`  
  
##  <a name="step21"></a>配置サービス指向ソリューション  
  
#### <a name="to-edit-the-binding-files-for-the-service-oriented-solution"></a>サービス指向ソリューションのバインド ファイルを編集するには  
  
1.  コマンド プロンプトで、ディレクトリを %BTSSolutionsPath%\SO\BTSSoln\Scripts フォルダーに変更します。次に、メモ帳を使用して Deployallbinding.xml を開き、次のように編集します。  
  
    -   SET MGMT_DB_SERVER のサーバー名および MBMT_DB を、BizTalk Server が使用するサーバー名およびデータベースに変更します。  
  
    -   SOLNDIR 変数の値を "%BTSSolutionsPath%\SO\BTSSoln" に変更します。  
  
2.  コマンド プロンプトで、ディレクトリを %BTSSolutionsPath%\SO\BTSSoln\Bindings フォルダーに変更します。  
  
3.  アダプター バージョンの場合は、メモ帳を使用して AdapterSOAOrchBindings.xml を開き、次のように編集します。  
  
    -   __MQ_SERVER_NAME のすべての出現を置換\_\_ MQSeries サーバーの名前。  
  
    -   __MQ_QMANAGER_NAME のすべての出現を置換\_\_ MQSeries キュー マネージャ名。  
  
    -   __PT_WS_SERVER_NAME のすべての出現を置換\_\_文字列で"\<アドレス > https://\__PT_WS_SERVER_NAME\_\_"は、サーバー名、保留中のトランザクションWeb サービスを展開します。 サーバー名が一致する必要があります、**共通名**の手順で、"Web サーバーの SSL の構成"です。 localhost を使用しないでください。  
  
    > [!NOTE]
    >  バインド ファイル AdapterSOAOrchBindings.xml はスタブ Web サービスを、  
    >   
    >  1.  Credit Limit バックエンド SAP システム  
    > 2.  Payment Tracking バックエンド システムとの統合を行う MQSeries アダプター  
    > 3.  HIS TI .NET コンポーネントを呼び出してメインフレーム バックエンド システムとの統合を行う Pending Transactions Web サービスとして使用します。  
    >   
    >  メインフレームを使用しない場合は、スタブ Web サービスを使用して Pending Transactions システム用のデータを生成する必要があります。  
  
4.  インライン バージョンの場合は、メモ帳を使用して InlineSOAOrchBindings.xml を開き、次のように編集します。  
  
    -   __MQ_SERVER_NAME のすべての出現を置換\_\_ MQSeries サーバーの名前。  
  
    -   __MQ_QMANAGER_NAME のすべての出現を置換\_\_ MQSeries キュー マネージャ名。  
  
#### <a name="to-deploy-the-service-oriented-solution"></a>サービス指向ソリューションを展開するには  
  
-   コマンド プロンプトで、ディレクトリを %BTSSolutionsPath%\SO\BTSSoln\Scripts フォルダーに変更し、次のコマンドを入力して &lt;localizedText&gt;Enter&lt;/localizedText&gt; キーを押します。  
  
    -   `Deployallbinding.cmd`  
  
    > [!NOTE]
    >  Deployallbinding.cmd を実行すると、BTSScn.SO.CustomerService という名前の BizTalk アプリケーションが作成され、アダプター バージョンおよびインライン バージョン用のバインド ファイルがインポートされます。  
  
##  <a name="step23"></a>メインフレームが利用できない場合は、スタブ Pending Transactions Web サービスを構成します。  
  
#### <a name="to-configure-the-stub-pending-transactions-web-service-for-using-the-adapter-version-without-a-mainframe"></a>スタブ Pending Transactions Web サービスを構成するには (メインフレームを使用せず、アダプター バージョンを使用する場合)  
  
1.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**を右クリックし、**既定の Web サイト**、 をポイント**新規**とをクリックして**仮想ディレクトリ**を実行する**仮想ディレクトリの作成ウィザード**です。  
  
     使用して、**仮想ディレクトリの作成ウィザード**、スタブ Pending Transactions Web サービス アダプター バージョン用の次の仮想ディレクトリを作成します。  
  
     Alias = Microsoft.Samples.BizTalk.WoodgroveBank.StubPendingTransactions  
  
     パス = \< *BizTalk インストール ディレクトリ*> \SDK\Scenarios\SO\BTSSoln\StubWebServices\PendingTrans  
  
     Access Permissions = Read, Run scripts  
  
2.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**、展開、**既定の Web サイト**を右クリックしてMicrosoft.Samples.BizTalk.WoodgroveBank.StubPendingTransactions をクリックして**プロパティ**、し、次のようを使用して設定を変更、**プロパティ** ダイアログ ボックス。  
  
    1.  **仮想ディレクトリ** タブで、設定、**アプリケーション プール**に\< *YourAppPool*> 向けの IIS の仮想ディレクトリを作成するには」の手順で作成します。ソリューション"です。  
  
    2.  **ディレクトリ セキュリティ**] タブで、をクリックして**編集**で、**認証とアクセス制御**ボックスで、グループ化し、[ **への匿名アクセスを有効にします。**. をクリックして**OK**を終了します。  
  
3.  **BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**、[btsscn.so.customerservice] を展開し、**送信ポート**を右クリックして**[pendingtransactionsolicitresponseport]**、クリックして**プロパティ**です。  
  
    1.  **全般** ページで、をクリックして**構成**を表示する、**トランスポートのプロパティ** ダイアログ ボックスし、変更、 **Web サービス URL**にスタブ Pending Transaction Web サービスをたとえば。  
  
         `http://localhost/Microsoft.Samples.BizTalk.WoodgroveBank.StubPendingTransactions/StubPendTransWS.asmx`  
  
    2.  すべてのダイアログ ボックスを閉じます。  
  
#### <a name="to-configure-the-stub-pending-transactions-web-service-for-using-the-inline-version-without-a-mainframe"></a>スタブ Pending Transactions Web サービスを構成するには (メインフレームを使用せず、インライン バージョンを使用する場合)  
  
1.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**を右クリックし、**既定の Web サイト**、 をポイント**新規**とをクリックして**仮想ディレクトリ**を実行する**仮想ディレクトリの作成ウィザード**です。  
  
     使用して、**仮想ディレクトリの作成ウィザード**、スタブ Pending Transactions Web サービス アダプター バージョン用の次の仮想ディレクトリを作成します。  
  
     Alias = Microsoft.Samples.BizTalk.WoodgroveBank.StubPendingTransactions  
  
     パス = \< *BizTalk インストール ディレクトリ*> \SDK\Scenarios\SO\BTSSoln\StubWebServices\PendingTrans  
  
     Access Permissions = Read, Run scripts  
  
2.  **インターネット インフォメーション サービス (IIS) マネージャー**、展開**Websites**、展開、**既定の Web サイト**を右クリックしてMicrosoft.Samples.BizTalk.WoodgroveBank.StubPendingTransactions をクリックして**プロパティ**、し、次のように設定を変更します。  
  
    1.  **仮想ディレクトリ** タブで、設定、**アプリケーション プール**に\< *YourAppPool*> 向けの IIS の仮想ディレクトリを作成するには」の手順で作成します。ソリューション"です。  
  
    2.  **ディレクトリ セキュリティ**] タブで、をクリックして**編集**で、**認証とアクセス制御**ボックスで、グループ化し、[ **への匿名アクセスを有効にします。**. をクリックして**OK**を終了します。  
  
3.  コマンド プロンプトを開いて、ディレクトリを %BTSSolutionsPath%\SO\BTSSoln\Scripts フォルダーに変更します。  
  
4.  コマンド プロンプトで、メモ帳を使用して SetConfigValuesInSSO.cmd ファイルを開きの値を設定、 **PendingTransactionsInlineURL**スタブ Pending Transaction Web サービスの URL にします。  
  
    -   `http://localhost/Microsoft.Samples.BizTalk.WoodgroveBank.StubPendingTransactions/StubPendTransWS.asmx`  
  
5.  コマンド プロンプトで「`SetConfigValuesInSSO.cmd`」と入力し、Enter キーを押します。  
  
##  <a name="step25"></a>開始、サービス指向ソリューション  
  
#### <a name="to-start-the-service-oriented-solution"></a>サービス指向ソリューションを開始するには  
  
1.  コマンド プロンプトを開き、ディレクトリを %BTSSolutionsPath%\SO\BTSSoln\Scripts フォルダーに変更して、次のコマンドを入力し Enter キーを押します。これにより、インライン バージョンおよびアダプター バージョン用のすべてのオーケストレーションが開始されます。  
  
    -   `startAll.vbs`  
  
2.  サービス指向ソリューションを実行します。 ソリューションの実行の詳細については、次を参照してください。[サービス指向ソリューションの実行方法](../core/how-to-run-the-service-oriented-solution.md)です。  
  
## <a name="next-steps"></a>次の手順  
 サービス指向ソリューションのインライン バージョンおよびアダプター バージョンをテストする[サービス指向ソリューションの実行方法](../core/how-to-run-the-service-oriented-solution.md)です。  
  
## <a name="see-also"></a>参照  
 [サービス指向ソリューションをインストールする前に](../core/before-installing-the-service-oriented-solution.md)   
 [指向ソリューションのスタブ バージョンのサービスをインストールする方法](../core/how-to-install-the-stub-version-of-the-service-oriented-solution.md)   
 [開発者のコンピュータ設定、サービス指向ソリューション](../core/developer-machine-setup-for-the-service-oriented-solution.md)