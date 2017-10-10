---
title: "複数の Continuation を使用して |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a38087-71ee-40b3-a957-6a2653bd6435
caps.latest.revision: "10"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 0e27a73fae39a55f05650c08397616f3cbe4fa80
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="using-multiple-continuations"></a>複数の Continuation の使用
複数のアクティビティが存在する環境で追跡プロファイル エディター (TPE) を使用するには、受信ポート、オーケストレーション、および送信ポートを正しい順序でマップするために、アクティビティが追跡されるシナリオを理解する必要があります。  
  
 追跡プロファイルでは、TPE によってアクティビティの開始と終了が自動的に評価されます。 アクティビティの開始は最初のデータが収集されたときであり、終了は最後のデータが収集されたときです。  
  
 ほとんどの場合、2 つのオーケストレーション間の Continuation など、単一の Continuation を作成する手順は、開発者にとって難しいものではありません。 TPE が複雑になるのは、複数の Continuation の場合です。  複数の Continuation のシナリオは、ビジネス アクティビティ監視 (BAM) アクティビティが複数の受信ポート、オーケストレーション、および送信ポートにまたがる場合です。 1 つのレコードに BAM データを収集するには、すべての BizTalk Server スケジュール間に Continuation を作成する必要があります。 このプロセスは、TPE ユーザー インターフェイス (UI) を使用して完了させる場合には、複雑になります。  
  
 このトピックでは、異なるシナリオで単一および複数の Continuation を作成する方法について説明します。  
  
#### <a name="base-scenario-description---multiple-receive-ports-orchestrations-and-send-ports"></a>基本シナリオの説明 - 複数の受信ポート、オーケストレーション、および送信ポート  
 このシナリオは、複数の受信ポート (R)、オーケストレーション (O)、および送信ポート (S) を持つ BizTalk Server で構成されます。 Continuation をリンクするには、一般的な interchangeID コンテキスト プロパティが使用されます。 activityID や他の一意識別子など、任意のコンテキスト プロパティを使用できます。 特定のコンテンツの選択は、このシナリオの説明とは関係ありません。  
  
 このシナリオでは、これらのポートおよびオーケストレーションから追跡されるデータ項目、マイルストーン、およびコンテキストの各プロパティの値に関する情報は指定されていません。 マッピングのその部分は、ビジネス ロジックに固有です。 目標は、完了したアクティビティ テーブルの 1 行に、すべてのポートおよびオーケストレーションから全 BAM データを取得することです。 オーケストレーションでメッセージを受信および処理できるさまざまな方法によって、興味深い課題とソリューションを示します。  
  
> [!NOTE]
>  1 つのポートまたは 1 つのオーケストレーションのシナリオは、複数のポートおよび複数のオーケストレーションのシナリオの特殊なケースと見なすことができます。  
  
#### <a name="scenario-solution-1---one-receive-port-and-one-orchestration"></a>シナリオのソリューション 1 - 1 つの受信ポートと 1 つのオーケストレーション  
 このシナリオでは、メッセージは 1 つの受信ポート (R1) だけで受信され、1 つのオーケストレーション (O1) だけで処理されます。  
  
 Continuation の作成手順は次のとおりです。  
  
1.  追跡プロファイルのフォルダー アクティビティ ツリー ビューで Continuation を作成します。  
  
2.  クリックして、コンテキスト プロパティ スキーマを選択して、**イベント ソースの選択**ボタンをクリックして、 **コンテキスト プロパティの**メニュー項目。  
  
3.  検索、 **interchangeId プロパティ**で、**コンテキスト プロパティ名**ボックスの一覧し、それを選択します。  
  
4.  プロパティ スキーマから、作成した Continuation フォルダーに interchangeID をマップします。  
  
5.  アクティビティ ツリーで新しく作成された interchangeID ノードを右クリックして、マップ元になるポートを選択します。  
  
6.  **ポートの選択**すべて表示されるダイアログ ボックスを選択**N**ポートを受信します。  
  
7.  フォルダー アクティビティ ツリーで ContinuationID フォルダーを作成します。  
  
8.  クリックして、各オーケストレーションを開いて、**イベント ソースの選択**ボタンをクリックして、 **オーケストレーション スケジュールの**メニュー項目。 各オーケストレーションから、オーケストレーションの図形を右クリックして、新しく作成された continuationID に interchangeID コンテキスト プロパティをマップします。  
  
 3 つのオーケストレーションによる展開では、追跡プロファイルは次のようになります。  
  
 ![TPE 複数 continuation シナリオ 1](../core/media/4761d680-7218-4404-a636-06739f70f344.gif "4761d680-7218-4404-a636-06739f70f344")  
  
