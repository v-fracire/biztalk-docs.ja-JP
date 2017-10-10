---
title: "ExpenseReportSubmission |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- orchestrations, examples
- examples, orchestrations
ms.assetid: d0bacab3-7092-44b8-a1c6-6f574a2db8bd
caps.latest.revision: "29"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 993d1874a95da2501636f941f1436fec894e87f6
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="expensereportsubmission"></a>ExpenseReportSubmission
ExpenseReportSubmission サンプルは、Microsoft Excel などのリッチ クライアントのドキュメントを [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オーケストレーションに送信する方法を示すものです。  
  
 リッチ クライアントを使用すると、データ検証、準備計算など多くのアクションをクライアント上で実行できます。 これによりバックエンド サーバーとの対話処理を最小限に抑えることができるので、低帯域幅接続しか使用できない場合に便利です。  
  
## <a name="prerequisites"></a>前提条件  
 開発環境が構成済みで、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Web サービスが利用可能になっていることを確認する必要があります。 詳細については、次を参照してください。 [Web サービスを有効にすると](../core/enabling-web-services.md)です。  
  
## <a name="what-this-sample-does"></a>このサンプルの処理  
 このサンプルでは、次の一連の手順で、経費報告書を Excel から [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] に直接送信します。  
  
1.  ユーザーが、Excel ワークシートで指定のサンプル手順を手動で実行します。  
  
2.  ワークシートのマクロ コードにより、ワークシートのデータが XML (Extensible Markup Language) 形式に変換され、XML メッセージが HTTP 接続経由で [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] に送信されます。  
  
3.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] を実行しているコンピューターが、XML 形式の経費報告書のメッセージを取得し、指定のスキーマを使用してメッセージの形式を検証した後、メッセージを別のフォルダーに格納します。  
  
4.  このサンプルでは示していませんが、実際はエンタープライズ リソース プランニング (ERP) システムなどの他のアプリケーションがこのワークシート ファイルを取得し、さらに処理を行います。  
  
## <a name="where-to-find-this-sample"></a>このサンプルの場所  
 \<*パスのサンプル*> \AdaptersUsage\ExpenseReportSubmission\  
  
 次の表は、このサンプルのファイルとその目的を示しています。  
  
