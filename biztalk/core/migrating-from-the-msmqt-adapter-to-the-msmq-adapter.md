---
title: "MSMQT アダプターから MSMQ アダプターへの移行 |Microsoft ドキュメント"
ms.custom: 
ms.date: 2015-12-07
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- performance, MSMQT adapters
- scaling, MSMQT adapters
- reliability, MSMQT adapters
- MSMQT adapters, transactional consistency
- migrating, MSMQT adapters
- MSMQT adapters, ordered delivery
- MSMQT adapters, migrating to MSMQ adapters
- MSMQT adapters, scaling
- MSMQT adapters, reliability
- MSMQ adapters, migrating MSMQT adapters
- high availability, MSMQT adapters
- MSMQT adapters, performance
- MSMQT adapters, availability
ms.assetid: 97126f70-0be5-4a2f-bcba-173fd932b6de
caps.latest.revision: "30"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 2b1fce448788a8c6c5721403dbb7e4e58609a31a
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="migrating-from-the-msmqt-adapter-to-the-msmq-adapter"></a>MSMQT アダプターから MSMQ アダプターへの移行
このトピックでは、ソリューションを BizTalk メッセージ キュー (MSMQT) アダプターからメッセージ キュー (MSMQ) アダプターに移行する前に、エンド ツー エンドの順次配送、トランザクションの一貫性、高可用性、およびスケーラビリティに関して考慮すべき事項について説明します。 このトピックでは、順次配送、トランザクションの一貫性、高可用性、およびスケーラビリティを次のように定義しています。  
  
-   **順次配送します。** 受信時と同じ順序で BizTalk Server からメッセージが送信されるようにすること。  
  
-   **トランザクションの一貫性。** 処理中のメッセージが、ハードウェア、ソフトウェア、またはネットワークの障害によって、損失したり重複しないようにすること。  
  
-   **高可用性です。** メッセージの処理に必要なサービスが常時利用できるようにすること。  
  
-   **スケーラビリティです。** 既存のメッセージ処理能力を拡大できること。  
  
## <a name="end-to-end-ordered-delivery"></a>エンド ツー エンドの順次配送  
 MSMQT アダプターでは、メッセージのエンド ツー エンドの順次配送が保証されます。 つまり、MSMQ アプリケーションは、MSMQT アダプターにバインドされた受信場所に 1、2、および 3 のメッセージを送信する場合、これらのメッセージをオーケストレーションに配信されるまたは送信ポートを同じ順序で BizTalk Server に: 1、2、3 つです。 この機能は、受信されたとき同じ順序で送信および実行する必要がある、株式市場の取り引きなどに使用できます。  
  
 MSMQT アダプターによるエンド ツー エンドの順次配送では、多数のコンポーネントが連動する必要があります。 MSMQT アダプターでは、順次配送を実現するために次のような一連のイベントが発生します。  
  
1.  リモート コンピューターの MSMQ API では、メッセージをメッセージ 1、メッセージ 2、メッセージ 3 の順で受信し、これらのメッセージをローカルのトランザクション キューに同じ順序 (1、2、3 の順) でプッシュします。  
  
2.  リモート コンピューターの MSMQ クライアントでは、キューからメッセージを取得し、MSMQT キューに 1、2、3 の順で送信します。  
  
3.  MSMQT アダプターでは、1、2、3 の順でメッセージを受信し、BizTalk メッセージ エージェント コンポーネントに同じ順序で渡します。  
  
4.  BizTalk メッセージ エージェント コンポーネントでは、メッセージを 1、2、3 の順でメッセージ ボックス データベースに送信します。  
  