#### <a name="scenario-solution-2---one-receive-port-and-multiple-orchestrations"></a>シナリオのソリューション 2 - 1 つの受信ポートと複数のオーケストレーション  
 このシナリオでは、メッセージは 1 つの受信ポートだけで受信され、個別のオーケストレーションによって処理されます。 この状況は、メッセージが各オーケストレーションに同時に送信された場合に発生します。  
  
 この場合、オーケストレーションごとに Continuation と continuationID が必要になります。 Continuation の作成プロセスはシナリオのソリューション 1 で説明する手順のようになります。 3 つのオーケストレーションの展開では、追跡プロファイルの結果は、次のような。  
  
 ![TPE 複数 continuation シナリオ 2](../core/media/3cebd82f-9192-4d52-84c7-584f24e8ecca.gif "3cebd82f-9192-4d52-84c7-584f24e8ecca")  
  
#### <a name="scenario-solution-3---content-based-routing"></a>シナリオのソリューション 3 - コンテンツ ベースのルーティング  
 このシナリオでは、コンテンツ ベースのルーティング (CBR) のソリューションを定義します。 メッセージは 1 つの受信ポートだけで受信され、1 つの送信ポートだけに送信されます。 このルーティングは、メッセージのコンテキスト プロパティの値に基づいて行われます。 この場合は、1 つの Continuation が必要です。 マッピングは次のようになります。  
  
 ![Continuation CBR シナリオ] (../core/media/4459a73d-515f-4d6d-a68f-b18eee072df8.gif "4459a73d-515f-4d6d-a68f-b18eee072df8")  
  
> [!NOTE]
>  上記のマッピングは、1 つの受信ポートだけで受信され、すべての送信ポートに送信されるメッセージでも有効です。  
  
#### <a name="scenario-solution-4---one-orchestration-multiple-send-ports"></a>シナリオのソリューション 4 - 1 つのオーケストレーション、複数の送信ポート  
 このシナリオでは、複数の送信を使用します。 ポート。 これは、処理ルールによって決定され、すべての送信ポートに送信されると、オーケストレーションの 1 つだけでは、メッセージが処理されます。 この場合は、1 つの Continuation が必要です。 マッピングは次のようになります。  
  
 ![Coninuation シナリオ 4](../core/media/3ab10b51-d306-4ad1-acb6-6731e23394ac.gif "3ab10b51-d306-4ad1-acb6-6731e23394ac")  
  
#### <a name="scenario-solution-5---sequential-orchestrations"></a>シナリオのソリューション 5 - 順次オーケストレーション  
 このシナリオでは、メッセージは各オーケストレーションで順に 1 つずつ処理され、Continuation を介して次のオーケストレーションに渡されます。 マッピングは次のようになります。  
  
 ![Continuation のシナリオ 5](../core/media/563cacee-104c-4f8a-9836-da90aecb7487.gif "563cacee-104c-4f8a-9836-da90aecb7487")  
  
### <a name="collecting-data-in-an-asynchronous-environment"></a>非同期環境でのデータの収集  
 Continuation を設定すると、BAM によって到着するデータが要求されます。 非同期環境では、応答をバックエンド プロセスから受信できません。  
  
 応答データが受信されないと、アクティビティ インスタンスは無限に待機します。 アクティビティは完了せず、レコードは BAM プライマリ インポート データベースのテーブルに残ります。 長時間実行されるトランザクションのケース、つまり残りのデータがいつ到着するかを確認する手段がない場合を考えてみます。 データの到着がビジネス ロジックまたはプロセスによって異なる場合は、アクティビティが完了としてマークされるタイムアウトが発生しません。 データは同日に到着したり、極端な場合には翌年に到着したりします。  
  
 これを解決するには、関連アクティビティを使用します。  
  
 アクティビティを 2 つのアクティビティに分割します。 2 つのアクティビティを関連付け、元のアクティビティに応答を関連付けます。  
  
 関連するアクティビティに関する詳細については、次を参照してください。[アクティビティ リレーションシップ](../core/activity-relationships.md)です。  
  
## <a name="see-also"></a>参照  
 [追跡プロファイル エディター](../core/tracking-profile-editor.md)