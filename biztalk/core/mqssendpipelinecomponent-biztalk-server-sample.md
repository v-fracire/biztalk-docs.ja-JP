---
title: "MQSSendPipelineComponent (BizTalk Server サンプル) |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- examples, MQSeries adapters
- pipelines, examples
- MQSeries adapters, examples
- examples, pipelines
ms.assetid: ac709e45-524b-45ab-9673-060790ecbed2
caps.latest.revision: "27"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 256731dbb6194aa1962d62ec9fdbe58a0fd60e03
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="mqssendpipelinecomponent-biztalk-server-sample"></a>MQSSendPipelineComponent (BizTalk Server サンプル)
このサンプルでは、一連の MQSeries プロパティ値を XML ファイルから読み取って、メッセージに適用する、パイプライン コンポーネントの作成方法を示します。  
  
## <a name="what-this-sample-does"></a>このサンプルの処理  
 このサンプルは、パイプライン コンポーネント プロジェクトおよびパイプライン コンポーネントを利用するパイプライン プロジェクトの 2 つの [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] プロジェクトで構成されています。  
  
## <a name="where-to-find-this-sample"></a>このサンプルの場所  
  
-   *\<サンプル パス >*\AdaptersUsage\MQSeriesAdapter\MQSSendPipelineComponent\SetMQSeriesHeaderPropertyComponent  
  
-   *\<サンプル パス >*\AdaptersUsage\MQSeriesAdapter\MQSSendPipelineComponent\SetMQSeriesHeaderPropertyPipeline  
  
 次の表は、このサンプルのファイルとその目的を示しています。  
  
|**ファイル**|**Description**|  
|--------------|---------------------|  
|SetMQSeriesHeaderPropertyComponent\SetMQSeriesHeaderPropertyComponent.sln、<br /><br /> SetMQSeriesHeaderPropertyComponent\SetMQSeriesHeaderPropertyComponent.csproj|パイプライン コンポーネントのプロジェクト ファイルとソリューション ファイルです。|  
|SetMQSeriesHeaderPropertyComponent\CSetMQSeriesHeaderPropertyComponent.cs|パイプライン コンポーネントの Visual C#® ソース ファイルです。|  
|SetMQSeriesHeaderPropertyComponent\SetMQSMQMDHdrProps.xml|パイプライン コンポーネントによって読み取られ、使用される MQSeries プロパティです。|  
|SetMQSeriesHeaderPropertyPipeline\SetMQSeriesHeaderPropertyPipeline.btproj、<br /><br /> SetMQSeriesHeaderPropertyPipeline\SetMQSeriesHeaderPropertyPipeline.sln|BizTalk パイプラインのプロジェクト ファイルとソリューション ファイルです。|  
|SetMQSeriesHeaderPropertyPipeline\SetMQSeriesHeaderPropertyPipeline.snk|BizTalk パイプライン プロジェクトの厳密な名前のキー ファイルです。|  
|SetMQSeriesHeaderPropertyPipeline\SetMQSeriesHeaderPropertyPipeline.btp|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] パイプラインです。|  
  
## <a name="how-to-use-this-sample"></a>このサンプルの使用方法  
 アプリケーションを作成するには、次の手順を実行します。  
  
1.  アプリケーション用のフォルダーを作成します。  
  
2.  パイプライン コンポーネント用に [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] プロジェクトを変更してコンパイルします。  
  
3.  コンパイルしたアセンブリとヘッダー ファイルを適切なフォルダーにコピーします。  
  
4.  [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] パイプライン用に [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] プロジェクトを変更します。  
  
5.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] パイプライン プロジェクトをコンパイルして展開します。  
  
6.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] の受信場所を設定します。  
  
7.  MQSeries キューを作成します。  
  
8.  送信ポートを設定します。  
  
9. 受信場所を有効にして送信ポートを開始します。  
  
## <a name="creating-the-folders-for-the-application"></a>アプリケーション用のフォルダーの作成  
 この手順では、アプリケーション用の適切なフォルダーを作成します。  
  
#### <a name="to-create-the-folders-for-the-application"></a>アプリケーション用のフォルダーを作成するには  
  
1.  という名前のフォルダーを作成する**temp** C:\ ドライブが既に存在しない場合にします。  
  
2.  下のフォルダーを作成、 **C:\temp**という名前のディレクトリ**Pickup3**です。  
  
