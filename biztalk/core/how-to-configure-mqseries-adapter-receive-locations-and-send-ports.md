---
title: "アダプター受信場所と送信ポートを MQSeries を構成する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MQSeries adapters, receive ports
- receive ports, MQSeries adapters
- MQSeries adapters, send ports
- configuring [MQSeries adapters], send ports
- configuring [MQSeries adapters], receive ports
- send ports, MQSeries adapters
- configuring [MQSeries adapters], receive locations
- MQSeries adapters, receive locations
- receive locations, MQSeries adapters
ms.assetid: 552aacde-9ec0-4459-b369-073676b6f926
caps.latest.revision: "29"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9c31a15615d74a2ca1471559aa25772725821889
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-configure-mqseries-adapter-receive-locations-and-send-ports"></a>アダプター受信場所と送信ポートを MQSeries を構成する方法
MQSeries アダプターの受信場所と送信ポートを構成できます。  
  
## <a name="to-configure-receive-locations-and-send-ports"></a>構成する受信場所と送信ポート  
 **受信ポートを作成し、受信場所。**  
  
1.  BizTalk Server 管理コンソールで、次のように展開します**BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**、の順に展開し、。受信場所を作成するアプリケーション。  
  
2.  右クリックし、**受信ポート**ノード、をクリックして**新規、**  をポイントし、**一方向の受信ポート**です。  
  
3.  適切な値を入力して、**ポートのプロパティ** ダイアログ ボックス。 については、**ポートのプロパティ**ダイアログ ボックスを参照してください[受信ポートを作成する方法](../core/how-to-create-a-receive-port.md)です。  
  
4.  BizTalk Server 管理コンソールを右クリックし、**受信ポート**ノードを作成し、をクリックして**プロパティ**です。  
  
5.  **受信ポートのプロパティ**ダイアログ ボックスで、左ペインで、select、**受信場所**、クリックして**新規**右側のウィンドウでします。  
  
