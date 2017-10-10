---
title: "MethodCall (BizTalk Server サンプル) |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- orchestrations, calling
- examples, orchestrations
- orchestrations, methods
ms.assetid: 6bdc72da-9478-403a-b706-3089b7374ac7
caps.latest.revision: "20"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d3973a5137075732d3c648bb8b0e575dd0d49c57
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="methodcall-biztalk-server-sample"></a>MethodCall (BizTalk Server サンプル)
MethodCall サンプルは、BizTalk Server オーケストレーションから .NET ベースのメソッドを呼び出す方法を示すものです。  
  
## <a name="what-this-sample-does"></a>このサンプルの処理  
 このサンプルでは、次の一連の手順を実行して .NET ベースのメソッドと連携します。  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オーケストレーションで、In フォルダーから XML 入力ファイルを取得します。 このファイルには、数値演算ライブラリで実行する加算または減算に関する情報が含まれています。  
  
2.  オーケストレーションで、インクルードされた数値演算ライブラリを呼び出し、XML 入力ファイルに指定されている加算または減算を実行します。  
  
3.  数値演算ライブラリ メソッドのいずれか適切な**追加**または**減算**要求された計算を実行し、その結果、XML ドキュメントとしてパッケージ化します。  
  
4.  オーケストレーションで、生成された .xml ファイルを Out フォルダに格納します。  
  
## <a name="how-this-sample-is-designed-and-why"></a>このサンプルのデザイン方法とその理由  
 このサンプルは、次の機能を実行します。  
  
-   昇格させたプロパティをオーケストレーション内で使用します。 InputSchema.xsd の 3 つの要素は、識別フィールドとして昇格されています。 オーケストレーションでは、入力メッセージの受信時にこれら 3 つのフィールドの値を取得し、オーケストレーション内で対応する宣言済みの変数に割り当てます。  
  
-   使用して、**判断**図形をオーケストレーションに"if then else"ロジックを表現します。 入力した後、オーケストレーションは、内部変数を識別フィールドの値を割り当てる、**判断**図形を加算または減算を実行するかどうかを確認します。 演算を実行する必要がない場合、オーケストレーションは終了します。  
  
-   オーケストレーションから外部アセンブリを呼び出します。 加算を実行する場合、オーケストレーションでは外部 C# アセンブリを呼び出し、2 つのパラメータを渡して加算を実行します。 減算も同様の手順です。  
  
    > [!NOTE]
    >  アセンブリをオーケストレーションから呼び出すには、アセンブリをグローバル アセンブリ キャッシュにインストールしておく必要があります。グローバル アセンブリ キャッシュにアセンブリがない場合、実行時に XLANG エラーが返されます。  
  
-   使用して、**メッセージの割り当て**出力メッセージを構築するために図形です。  
  
-   次のコードを式図形に配置することにより、オーケストレーションをデバッグします。  
  
    ```  
    System.Diagnostics.Debug.WriteLine(iResult);  
    ```  
  
     次のコードを使用して、結果をイベント ログに書き込むこともできます。  
  
    ```  
    System.Diagnostics.EventLog.WriteEntry("MethodCall SDK Sample Debug", System.String.Format("Result = {0}", iResult);  
    ```  
  
## <a name="where-to-find-this-sample"></a>このサンプルの場所  
 \<*パスのサンプル*> \Orchestrations\MethodCall\  
  
 次の表は、このサンプルのファイルとその目的を示しています。  
  
|ファイル|Description|  
|---------------|-----------------|  
|Cleanup.bat|アセンブリの展開を解除し、グローバル アセンブリ キャッシュからアセンブリを削除するために使用されます。 送信ポートと受信ポートが削除されます。 必要に応じて、Microsoft インターネット インフォメーション サービス (IIS) の仮想ディレクトリが削除されます。|  
|Input.xml|サンプル入力ファイルです。|  
|Setup.bat|このサンプルをビルドおよび初期化するために使用されます。|  
|\MathLibrary フォルダには、次のファイルが含まれます。<br /><br /> AssemblyInfo.cs、MathHelper.cs、MathLibrary.csproj|このサンプルで使用する数値演算ライブラリのプロジェクト ファイルとソース ファイルです。|  
|\MethodCallSample フォルダには、次のファイルが含まれます。<br /><br /> InputSchema.xsd、OutputSchema.xsd|それぞれ、入力 .xml ファイルと出力 .xml ファイルのスキーマです。|  
|\MethodCallSample フォルダには、次のファイルが含まれます。<br /><br /> MethodCallSample.btproj、MethodCallSample.sln|このサンプルのプロジェクト ファイルとソリューション ファイルです。|  
|\MethodCallSample フォルダには、次のファイルが含まれます。<br /><br /> MethodCallSampleBinding.xml|ポートのバインドなど、自動化されたセットアップに使用されます。|  
|\MethodCallSample フォルダには、次のファイルが含まれます。<br /><br /> MethodCallService.odx|数値演算ライブラリを呼び出し、要求された計算を実行する [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オーケストレーションです。|  
  
## <a name="building-and-initializing-this-sample"></a>このサンプルのビルドと初期化  
  
#### <a name="to-build-and-initialize-the-methodcall-sample"></a>MethodCall サンプルをビルドおよび初期化するには  
  
1.  コマンド ウィンドウで、次のフォルダーに移動します。  
  
     \<*パスのサンプル*> \Orchestrations\MethodCall  
  
2.  次の操作を実行する Setup.bat ファイルを実行します。  
  
    -   MethodCall フォルダに、このサンプルの入力 (In) フォルダと出力 (Out) フォルダを作成します。  
  
    -   このサンプル用に [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] プロジェクトをコンパイルし、生成されたアセンブリを展開します。  
  
    -   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 受信場所と、オーケストレーションの送信ポートおよび受信ポートを作成しバインドします。  
  
    -   受信場所を有効にし、送信ポートを開始します。 オーケストレーションを参加させ、開始します。  
  
> [!NOTE]
>  このサンプルを実行する前に、ビルドと初期化のプロセス中に [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] でエラーが報告されていないことを確認する必要があります。  
  
## <a name="running-this-sample"></a>このサンプルの実行  
  
#### <a name="to-run-the-methodcall-sample"></a>MethodCall サンプルを実行するには  
  
1.  ファイル Input.xml を In フォルダにコピーします。  
  
2.  .xml ファイルが Out フォルダに作成されることを確認します。 このファイルには、要求された加算または減算の計算結果が含まれています。 このファイルの名前の形式が\< *MessageID*> .xml、場所 *\<MessageID >*メッセージを一意に識別する GUID が生成されます。  
  
3.  入力ファイルを変更し、別の加算または減算を要求することもできます。  
  
## <a name="uninstalling-this-sample"></a>このサンプルのアンインストール  
  
#### <a name="to-uninstall-the-methodcall-sample"></a>MethodCall サンプルをアンインストールするには  
  
1.  [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]コマンド プロンプトでディレクトリ変更コマンド (**cd**) に\<*サンプル パス*> \Orchestrations\MethodCall\\です。  
  
2.  Cleanup.bat を実行します。  
  
## <a name="see-also"></a>参照  
 [オーケストレーション (BizTalk Server Samples フォルダ)](../core/orchestrations-biztalk-server-samples-folder.md)