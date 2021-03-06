---
title: SendMSMQMessage |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSMQ adapters, examples
- examples, MSMQ adapters
ms.assetid: 398bc396-0c66-4d55-886a-0d9bdab6476f
caps.latest.revision: 26
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 27c6a0f6b9e35b68fccd38d62fe7e1ae86f4f6ad
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37024496"
---
# <a name="sendmsmqmessage"></a>SendMSMQMessage
SendMSMQMessage サンプルは、.NET ベースのアプリケーションから MSMQ ポートにメッセージを送信する方法を示します。 Microsoft を構成する方法についても用意されています。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] MSMQ 受信場所を使用します。  

 メッセージ キューの多くの操作が非同期であることに注意が必要です。 多くは、MSMQ API 呼び出し (たとえば、 **System.Messaging.MessageQueue.Send**)、要求された操作が完全に完了する前に、呼び出し元に戻ります。 MSMQ には、操作完了後にアプリケーションにフィードバックを配信するメカニズムが用意されています。 このメカニズムでは、"管理キュー" を使用します。 MSMQ は管理キューにメッセージ形式でフィードバックを返します。 MSMQ がフィードバックを返す管理キューは、元の MSMQ API 呼び出しが行われたときに指定されます。 そのため、たとえばを使用してメッセージを送信するときに、 **System.Messaging.MessageQueue.Send** API、アプリケーションを指定できます管理キューの名前を使用して、 **PROPID_M_ADMIN_QUEUE**メッセージ プロパティ呼び出しで渡されるメッセージの**System.Messaging.MessageQueue.Send**します。 アプリケーションの成功を示すリターン コードが取得場合でも、 **System.Messaging.MessageQueue.Send**呼び出し、メッセージの送信操作後で失敗した場合、MSMQ メッセージを書き込みますそれに対応する指定の管理キューにします。 送信エラーによりメッセージが消失と診断がキャプチャされません、アプリケーションが管理キューを指定しない場合、実際には、メッセージは証拠も残らない表示されなくなります。 エラーの可能性がある、この例では、非トランザクションを行うための MSMQ の場合は、トランザクション キューに送信を数多くあります。  

 このサンプルのコンテキストでは、コードが呼び出しでトランザクションの種類を指定することが重要**System.Messaging.MessageQueue.Send**メッセージをキューに指定されたトランザクションのサポートと一貫性があります。送信されます。 この処理が行われない場合や、(このサンプルのように) 管理キューが指定されていない場合、MSMQ は何の通知もなく送信メッセージを破棄します (つまり、アプリケーションにエラー コードが返されたり、イベント ログに診断が書き込まれたりすることはありません)。  

## <a name="where-to-find-this-sample"></a>このサンプルの場所  
 \<パスのサンプル\>\AdaptersUsage\SendMSMQMessage\  

 次の表は、このサンプルのファイルとその目的を示しています。  


|                                 [ファイル]                                 |                                                                      説明                                                                       |
|-----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| App.ico、AssemblyInfo.cs、SendMSMQMessage.csproj、SendMSMQMessage.sln |                           プロジェクト、ソリューション、およびこのサンプルの簡単なグラフィカル アプリケーションの他の関連ファイルを提供します。                           |
|                         Form1.cs、Form1.resx                          | このサンプル用の簡単なグラフィカル アプリケーションの Microsoft [!INCLUDE[btsVCSharp](../includes/btsvcsharp-md.md)].NET ソース ファイルおよびフォーム ファイルを提供します。 |

