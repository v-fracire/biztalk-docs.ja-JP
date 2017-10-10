---
title: "チュートリアル: BizTalk Adapter for TIBCO Rendezvous を使用してデータを受信する |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 58e7a739-701d-4085-a840-54f81c55e943
caps.latest.revision: "11"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: de436413f10cf4882b5c4e4b21af7bac6a3234c0
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="tutorial-using-the-biztalk-adapter-for-tibco-rendezvous-to-receive-data"></a>チュートリアル: BizTalk Adapter for TIBCO Rendezvous を使用したデータの受信
BizTalk Adapter for TIBCO Rendezvous を使用して TIBCO システムからデータを受信できます。 このチュートリアルでは、これを示す SDK サンプルについて説明します。  
  
## <a name="prerequisites"></a>前提条件  
  
-   このサンプルをビルドして展開するには、アダプターが実行されている [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] に [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] をインストールしてください。  
  
## <a name="what-this-sample-does"></a>このサンプルの処理  
 このサンプルでは、BizTalk Adapter for TIBCO Rendezvous を使用して TIBCO システムからデータを受信します。 オーケストレーションがメッセージを処理し、ファイル アダプターを使用して、指定されたフォルダーにデータを XML ファイルとして書き込みます。  
  
## <a name="how-this-sample-is-designed-and-why"></a>このサンプルのデザイン方法とその理由  
 このサンプルは、[!INCLUDE[vs2010](../includes/vs2010-md.md)] でデザインされ、BizTalk Adapter for TIBCO Enterprise Message Service を BizTalk オーケストレーションと組み合わせて使用する基本的な機能を紹介する目的で作成されました。  
  
> [!NOTE]
>  このサンプルでは、処理するアプリケーション用の TIBCO からメッセージを送信する方法を理解していることを前提としています。  
  
## <a name="where-to-find-this-sample"></a>このサンプルの場所  
 このサンプルの既定の場所は、次のとおりです。  
  
 C:\Program Files\Microsoft BizTalk Adapters for Enterprise Applications\TIBCO(r) Rendezvous(r)\Sdk\OneWayReceive  
  
 次の表は、このサンプルのファイルとその目的を示しています。  
  
|**ランタイム プロジェクト ファイル名**|**ランタイム プロジェクト ファイルの説明**|  
|----------------------------------|------------------------------------------|  
|OneWayReceive.btproj、<br /><br /> OneWayReceive.sln|アプリケーションのプロジェクトおよびソリューション ファイル。|  
|PureMessage.xsd|アプリケーションのスキーマ ファイルです。|  
|TIBCORvOWR.odx|アプリケーションが使用するオーケストレーション。|  
|TIBCORv.snk|厳密な名前のキー ファイル。|  
  
## <a name="how-to-use-this-sample"></a>このサンプルの使用方法  
  
#### <a name="create-a-new-instance-of-the-biztalk-adapter-for-tibco-rendezvous"></a>BizTalk Adapter for TIBCO Rendezvous の新しいインスタンスを作成する  
  
1.  起動して、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールです。 をクリックして**開始**、**すべてのプログラム**、 [!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]、[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]です。  
  
2.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、 [!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]、展開**BizTalk グループ**、展開**プラットフォームの設定**、クリックして**アダプター**です。  
  
3.  右クリック**アダプター**を指す**新規**、**アダプターしています.** 表示する、**アダプター プロパティ**ダイアログ。  
  
4.  値を入力して、**名前**フィールド、たとえば**TIBCO Rendezvous**です。  
  
5.  選択**TIBCO(r) Rendezvous(r)**で利用可能なアダプターの一覧から、**アダプター**ドロップダウン リスト をクリック**OK**です。  
  
#### <a name="create-a-biztalk-receive-port"></a>BizTalk 受信ポートを作成する  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、[ **BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**を展開して**BizTalk アプリケーション 1**、] をクリック**受信ポート**です。  
  
2.  受信ポート フォルダーを右クリックし、をクリックして**新規**、**一方向の受信ポートしています.**を表示する、**受信ポートのプロパティ**ダイアログ。  
  
3.  値を入力、**名前**フィールド、たとえば**TIBCORvOneWayRP**、 をクリック**OK**です。  
  
#### <a name="create-a-biztalk-receive-location"></a>BizTalk の受信場所を作成する  
  
1.  右クリックし、新しい受信ポートをクリックし、**新規**、**受信場所の追加.** 表示する、**受信場所のプロパティ**ダイアログ。  
  
2.  値を入力して、**名前**フィールド、たとえば**TIBCORvOneWayRL**です。  
  
3.  使用可能なアダプターの一覧から TIBCO Rendezvous アダプターを選択して、**型**ドロップダウン リスト ボックスし、をクリックして、**構成**アダプターを表示するにはボタン**トランスポートのプロパティ**  ダイアログ ボックス。  
  
    > [!NOTE]
    >  この値は、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールで TIBCO アダプターを作成したときに指定した名前です。  
  
4.  値を入力して、 **RendezvousSubjectName**下にある、 **AdapterRequiredProperties**です。  
  
5.  値を入力して、**証明されたリスナーのプロパティ**:  
  
    |**プロパティ**|**値**|  
    |------------------|---------------|  
    |台帳ファイル名|永続的な認証されたメッセージ配信に使用する台帳ファイル名。|  
    |再利用可能な名前|認証されたメッセージ配信に使用する再利用可能な送信者名です。 この名前は、ネットワーク上のすべての認証されたメッセージの送信者名の中で一意である必要があります。|  
  
6.  値を入力して、**資格情報**:  
  
    |**プロパティ**|**値**|  
    |------------------|---------------|  
    |Password|TIBCO Rendezvous サーバーのパスワード。|  
    |ユーザー名|TIBCO Rendezvous サーバーのユーザー名。|  
  
