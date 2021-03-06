---
title: メッセージのルーティングを使用して失敗しました |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- bts10.ops.tsroutingfailure
ms.assetid: d081934c-600e-44ce-8ba4-fb646d494589
caps.latest.revision: 33
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d5c3f4fa3b978775c9f2c8fa91467b88cc74eae8
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36976571"
---
# <a name="using-failed-message-routing"></a>失敗したメッセージのルーティングの使用
エラー処理機能を使用すると、設計者は、失敗したメッセージを保留キューに配置する従来の処理 (現在では、既定の処理) の代わりに、失敗したメッセージの自動処理を指定できます。 この自動処理では、サブスクライブしているルーティング先 (送信ポートやオーケストレーションなど) にエラー メッセージをルーティングします。 エラー メッセージは、元のメッセージのクローンであり、以前昇格させたすべてのプロパティが降格されています。また、特定のメッセージの失敗に関連した、選択済みのプロパティがメッセージ コンテキストに昇格されています。  
  
> [!WARNING]
>  失敗したメッセージには、元のメッセージのコピーが含まれます。 元のメッセージに重要な情報が含まれる場合、重要な情報が誤って開示されることを防ぐように、失敗したメッセージの手動プロセスおよび自動プロセスをデザインしてください。  
  
## <a name="what-does-failed-message-routing-consist-of"></a>失敗したメッセージのルーティングの構成要素  
 失敗したメッセージのルーティングが有効になっていると、BizTalk Server では、メッセージを保留せずに、メッセージをルーティングします。 失敗したメッセージのルーティングは、受信ポートおよび送信ポートで使用できます。結果は次のようになります。  
  
- 失敗したメッセージのルーティングが受信ポートに対して有効になっており、受信パイプラインまたはルーティングでメッセージが失敗した場合、失敗したメッセージが生成されます。 逆アセンブリ フェーズ中 (または前) にエラーが発生した場合、エラー メッセージは、元のインターチェンジのクローンになります。  
  
- 失敗したメッセージのルーティングが送信ポートに対して有効になっており、送信パイプラインでメッセージが失敗した場合、失敗したメッセージが生成されます。  
  
  失敗したメッセージが生成されると、失敗したメッセージが公開される前に、BizTalk Server は、エラー報告に関連するメッセージ コンテキスト プロパティを昇格し、通常のメッセージ コンテキスト プロパティを降格します。 失敗したメッセージのルーティングが無効な場合の既定の処理では、失敗したメッセージが保留されませんが、ルーティングが有効な場合の処理では、失敗したメッセージが保留されることに注意してください。  
  
## <a name="what-kinds-of-messaging-failures-trigger-an-error-message"></a>エラー メッセージの発生原因となるメッセージの失敗  
 アダプター処理、パイプライン処理、マッピング、またはメッセージのルーティングでエラーが発生した場合、失敗したメッセージのルーティングが有効になっていれば、エラー メッセージが生成されます。 オーケストレーションが受信ポートからメッセージを受信しているとき (または、送信ポートにメッセージを送信しているとき) にメッセージ エラーが発生した場合、生成されるエラー メッセージは、オーケストレーションがバインドしているメッセージ ポートに関連付けられます。  
  
## <a name="subscribing-to-an-error-message"></a>エラー メッセージのサブスクライブ  
 エラー メッセージは、受信用にサブスクライブしているオーケストレーションまたは送信ポートに配信されます。 通常、サブスクリプションは、メッセージ エラーが発生したポート (送信ポートまたは受信ポート) の名前に基づいて、エラー メッセージを選択します。 また、サブスクリプションは、エラーが発生したメッセージ コンテキストに昇格させる他のプロパティ ( **InboundTransportLocation** や **FailureCode**など) に対して、フィルターを設定できます。  
  
## <a name="error-message-specification"></a>エラー メッセージの仕様  
 エラー メッセージは、失敗した元のメッセージのクローンであり、以前昇格させたすべてのプロパティが降格されています。また、エラー固有のプロパティ セットがメッセージ コンテキストに昇格されています。 エラー メッセージの受信を指定していないサブスクライバーへの予期しない配信を防止するため、以前昇格させたプロパティは降格されます。 エラー メッセージは、サブスクライバー (オーケストレーション、送信ポート、および送信ポート グループ) への配信のために公開されます。  
  
 すべてのエラー メッセージのコンテキストに昇格されるプロパティ、 **ErrorReport** BizTalk Server で名前空間。 次のようなプロパティがあります。  
  
