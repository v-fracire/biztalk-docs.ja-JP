---
title: メッセージ コンテキスト プロパティを使用する方法 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- orchestrations, building
- building, insufficient configuration
ms.assetid: 6ca95017-74e0-42d7-befa-93e0c1e1ecd1
caps.latest.revision: 16
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 084eae49777b62b190e8e090c0b1045d301d420b
ms.sourcegitcommit: 5abd0ed3f9e4858ffaaec5481bfa8878595e95f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2017
ms.locfileid: "25975320"
---
# <a name="how-to-use-message-context-properties"></a>メッセージ コンテキストのプロパティの使用方法
システム プロパティとは、BizTalk メッセージング エンジンとそのコンポーネントによって主に内部で使用されるプロパティです。 一般的に、これらのプロパティのエンジンによって設定されている値を変更することは、エンジンの実行ロジックに影響を与えるため推奨されません。 ただし、変更できるプロパティは数多くあります。  
  
 次の表に、メッセージング エンジンによって昇格可能なメッセージ コンテキストのプロパティの一覧を示します。 これらのプロパティを使用して、Microsoft [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] で送信ポートやオーケストレーションのフィルター式を作成できます。 例を次に示します。  
  
```  
PortName = MyMessage(BTS.ReceivePortName);  
MyFileName = MyMessage(BTS.ReceivedFileName);  
MySubject= MyMessage(POP3.Subject);  
```  
  
 別の表に、一部の BizTalk アプリケーションで使用できる追加のプロパティを示します。これらは昇格できません。  
  