## <a name="modifying-and-compiling-the-project-for-the-pipeline-component"></a>パイプライン コンポーネント用のプロジェクトの変更とコンパイル  
 この手順では、パイプライン コンポーネント用に [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] プロジェクトを変更してコンパイルします。  
  
#### <a name="to-modify-and-compile-the-project-for-the-pipeline-component"></a>パイプライン コンポーネント用にプロジェクトを変更およびコンパイルするには  
  
1.  ソリューション ファイルをダブルクリックして**SetMQSeriesHeaderPropertyComponent\SetMQSeriesHeaderPropertyComponent.sln**でソリューションを開く[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]です。  
  
2.  クラス ファイルをダブルクリックして**CSetMQSeriesHeaderPropertyComponent.cs**でクラス ファイルを開く[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]です。  
  
3.  変数を見つけて**samplesDir**、場所にこの変数が設定されていることを確認**C:\temp**です。  
  
4.  ソリューション エクスプ ローラーでソリューションを右クリックし、をクリックして**ビルド**です。 ある dll プロジェクトをコンパイルこれは、 **SetMQSeriesHeaderPropertyComponent\SetMQSeriesHeaderPropertyComponent\bin\Debug\\** ディレクトリ。  
  
## <a name="copying-the-assembly-and-header-file-to-appropriate-folders"></a>適切なフォルダーへのアセンブリとヘッダー ファイルのコピー  
 この手順では、コンパイルしたアセンブリとヘッダー ファイルを適切なフォルダーにコピーします。  
  
#### <a name="to-copy-the-compiled-assembly-and-header-file-to-the-appropriate-folders"></a>コンパイルしたアセンブリとヘッダー ファイルを適切なフォルダーにコピーするには  
  
1.  コンパイル済みのアセンブリをコピー **SetMQSeriesHeaderPropertyComponent.dll** BizTalk パイプライン コンポーネント フォルダーにします。 BizTalk パイプライン コンポーネント フォルダーの既定の場所は [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]Pipeline Components です。  
  
2.  MQHeader プロパティ ファイルをコピー **SetMQSMQMDHdrProps.xml**を**C:\temp**ディレクトリ。  
  
## <a name="modifying-the-project-for-the-biztalk-server-pipeline"></a>BizTalk Server パイプライン用のプロジェクトの変更  
 この手順では、[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] パイプライン用に [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] プロジェクトを変更します。  
  
#### <a name="to-modify-the-project-for-the-biztalk-server-pipeline"></a>BizTalk Server パイプライン用にプロジェクトを変更するには  
  
1.  [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]、ソリューション ファイルをダブルクリックして、ソリューションを開く**SetMQSeriesHeaderPropertyPipeline\SetMQSeriesHeaderPropertyPipeline.sln**です。  
  
2.  プロジェクトの厳密な名前キー ファイルを作成します。 この操作を行うには、次の手順を実行します。  
  
    1.  [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] コマンド プロンプトを開きます。  
  
    2.  ディレクトリに移動\<サンプル パス > \AdaptersUsage\MQSeriesAdapter\MQSSendPipelineComponent です。  
  
    3.  次のように入力します。  
  
         `sn -k MQSSendPipelineComponent.snk`  
  
    4.  Enter キーを押します。 これにより、キー ファイルが作成されます。  
  
3.  **ソリューション エクスプ ローラー**プロジェクトを右クリックしをクリックして、**プロパティ**を ([center] ウィンドウで) プロジェクトのプロジェクト デザイナーを起動します。  
  
    1.  プロジェクト デザイナーでクリックして**署名**タブです。  
  
    2.  右側のペインで、**アセンブリに署名**オプション.  
  
    3.  ドロップダウン リストをクリックして、**厳密な名前キー ファイルを選択して** をクリックし、**参照**です。  
  
    4.  参照\<サンプル パス > \AdaptersUsage\MQSeriesAdapter\MQSSendPipelineComponent\MQSSendPipelineComponent.snk をクリックして**開く**です。  
  