6.  **受信場所のプロパティ**] ダイアログ ボックスで、**トランスポート**横**型**[ **MQSeries**ドロップダウン リストから一覧で、クリックして**構成**です。  
  
7.  **MQSeries トランスポートのプロパティ** ダイアログ ボックスで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**バッチ サイズ**|メッセージの最大バッチ サイズを KB 単位で設定します。 **注:**場合、**トランザクションがサポートされている**受信場所のプロパティに設定されて**はい**; 各メッセージ バッチは、Microsoft のコンテキストでメッセージ ボックス データベースに送信分散トランザクション コーディネーター (MSDTC) トランザクション。 メッセージ バッチ用に作成された MSDTC トランザクションは、そのメッセージ バッチのすべてのメッセージがメッセージ ボックスに保存され、適切なサブスクライバー キューに置かれるまで、開いたままになります。 したがって、この MSDTC トランザクションの期間を増やしてとして、**最大バッチ サイズ**パラメーターが増加します。 多数の MSDTC トランザクションのオープンを同時に持つことができますに悪影響を与える全体的なパフォーマンスは、ので、**最大バッチ サイズ**トランザクションのサポートが有効にすると、パラメーターを非常に大きな値を設定しない必要があります。|  
    |**順次処理**|MQSeries キューからメッセージを受信するときのメッセージ順序を保存するかどうかを設定します。 **注:**特定のキューについてメッセージの順序を保つためには、BizTalk ホスト インスタンスを 1 つだけはメッセージを受信する MQSeries キューからです。 <br /><br /> **既定値:** False|  
    |**キュー**|情報が設定されます、**キュー定義** ダイアログ ボックス。 **注:**の URI を送信ポートまたは受信場所は、256 文字を超えることはできません。|  
    |**トランザクション**|アダプターは、BizTalk Server と MQSeries Server 間の Microsoft 分散トランザクション コーディネーター (DTC) トランザクションを開始します。 設定すると**いいえ**、メッセージ配信の保証はありません。<br /><br /> **既定値:** False|  
  
8.  **MQSeries トランスポートのプロパティ**ダイアログ ボックスで、をクリックして**OK**を設定する、**アドレス (URI)**ボックスに、**受信場所のプロパティ** ダイアログ ボックス。  
  
9. **受信場所のプロパティ** ダイアログ ボックスで、受信場所の構成を完了し、をクリックするには、適切な値を入力して**OK**設定を保存します。 については、**受信場所のプロパティ**ダイアログ ボックスを参照してください[受信場所を作成する方法](../core/how-to-create-a-receive-location.md)です。  
  
 **送信ポートを作成します。**  
  
1.  BizTalk Server 管理コンソールで、新しい静的送信ポートを作成します。 参照してください[送信ポートを作成する方法](../core/how-to-create-a-send-port2.md)詳細についてはします。 すべての送信ポートのオプションを構成し、指定**MQSeries**の**型**オプション、**トランスポート**のセクションで、**全般**タブです。  
  
2.  **全般**] タブの [、**トランスポート**セクションで、をクリックして、**構成**横に**型**です。  
  
3.  **MQSeries トランスポートのプロパティ** ダイアログ ボックスで、次の操作します。  
  
    |プロパティ|Description|  
    |--------------|-----------------|  
    |**フラグメント化サイズ**|アダプターと MQSAgent との間でメッセージが送信されるときのメッセージ チャンク サイズを KB 単位で設定します。|  
    |**SSO 関連アプリケーション**|シングル サインオン (SSO) 関連のアプリケーションを設定します。 ユーザー ID とパスワードを SSO から使用されます、 **MQMD_UserIdentifier**、および**MQIIH_Authenticator** (または**MQCIH_Authenticator**) プロパティそれぞれします。<br /><br /> **既定値:**空白|  
    |**データ変換**|MQSeries for Windows サーバーの ANSI コード ページにメッセージを変換します。<br /><br /> 選択**はい**Unicode から ANSI に変換を実行します。<br /><br /> **既定値:**なし|  
    |**順序付け**|MQSeries を設定して、メッセージが MQSeries キューに送信されるときのメッセージの順序を保存します。<br /><br /> 選択**はい**メッセージの順序を維持するためにします。 **注:**設定する必要があります、**配信通知**プロパティをオーケストレーションに**送信**送信ポートのです。 <br /><br /> **既定値:**なし|  
    |**キューの定義**|情報を設定、**キュー定義** ダイアログ ボックスまたはフィールドに直接できます。 **注:**の URI を送信ポートまたは受信場所は、256 文字を超えることはできません。|  
    |**セグメント化の許可**|個別のメッセージが MQSeries キューのメッセージの最大長を超えた場合に MQSeries キュー マネージャーのセグメント化を使用します。 選択した場合**はい**、MQSeries キューにセグメント化されたメッセージを格納します。<br /><br /> **既定値:**なし|  
    |**トランザクションのサポート**|アダプターで、BizTalk Server と MQSeries Server との間の DTC トランザクションを開始します。 設定すると**いいえ**、メッセージ配信の保証はありません。<br /><br /> **既定値:**はい**注:**異なる送信ポートを構成しないでください**トランザクションがサポートされて**同じ MQSeries キューにメッセージを送信の設定。 **注:**テスト シナリオを除いてこのプロパティは常に設定の既定値に**はい**です。 このプロパティの値を設定**いいえ**本番環境予期しない問題が発生する可能性があります。|  
  
     次の図は、上記のプロパティの構成例を示しています。  
  
     ![MQSeries トランスポートのプロパティ ダイアログ ボックス](../core/media/bts-dev-mqsendtransportprops.gif "BTS_Dev_MQSendTransportProps")  
  
4.  省略記号ボタン (**.**) の右側にあるボタン、**キュー定義**ボックス、キューを定義します。 使用することができます、**エクスポート**ダイアログ ボックスで、同じように、すぐにキューを作成するのにまたはキューを定義するスクリプトにエクスポートして、受信場所にする必要があります。  
  
5.  をクリックして**OK**各 ダイアログ ボックスを閉じ、設定を保存します。  
  
 **送信ポートを参加させる送信ポートの開始し、受信場所を有効にします。**  
  
1.  送信ポートを右クリックし、をクリックして**Enlist**送信ポートを参加させることです。  
  
2.  送信ポートを右クリックし、をクリックして**開始**を送信ポートを開始します。  
  
3.  受信場所を右クリックし、をクリックして**を有効にする**受信場所を有効にします。  
  
4.  イベント ログで、BizTalk Server エラーが発生していないかどうかを確認します。  
  
## <a name="see-also"></a>参照  
 [MQSeries アダプターを構成する方法は、送信し、受信ハンドラー](../core/how-to-configure-mqseries-adapter-send-and-receive-handlers.md)   
 [MQSeries アダプターの構成](../core/configuring-the-mqseries-adapter.md)