|プロパティ|昇格のタイミングと場所|型|Description|  
|--------------|-----------------------------------|----------|-----------------|  
|BTS.AckFailureCategory|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:int|識別、 **ErrorCategory**場所と中断理由を提供します。|  
|BTS.AckFailureCode|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:string|識別、 **ErrorCode**場所と中断理由を提供します。|  
|BTS.AckID|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:string|識別、 **MessageID**元のメッセージ。|  
|BTS.AckInboundTransportLocation|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:string|識別、 **InboundTransportLocation**元のメッセージ。|  
|BTS.AckOutboundTransportLocation|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:string|識別、 **OutboundTransportLocation**元のメッセージ。|  
|BTS.AckOwnerID|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:string|元のメッセージからインスタンス ID を識別します。|  
|BTS.AckReceivePortID|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:string|識別、 **ReceivePortID**元のメッセージ。|  
|BTS.AckReceivePortName|受信確認メッセージのメッセージング エンジンによって昇格されます。|xs:string|識別、 **ReceivePortName**元のメッセージ。|  
|BTS.AckSendPortID|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:string|識別、 **SendPortID**元のメッセージ。|  
|BTS.AckSendPortName|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:string|識別、 **SendPortName**元のメッセージ。|  
|BTS.AckType|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:string|オーケストレーションにより受信確認と未受信を監視できます。 受信確認の値は ACK、否定受信確認の値は NACK になります。|  
|BTS.ActionOnFailure|このプロパティは、IBTTTransportBatch::SubmitMessage() API を呼び出して BizTalk にメッセージを送信する前にアダプターによって設定できます。|xs:int|受信パイプラインにエラーが発生した場合、メッセージング エンジンの動作を制御します。 通常、メッセージング エンジンでは失敗したメッセージが保留されますが、HTTP のような特定のアダプターは、受信パイプラインのエラー時にメッセージを保留するのではなく、エラーをクライアントに報告します。<br /><br /> 有効な値:<br /><br /> -既定値です。 プロパティが存在しない場合、メッセージング エンジンは自動的にメッセージを保留しようとします。<br />-   0. メッセージング エンジンが自動的にメッセージを保留しないことを示します。<br /><br /> 他の値は将来使用するために予約されています。|  
|BTS.CorrelationToken|このプロパティをメッセージ コンテキストに設定すると、メッセージング エンジンによって昇格されます。 このプロパティは、要求 - 応答のアダプターまたはオーケストレーションがメッセージ ボックス データベースに要求メッセージを送信する場合に、暗黙的にコンテキストに設定されます。|xs:string|要求 - 応答ポートへの応答のルーティングを有効にします。|  
|BTS.EpmRRCorrelationToken|要求 - 応答メッセージの実行時にメッセージング エンジンによって昇格されます。 プロパティは、メッセージがメッセージ ボックス データベースに送信される前に昇格されます。|xs:int|メッセージング エンジンによって内部で使用されます。 メッセージの要求応答ストリームのサーバー名、プロセス ID、および一意の GUID を指定します。|  
|BTS.InboundTransportLocation|メッセージ ボックス データベースに公開する前に、受信アダプターからメッセージを受け取った後に、メッセージング エンジンによって昇格されます。|xs:string|メッセージをハンドラーで受信する場所 (URI) を指定します。|  
|BTS.InboundTransportType|メッセージ ボックス データベースに公開する前に、受信アダプターからメッセージを受け取った後に、メッセージング エンジンによって昇格されます。|xs:string|このメッセージを受信して FILE、HTTP などのサーバーに送信したアダプターの種類を指定します。|  
|BTS.InterchangeSequenceNumber|受信アダプターからメッセージを受け取った後、メッセージ ボックス データベースに公開する前に、メッセージング エンジンによって昇格されます。|xs:int|インターチェンジのドキュメントのシーケンス番号を示します。 ドキュメントが個別のドキュメントに逆アセンブルされるインターチェンジの一部でない場合は、この値は 1 をなります。 プロパティは、オーケストレーション、送信パイプラインで読み取ることができ、アダプターを送信します。|  
|BTS.IsDynamicSend|メッセージ コンテキストで設定できます。 このプロパティは昇格されず、送信操作にのみ適用されます。|xs:boolean|送信操作が動的送信ポートを使用して行われる場合、メッセージング エンジンによって値が true に設定されメッセージ コンテキストに書き込まれます。 送信パイプラインで静的送信ポート用に動的にプロパティを設定する場合は、この値を true に設定する必要があります。|  
|BTS.MessageDestination|このプロパティは、GetNext() からメッセージが返されたときに、逆アセンブラー パイプライン コンポーネントによって受信パイプラインで設定できます。|xs:string|このプロパティは、主に逆アセンブラーの [回復可能なインターチェンジ処理] のサポートに使用され、メッセージをメッセージ ボックスに公開するか、または保留キューに入れて中断するかを制御します。 パイプラインでインターチェンジに無効なメッセージが検出された場合、メッセージを中断して処理を続行するには、MessageDestination = SuspendQueue を設定します。またこれによって、エンジンが逆アセンブラーで GetNext() を呼び出したときにメッセージを返すことができます。<br /><br /> 有効な値:<br /><br /> -既定値です。 プロパティが存在しない場合、メッセージは有効と見なされ、メッセージ ボックスに公開されます。<br />-SuspendQueue です。 メッセージング エンジンにメッセージを中断するよう指示します。 **注:** パイプライン/マッピング メッセージと、アダプター (ワイヤ メッセージなど) によって送信されるメッセージではなく、中断されたメッセージが表示されます。|  
|BTS.MessageType|メッセージ解析中に逆アセンブラー パイプライン コンポーネントによって昇格されます。|xs:string|メッセージの種類を指定します。 メッセージの種類がドキュメント スキーマの名前空間とドキュメントのルート ノードの組み合わせとして定義されている: です http://<*MyNamespace*>#<*MyRoot*> 。|  
|BTS.OutboundTransportLocation|このプロパティをメッセージ コンテキストに設定すると、メッセージング エンジンによって昇格されます。 このプロパティは、オーケストレーションが送信ポートにメッセージを送信する場合に、暗黙的にメッセージ コンテキストに設定されます。 このプロパティは、オーケストレーションまたはパイプラインで明示的に設定することもできます。|xs:string|メッセージが送信された送信先 URI を指定します。 URI など含めることはアダプター プレフィックス **http://** です。 アダプター プレフィックスは、メッセージング エンジンで、メッセージを送信するときに使用するアダプターの種類を決定するのに使用されます。 場合は、両方のアダプター プレフィックスと**BTS です。OutboundTransportType**プロパティが設定されているアダプターの種類から**BTS です。OutboundTransportType**常に、プレフィックス、アダプターの種類よりも優先されます。<br /><br /> 有効な値:<br /><br /> BizTalk メッセージ キュー: **DIRECT =**、**プライベート =**、および**パブリック =**<br /><br /> ファイル: **file://**<br /><br /> FTP: **FTP://**<br /><br /> HTTP: **http://** と**https://**<br /><br /> SMTP: **mailto:**<br /><br /> SOAP: **SOAP://**<br /><br /> SQL: **SQL://**|  
|BTS.OutboundTransportType|このプロパティをメッセージ コンテキストに設定すると、メッセージング エンジンによって昇格されます。 このプロパティは、オーケストレーションが送信ポートにメッセージを送信する場合に、暗黙的にコンテキストに設定されます。 このプロパティを設定することも明示的にオーケストレーションまたはパイプライン。|xs:string|メッセージの送信に使用するアダプターの種類を指定します。 使用可能なアダプターの種類は**ファイル**、 **FTP**、 **HTTP**、 **SMTP**、 **SOAP**、および**SQL**です。<br /><br /> このプロパティに設定される値とアドレスで指定されるアダプター プレフィックスは、大文字と小文字を区別しません。|  
|BTS.PropertiesToUpdate|再送信または中断されたエラー メッセージの一部のプロパティ値を予約する場合、アダプターによってこのプロパティが設定されます。<br /><br /> つまり、メッセージが再送信または再開された場合、指定したプロパティがコンテキストに設定されます。|xs:string|プロパティ名、名前空間、および値を表す要素を持つ XML 文字列を含んでいます。|  
|BTS.ReceivePortID|メッセージ ボックス データベースに公開する前に、受信アダプターからメッセージを受け取った後に、メッセージング エンジンによって昇格されます。|xs:int|メッセージを受信した受信ポートを特定します。|  
|BTS.ReceivePortName|メッセージ ボックス データベースに公開する前に、受信アダプターからメッセージを受け取った後に、メッセージング エンジンによって昇格されます。|xs:string|メッセージを受信した受信ポートのユーザー フレンドリ名。|  
|BTS.RouteDirectToTP|ループ バックまたは要求 - 応答の実行時のメッセージでメッセージング エンジンによって昇格されます。 プロパティは、メッセージがメッセージ ボックス データベースに送信される前に昇格されます。|xs:boolean|ループバックおよび要求 - 応答のシナリオを有効にするために、メッセージング エンジンによって内部で使用されます。|  
|BTS.SPGroupID|メッセージがオーケストレーションから送信ポートに送信されるときに、メッセージング エンジンによって昇格されます。|xs:string|送信ポート グループの ID を指定します。|  
|BTS.SPID|メッセージをオーケストレーションから送信ポートに送信したときに、メッセージング エンジンによって昇格されます。|xs:string|送信ポートの ID を指定します。|  
|BTS.SPName|送信請求 - 応答の送信ポートから応答メッセージを公開しているときに、メッセージング エンジンによって昇格されます。|xs:string|送信請求 - 応答の送信ポートからの応答メッセージをサブスクライブするために使用します。 値は送信ポートの名前です。|  
|BTS.SPTransportBackupID|メッセージがオーケストレーションから送信ポートに送信されるときに、メッセージング エンジンによって昇格されます。|xs:string|送信ポートのバックアップ アダプターの ID を指定します。|  
|BTS.SPTransportID|メッセージがオーケストレーションから送信ポートに送信されるときに、メッセージング エンジンによって昇格されます。|xs:string|送信ポートのプライマリ アダプターの ID を指定します。|  
|BTS.SuspendAsNonResumable|このプロパティは、SubmitMessage() を呼び出す前、またはオーケストレーションでメッセージを送信ポートに送信する前に、アダプターによって設定できます。 **注:** SubmitRequestMessage() はこのプロパティを無視; 双方向のメッセージは再開可能な常に中断されます。|xs:boolean|メッセージング エンジンでメッセージ エラー時にメッセージを再開不可として中断するかどうかを制御します。 通常、メッセージは再開可能として中断されますが、これが不適切な場合があります。たとえば、順次配送の送受信ポートのメッセージを再開すると、メッセージの順序が途切れます。<br /><br /> 有効な値:<br /><br /> 場合は false。 メッセージは再開可能として中断されます (既定)。<br />場合は true。 メッセージは再開不可として中断されます。|  
|BTS.SuspendMessageOnRoutingFailure|メッセージ ボックス データベースに公開する前に、受信アダプターからメッセージを受け取った後に、メッセージング エンジンによって昇格されます。|xs:boolean|受信メッセージにルーティング エラーが発生したときの動作を指定します。<br /><br /> 有効な値:<br /><br /> -既定値または false を指定します。 プロパティが存在しない、または False に設定されている場合、エンジンはルーティング エラーが発生したときにアダプターにエラーを通知します。<br />場合は true。 ルーティング エンジンは、ルーティング エラーが発生すると、自動的にメッセージを中断します。 **注:** パイプライン/マッピング メッセージと、アダプター (ワイヤ メッセージなど) によって送信されるメッセージではなく、中断されたメッセージが表示されます。|  
  
 この名前空間には、一部の BizTalk アプリケーションに役立つ情報を含んでいる他のプロパティが多数あります。  
  
