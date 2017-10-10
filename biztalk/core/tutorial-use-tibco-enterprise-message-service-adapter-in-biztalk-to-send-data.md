---
title: "チュートリアル: BizTalk Adapter for TIBCO Enterprise Message Service を使用してデータを送信する |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1912d594-3839-4e04-bc40-93bd7cc0b309
caps.latest.revision: "16"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 913e8c0a3f44673d5bf06bf48d7c1ccf8b7a4ee2
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="tutorial-using-the-biztalk-adapter-for-tibco-enterprise-message-service-to-send-data"></a>チュートリアル: BizTalk Adapter for TIBCO Enterprise Message Service を使用したデータの送信
BizTalk Adapter for TIBCO Enterprise Message Service (EMS) を使用して TIBCO システムにデータを送信できます。 このチュートリアルでは、これを示す SDK サンプルについて説明します。  
  
## <a name="prerequisites"></a>前提条件  
  
-   BizTalk Adapter for TIBCO EMS を使用するには、TIBCO EMS C# API の TIBCO.EMS.dll をグローバル アセンブリ キャッシュ (GAC) に追加する必要があります。 アセンブリのインストールの詳細については、次を参照してください。 [TIBCO Enterprise Message Service の要件と制限事項](../core/tibco-enterprise-message-service-requirements-and-limitations.md)です。  
  
-   このサンプルをビルドして展開するには、アダプターが実行されている [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] に [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] をインストールしてください。  
  
## <a name="what-this-sample-does"></a>このサンプルの処理  
 このサンプルでは、ファイル フォルダーから XML ファイルを取得し、そのファイルをオーケストレーションに送信し、BizTalk Adapter for TIBCO Enterprise Message Service を使用して TIBCO システム内にレコードを作成します。  
  
## <a name="how-this-sample-is-designed-and-why"></a>このサンプルのデザイン方法とその理由  
 このサンプルは、[!INCLUDE[vs2010](../includes/vs2010-md.md)] でデザインされ、BizTalk Adapter for TIBCO Enterprise Message Service を BizTalk オーケストレーションと組み合わせて使用する基本的な機能を紹介する目的で作成されました。  
  
## <a name="where-to-find-this-sample"></a>このサンプルの場所  
 このサンプルの既定の場所は、次のとおりです。  
  
 C:\Program Files\Microsoft BizTalk Adapters for Enterprise Applications\TIBCO(r) Enterprise Message Service(TM)\Sdk\OneWaySend  
  
 次の表に、サンプル内のファイルとその説明を示します。  
  
|**ランタイム プロジェクト ファイル名**|**ランタイム プロジェクト ファイルの説明**|  
|----------------------------------|------------------------------------------|  
|OneWaySend.btproj<br /><br /> OneWaySend.sln|アプリケーションのプロジェクトおよびソリューション ファイル。|  
|Schema.xsd|アプリケーションのスキーマ ファイルです。|  
|Orchestration.odx|アプリケーションが使用するオーケストレーション。|  
|TIBCOEMSOneWaySend.snk|厳密な名前のキー ファイル。|  
  
## <a name="how-to-use-this-sample"></a>このサンプルの使用方法  
  
#### <a name="create-a-new-instance-of-the-biztalk-adapter-for-tibco-ems"></a>BizTalk Adapter for TIBCO EMS の新しいインスタンスを作成する  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールを起動します。 をクリックして**開始**、**すべてのプログラム**、 **Microsoft** [!INCLUDE[btsBizTalkServer2006r3ui](../includes/btsbiztalkserver2006r3ui-md.md)]、 **BizTalk Server 管理**です。  
  
2.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、 **BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**プラットフォームの設定**をクリックして**アダプター**です。  
  
3.  右クリック**アダプター**を指す**新規**、**アダプター**を表示する、**アダプターのプロパティ**ダイアログ。  
  
4.  値を入力して、**名前**フィールド、たとえば**TIBCO EMS**です。  
  
5.  選択**TIBCO Enterprise Message System**で利用可能なアダプターの一覧から、**アダプター**ドロップダウン リスト をクリック**OK**です。  
  
#### <a name="create-a-biztalk-send-port"></a>BizTalk 送信ポートを作成する  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、[ **BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**を展開して**BizTalk アプリケーション 1**、] をクリック**送信ポート**です。  
  
2.  右クリック**送信ポート**を指す**新規**、**静的な一方向送信ポート**を表示する、**送信ポートのプロパティ**ダイアログ。  
  
3.  値を入力して、**名前**フィールド、たとえば**TIBCOEMSOneWaySP**です。  
  