5.  メッセージ ボックス データベースでは、メッセージをルーティングして、メッセージがオーケストレーションまたは送信ポートの同じインスタンスにルーティングされた場合に、メッセージが同じ順序 (1、2、3 の順) でインスタンスに配信されるようにします。  
  
 [!INCLUDE[btsBizTalkServer2004](../includes/btsbiztalkserver2004-md.md)] では、MSMQT アダプターでのみエンド ツー エンドの順次配送が保証されます。 他の統合 BizTalk アダプターでは、上記の手順 3. ～ 5. でメッセージの順序が入れ替わる可能性があります。 他の多くの統合アダプターでは、手順 3. でエンド ポイント マネージャーという名前のコンポーネントが使用されますが、このコンポーネントは、マルチスレッド化されているので、メッセージの順序が維持されません。 [!INCLUDE[btsBizTalkServer2004](../includes/btsbiztalkserver2004-md.md)] の MSMQ アダプターでは、"シリアル処理" 機能を使用して手順 3. のメッセージの順序を維持することはできますが、メッセージ エージェント コンポーネントに送信するメッセージの順序を維持するように指示しないため、メッセージがオーケストレーションまたは送信ポートに同じ順序でルーティングされない場合があります。  
  
 **エンド ツー エンドの MSMQ アダプターで順次配送**  
  
 エンド ツー エンドの MSMQ アダプターで順次配送を実現するためには、次の手順を実行します。  
  
1.  有効にする、**順次配送**受信側のプロパティは、サブスクライブするオーケストレーションのポートまたは送信ポート。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]オーケストレーションの受信ポートと送信ポートが設定されて、**順次配送**構成オプション。 このオプションを有効にすると、オーケストレーションの受信ポートまたは送信ポートでは、メッセージ ボックス データベースに対して、データベースで受信したときと同じ順序でメッセージを配信するように指定することができます。  
  
2.  設定、**順次処理**MSMQ アダプターにバインドされている受信場所のプロパティ`True`です。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、MSMQ トランスポートを使用する受信場所で順次処理が使用されるように構成することができます。このオプションを有効にすると、メッセージ ボックス データベースには、受信時と同じ順序でメッセージが配信されます。  
  
3.  設定、**トランザクション**MSMQ アダプターにバインドされている受信場所のプロパティ`True`です。  
  
4.  MSMQ 受信場所で監視されている MSMQ キューが "トランザクション" とマークされていることを確認します。 メッセージの順次配送を実現するには、このプロパティが MSMQ キューに設定されている必要があります。  
  
> [!NOTE]
>  順次配送は、BizTalk 受信場所で監視されている MSMQ キューが 1 台のコンピューターで処理されている場合にのみ保証されます。 このことは、このトピックの後半で説明するように、スケーラビリティの問題となることがあります。  
  
## <a name="transaction-usage-when-processing-messages-with-the-msmqt-adapter-vs-the-msmq-adapter"></a>MSMQT アダプターと MSMQ アダプターの、メッセージ処理におけるトランザクション使用の比較  
 MSMQT アダプターと MSMQ アダプターによるメッセージの処理方法は、トランザクションの使用に関して大きく異なります。  
  
 MSMQT アダプターを使用すると、ネットワークから受信したメッセージの処理と、受信したメッセージの BizTalk Server による処理は単一のトランザクションで行われます。 また、BizTalk Server により、送信者に対して ACK メッセージが生成され、メッセージが受信され正常に処理されたことが通知されます。  
  
 MSMQ アダプターを使用すると、ネットワークから受信したメッセージの処理と、受信したメッセージの BizTalk Server による処理は個別の 2 つのトランザクションで行われます。1 つのトランザクションではネットワークから受信したメッセージを処理し、もう 1 つのトランザクションでは、BizTalk Server によるメッセージの処理が行われます。 また、送信者に対して ACK メッセージが生成されますが、これはネットワークからメッセージを正常に受け取ったことを示すもので、メッセージが BizTalk Server によって正常に処理されたことを示すものではありません。 Microsoft メッセージ キュー サーバーでは、BizTalk Server がインストールされているかどうかに関係なく、ネットワークからメッセージを受信し、ローカルの MSMQ キューにメッセージを保存すると、送信者に ACK メッセージを送信します。 メッセージが MSMQ キューに保存されると、BizTalk MSMQ アダプターではメッセージを取得して処理し、メッセージ ボックス データベースに公開します。 この処理でエラーが発生すると、メッセージは BizTalk Server の保留キューに送信されるか、(トランザクション処理を使用している場合は) ローカルの MSMQ キューに残ったままになり、送信者には BizTalk Server でのメッセージ処理に失敗したことは通知されません。  
  
 BizTalk Server でメッセージが正常に処理されたときに ACK を受信する必要がある場合、MSMQT アダプターから MSMQ アダプターに移行する際にはアプリケーション レベルの ACK を追加する必要があります。 また、オーケストレーションとメッセージを送信するアプリケーションを更新して、アプリケーション レベルの ACK を実装する必要があります。  
  
