---
title: OperationsSamples (BizTalk Server サンプル) |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3c9e3f3e-a570-4edd-aa2e-3f8e2e37c8a0
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a2a871afd76d6dd46cb4aa5d72d1c23b332ad90e
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36969499"
---
# <a name="operationssamples-biztalk-server-sample"></a>OperationsSamples (BizTalk Server サンプル)
OperationsSamples サンプルは、Operations オブジェクト モデルを使用して、さまざまな操作を実行する方法を具体的に示します。  
  
## <a name="what-this-sample-does"></a>このサンプルの処理  
 このサンプルは、次の操作方法を示します。  
  
- 追跡プロファイルを使用して、オーケストレーションにアクティビティのコメントを付ける。  
  
- BAM 追跡データベースを使用して、アクティビティ ID を検索し、関連するオーケストレーション インスタンスを検索する ID を使用する方法。  
  
- 検索して、メッセージ フローを使用して操作する方法、 **MessageFlow**クラスおよびその他の Operations オブジェクト モデル クラスと Api。  
  
- ポートにアクセスする方法、メッセージ、およびから派生したクラスを使用して他のインスタンス、**インスタンス**クラス。  
  
  サンプルには、上の操作をサポートする多くの有益なヘルパー クラスとメソッドが含まれています。 これらと他のコードの特長については、次のセクションで説明します。  
  
## <a name="how-this-sample-is-designed-and-why"></a>このサンプルの目的とその理由  
 このサンプルは、Operations オブジェクト モデルの主要クラスおよびメソッドの機能を紹介し、ユーザーに公開されている BAM 追跡データベースでクエリを実行する方法を示すことを目的としています。  
  
 Operations オブジェクト モデルには、BizTalk Server 内でメッセージや他のインスタンスを操作できるクラスが含まれています。  
  
### <a name="using-a-bam-activity-id"></a>BAM アクティビティ ID の使用  
 このサンプルでは、BAM との対話方法と、ユーザーに公開されている追跡データベースのビューを使用して、ビジネス データを使ってメッセージ ボックスのライブ メッセージを見つける方法を示します。 サンプルでは、注文書番号に対応するオーケストレーション ID を取得して、この作業を行います。 このタスクを成功させるには、次のことを行う必要があります。  
  
1. ビジネス データ (注文書番号) を使用して、アクティビティ ID を検索します。 この手順では、ビジネス データを内部 ID にマップして、追加情報の検索に使用できるようにします。  
  
2. アクティビティ ID に関連する BAM 参照を取得します。  
  
3. 種類が "BizTalkService" の参照を検索し、オーケストレーションを参照します。 見つかったら、そのインスタンス ID を返します。  
  
   この機能は、 **BAMWebService.GetOrchestrationID**静的メソッドと、BamManagementService.cs ソース ファイルでクラスとメソッドを含む関連ヘルパー メソッド。  
  
### <a name="suspending-terminating-and-resuming-an-instance"></a>インスタンスの中断、終了、および再開  
 サンプル プログラムが含まれています、 **Samples.OperateOnInstance**メソッドを操作とインスタンス ID を受け取り、インスタンスで指定された操作を実行します。 有効な操作がによって定義されている、 **InstanceOperation**列挙しており、Suspend、Terminate、再開します。 これらの操作は、biztalkoperations のメソッドに直接マップ-**SuspendInstance**、 **TerminateInstance**、および**ResumeInstance**します。  
  
 メソッドは ArgumentException と SqlException の両方の例外を処理します。 Operations オブジェクト モデルのクラスおよびメソッドの操作時に、SqlException を含む例外が発生する可能性があるので注意してください。  
  
> [!NOTE]
>  Operations メソッドの多くは、データベースにアクセスする必要があります。 これらのメソッドによって例外がスローされる可能性があることを予測し、適切に処理する必要があります。  
  
### <a name="retrieving-all-live-messages"></a>すべてのライブ メッセージの取得  
 次のコードに示すように、Operations オブジェクト モデルでは、取得可能なすべてのライブ メッセージを簡単に繰り返すことができます。  
  