4.  先ほど作成したパイプライン コンポーネントに既に追加されて、**プリアセンブル**このパイプライン プロジェクトのステージ。 このコンポーネントがまだ追加されていない場合は、次の手順に従って追加する必要があります。  
  
    1.  [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] IDE をクリックして、**ツールボックス**左側にあるタブ。  
  
    2.  右クリックし、**ツールボックス**、 をクリック**アイテムの選択**です。  
  
    3.  **ツールボックス アイテムの選択**ダイアログ ボックスで、をクリックして、 **BizTalk パイプライン コンポーネント**] タブで、[、 **MQseries ヘッダー プロパティを設定するカスタム コンポーネント**コンポーネント、およびをクリックして**OK**です。  
  
    4.  ドラッグ、 **MQseries ヘッダー プロパティを設定するカスタム コンポーネント**コンポーネントを**プリアセンブル**このパイプラインのステージ。  
  
## <a name="compiling-and-deploying-the-pipeline-project"></a>パイプライン プロジェクトのコンパイルと展開  
 この手順では、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] パイプライン プロジェクトをコンパイルして展開します。  
  
#### <a name="to-compile-and-deploy-the-pipeline-project"></a>パイプライン プロジェクトをコンパイルおよび展開するには  
  
1.  ソリューション エクスプ ローラー ウィンドウで、ソリューションを右クリックし、をクリックして**ソリューションの配置**です。 これにより、ソリューションがビルドされ、アセンブリが BizTalk 管理データベースに展開されます。  
  
2.  次の手順に従って、アセンブリが BizTalk 管理データベースに展開されたことを確認します。  
  
    1.  BizTalk 管理コンソールを開きます。  
  
    2.  クリックして展開**BizTalk グループ [\<servername >:\<管理データベース >]**を展開し、をクリックし、**アセンブリ**フォルダーです。  
  
         展開されたパイプライン アセンブリは、の下に表示する必要があります、**アセンブリ**フォルダーです。  
  
## <a name="creating-the-receive-location"></a>作成する、受信場所  
 この手順では、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] の受信場所を作成します。  
  
#### <a name="to-create-the-receive-location"></a>受信場所を作成するには  
  
1.  BizTalk Server 管理コンソールで、右クリック**受信ポート**、 をポイント**新規**、クリックして**一方向の受信ポート**です。  
  
2.  **一方向受信ポートのプロパティ** ダイアログ ボックスで、**名前**ボックスに「MQReply」を入力し、 をクリック**OK**です。  
  
3.  左側のウィンドウでをクリックして**受信場所** タブをクリックして**新規**です。  
  
4.  **受信場所のプロパティ** ダイアログ ボックスで、**名前**フィールドに「ReceiveFile」を入力します。  
  
5.  **トランスポートの種類**ボックスで、**ファイル**です。  
  
6.  **受信ハンドラー**フィールドで、 **BizTalkServerApplication**です。  
  
7.  **受信パイプライン**フィールドで、 **Microsoft.BizTalk.DefaultPipelines.PassThruReceive**です。  
  
8.  **受信フォルダー**フィールドに「C:\temp\Pickup3」を入力します。  
  
9. **ファイル マスク**フィールドに「"*.\*"です。  
  
10. をクリックして**OK**、順にクリック**ok**を終了するには、もう一度、**受信場所のプロパティ** ダイアログ ボックス。  
  
## <a name="creating-a-mqseries-queue-through-the-mqseries-explorer"></a>MQSeries エクスプローラーを使用した MQSeries キューの作成  
 MQSeries Server for Windows のインストールに必要なアクセス許可があればは、アダプターのダイアログ ボックスで、使用して MQSeries キューを作成し、次の手順をスキップできます。  
  
 このようなアクセス許可を持っていない場合は、次の手順に従って、IBM WebSphere MQ エクスプローラーを使用してキューを作成できます。  
  
#### <a name="to-create-a-mqseries-queue-through-the-mqseries-explorer"></a>MQSeries エクスプローラーを使用して MQSeries キューを作成するには  
  
1.  をクリックして**開始**、 をポイント**プログラム**、 をポイント**IBM WebSphere MQ**、順にクリック**WebSphere MQ エクスプ ローラー**です。  
  
2.  ダブルクリックして**キュー マネージャー**、し、既定のキュー マネージャーをダブルクリックします。 既定のキュー マネージャーは、通常の名前**qm _**\<*machine_name*> 場所*machine_name*お使いのコンピューターの名前を指定します。  
  
3.  右クリック**キュー**、 をポイント**新規**、クリックして**ローカル キュー**です。  
  