## <a name="how-to-use-this-sample"></a>このサンプルの使用方法  
 このサンプルに含まれている簡単なグラフィカル アプリケーションのコードは、Microsoft Office などの .NET 対応のアプリケーションや ASP.NET ページなどから [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 内の MSMQ 受信場所へメッセージを送信する方法の例として使用できます。  

## <a name="building-and-initializing-the-sample"></a>サンプルのビルドおよび初期化  

#### <a name="to-build-the-sample-executable"></a>実行可能サンプル ファイルをビルドするには  

1. [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] を使用して、ソリューション ファイル SendMSMQMessage.sln を開きます。  

2. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  

## <a name="configuring-biztalk-server-and-creating-the-msmq-queue"></a>BizTalk Server の構成と MSMQ キューの作成  
 次の手順を使用して [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] を構成し、サンプルを実行するための MSMQ キューを作成します。  

#### <a name="to-create-the-msmq-queue-in-windows-server-2008-r2-or-windows-server-2008-sp2"></a>Windows Server 2008 R2 または Windows Server 2008 SP2 で MSMQ キューを作成するには  

1.  クリックして**開始**を右クリックして**コンピューター**、順にクリックします**管理**します。  

2.  展開、**機能**ノード。  場合**メッセージ キュー**は右クリックしてインストールされていない**機能**選択**機能の追加**。  確認**メッセージ キュー**、 をクリックして**次**、順にクリックします**インストール**そのシステムで MSMQ をインストールします。  

3.  展開、**メッセージ キュー**ノード。  

4.  右クリックし、**専用キュー**ノード、をクリックして**新規**、順にクリックします**プライベート キュー**します。  

5.  **キュー名**、入力`test`します。 いることを確認、**トランザクション** チェック ボックスをオンします。  

6.  **[OK]** をクリックします。  

#### <a name="to-create-the-msmq-queue-in-windows-7-or-windows-vista-sp2"></a>Windows 7 または Windows Vista SP2 で MSMQ キューを作成するには  

1.  クリックして**開始**を右クリックして**コンピューター**、順にクリックします**管理**します。  

2.  展開**サービスとアプリケーション**の順に展開し、**メッセージ キュー**ノード。  

    > [!NOTE]
    >  場合**メッセージ キュー** 、コンピューターにインストールされていないに移動して**コントロール パネル > プログラム > プログラムと機能**、し、**オンまたはオフにする Windows 機能**します。 すべての機能を確認**Microsoft メッセージ キュー (MSMQ) Server**、順にクリックします**OK**。  

3.  右クリックし、**専用キュー**ノード、をクリックして**新規**、順にクリックします**プライベート キュー**します。  

4.  **キュー名**、入力**テスト**します。 いることを確認、**トランザクション** チェック ボックスをオンします。  

5.  **[OK]** をクリックします。  

#### <a name="to-configure-biztalk-server"></a>BizTalk Server を構成するには  

1. メッセージを受信するフォルダーを選択します。 次の手順は、C:\Demo\Report を選択したが、別のフォルダーに必要な手順を調整することを想定しています。  

2. 開く、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソール。  

3. という名前の新しいアプリケーションを作成する**MSMQSample**します。  

4. 右クリック**受信ポート**、 をクリックして**新規**、 をクリックし、**一方向の受信ポート**します。  

5. **受信ポートのプロパティ** ダイアログ ボックスで、**名前**ボックスの入力**MyReceivePort**、順にクリックします**ok**します。  

6. 右クリック**受信場所**、 をクリックして**新規**、 をクリックし、**一方向の受信場所**します。 **受信ポートの選択**ダイアログ ボックスで、選択した受信ポートが作成され、クリックして**OK**します。  

7. **受信場所のプロパティ** ダイアログ ボックスで、**名前**ボックスに、受信ポートの名前を入力します。 **MSMQReceiveLocation**します。  

8. **受信場所のプロパティ** ダイアログ ボックスで、トランスポートの種類を選択します**MSMQ**します。  

9. クリックして**構成**を開く、 **MSMQ トランスポートのプロパティ** ダイアログ ボックス。 設定**キュー**に`localhost\private$\test`に設定して、**トランザクション**に`True`、順にクリックします**OK**。  

10. アプリケーションを展開し、選択**送信ポート**を選択します**新規**、**静的な一方向送信ポート**します。  

11. **送信ポートのプロパティ** ダイアログ ボックスで、**名前**ボックスで、送信ポートの名前を入力します。 **MySendPort**します。  

12. 設定、**トランスポートの種類**プロパティを**ファイル**します。  

13. クリックして**構成**を開く、 **File トランスポートのプロパティ** ダイアログ ボックス。  

14. **FILE トランスポートのプロパティ**ダイアログ ボックスで、セット、**先フォルダー**プロパティを**C:\Demo\Report**、他のプロパティの既定の設定を保持し、クリックして**OK**します。  

15. 選択**フィルター**、設定して新しい行を追加および**プロパティ**に**BTS します。ReceivePortName**します。 ままに、**演算子**列に設定**==**、設定、**値**列を**MyReceivePort**をクリックして**OK**します。  

16. 右クリックし、新しい送信ポート をクリックし、**参加**します。  

17. 右クリックし、新しい送信ポートをもう一度 をクリックし、**開始**します。  

18. 右クリックし、新しい受信場所 をクリックし、**を有効にする**します。  

    [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] このサンプルを使用する準備ができました。  

## <a name="running-the-sample"></a>サンプルを実行します。  
 次の手順を使用して、SendMSMQMessage サンプルを実行します。  

#### <a name="to-run-the-sample"></a>サンプルを実行するには  

1. コマンド ウィンドウで、次のフォルダーに移動します。  

    \<パスのサンプル\>\AdaptersUsage\SendMSMQMessage\bin\Debug  

2. SendMSMQMessage.exe ファイルを実行すると、このサンプルのユーザー インターフェイスを提供するグラフィカル アプリケーションが起動します。  

3. グラフィカル アプリケーションでの**BizTalk コンピューター名**ボックスに、ローカル コンピューターの名前を入力します。  

4. お試しください、 **Send Wrapped**オプション。  

   1. 内のテキストを変更する必要に応じて、**メッセージ本文**ボックス。  

   2. クリックして**ラップされた送信**します。  

      操作が成功すると、次の操作が表示されます。  

   - 単語**成功**ボタンのすぐ上のボックスに赤いフォントで表示されます。  

   - 送信先フォルダー C:\Demo\Reports にファイルが表示されます。 このファイルにはからテキストが含まれています、**メッセージ本文**ボックス .NET メッセージ キュー ライブラリによって単純な XML タグにラップします。  

     操作に失敗すると、ボタンのすぐ上のボックスにエラー メッセージが表示されます。  

5. お試しください、 **Send Exact**オプション。  

   1. 内のテキストを変更する必要に応じて、**メッセージ本文**ボックス。  

   2. クリックして**Send exact**します。  

      操作が成功すると、次の操作が表示されます。  

   - 単語**成功**ボタンのすぐ上のボックスに赤いフォントで表示されます。  

   - 送信先フォルダー C:\Demo\Reports にファイルが表示されます。 このファイルにはからテキストが含まれています、**メッセージ本文**ボックス、テキスト ボックスに表示されているとおりです。  

     操作に失敗すると、ボタンのすぐ上のボックスにエラー メッセージが表示されます。  

## <a name="see-also"></a>参照  
 [アダプタ サンプル – 使用法](../core/adapter-samples-usage.md)