|プロパティ名|データ型|昇格|説明|  
|-------------------|---------------|--------------|-----------------|  
|FailureCode|System.String|はい|エラー コードです。 BizTalk Server 管理コンソールに表示される 16 進数の値です。|  
|FailureCategory|System.Int32|はい|このプロパティは使用されません。 値は未定義です。|  
|説明|System.String|いいえ|エラーの説明です。 このメッセージの失敗に関してアプリケーション イベント ログに書き込まれる診断テキストと同じです。|  
|[MessageType]|System.String|はい|失敗したメッセージの種類です。メッセージの種類を確定できない場合は空です。<br /><br /> BizTalk Server は、メッセージの種類を使用して、メッセージを XML スキーマに関連付けます。 メッセージの種類は、スキーマのルート ノードを持つスキーマ名前空間を連結して形成されます: http://mynamespace#rootnode します。 **注:** メッセージ失敗メッセージの種類を決定する前にこのプロパティがないことを設定します。|  
|ReceivePortName|System.String|受信ポートでの受信処理中にエラーが発生した場合は **"昇格しました"** <br /><br /> 送信ポートでエラーが発生した場合は **"昇格していません"** |エラーが発生した場合の受信ポートの名前です。|  
|InboundTransportLocation|System.String|受信ポートでの受信処理中にエラーが発生した場合は **"昇格しました"** <br /><br /> 送信ポートでエラーが発生した場合は **"昇格していません"** |エラーが発生した場合の受信場所の URI です。|  
|SendPortName|System.String|送信ポートでの送信処理中にエラーが発生した場合は **"昇格しました"** <br /><br /> 受信ポートでエラーが発生した場合は **"昇格していません"** |エラーが発生した場合の送信ポートの名前です。|  
|OutboundTransportLocation|System.String|送信ポートでの送信処理中にエラーが発生した場合は **"昇格しました"** <br /><br /> 受信ポートでエラーが発生した場合は **"昇格していません"** |エラーが発生した場合の送信場所の URI です。|  
|ErrorType|System.String|はい|エラーに含まれるメッセージの種類を示します。 このプロパティは、常に **FailedMessage**値を含みます。つまり、失敗した元のメッセージがエラーに格納されます。|  
|RoutingFailureReportID|System.String|はい|このプロパティは、ルーティングのエラーが発生した際に BizTalk Server が生成するルーティング エラー報告の ID を提供します。 ルーティング エラー報告は、BizTalk Server が生成して保留する特殊なメッセージです。 このメッセージには、本文がありません。ただし、失敗したメッセージのコンテキストが含まれています。 この ID を使用することにより、エラーを処理するオーケストレーションや送信ポートは、メッセージ ボックス データベースに対してクエリを実行し、ルーティング エラー報告を処理します。 たとえば、失敗したメッセージを取得した後に、オーケストレーションがルーティング エラー報告を終了させる場合などに、この ID が使用されます。|  
  
## <a name="handling-error-messages"></a>エラー メッセージの処理  
 オーケストレーションまたは送信ポートのサブスクリプションのフィルターが、エラー メッセージのメッセージ コンテキストへ昇格させたプロパティに一致した場合に、エラー処理が指定されます。  
  
## <a name="security-implications"></a>セキュリティの影響  
 元のメッセージに関連付けられている ID (受信パイプラインのパーティの解決ステージで決められた最初の ID または最後の ID) は、エラー メッセージに割り当てられます。  
  
 サブスクライブの対象となる、認証されたポートおよびオーケストレーションへのメッセージ配信を制限するセキュリティ メカニズムも、エラー メッセージに適用されます。  
  
 エラー メッセージにサブスクライブする送信ポートが適切な解読証明書を使用して構成されていない場合は、エラー メッセージを受信しません。このエラー メッセージは、BizTalk Server で元のメッセージを受信したときに使用した受信パイプラインの、復号化ステージ中 (または前) に発生したメッセージ エラーによって生成されます。 エラー メッセージが受信されなかった場合、失敗したメッセージは、保留キューに配置されます。  
  
## <a name="adapter-messaging-failure"></a>アダプターのメッセージ エラー  
 アダプターがメッセージを保留すると、エラー メッセージが生成されます。 メッセージを保留しないと、エラー メッセージは生成されません。  
  