4.  **ローカル キューの作成**ダイアログ ボックスで、**キュー名**、型**SETHEADER**、クリックして**[ok]**です。  
  
## <a name="creating-the-send-port-and-mqseries-queue"></a>送信ポートと MQSeries キューの作成  
 この手順では、出力メッセージ用の送信ポートを作成します。 MQSeries キューは、送信ポートがまだ作成されていない場合に送信ポートを作成したときにも作成されます。  
  
#### <a name="to-create-the-send-port-and-mqseries-queue"></a>送信ポートと MQSeries キューを作成するには  
  
1.  右クリック**送信ポート**、 をポイント**新規**、クリックして**静的な一方向送信ポート**です。  
  
2.  **送信ポートのプロパティ** ダイアログ ボックスで、**名前**ボックスに「mqsolicitresponse"です。  
  
3.  **トランスポートの種類**ボックスで、 **MQSeries**です。  
  
4.  **送信パイプライン**ボックスで、 **[setmqseriesheaderpropertypipeline.setmqseriesheaderssendpipeline]**です。  
  
5.  **フィルター**、次の名前/値ペアを持つ新しいエントリを追加します。  
  
    -   設定**プロパティ**に"BTS です。ReceivePortName"です。  
  
    -   設定**演算子**「= =」にします。  
  
    -   設定**値**を"ReceiveFile"です。  
  
        > [!NOTE]
        >  これにより、ReceiveFile 受信ポートで受信したメッセージをサブスクライブするように送信ポートが設定されます。  
  
6.  をクリックして**トランスポート**です。  
  
7.  **アドレス (URI)**フィールドで省略記号 (...) ボタンをクリックします。  
  
8.  **MQSeries トランスポートのプロパティ** ダイアログ ボックスで、**キュー定義**フィールドで省略記号 (...) ボタンをクリックします。  
  
9. **キュー定義** ダイアログ ボックスで、**サーバー名**フィールドに、コンピューター名を入力します。  
  
10. **キュー マネージャー**フィールドで、既定のキュー マネージャーを選択します。  
  
11. キューのフィールドに「SETHEADER」を入力し、、クリックして**エクスポート**です。  
  
12. **エクスポート**ダイアログ ボックスで、をクリックして**キューの作成**、順にクリック**[ok]**または**実行**すべてのダイアログを終了するまでです。  
  
## <a name="enabling-the-receive-location-and-starting-the-send-port"></a>受信場所の有効化と送信ポートの開始  
 この手順では、受信場所を有効化し、送信ポートを開始します。  
  
#### <a name="to-enable-the-receive-location-and-start-the-send-port"></a>受信場所を有効にして送信ポートを開始するには  
  
1.  BizTalk Server 管理コンソールで **受信ポート**です。  
  
2.  詳細ウィンドウで右クリックし、 **MQIn**受信場所をクリックして**を有効にする**です。  
  
3.  詳細ウィンドウで右クリックし、 **SetMQHeader**送信ポートをクリックして**開始**です。  
  
## <a name="testing-the-application"></a>アプリケーションのテスト  
 この手順では、アプリケーションをテストします。  
  
#### <a name="to-test-the-application"></a>アプリケーションをテストするには  
  
1.  ファイルを配置、 **C:\Temp\Pickup3**フォルダーです。  
  
2.  WebSphere MQ エクスプローラーを起動し、SETHEADER キューをダブルクリックして、SETHEADER キュー内のメッセージを検証します。  
  
     SETHEADER キュー内のメッセージのすべてのコンテキスト プロパティを表示するには、次の手順に従います。  
  
    1.  ダブルクリックして、 **SETHEADER**を表示するキュー、 **Message Browser**  ダイアログ ボックス。  
  
    2.  **Message Browser**ダイアログ ボックスで、をクリックして**列**を表示する、**メッセージの表示/非表示列** ダイアログ ボックス。  
  
    3.  **使用可能な列**で表示するのには、各エントリをダブルクリックして、 **Message Browser**クリックしてダイアログ ボックスで、 **OK**です。  
  
3.  各メッセージのメッセージ コンテキスト プロパティに表示するか、 **Message Browser**  ダイアログ ボックス。  
  
## <a name="see-also"></a>参照  
 [MQSeries アダプタ サンプル](../core/mqseries-adapter-samples.md)