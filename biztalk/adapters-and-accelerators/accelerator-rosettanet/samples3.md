---
title: Samples3 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SDK samples
- examples, developing
- developing, examples
ms.assetid: b940111e-4f71-494b-b7a3-d2e8310bea51
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: f509668bb8da8021b14a7252a3902cb01da9fd5a
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37006115"
---
# <a name="samples"></a>サンプル
このセクションに説明します、Microsoft® に含まれるサンプル[!INCLUDE[BTARN_CurrentVersion_FirstRef](../../includes/btarn-currentversion-firstref-md.md)]ソフトウェア開発キット (SDK)。 ここでは、サンプルの構築方法、実行方法、予想される実行結果など、各サンプルについて詳しく説明します。  

 サンプルが含まれている、 \<*ドライブ*\>: \Program Files\\Microsoft BizTalk\<バージョン\>Accelerator for rosettanet \sdk\ フォルダー。  

## <a name="in-this-section"></a>このセクションの内容  

- アダプター サンプル フォルダー  

  -   [ApplicationAdapter](../../adapters-and-accelerators/accelerator-rosettanet/applicationadapter.md)します。 メッセージ通知メカニズムを組み込む方法を示します。  

  -   [ValidationAdapter](../../adapters-and-accelerators/accelerator-rosettanet/validationadapter.md)します。 メッセージに対して特別な検証ルールを実行する方法を示します。  

- メッセージング サンプル フォルダー  

  -   [FileTransport サンプル](../../adapters-and-accelerators/accelerator-rosettanet/filetransport-sample.md)します。 ファイル ポートを使用するように BTARN を設定する方法を示します。  

  -   [GetMessages サンプル](../../adapters-and-accelerators/accelerator-rosettanet/getmessages-sample.md)します。 否認不可テーブル、基幹業務 (LOB) テーブルのいずれかからメッセージを取得する方法を示します。  

  -   [メッセージ送信 ASPX サンプル](../../adapters-and-accelerators/accelerator-rosettanet/message-submission-aspx-sample.md)します。 Service Content をプライベート プロセスに送信するためのサンプルの .aspx コードを提供します。 また、PIP (Partner Interface Process) アクション メッセージをその Service Content に送信するための HTML も提供します。  

  -   [Tracking サンプル](../../adapters-and-accelerators/accelerator-rosettanet/tracking-sample.md)します。 BTARN を使用して送受信されるメッセージの状態を表示するためのサンプルの .aspx コードを提供します。  

- オーケストレーション サンプル フォルダー  

  -   [ビジネス ルールを使用した 3A4 プライベート レスポンダー オーケストレーション](../../adapters-and-accelerators/accelerator-rosettanet/3a4-private-responder-orchestration-using-a-business-rule.md)します。 マップを使用して要求メッセージを応答メッセージに変換することにより、PIP 関連のビジネス プロセスを自動化する方法を示します。  

  -   [ダブル アクション PIPAutomation オーケストレーション](../../adapters-and-accelerators/accelerator-rosettanet/double-action-pipautomation-orchestration.md)します。 着信メッセージのタイプに基づいて応答メッセージのタイプを自動的に判断することにより、ビジネス プロセスを自動化する方法を示します。  

  -   [3 a 2 応答のマップ サンプルを 3 a 2 要求](../../adapters-and-accelerators/accelerator-rosettanet/3a2-request-to-3a2-response-map-sample.md)します。 3A2 要求スキーマを 3A2 応答スキーマにマップする方法を示します。  

  -   [3A4 要求から 3A4 応答のマップ サンプルへ](../../adapters-and-accelerators/accelerator-rosettanet/3a4-request-to-3a4-response-map-sample.md)します。 3A4 要求スキーマを 3A4 応答スキーマにマップする方法を示します。  

  -   [PrivateInitiator サンプル](../../adapters-and-accelerators/accelerator-rosettanet/privateinitiator-sample.md)します。 開始側プライベート プロセス オーケストレーションを作成する方法を示します。  

  -   [PrivateResponder サンプル](../../adapters-and-accelerators/accelerator-rosettanet/privateresponder-sample.md)します。 応答側プライベート プロセス オーケストレーションを作成する方法を示します。  

  -   [HubScenario サンプル](../../adapters-and-accelerators/accelerator-rosettanet/hubscenario-sample.md)します。 中間ハブに送信されたメッセージを最終的な受信者に送信されるメッセージに変換する方法を示します。  

- パイプライン サンプル フォルダー  

  - [送信パイプライン](../../adapters-and-accelerators/accelerator-rosettanet/send-pipeline.md)します。 [!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] パイプラインを使用して送信 XML メッセージを同等の RNIF メッセージに変換する方法を示します。  

  - [受信パイプライン](../../adapters-and-accelerators/accelerator-rosettanet/receive-pipeline.md)します。 [!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] パイプラインを使用して着信 RNIF メッセージを同等の XML メッセージに変換する方法を示します。  

  - [メッセージ エディタ パイプライン サンプル](../../adapters-and-accelerators/accelerator-rosettanet/message-editor-pipeline-sample.md)します。 カスタム パイプライン コンポーネントを作成して着信メッセージを編集する方法を示します。  

- スキーマ サンプル フォルダー  

  -   [スキーマのサンプル](../../adapters-and-accelerators/accelerator-rosettanet/schema-samples.md)します。 PIP XML スキーマ、RosettaNet 次世代スキーマ、RNIF スキーマなど、SDK に含まれているサンプル スキーマについて説明します。 これらのスキーマの使用手順にもリンクされています。  

- Web アプリケーション サンプル フォルダー  

  -   [RNIFSend](../../adapters-and-accelerators/accelerator-rosettanet/rnifsend.md)します。 開始側から応答側に RNIF メッセージを送信する ASPX ページをカスタマイズする方法を示します。  

  -   [RNIFReceive](../../adapters-and-accelerators/accelerator-rosettanet/rnifreceive.md)します。 応答側で RNIF メッセージを受信する ASPX ページをカスタマイズする方法を示します。  

- [停止し開始オーケストレーション、送信ポート、および受信場所をプログラムで](../../adapters-and-accelerators/accelerator-rosettanet/code-to-stop-and-start-orchestrations-send-ports-and-receive-locations.md)します。 すべてのオーケストレーション、送信ポート、および受信場所の停止および開始をまとめて行ったり、1 つずつ行ったりする方法を示します。
