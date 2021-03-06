---
title: パイプラインを実行する式を使用する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ExecuteReceivePipeline() method
- pipelines, schema resolution
- ExecuteSendPipeline() method
- SendPipelineInputMessages class
- pipelines, restrictions
- pipelines, errors
- XLANGPipelineManager class
- receive pipelines, orchestrations
- ReceivePipelineOutputMessages class
- orchestrations, pipelines
- pipelines, component types
- send pipelines, orchestrations
- pipelines, states
- pipelines, executing
- Microsoft.XLANGs.Pipeline namespace
- pipelines, transactional
- pipelines, orchestrations
- Message Assignment shape [Orchestration Designer], pipelines
ms.assetid: f947fa73-526c-4747-8de7-df557a93056c
caps.latest.revision: 26
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e8c0b0e79f79c351d84ed22b12a5eba8bdc9f3a4
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37005171"
---
# <a name="how-to-use-expressions-to-execute-pipelines"></a>パイプラインを実行する式の使用方法
[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、オーケストレーション内からパイプラインを同期的に呼び出すことができます。 これにより、オーケストレーションで、パイプライン (送信または受信) にカプセル化されたメッセージ処理をデータの本体に対して利用することができます。そのデータをメッセージング インフラストラクチャに送信する必要はありません。  
  
 この機能を使用すると、オーケストレーションから送信パイプラインを呼び出して、複数のメッセージを 1 つの送信インターチェンジに統合することができます。 反対に、オーケストレーションから受信パイプラインを呼び出して、メッセージング インフラストラクチャの外部で取得されたインターチェンジをデコードおよび逆アセンブルすることもできます。メッセージ ボックスを通過する場合の処理コストが発生することもありません。  
  
## <a name="details"></a>詳細  
 オーケストレーション内のメソッドを使用して、 **XLANGPipelineManager**クラス (で、 **Microsoft.XLANGs.Pipeline**名前空間) を呼び出す送信または受信パイプライン。  受信パイプラインは、BizTalk メッセージングのメッセージ受信のコンテキストでパイプラインが実行される場合と同じように、単一のメッセージまたはインターチェンジを処理して 0 個以上のメッセージを生成します。 送信パイプラインも、BizTalk メッセージングのメッセージ送信のコンテキストでパイプラインが実行される場合と同じように、1 つ以上のメッセージを処理して単一のメッセージまたはインターチェンジを生成します。  
  
## <a name="calling-a-receive-pipeline"></a>受信パイプラインの呼び出し  
 アプリケーションがオーケストレーションから受信パイプラインを呼び出すために、 **ExecuteReceivePipeline()** のメソッド、 **XLANGPipelineManager**クラス。  このメソッドは、1 つのインターチェンジを使用し、0 個以上のメッセージのコレクションを返します (のインスタンスに含まれている、 **ReceivePipelineOutputMessages**クラス)。 このメソッドの構文の .NET クラス ライブラリの参照の詳細については、 **XLANGPipelineManager**クラス。  
  
 オーケストレーションから受信パイプラインを実行するための API を以下に示します。  
  
 `// Execute receive pipeline`  
  
 `static public ReceivePipelineOutputMessages ExecuteReceivePipeline(System.Type receivePipelineType, XLANGMessage msg);`  
  
 受信パイプラインへの呼び出しを行うことが通常、**式**オーケストレーション内の図形。  
  
 オーケストレーションから受信パイプラインを呼び出すには、オーケストレーション プロジェクトでパイプライン アセンブリを参照する必要があります。 次に、受信パイプラインを呼び出すオーケストレーションの例を示します。  
  
 ![受信パイプラインの呼び出し画面](../core/media/callingreceivepipelinefromorchestration.gif "CallingReceivePipelineFromOrchestration")  
  
 詳細な例は、SDK サンプルを参照してください。[で構成されるメッセージ プロセッサ (BizTalk Server サンプル)](../core/composed-message-processor-biztalk-server-sample.md)します。  
  
> [!NOTE]
>  型の変数**ReceivePipelineOutputMessages**オーケストレーションのアトミックのスコープ内でのみ宣言できます。  この型の変数はシリアル化できないため、オーケストレーションの永続化が維持されないからですが、オーケストレーションはアトミックのスコープ内で実行されるときは永続化されません。  したがって、受信パイプラインはアトミックのスコープ内でしか実行できないことになります。  
  
> [!NOTE]
>  呼び出すときに**PassThruReceive**パイプラインまたはオーケストレーション内からカスタム パイプライン コンポーネントでは、受信メッセージの種類に関係なく System.Xml.XmlDocument が XML か、受信メッセージの変数の型を宣言する必要があります. したがって、受信メッセージが XML メッセージ以外 (フラット ファイル形式のメッセージなど) の場合は、処理しようとすると例外が発生します。 これは、オーケストレーション エンジンが上記のシナリオでは受信メッセージの種類に関係なく System.Xml.XmlDocument を使用するためです。  
  
## <a name="calling-a-send-pipeline"></a>送信パイプラインの呼び出し  
 アプリケーションがオーケストレーションから送信パイプラインを呼び出す、 **ExecuteSendPipeline()** のメソッド、 **XLANGPipelineManager**クラス。 このメソッドは 1 つまたは複数のメッセージのコレクション (のインスタンスに含まれている、 **SendPipelineInputMessages**クラス) を 1 つのインターチェンジを返します。 このメソッドの構文の .NET クラス ライブラリの参照の詳細については、 **XLANGPipelineManager**クラス。  送信パイプラインの実行を呼び出し、新しいインターチェンジを生成するため、 **ExecuteSendPipeline()** メソッドは、そのメッセージの割り当て図形内で行う必要があります。  
  
 オーケストレーションから送信パイプラインを実行するための API を以下に示します。  
  
 `// Execute a send pipeline`  
  
 `static public ExecuteSendPipeline(System.Type sendPipelineType, SendPipelineInputMessages inputMsgs, XLANGMessage msg);`  
  
 送信パイプラインの呼び出しを行う必要がある、**メッセージの割り当て**オーケストレーション内の図形。  
  
 オーケストレーションから送信パイプラインを呼び出すには、オーケストレーション プロジェクトでパイプライン アセンブリを参照する必要があります。  次に、送信パイプラインを呼び出すオーケストレーションの例を示します。  
  
 ![送信パイプラインの呼び出し画面](../core/media/example-callingsendpipelinefromorchestration.gif "Example_CallingSendPipelineFromOrchestration")  
  
> [!NOTE]
>  既定の XMLTransmit パイプラインを呼び出す際には、メッセージ コンテキスト プロパティの XMLNORM.EnvelopeSpecName をエンベロープ スキーマの完全修飾名に設定する必要があります。 以下に例を示します。  
>   
>  `MyMessage(XMLNORM.EnvelopeSpecName) = "PipelineSchemas.POEnv, PipelineSchemas, Version=1.0.0.0, Culture=nuetral, PublicKeyToken=12e5cc95621c33e8";`  
  
 詳細な例は、SDK サンプルを参照してください。[アグリゲーター (BizTalk Server サンプル)](../core/aggregator-biztalk-server-sample.md)します。  
  
## <a name="pipeline-execution---behavioral-differences"></a>パイプラインの実行の動作の違い  
 送信パイプラインや受信パイプラインは、オーケストレーションによって呼び出された場合も、メッセージング インフラストラクチャ内 (受信場所や送信ポート) で実行された場合とほとんど同じように実行されます。  ただし、次に示すような動作の違いもあります。  
  
### <a name="differences-within-pipeline-stages"></a>パイプラインのステージ内の違い  
 送信パイプラインや受信パイプラインのステージは、パイプラインがオーケストレーションから呼び出された場合も、パイプラインが BizTalk メッセージング インフラストラクチャから呼び出された場合とほとんど同じように実行されますが、次に示すような例外もあります。  
  
-   アセンブラー/逆アセンブラー: アセンブラーおよび逆アセンブラー ステージは処理されません**追跡プロファイルの**データ。  
  
-   エンコーダー/デコーダー: MIME エンコーダーが、ホストが関連付けられているホストで構成された証明書を使用してメッセージがデジタル署名します。  SMIME エンコーダーでは、パイプラインに渡されたメッセージのコンテキストの証明書を使用してメッセージが暗号化されます。  
  
### <a name="schema-resolution"></a>スキーマの解決  
 オーケストレーションからパイプラインを実行する際には、次の 2 つのスキーマ検索アルゴリズムがサポートされます。  
  
- 種類による解決  
  
- 名前による解決  
  
  重複するスキーマが展開されていた場合に適切なスキーマを選択するアルゴリズムのロジックは、メッセージング インフラストラクチャのコンテキストで実行された場合に使用されるものと同じです。  
  
### <a name="transactional-pipelines"></a>トランザクション パイプライン  
 トランザクション コンポーネントを呼び出すステージがあるパイプラインでは、トランザクション コンテキストを使用できません。  すべての呼び出しに**IPipelineContext.GetTransaction()** がスローされます**NotSupportedException**します。  このようなパイプラインをオーケストレーションから実行できないわけではありませんが、パイプラインでこの状況を検出して処理する必要があります。  
  
### <a name="message-destination"></a>メッセージ送信先  
 パイプライン コンポーネントによるメッセージ送信先の制御は、このコンテキストではサポートされません。  コンテキスト プロパティを設定**MessageDestination**または**SuspendOnRoutingFailure**により、 **XLANGPipelineManagerException**がスローされます。  
  
### <a name="pipeline-component-types"></a>パイプライン コンポーネントの種類  
 オーケストレーションから呼び出すには、パイプライン コンポーネントが次のいずれかに基づいている必要があります。  
  
-   NET Framework Version 1.1  
  
-   NET Framework Version 2.0  
  
-   .NET Framework Version 3.0  
  
-   .NET Framework Version 3.5  
  
-   .NET Framework Version 4.0  
  
-   NET Framework Version 2.0  
  
-   COM (COM)  
  
## <a name="restrictions"></a>制限  
 次の種類のパイプライン**できません**オーケストレーション内から実行します。  
  
- トランザクション パイプライン  
  
- 回復可能パイプライン。  
  
- BAM インターセプター API を呼び出すパイプライン (、 **NotSupportedException**がスローされます)。  
  
- 同じパイプライン インスタンスを並列図形の別の分岐で実行することはできません (すべての分岐で同期されたスコープに配置されている場合を除く)。  
  
- [!INCLUDE[btsBizTalkServer2006](../includes/btsbiztalkserver2006-md.md)] SDK でビルドされた既存のパイプライン (アセンブリ)。  
  
## <a name="failure-modes-and-effects"></a>エラー モードと結果  
 パイプラインの実行で、BizTalk Server メッセージング インフラストラクチャから呼び出された場合はメッセージを保留するようなエラーが発生した場合、代わりに例外がスローされます。  スローされる例外は、型の**Microsoft.XLANGs.Pipeline.XLANGPipelineManagerException**します。  この例外は、呼び出し元オーケストレーションの catch ブロックで処理できます。  スローされた例外がオーケストレーションでキャッチされなかった場合は、XLANG エンジンがエラーを報告します。このエラーのテキストには、スローされた例外の情報が含まれています。  
  
 この例外は、パイプライン コンポーネントによって生成されたエラー メッセージの書式設定を実行します。  
  
 **メッセージ**のプロパティ、 **XLANGPipelineManagerException**クラスには、パイプラインの実行エラーの詳細が含まれています。 詳細は次のような形式になっています。  
  
- パイプラインの実行中にエラーが発生しました\<型をパイプライン\>します。  エラーの詳細\<形式のエラー メッセージ\>します。  
  
  このメッセージの\<パイプラインの種類\>パイプライン クラスの名前を指定し、\<形式のエラー メッセージ\>パイプラインの実行中に発生した特定のエラーの説明を示します。  
  
  たとえば、オーケストレーションが受信パイプラインを呼び出すし、パイプラインのコンポーネントのいずれも、メッセージの値が認識されるため、パイプラインの実行が失敗した場合、 **XLANGPipelineManagerException**のプロパティにはなります。  
  
|XLANGPipelineManagerException のプロパティ|値|  
|--------------------------------------------|-----------|  
|メッセージ|受信パイプラインの実行エラーです "MyPipelines.ReceivePipeline"。 エラーの詳細:"逆アセンブル ステージのコンポーネントはデータを認識できません。|  
|コンポーネント|String.Empty|  
  
 オーケストレーションが送信パイプラインを呼び出すし、検証エラー、内のテキストがあるために、パイプラインの実行が失敗した場合、別の例として、**メッセージ**プロパティの**XLANGPipelineManagerException**になります。  
  
|XLANGPipelineManagerException のプロパティ|値|  
|--------------------------------------------|-----------|  
|メッセージ|送信パイプライン "MyPipelines.SendPipeline" を実行中にエラーが発生しました。  エラーの詳細:"ドキュメントの検証に失敗しました:"、\<要素名\>要素が無効です - 値\<要素値\>datatype 'String' - Pattern 制約が失敗しました無効です""。|  
|コンポーネント|“Microsoft.BizTalk.Component.XmlValidator”|