|プロパティ|昇格のタイミングと場所|型|Description|  
|--------------|-----------------------------------|----------|-----------------|  
|BTS.AckDescription|受信確認メッセージをメッセージ ボックス データベースに公開する前に、メッセージング エンジンによって設定されます。|xs:string|識別、 **ErrorDescription**場所と中断理由を提供します。|  
|BTS.EncryptionCert|昇格できません。|xs:int|暗号化証明書に対応する拇印を特定します。 オーケストレーションまたはカスタム パイプライン コンポーネントは署名および暗号化されたメッセージを受信する要求-応答ポートで応答を暗号化するためのパイプラインで MIME/SMIME エンコーダー パイプライン コンポーネントの前に配置でこのプロパティを設定します。|  
|BTS.InterchangeID|サーバーに到着する各メッセージのメッセージング エンジンによって設定されます。|xs:string|同じインターチェンジ メッセージから生成されたドキュメントをグループ化するために使用する一意の ID を定義します。|  
|BTS.Loopback|ループバック実行の要求メッセージを送信する場合に、アダプターによって設定されます。|xs:boolean|メッセージをループバック実行のためにサーバーに送信するかどうかを定義します。 ループバック実行では、要求メッセージは、メッセージ ボックス データベースに公開され、そこで応答として受信アダプターに直接ルーティングされます。|  
|BTS.SignatureCertificate|メッセージをサーバーに送信するときに、一部のアダプターによって設定されます。 このプロパティは、パーティの解決パイプライン コンポーネントで使用されます。|xs:string|BizTalk Server が受信したメッセージの署名に使用される署名証明書の拇印を特定します。|  
|BTS.SourcePartyID|受信メッセージのパーティが特定された後で、パーティの解決パイプライン コンポーネントによって設定されます。|xs:string|BizTalk パーティの ID。|  
|BTS.SSOTicket|受信アダプターがこのプロパティをサポートする場合、メッセージをサーバーに公開するときに設定されます。|xs:string|チケットには、現在のユーザーの暗号化されたドメインとユーザー名、およびチケットの有効期限が含まれています。 チケットは、送信先エンドポイントを認証する場合にユーザーの資格情報を取得するため、SSO 対応のアダプターで使用されます。|  
|BTS.WindowsUser|メッセージをサーバーに送信するときに、一部のアダプターによって設定されます。 このプロパティは、パーティの解決パイプライン コンポーネントで使用されます。|xs:string|メッセージをサーバーに送信したユーザーのアカウントを指定します。|  
  
 パイプライン コンポーネントとアダプターに関連付けられたプロパティとプロパティ スキーマについての追加情報は、以下のトピックを参照してください。  
  