4.  使用可能なアダプターの一覧から TIBCO EMS アダプターを選択して、**型**ドロップダウン リスト ボックスし、をクリックして、**構成**アダプターを表示するにはボタン**トランスポートのプロパティ**ダイアログ ボックス。  
  
    > [!NOTE]
    >  この値は、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールで TIBCO Enterprise Message System アダプターを作成したときに指定された名前です。  
  
5.  値を入力して、**サーバー接続の定義**:  
  
    |**プロパティ**|**値**|  
    |------------------|---------------|  
    |転送先|サーバーの送信先キューまたはトピック名。|  
    |[ポート番号]|TIBCO サーバーが待ち受けしているポート。 既定値は 7222 です。|  
    |[サーバー名]|TIBCO EMS サーバーの名前。|  
  
6.  値を入力して、**ユーザーの資格情報**:  
  
    |**プロパティ**|**値**|  
    |------------------|---------------|  
    |Password|TIBCO EMS サーバーのパスワード。|  
    |ユーザー名|TIBCO EMS サーバーのユーザー名。|  
  
     プロパティの詳細については、次を参照してください。 [TIBCO Enterprise メッセージ サービス送信ハンドラーの作成](../core/creating-tibco-enterprise-message-service-send-handlers.md)です。  
  
7.  **[OK]**をクリックします。  
  
8.  選択、 **XML Transmit**パイプラインで使用可能なパイプラインの一覧から、**送信パイプライン**ドロップダウン リスト をクリック**OK**です。  
  
9. 送信ポートを右クリックし、をクリックして**開始**を参加させて、送信ポートを開始します。  
  
#### <a name="create-a-file-receive-port"></a>ファイル受信ポートを作成する  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、[ **BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**を展開して**BizTalk アプリケーション 1**、] をクリック**受信ポート**です。  
  
2.  受信ポート フォルダーを右クリックし、をクリックして**新規**、**一方向の受信ポート**受信ポートのプロパティ ダイアログを表示します。  
  
3.  値を入力、**名前**フィールド、たとえば**TIBCOEMSOneWayFileRP**、 をクリック**OK**です。  
  
#### <a name="create-a-file-receive-location"></a>ファイル受信場所を作成する  
  
1.  監視対象のファイル受信場所となるフォルダー (たとえば C:\Filesource) を作成します。  
  
2.  右クリックし、新しい受信ポートをクリックし、**新規**、**受信場所の**を表示する、**受信場所のプロパティ**ダイアログ。  
  
3.  値を入力して、**名前**フィールド、たとえば**TIBCOEMSOneWayFileRL**です。  
  
4.  選択**ファイル**で使用可能なアダプターの一覧から、**型**ドロップダウン リスト ボックスし、をクリックして、**構成**アダプターを表示するにはボタン**トランスポートプロパティ** ダイアログ ボックス。  
  
5.  用に作成したフォルダーの場所を入力、**受信フォルダー**プロパティをクリック**OK**です。  
  
6.  選択**[xmlreceive]**で使用可能なパイプラインの一覧から、**受信パイプライン**ドロップダウン リスト ボックスし、をクリックして**OK**です。  
  
7.  受信場所を右クリックし、をクリックして**を有効にする**です。  
  
#### <a name="generate-a-document-instance-from-the-adapter-schema"></a>アダプター スキーマからドキュメント インスタンスを生成する  
  
1.  ソリューション エクスプ ローラーで、Schema.xsd を右クリックし、をクリックして**プロパティ**です。  
  
2.  プロパティ ウィンドウでクリックして選択、**出力インスタンス ファイル名**オプションで 、**全般**カテゴリ。  
  
3.  表示するには、省略記号ボタン (...) をクリックして、 **出力ファイルの**ダイアログ。  
  
4.  たとえば、フォルダーと出力ファイル インスタンスの名前を指定**C:\instance.xml**  をクリック**保存**です。  
  
    > [!NOTE]
    >  ファイル受信場所に指定したフォルダーの場所は、ここに指定しないでください。  
  
5.  ソリューション エクスプ ローラーで、Schema.xsd を右クリックし、をクリックして**インスタンスの生成**を指定した場所にドキュメント インスタンスを生成します。  
  
#### <a name="modify-the-generated-document-instance"></a>生成されたドキュメント インスタンスを変更する  
  