## <a name="high-availability-transactional-in-order"></a>高可用性 (トランザクション、順次)  
 MSMQT アダプターの高可用性を実現するには、受信ホストに複数のコンピューターを追加し、フォールト トレランスのネットワーク負荷分散 (NLB) を構成または既定の BizTalk ホストをクラスター化することができます。 NLB を構成した環境で MSMQT アダプターを実行している場合、1 台のサーバーがダウンしても、そのサーバーの負荷は残りのサーバーで処理されます。 クラスター化したホストで MSMQT アダプター ハンドラーを実行している場合、いずれかのホスト ノードで障害が発生しても、クラスター化されたホストは、クラスター ソフトウェアにより他のノードにフェールオーバーされます。 MSMQ アダプターを使用している場合、MSMQ アダプターでは中間ストレージとしてローカルの MSMQ キューが使用されるため、データ損失が発生しないトランザクション処理が必要な場合、NLB は機能しません。 このシナリオでは、コンピューターで障害が発生すると、ローカルの MSMQ キューに配信されていて、MSMQ アダプターで処理されていないメッセージは失われます。  
  
 MSMQ アダプターで高可用性とトランザクションの一貫性を提供するには、次の操作を行う必要があります。  
  
1.  BizTalk Server の Windows Server クラスター グループのクラスター化されたリソースとして、Microsoft メッセージ キュー (MSMQ) を構成します。  
  
2.  クラスター化された MSMQ リソースと同じクラスター グループ内のクラスター リソースとして構成されている BizTalk ホスト インスタンスで、MSMQ アダプターの受信ハンドラーを構成します。  
  
3.  クラスター化された MSMQ リソースで依存関係が維持されるように、BizTalk ホスト インスタンスのクラスター リソースを構成します。  
  
 このアーキテクチャで順次配送を実装するには、「--エンドツー エンド MSMQ アダプターで順次配送します」前に示した手順に従います  
  