-   [ファイル アダプター プロパティ スキーマおよびプロパティ](../core/file-adapter-property-schema-and-properties.md)
  
-   [FTP アダプター プロパティ スキーマおよびプロパティ](../core/ftp-adapter-property-schema-and-properties.md)  
  
-   [HTTP アダプター プロパティ スキーマおよびプロパティ](../core/http-adapter-property-schema-and-properties.md)  
  
-   [MSMQ アダプター プロパティ スキーマおよびプロパティ](../core/msmq-adapter-property-schema-and-properties.md)  
  
-   [SMTP アダプター プロパティ スキーマおよびプロパティ](../core/smtp-adapter-property-schema-and-properties.md)  
  
-   [SOAP アダプター プロパティ スキーマおよびプロパティ](../core/soap-adapter-property-schema-and-properties.md)  
  
-   [BizTalk Framework スキーマおよびプロパティ](../core/biztalk-framework-schema-and-properties.md)  
  
-   [MQSeries アダプター プロパティ](../core/mqseries-adapter-properties.md)  
  
-   [POP3 アダプター プロパティ スキーマおよびプロパティ](../core/pop3-adapter-property-schema-and-properties.md)  
  
-   [Windows SharePoint Services アダプターのプロパティに関するリファレンス](../core/windows-sharepoint-services-adapter-properties-reference.md)  
  
-   [MIME/SMIME プロパティ スキーマおよびプロパティ](../core/mime-smime-property-schema-and-properties.md)  
  
-   [XML とフラット ファイル プロパティ スキーマおよびプロパティ](../core/xml-and-flat-file-property-schema-and-properties.md)  
  
## <a name="see-also"></a>参照  
 [BizTalk メッセージ コンテキストのプロパティについて](../core/about-biztalk-message-context-properties.md)   
 [動的ポートに値を代入する式を使用する方法](../core/how-to-use-expressions-to-assign-values-to-dynamic-ports.md)