|ファイル|Description|  
|---------------|-----------------|  
|Cleanup.bat|必要に応じて、アセンブリの展開の解除とグローバル アセンブリ キャッシュ (GAC) からのアセンブリの削除、送信および受信ポートの削除、Microsoft インターネット インフォメーション サービス (IIS) の仮想ディレクトリの削除などを行います。|  
|ExpenseReport.15.3.xls|経費報告書のレイアウトの Excel ワークシートです。マクロとその呼び出し用ボタンが用意されています。|  
|MessageExample.xml|XML 形式の経費報告書のサンプルです。|  
|Setup.bat|このサンプルを作成および初期化します。|  
|\BTSExpenseDemo フォルダーには、次のファイルが含まれています。<br /><br /> AssemblyInfo.cs、<br /><br /> BTSExpenseDemo.btproj、<br /><br /> BTSExpenseDemo.sln|このサンプルのプロジェクト ファイル、ソリューション ファイル、その他の関連ファイルを提供します。|  
|\BTSExpenseDemo フォルダーには、次のファイルが含まれています。<br /><br /> BTSExpenseDemoBinding.xml|ポートのバインドなどの自動化されたセットアップに使用されます。|  
|\BTSExpenseDemo フォルダーには、次のファイルが含まれています。<br /><br /> BTSExpenseOrchestration.odx|このサンプルの [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オーケストレーションを提供します。|  
|\BTSExpenseDemo フォルダーには、次のファイルが含まれています。<br /><br /> SchemaExpenseReport.xsd|XML 形式の経費報告書のスキーマを提供します。|  
  
### <a name="to-build-and-initialize-this-sample"></a>このサンプルを作成および初期化するには  
  
1.  コマンド ウィンドウで、次のフォルダーに移動します。  
  
     \<*パスのサンプル*> \AdaptersUsage\ExpenseReportSubmission  
  
2.  次の操作を実行する Setup.bat ファイルを実行します。  
  
    -   このサンプル用に Microsoft [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] プロジェクトをコンパイルし、生成されたアセンブリを展開します。  
  
    -   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] の送信ポートおよび受信ポートを作成し、バインドします。  
  
        > [!NOTE]
        >  このサンプルは、ポートを作成してバインドする際に、以下の警告を表示します。  
        >   
        >  `Warning: Receive handler not specified for receive location "BTSExpenseReceiveLocation"; updating with first receive handler with matching transport type.`  
        >   
        >  `Warning: Host not specified for orchestration "Microsoft.Samples.BizTalk.BTSExpenseDemo.BTSOrchestration"; updating with first available host`」をご覧ください。  
        >   
        >  これらの警告は、無視してもかまいません  (インストールでの名前付け方法はユーザーによって異なる可能性があるため、ホスト名と受信ハンドラーはバインド ファイルから除外されています。)  
  
    -   受信場所を有効にし、送信ポートを開始します。  
  
    -   IIS を構成します。  
  
    -   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オーケストレーションをバインドして、開始します。  
  
    -   HTTP アドレスを、Excel ワークシートで想定されている場所に設定します。  
  
    > [!NOTE]
    >  BizTalk ISAPI フィルターの詳細については、次を参照してください。 [HTTP の受信場所の IIS を構成する方法](../core/how-to-configure-iis-for-an-http-receive-location.md)です。  
  
    > [!NOTE]
    >  このサンプルを実行する前に、ビルドと初期化のプロセス中に [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] でエラーが報告されていないことを確認する必要があります。  
  
    > [!NOTE]
    >  Setup.bat ファイルを実行せずに、このサンプルのプロジェクトを開いてビルドする場合は、最初に .NET Framework の厳密名ユーティリティ (sn.exe) を使用して、厳密な名前のキー ペアを作成する必要があります。 結果として得られるアセンブリに署名するのにには、このキー ペアを使用します。  
  
    > [!NOTE]
    >  Setup.bat によって行われた変更を元に戻すには、Cleanup.bat を実行します。 Setup.bat を 2 回目に実行する場合は、その前に Cleanup.bat を実行してください。  
  
3.  Setup.bat ファイルを実行すると、このサンプルの仮想ディレクトリが構成され、既定の Web サイトに関連付けられた IIS アプリケーション プールで実行されるよう設定されます。  このサンプルでのユーザーのコンテキストで実行する仮想ディレクトリを構成する、 **BizTalk Isolated Host Users**と**IIS_WPG**ユーザー グループを新しいを実行する仮想ディレクトリを構成する必要がありますIIS アプリケーション プール。  仮想ディレクトリを新しい IIS アプリケーション プールで実行するよう構成するには、次の手順を実行します。  
  
    > [!NOTE]
    >  別の SDK サンプル用に新しいアプリケーション プールを作成済みの場合は、次の箇条書きの最後の項目に進むことができます。  
  
    1.  をクリックして**開始**、 をポイント**プログラム**、 をポイント**管理ツール**、クリックして**インターネット インフォメーション サービス (IIS) マネージャー**.  
  
    2.  **インターネット インフォメーション サービス (IIS) マネージャー**に移動し、**アプリケーション プール**フォルダーです。  
  
    3.  右クリックし、**アプリケーション プール**フォルダーとクリック**新規**、**アプリケーション プールしています.**  
  
    4.  名前を入力、**アプリケーション プール ID:** BizTalkSDKSamples などのことを確認、**新しいアプリケーション プールに既定の設定を使用して**オプションが選択されているし、をクリックして**OK**に新しいアプリケーション プールを作成します。  
  
    5.  新しいアプリケーション プールを右クリックし、をクリックして**プロパティ**です。  
  
    6.  をクリックして、 **Identity**プロパティ ダイアログ ボックスのタブ ボックスし、このアプリケーション プールのメンバーであるユーザーを実行する id を変更する、 **BizTalk Isolated Host Users**ユーザー グループ。  このユーザーは、ローカルのメンバーでもある必要があります**IIS_WPG**ユーザー グループ。  
  
    7.  この SDK サンプルの仮想ディレクトリを、新しいアプリケーション プールで実行するよう構成します。 **アプリケーション プール:**設定は、**仮想ディレクトリ**仮想ディレクトリのプロパティ ダイアログ ボックスのタブです。 このサンプルは、用に作成された仮想ディレクトリ**ExpenseReportSubmission**です。  
  