1.  生成されたドキュメント インスタンスをメモ帳などのテキスト エディターで開き、ドキュメント インスタンスの内容を編集して、データによって TIBCO システムで一意のレコードが生成されるようにします。 データ ファイルの最初の部分を例として次に示します。  
  
    ```  
    <ns0:Root xmlns:ns0="http://TibcoEMSOne_WaySend.TibcoEMSOneWaySendSchema">  
      <Name>Punya Palit</Name>  
      <MailAddress>Prose Ware, Inc.</MailAddress>  
    </ns0:Root>  
    ```  
  
2.  変更したドキュメント インスタンスを保存します。  
  
#### <a name="build-and-deploy-the-project"></a>プロジェクトのビルドと展開  
  
1.  ソリューション エクスプ ローラーで OneWaySend プロジェクトを右クリックし、をクリックして**プロパティ**プロジェクトのプロジェクト デザイナーを起動します。  
  
2.  クリックして、**展開**タブです。  
  
3.  適切な値を入力、**サーバー**プロパティおよび**構成データベース**プロパティの  **BizTalk グループ**カテゴリ。  
  
4.  ソリューション エクスプ ローラーで OneWaySend プロジェクトを右クリックし、をクリックして**展開**プロジェクトをビルドしてアセンブリを展開する、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]構成データベース。  
  
#### <a name="bind-and-enlist-the-orchestration"></a>オーケストレーションをバインドして参加させる  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、[ **BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**を展開して**BizTalk アプリケーション 1**、] をクリック**オーケストレーション**です。  
  
2.  をクリックして、**更新**MMC ツールバーまたはキーを押してボタン、 **f5 キーを押して**を更新するキーボードのキー、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールの表示。  
  
3.  表示するオーケストレーションをダブルクリック、**オーケストレーションのプロパティ**ダイアログ。  
  
4.  をクリックして**バインド**オーケストレーションのバインド オプションを表示するダイアログ ボックスの左ペインでします。  
  
5.  バインド オプションに適切な値を指定します。次に例を示します。  
  
    |**パラメーター**|**値**|  
    |-------------------|---------------|  
    |Host|BizTalkServerApplication|  
    |FileReceivePort|TIBCOEMSOneWayFileRP|  
    |TibcoEMSOneWaySendPort|TIBCOEMSOneWaySP|  
  
6.  [OK] をクリックします。  
  
#### <a name="start-the-orchestration"></a>オーケストレーションを開始します。  
  
-   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールでは、オーケストレーションを右クリックし、をクリックして**開始**を参加させて、オーケストレーションを開始します。  
  
#### <a name="drop-a-document-instance-into-the-folder-monitored-by-the-file-receive-location"></a>ファイル受信場所の監視対象フォルダーにドキュメント インスタンスをドロップする  
  
-   先ほど作成したドキュメント インスタンスを、アプリケーションが監視するファイル受信フォルダーにコピーします。  
  
#### <a name="verify-that-the-tibco-system-is-updated"></a>TIBCO システムが更新されていることを確認する  
  
-   TIBCO Web インターフェイスを使用して、XML ファイルのデータからレコードが作成されたことを確認します。  
  
 ドキュメント インスタンスが正常に処理された場合、次の一連のイベントが発生します。  
  
1.  ファイル アダプターがフォルダーからファイルを取得し、メッセージボックスに BizTalk メッセージとして公開します。  
  
2.  この公開されたメッセージをオーケストレーションがサブスクライブします。その結果、BizTalk メッセージング エンジンによってオーケストレーションのインスタンスがアクティブ化され、メッセージがオーケストレーション インスタンスに送信されます。  
  
3.  オーケストレーション インスタンスがオーケストレーションで指定されたロジックを使用してメッセージを処理し、メッセージ ボックスにメッセージを返します。  
  
4.  この公開されたメッセージを TIBCO 送信ポートがサブスクライブします。その結果、BizTalk メッセージング エンジンによってこのメッセージが TIBCO 送信ポートに送信されます。  
  
5.  送信ポートがメッセージを BizTalk Adapter for TIBCO Enterprise Message Service. に渡します。  
  
6.  BizTalk Adapter for TIBCO Enterprise Message Service がメッセージを TIBCO システムに送信します。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: BizTalk Adapter for TIBCO Enterprise Message Service を使用してデータを受信するには](../core/tutorial-us-the-biztalk-adapter-for-tibco-message-service-to-receive-data.md)   
 [チュートリアル: Microsoft BizTalk Adapter を使用して TIBCO Enterprise Message Service の](../core/tutorials-use-the-microsoft-biztalk-adapter-for-tibco-message-service.md)   
 [作業の開始](../core/getting-started-with-biztalk-adapter-for-tibco-enterprise-message-service.md)