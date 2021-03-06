---
title: HTTPRequestResponse |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- HTTP adapters, examples
- examples, HTTP adapters
ms.assetid: 81c66f61-d86c-49cf-8d24-21c67c68bc5a
caps.latest.revision: 35
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ecea06f7637d7fee46593d412f1570d26b7eaeb1
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37019527"
---
# <a name="httprequestresponse"></a>HTTPRequestResponse
HTTPRequestResponse サンプルは、Microsoft [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Internet Server API (ISAPI) フィルターを使用して ASP.NET アプリケーションと [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オーケストレーションの通信を行う方法を示します。  

## <a name="what-this-sample-does"></a>このサンプルの処理  
 このサンプルでは、ASP.NET アプリケーションは、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ISAPI フィルターに要求を送信します。 オーケストレーションは、このメッセージを受信し、同期応答を使用して ASP.NET アプリケーションにメッセージを返します。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ISAPI フィルターを使用することにより、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オーケストレーションと ASP.NET アプリケーションの統合を実現できます。  

 このサンプルでは、以下の手順を使用して、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] と ASP.NET アプリケーションの間で、注文書 (PO) および PO の受信確認メッセージを交換します。  

1. ASP.NET アプリケーションが HTTP 要求を使用して、XML PO メッセージを [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] に送信します。  

2. [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は XML PO メッセージを受け取り、XML PO 受信確認メッセージを構築します。その後、そのメッセージを HTTP 応答で ASP.NET アプリケーションに返します。  

   ASP.NET アプリケーションは XML PO 受信確認応答を受け取り、応答から抽出されたステータス情報で Web フォームを更新します。  

## <a name="where-to-find-this-sample"></a>このサンプルの場所  
 *\<パスのサンプル\>* \AdaptersUsage\HTTPRequestResponse\  

 次の表は、このサンプルのファイルとその目的を示しています。  


|                                                                                                     ファイル                                                                                                      |                                                                                             説明                                                                                             |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                                                   Cleanup.bat                                                                                                    |  必要に応じて、アセンブリの展開の解除とグローバル アセンブリ キャッシュ (GAC) からのアセンブリの削除、送信および受信ポートの削除、Microsoft インターネット インフォメーション サービス (IIS) の仮想ディレクトリの削除などを行います。   |
|                                                                               HTTPRequestResponse.btproj、HTTPRequestResponse.sln                                                                                |                            HTTP 要求の受信、PO メッセージの処理、および応答の発行を行う BizTalk プロジェクトのプロジェクト ファイルおよびソース ファイルを提供します。                             |
|                                                                                          HTTPRequestResponseBinding.xml                                                                                          |                                                                           ポートのバインドなど、自動化されたセットアップを提供します。                                                                            |
|                                                                                             POAck.xsd、POSchema.xsd                                                                                              |                                                            PO 受信確認および PO .xml ファイルのスキーマをそれぞれ提供します。                                                             |
|                                                                                            POReceiveOrchestration.odx                                                                                            |         PO の受信、PO の処理、および PO 受信確認を行う [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オーケストレーションを提供します。          |
|                                                                                                    Setup.bat                                                                                                     |                                                                                 このサンプルを作成および初期化します。                                                                                 |
| \RequestResponse フォルダー内<br /><br /> AssemblyInfo.cs、default.aspx、default.aspx.cs、Global.asax、Global.asax.cs、RequestResponse.csproj、RequestResponse.csproj.webinfo、RequestResponse.sln、Web.config | このサンプルのドライバーとして機能する ASP.NET アプリケーションを構成するファイル (プロジェクト ファイルとソリューション ファイル、ASPX ファイル、Microsoft Visual C# .NET ソース ファイルなど) を含みます。 |

## <a name="building-and-initializing-this-sample"></a>このサンプルのビルドと初期化  
 次の手順を使用して、HTTPRequestResponse サンプルをビルドおよび初期化します。  

#### <a name="to-build-and-initialize-this-sample"></a>このサンプルを作成および初期化するには  

1. コマンド ウィンドウで、次のフォルダーに移動します。  

    \<*パスのサンプル*\>\AdaptersUsage\HTTPRequestResponse  

2. ファイルは、次の操作を実行します。 Setup.bat を実行します。  

   - このサンプルを実行する ASP.NET アプリケーションをコンパイルし構成します。  

     > [!NOTE]
     >  IIS マネージャーでアプリケーション プールを作成、設定、 **DefaultAppPool** .NET Framework バージョンを **.Net Framework v4.0**します。  

   - このサンプルで使用する [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オーケストレーションをコンパイルし、展開します。  

   - コンパイルし、Microsoft の展開[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]このサンプルのプロジェクト。  

   - 必要な [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ポートを作成しバインドします。  

   - [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オーケストレーションを開始します。  

     > [!IMPORTANT]
     >  Web アプリケーションを実装するサンプル コード (Default.aspx.cs) を変更して環境を反映する必要があります。  
     >   
     >  http://\<*サーバー名*\>/\<*仮想 dir*\>>/btshttpreceive.dll 場所`<servername>`Web の名前を指定しますサーバーに、投稿して`<`*仮想ディレクトリ*`>`はこのファイルが存在する仮想ディレクトリです。  

     > [!NOTE]
     >  このサンプルを実行する前に、BizTalk がビルド プロセス中および初期化プロセス中にエラーを報告していないことを確認してください。  

     > [!NOTE]
     >  開き、Setup.bat ファイルを実行することがなくこのサンプルでは、プロジェクトをビルドする場合は、まず、.NET Framework の厳密名ユーティリティ (sn.exe) を使用して厳密な名前キーのペアを作成する必要があります。 このキー ペアは、生成されたアセンブリの署名に使用します。 プロジェクトをビルドする前に、default.aspx.resx および Global.asax.resx への参照を RequestResponse.csproj ファイルから手動で削除する必要もあります。  

     > [!NOTE]
     >  Setup.bat によって行われた変更を元に戻すには、Cleanup.bat を実行します。 Setup.bat を 2 回目に実行する場合は、その前に Cleanup.bat を実行してください。  

     > [!NOTE]
     >  構成する必要があり、受信アダプターを有効に HTTP を使用する IIS。 詳細については、次を参照してください。 [IIS の HTTP 受信場所を構成する方法](../core/how-to-configure-iis-for-an-http-receive-location.md)します。  

3. Setup.bat ファイルを実行すると、このサンプルの仮想ディレクトリが構成され、既定の Web サイトに関連付けられた IIS アプリケーション プールで実行されるよう設定されます。  内のユーザーのコンテキストで実行するには、このサンプル用の仮想ディレクトリを構成する、 **BizTalk 分離ホスト ユーザー**と**IIS_IURS**ユーザー グループの場合は、新しいで実行する仮想ディレクトリを構成する必要がありますIIS アプリケーション プール。 仮想ディレクトリを新しい IIS アプリケーション プールで実行するよう構成するには、次の手順を実行します。  

   > [!NOTE]
   >  別の SDK サンプル用に新しいアプリケーション プールを作成済みの場合は、次の最後の手順に進むことができます。  

   1.  クリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**管理ツール**、順にクリックします**インターネット インフォメーション サービス (IIS) マネージャー**.  

   2.  **インターネット インフォメーション サービス (IIS) マネージャー**に移動し、**アプリケーション プール**フォルダー。  

   3.  右クリックし、**アプリケーション プール**フォルダーとクリック**新規**、**アプリケーション プールしています.**  

   4.  名前を入力、**アプリケーション プール ID:** 、BizTalkSDKSamples などことを確認します、**新しいアプリケーション プールの既定の設定を使用して**オプションが選択されているし、をクリックして**OK**に新しいアプリケーション プールを作成します。  

   5.  新しいアプリケーション プールを右クリックし、をクリックし、**プロパティ**します。  

   6.  をクリックして、 **Identity**  タブのプロパティ ダイアログ ボックスし、このアプリケーション プールのメンバーであるユーザーに実行する id を変更、 **BizTalk 分離ホスト ユーザー**ユーザー グループ。  このユーザーは、ローカルのメンバーでもある必要があります**IIS_IURS**ユーザー グループ。  

   7.  この SDK サンプルの仮想ディレクトリを、新しいアプリケーション プールで実行するよう構成します。 **アプリケーション プール**設定は、**仮想ディレクトリ**仮想ディレクトリのプロパティ ダイアログ ボックスのタブ。 このサンプルで作成される仮想ディレクトリは、HttpRequestResponseSample という名前になります。  

## <a name="running-this-sample"></a>このサンプルの実行  
 次の手順を使用して、HTTPRequestResponse サンプルを実行します。  

#### <a name="to-run-this-sample"></a>このサンプルを実行するには  

1.  Internet Explorer に移動します。 http://localhost/RequestResponse/ します。  

2.  Web フォームで、必要なフィールドに入力し、クリックして**Place Order**して注文を送信します。  

3.  応答を受信した後、Web フォームが更新される際に注文のステータスを確認します。  

## <a name="comments"></a>コメント  
 **BTSHTTPReceiveISAPI**このサンプルで使用される拡張機能が 1 台のコンピューターの既定のインストールで動作するよう構成します。 このサンプルに追加の構成を拡張するを参照してください。 [HTTP アダプター](../core/http-adapter.md)します。  

 このサンプルは、Web フォームまたは一般的な HTTP を介して [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] にデータを送信するために必要なアプリケーションに拡張できます。 このサンプルの ASP.NET アプリケーションの部分を拡張すると、さらに多くの情報をクエリして、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] にデータを送信する前にその他の処理を実行できます。  

## <a name="see-also"></a>参照  
 [HTTP アダプター サンプル](../core/http-adapter-samples.md)