4.  IIS の Web サービス拡張を HTTPReceive.dll 用に追加します。  
  
    1.  **インターネット インフォメーション サービス (IIS) マネージャー**に移動し、 **Web サービス拡張**フォルダーです。  
  
    2.  右クリックし、 **Web サービス拡張**フォルダーと選択**新しい Web サービス拡張を追加**を表示する、**新しい Web サービス拡張** ダイアログ ボックス。  
  
    3.  入力**ExpenseReportSubmission**の**拡張機能の名前。**  
  
    4.  をクリックして**追加**を表示する、 **Add file**  ダイアログ ボックス。  
  
    5.  をクリックして**参照**を表示する、**開く** ダイアログ ボックスに移動して *\<BizTalk Server のインストール フォルダー >*\HttpReceive\BTSHTTPReceive.dll とをクリックして**開く**をクリックし、 **ok**です。  
  
    6.  ためのオプションを有効にする**拡張機能の状態を許可 に設定** をクリック**OK**です。  
  
## <a name="running-this-sample"></a>このサンプルの実行  
 次の手順を使用して、ExpenseReportSubmission サンプルを実行します。  
  
> [!NOTE]
>  Microsoft Excel の強化されたセキュリティ機能を使用している場合、ワークシート内のマクロが無効になることがあります。 信頼できるソースからの未署名のマクロを実行する方法については、Excel で提供されている指示に従ってください。  
  
#### <a name="to-run-this-sample"></a>このサンプルを実行するには  
  
1.  このサンプルに含まれている Excel ファイルの ExpenseReport.15.3.xls を開きます。  
  
2.  必要に応じて、ワークシート内のサンプル データを変更します。ただし、書式は変更しないでください。  
  
3.  クリックして、スプレッドシートで**開始**ローカル計算を実行します。  
  
     ボタンのテキストがから変更**開始**に**送信**です。  
  
4.  クリックして、スプレッドシートで**送信**です。  
  
5.  送信されたメッセージのテキストと、表の上部に黄色の背景で表示される結果 (セル C7)、および表の下方右側に表示される実際のリターン コードと説明テキスト (セル G23) を確認します。  
  
     送信に失敗した場合は、もう 1 度実行してください。 「コメント」セクションのトラブルシューティングの表も参照してください。  
  
## <a name="comments"></a>コメント  
 このサンプルのシナリオが発生するのは、たとえば、フィールド営業員が使用するコンピューターに古いバージョンの Microsoft Windows が搭載されており、そのバージョンでは .NET Framework がサポートされておらず、より新しいバージョンの Windows にアップグレードすることも考えられていないといったケースです。  
  
 このサンプルでは、次のような基本機能を実行します。  
  
-   リッチ クライアント (.NET ベース以外) からの送信  
  
-   Microsoft Office 統合  
  
-   HTTP 受信接続  
  
-   簡単なオーケストレーション  
  
-   ファイル アダプター  
  
 考えられる送信エラーとその解決方法を次の表に示します。  
  
|HTTP エラー コード|対処方法|  
|---------------------|---------------------|  
|401 権限がありません|仮想ディレクトリでの匿名アクセスを有効にします。|  
|503 サービス利用不可、その他 400 ～ 500 番台の大半の HTTP コード|ホストが実行されていることと、サービスが展開され、正しいポートにバインドされて開始されていることを確認します。|  
  
## <a name="see-also"></a>参照  
 [アダプタ サンプル – 使用状況](../core/adapter-samples-usage.md)