## <a name="transactional-receive-pipelines"></a>トランザクション受信パイプライン  
 トランザクション受信パイプラインが例外をスローすると (トランザクションを中止する必要がある場合に指定する)、トランザクションが中止され、エラー メッセージが生成されます。  
  
 トランザクション受信パイプラインが明示的にメッセージを中断すると (MessageDestination = SuspendQueue を指定する)、現在のトランザクションを続行して (後続のステージで中止が指定されている場合を除いてコミットされる可能性がある)、エラー メッセージが生成されます。  
  
## <a name="solicit-response-send-ports"></a>送信請求 - 応答の送信ポート  
 オーケストレーションからの要求メッセージの送信またはその応答の受信処理に失敗した場合、失敗したメッセージがルーティングされているかどうかに関係なく、オーケストレーションは例外を取得します。  
  
 送信請求 - 応答の送信ポートが要求 - 応答の受信ポートに接続されている場合、受信ポートは、失敗したメッセージがルーティングされているかどうかに関係なく、応答メッセージ (送信が成功した場合) または NACK (送信が失敗した場合) を取得します。  
  
## <a name="one-way-send-ports"></a>一方向の送信ポート  
 配信通知のために構成された送信ポートを通じてメッセージをオーケストレーションから送信する場合、エラー メッセージがルーティングされているかどうかに関係なく、オーケストレーションは配信通知を受け取ります。 つまり、送信ポートは、処理中にポートでメッセージ エラーが発生しても、オーケストレーションに対して配信通知を生成します。 通知では、ポートへの配信を確認しますが、ポートを通じた正常な処理は扱いません。  
  
## <a name="resuming-suspended-messages"></a>保留されたメッセージの再開  
 受信処理 (受信アダプターからの処理および受信アダプターを含む処理。ただし、メッセージ ボックスへのパブリケーションを含まない) に失敗したが、エラー処理されていないメッセージのほとんどは、再開可能な状態で保留されます。 双方向の受信ポートからのメッセージを要求する例外は、再開不可として保留されます。  
  
 通常、メッセージは、元の形式 (パイプライン処理の前の状態) で保留されます。ただし、例外が 2 つあります。  
  
-   **パイプライン コンポーネントによって保留されたメッセージ。** BizTalk Server は、失敗したパイプライン コンポーネントにメッセージが提供されたときと同じ形式で、この種類のメッセージを保留します。 メッセージを再開すると、パイプラインの最初からパイプライン処理が行われます。 このため、元のエラーが発生したステージの前のパイプライン ステージにおけるパイプライン コンポーネントを準備して、メッセージを最初に処理したときとは異なる形式で "同じ" メッセージを処理する必要があります。  
  
-   **回復可能なメッセージはインターチェンジ逆アセンブリ、その後のルーティングに失敗しました。** BizTalk Server は、メッセージが公開されたときと同じ形式で、この種類のメッセージを保留します。 これは、パイプラインの実行 **後** のメッセージの形式です。 メッセージを再開すると、パイプライン処理がスキップされ、メッセージ ボックス データベースに直接メッセージが公開されます。  
  
## <a name="scenarios-leading-to-suspended-non-resumable-messages"></a>中断 (再開不可) メッセージに至るシナリオ  
 メッセージが中断されたとき、多くの場合メッセージは再開可能ですが、再開不可となることもあります。このシナリオは次のとおりです。  
  
-   エラー時に続行するよう構成された順次配送送信ポートで、パイプライン、マッピング、または送信のエラーが発生した場合。  
  
-   順次配送受信ポートで、エラー発生時に再開不可としてメッセージを中断するようアダプターが構成されている場合。 たとえば、MSMQ アダプターで "エラー時" が "中断 (再開不可)" に設定されている場合、または MQSeries アダプターで "再開不可として保留" が有効になっている場合は、エラーが発生したメッセージは再開不可として中断されます。  
  
-   双方向受信ポートで、応答メッセージに、パイプライン、マッピング、または送信のエラーが発生した場合。  
  
-   双方向受信ポートで、受信メッセージに、パイプライン、マッピング、または送信のエラーが発生した場合。 アダプターによって動作は異なる可能性があります。 たとえば HTTP アダプターの場合、既定ではメッセージは中断されませんが、中断するよう構成することもできます。  
  
## <a name="see-also"></a>参照  
 [エラー処理](../core/error-handling.md)   
 [受信確認の使用](../core/using-acknowledgments.md)   
 [メッセージの順次配送](../core/ordered-delivery-of-messages.md)