## <a name="high-availability-nontransactional-not-in-order"></a>高可用性 (非トランザクション、非順次)  
 高可用性が必要でも、トランザクション処理を必要としない場合があります。このような場合には、MSMQ アダプターを使用し、NLB を実装して、NLB に含まれる複数の BizTalk Server コンピューターで MSMQ 送信ハンドラーと受信ハンドラーを構成したホスト インスタンスを実行することによって高可用性を実現できます。 MSMQ で NLB を実装するときにする必要がありますベスト プラクティスに従って Microsoft サポート技術情報の資料 899611 に記載されている"ネットワーク経由でメッセージ キューが機能する方法の負荷分散 (NLB)"で使用可能な[http://go.microsoft.com/fwlink/?LinkId = 57510](http://go.microsoft.com/fwlink/?LinkId=57510)です。 このシナリオでは、いずれかの BizTalk Server コンピューターで障害が発生すると、その BizTalk Server のホスト インスタンスで実行されているメッセージは、BizTalk Server コンピューターが復旧するまで利用できません。 この構成では、利用できない BizTalk Server コンピューターがあると、NLB により要求が他の BizTalk Server コンピューターにルーティングされるので、高可用性を実現できます。  
  
## <a name="scalability-nontransactional-not-in-order"></a>スケーラビリティ (非トランザクション、非順次)  
 スケーラビリティは、高可用性 (非トランザクション) のガイドラインに従い、ホスト インスタンスを追加することで実現できます。 このアーキテクチャでは、高速な配信とスケーラビリティを実現できますが、順次配送は実現できません。  
  
## <a name="scalability-transactional-not-in-order"></a>スケーラビリティ (トランザクション、非順次)  
 配信順序を問わないメッセージのトランザクション配信を実現するには、NLB を MSMQ および Windows クラスタリングと組み合わせて使用できます。 このアーキテクチャでは、Windows クラスターごとに「高可用性 (トランザクション、順次)」の手順に従って、2 つの個別の Windows クラスター環境に、少なくとも 2 つのクラスター グループを構成する必要があります。 その後、NLB を実装すると、クラスター グループ間で負荷を分散できるようになります。 Windows NLB は Windows クラスターでの実行がサポートされていないため、このシナリオではハードウェア NLB ソリューションが必要です。 次の図に、このアーキテクチャを示します。  
  
 ![クラスター グループ間の負荷分散](../core/media/scaleclusteredmsmqwithnlb.gif "ScaleClusteredMSMQwithNLB")  
  
> [!NOTE]
>  このアーキテクチャでは順次配送は実現されません。  
  
## <a name="scalability-transactional-in-order"></a>スケーラビリティ (トランザクション、順次)  
 MSMQ 3.0 以前を使用している場合、高可用性、トランザクションの一貫性、および順次配送を提供するアーキテクチャのスケール アウトには問題があります。これは、BizTalk Server コンピューターとリモート MSMQ サーバーの両方で MSMQ 4.0 を実行していない限り、リモートのトランザクションの読み込みがサポートされていないためです。 MSMQ 3.0 以前を使用する場合、スケール アウトは複数のローカル MSMQ キューを使用して行う必要があります。 さらに、このシナリオでは、NLB への MSMQ セッションの TCP/IP 接続が切断されると、NLB によって別のコンピューターに復元されることがあり、このことが原因でメッセージが正しい順序で配信されなくなることがあります。  
  
 この制限を回避する手段の 1 つとしては、送信先キューを別のコンピューターに割り当てることによって、メッセージ配信の負荷分散を手動で行う方法があります。 これは、特定の BizTalk ホスト インスタンスを特定の MSMQ キューに関連付けることによって行えます。 たとえば、ある特定の取り引き先から大量のドキュメントを受信する場合、特定の BizTalk Server コンピューターに、この取引先専用の個別のホストと受信キューを作成します。  
  
 可能ならば、リモート トランザクションの読み込みと負荷分散が必要な場合は、リモート コンピューターで MSMQ 4.0 を実行します。  
  
## <a name="summary"></a>概要  
 次の表に、特定の機能を実現するために実装するアーキテクチャの概要を示します。  
  
|**機能**|**NLB でもクラスター**|**NLB**|**Cluster**|**NLB とクラスター**|  
|-----------------------|---------------------------------|-------------|-----------------|-------------------------|  
|エンド ツー エンドの順次配送|はい|いいえ|はい|可 (手動による構成が必要です)|  
|トランザクションの一貫性|不可 (サービスでエラーが発生すると、メッセージが損失または重複することがあります)|不可|はい|はい|  
|高可用性|不可|はい|可|はい|  
|スケーラブルです|不可|可|いいえ|はい|  
  
## <a name="see-also"></a>参照  
 [Windows Server クラスターを使用して BizTalk Server Hosts2 の高可用性を実現するには](../core/use-windows-cluster-to-provide-high-availability-for-biztalk-hosts.md)