```  
BizTalkOperations _operations = new BizTalkOperations()  
IEnumerable messages = _operations.GetMessages();  
foreach (BizTalkMessage msg in messages)  
…  
```  
  
 OperationsSamples プログラムは、この手順をさらに一歩進め、メッセージ部分の数や種類と共に、メッセージ ID とメッセージの種類を含む、各メッセージに関する情報にアクセスする方法を示します。 このコードを変更して、BizTalk Server で、取得可能なライブ メッセージの多くまたはすべてで繰り返す必要があるシナリオに使用できます。  
  
> [!NOTE]
>  数百または数千のメッセージが存在する場合があります。 リスト全体をスキャンすると、パフォーマンスが低下することがあります。  
  
## <a name="where-to-find-this-sample"></a>このサンプルの場所  
 このサンプルは、SDK がある次の場所にあります。  
  
 \<*パスのサンプル*\>\Admin\OperationsOM\OperationsSamples\  
  
 次の表は、このサンプルのファイルとその目的を示しています。  
  
|ファイル|説明|  
|---------------|-----------------|  
|BamManagementService.cs|BAM Web サービスの Web プロキシ クラスです。|  
|Cleanup.bat|サンプル オーケストレーションを削除し、HelloWorld サンプルを元の状態に戻します。|  
|HelloOrchestration.btt|BizTalk イベント ソースを BAM ターゲット アクティビティにマップするときに使用する追跡プロファイルです。|  
|HelloOrchestration.xls|BAM 定義スタイルシート。|  
|OperationsSamples.cs|Operations オブジェクト モデルのさまざまな側面を示すコードを含む C# ソース ファイルです。|  
|OperationsSamples.csproj、OperationsSamples.sln、AssemblyInfo.cs|このサンプルのプロジェクト、ソリューション、およびアセンブリ情報です。|  
|Setup.bat|HelloWorld オーケストレーション サンプルを変更して、このサンプルをビルドおよび初期化するのに使用します。 サンプル オーケストレーションのインストール、BAM アクティビティ定義および追跡プロファイル エディター ファイルの展開、ポートの構成、受信場所へのサンプル ファイルのドロップを実行します。|  
  
## <a name="how-to-use-this-sample"></a>このサンプルの使用方法  
 このサンプルを使用して、Operations オブジェクト モデルで使用できる機能を試してください。 既存のルーチンを変更して、メッセージを異なる方法で検索および操作したり、BizTalk Server 管理コンソールのグループ ハブの一部を複製する新しいコードを追加します。  
  
 次のタスクを行うこともできます。  
  
-   カスタム アプリケーションに、グループのハブの最も使用頻度のサブセットをレプリケートするアプリケーションを作成します。  
  
-   ポートを作成し、新しい取引先にテスト メッセージを送信するカスタム プロビジョニング アプリケーションを作成する。  
  
-   サンプル プログラムを、1 件の注文書または一連の注文書に関する情報を画面、XML ファイル、またはテキスト レポートに出力するコマンド ライン ユーティリティに変更する。  
  
## <a name="installing-sample-support-files"></a>サンプル サポート ファイルのインストール  
 このセクションでは、サンプルをインストールして実行するために必要な手順を説明します。  
  
> [!NOTE]
>  このサンプルをインストールして実行する前に、BAM がインストールされ、機能していることを確認してください。 BAM がインストールされていないと、このサンプルは動作しません。  
  
#### <a name="to-compile-and-install-the-support-files-for-this-sample"></a>このサンプルのサポート ファイルをコンパイルおよびインストールするには  
  
1.  コマンド ウィンドウで、次のフォルダーに移動します。  
  
     `<Samples Path>\Admin\OperationsOM\OperationSamples`  
  