7.  値を入力して、 **RendezvousTransport**:  
  
    |**プロパティ**|**値**|  
    |------------------|---------------|  
    |デーモン|Rendezvous トランスポート デーモン パラメーター。|  
    |ネットワーク|Rendezvous トランスポート ネットワーク パラメーター。|  
    |サービス|Rendezvous トランスポート サービス パラメーター。|  
  
     プロパティの詳細については、次を参照してください。[設定 TIBCO Rendezvous 受信トランスポートのプロパティ](../core/setting-tibco-rendezvous-receive-transport-properties.md)です。  
  
8.  **[OK]**をクリックします。  
  
9. 選択**[xmlreceive]**で使用可能なパイプラインの一覧から、**受信パイプライン**ドロップダウン リスト ボックスし、をクリックして**OK**です。  
  
10. 受信場所を右クリックし、をクリックして**を有効にする**です。  
  
#### <a name="create-a-one-way-file-send-port"></a>一方向 FILE 送信ポートを作成する  
  
1.  送信ポートが使用する送信先フォルダー (たとえば、C:\FilesOut) を作成します。  
  
2.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、[ **BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**を展開して**BizTalk アプリケーション 1**、] をクリック**送信ポート**です。  
  
3.  右クリック**送信ポート**を指す**新規**、**静的な一方向送信ポートしています.** 表示する、**送信ポートのプロパティ**ダイアログ。  
  
4.  値を入力して、**名前**フィールド、たとえば**TIBCORvOneWayFileSP**です。  
  
5.  選択**ファイル**で使用可能なアダプターの一覧から、**型**ドロップダウン リスト ボックスし、をクリックして、**構成**アダプターを表示するにはボタン**トランスポートプロパティ** ダイアログ ボックス。  
  
6.  **コピー先フォルダー**プロパティ、先ほど作成したフォルダーの場所を入力し、をクリックして**OK**です。  
  
7.  選択、 **xmltransmit**パイプラインで使用可能なパイプラインの一覧から、**送信パイプライン**ドロップダウン リスト をクリック**OK**です。  
  
8.  送信ポートを右クリックし、をクリックして**開始**を参加させて、送信ポートを開始します。  
  
#### <a name="build-and-deploy-the-project"></a>プロジェクトのビルドと展開  
  
1.  ソリューション エクスプ ローラーで OneWayReceive プロジェクトを右クリックし、をクリックして**プロパティ**プロジェクトのプロジェクト デザイナーを起動します。  
  
2.  クリックして、**展開**タブです。  
  
3.  適切な値を入力、**サーバー**プロパティおよび**構成データベース**プロパティの  **BizTalk グループ**カテゴリ。  
  
4.  ソリューション エクスプ ローラーで OneWayReceive プロジェクトを右クリックし、をクリックして**展開**プロジェクトをビルドしてアセンブリを展開する、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]構成データベース。  
  
#### <a name="bind-and-enlist-the-orchestration"></a>オーケストレーションをバインドして参加させる  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、[ **BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**を展開して**BizTalk アプリケーション 1**、] をクリック**オーケストレーション**です。  
  
2.  をクリックして、**更新**ボタンをクリックして、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソール ツールバーまたはキーを押して、 **f5 キーを押して**を更新するキーボードのキー、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールの表示。  
  
3.  表示するオーケストレーションをダブルクリック、**オーケストレーションのプロパティ**ダイアログ。  
  
4.  をクリックして**バインド**オーケストレーションのバインド オプションを表示するダイアログ ボックスの左ペインでします。  
  
5.  バインド オプションに適切な値を指定します。次に例を示します。  
  
    |**パラメーター**|**値**|  
    |-------------------|---------------|  
    |Host|BizTalkServerApplication|  
    |SendPort|TIBCORvOneWayFileSP|  
    |ReceivePort|TIBCORvOneWayRP|  
  
6.  **[OK]**をクリックします。  
  
#### <a name="start-the-orchestration"></a>オーケストレーションを開始します。  
  
-   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールでは、オーケストレーションを右クリックし、をクリックして**開始**を参加させて、オーケストレーションを開始します。  
  
#### <a name="verify-that-the-application-receives-a-message"></a>アプリケーションがメッセージを受信することの確認  
  
-   ファイル送信ポートの送信先として構成されているフォルダーを開いて、出力ドキュメントが生成されていることを確認します。  
  
 ドキュメント インスタンスが正常に処理された場合、次の一連のイベントが発生します。  
  
1.  TIBCO Rendezvous アダプターが TIBCO システムからメッセージを取得し、BizTalk メッセージとしてメッセージ ボックスに公開します。  
  
2.  オーケストレーションがこの公開されたメッセージをサブスクライブします。これにより、BizTalk メッセージング エンジンがオーケストレーションのインスタンスをアクティブ化し、オーケストレーション インスタンスにメッセージを送信できるようにします。  
  
3.  オーケストレーション インスタンスがメッセージ ボックスにメッセージを返します。  
  
4.  ファイル送信ポートがこのメッセージをサブスクライブし、BizTalk がメッセージをファイル アダプターに送信します。  
  
5.  ファイル アダプターが、結果セットを含むメッセージを指定の出力フォルダーに書き込みます。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: BizTalk Adapter for TIBCO Rendezvous を使用してデータを送信するには](../core/tutorial-using-the-biztalk-adapter-for-tibco-rendezvous-to-send-data.md)   
 [チュートリアル: Microsoft BizTalk Adapter を使用して TIBCO Rendezvous の](../core/tutorials-using-the-microsoft-biztalk-adapter-for-tibco-rendezvous.md)   
 [作業の開始](../core/getting-started-with-biztalk-adapter-for-tibco-rendezvous.md)