2.  Setup.bat を実行します。処理内容は次のとおりです。  
  
    -   送信および受信ディレクトリの作成  
  
    -   送信および受信ポートの作成と起動  
  
    -   `<Samples Path>`\Orchestrations\HelloWorld フォルダーの HelloWorld オーケストレーションのコンパイルと展開  
  
    -   HelloWorld オーケストレーション用に公開キー トークンを変更  
  
    -   BAM アクティビティ定義および追跡プロファイル エディター ファイルの展開  
  
    -   出力ディレクトリの名前の変更  
  
    > [!NOTE]
    >  インストールを中止するには、最初の "press any key to continue" プロンプトで Ctrl キーを押しながら C キーを押します。 スクリプトが停止し、HelloWorld サンプルは元の状態のままです。 2 番目および最後のプロンプトで Ctrl キーを押しながら C キーを押しても、インストールは終了しません。 この場合は、Cleanup.bat を実行して、OperationsOM サンプルをアンインストールし、HelloWorld サンプルを復元してください。  
  
## <a name="running-this-sample"></a>このサンプルの実行  
 次の手順で、OperationsOM サンプルを実行します。  
  
#### <a name="to-compile-and-run-the-sample"></a>サンプルをコンパイルおよび実行するには  
  
1.  をクリックして**開始**を選択します**すべてのプログラム**を選択します**Microsoft BizTalk Server**、し、 **BizTalk Server 管理**します。  
  
2.  BizTalk Server 管理コンソールで  **BizTalk Server 管理**、展開**BizTalk グループ**、展開**プラットフォームの設定**順に展開**ホスト インスタンスの**します。  
  
3.  右クリック**BizTalkServerApplication**、 をクリックし、**再起動**します。  
  
    > [!NOTE]
    >  製品を構成してからホスト インスタンスを再起動していない場合は、BAM に正しい作業データベースを設定するために、BizTalkServerApplication ホスト インスタンスの再起動が必要です。  
  
4.  Windows エクスプローラーから、次のフォルダーに移動します。  
  
     `<Samples Path>\Admin\OperationsOM\OperationSamples`  
  
5.  ダブルクリックして、 **OperationsOM.sln**プロジェクト ファイルを Visual Studio に読み込みます。  
  
6.  F5 キーを押して、サンプルを実行します。  
  
     --または--  
  
     **ビルド** メニューのをクリックして**ソリューションのリビルド**します。 ビルドが完了したらは、Windows エクスプ ローラーを使用して、移動する`<Samples Path>\Admin\OperationsOM\OperationSamples\bin\Debug,`し、ダブルクリック**OperationsSamples.exe**します。  
  
## <a name="classes-or-methods-used-in-this-sample"></a>このサンプルで使用されるクラスまたはメソッド  
 [Microsoft.BizTalk.Operations.BizTalkOperations](http://msdn.microsoft.com/library/microsoft.biztalk.operations.biztalkoperations.aspx) &#124; [Microsoft.BizTalk.Operations.MessageFlow](http://msdn.microsoft.com/library/microsoft.biztalk.operations.messageflow.aspx) &#124; [Microsoft.BizTalk.Operations.SendPortInstance](http://msdn.microsoft.com/library/microsoft.biztalk.operations.sendportinstance.aspx)&#124; [Microsoft.BizTalk.Operations.RoutingFailureInstance](http://msdn.microsoft.com/library/microsoft.biztalk.operations.routingfailureinstance.aspx) &#124; [Microsoft.BizTalk.Operations.OrchestrationInstance](http://msdn.microsoft.com/library/microsoft.biztalk.operations.orchestrationinstance.aspx) &#124; [Microsoft.BizTalk.Operations.MSMQtInstance](http://msdn.microsoft.com/library/microsoft.biztalk.operations.msmqtinstance.aspx) &#124; [Microsoft.BizTalk.Operations.TrackedServiceInstance](http://msdn.microsoft.com/library/Microsoft.BizTalk.Operations.TrackedServiceInstance.aspx)  
  
## <a name="see-also"></a>参照  
 [Admin-OperationsOM (BizTalk Server Samples フォルダー)](../core/admin-operationsom-biztalk-server-samples-folder.md)