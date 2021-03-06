---
title: BizTalk Server のゾンビ |Microsoft Docs
description: BizTalk Server のゾンビ メッセージの一般的な原因
ms.custom: ''
ms.date: 03/23/2016
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0c684891-e984-442f-b5fd-de5f7cf32b44
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e6a243e772fe5bc8408288167d3e8882a74e9a57
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36976587"
---
# <a name="zombies-in-biztalk-server"></a>BizTalk Server のゾンビ

## <a name="what-is-a-zombie"></a>ゾンビとは  
  
-   ゾンビ メッセージとは、メッセージ ボックスから実行中のオーケストレーションに渡され、オーケストレーションの終了時に "インフライト" であったメッセージのことです。 "インフライト" メッセージとは、サービス インスタンスに回送され、そのサービス インスタンス宛てのメッセージ ボックス キューに入っているメッセージのことです。 このメッセージは、サブスクライブを行なうオーケストレーション インスタンスによって処理されません。そのため、メッセージが中断され、メッセージの ServiceInstance/状態値が "中断 (再開不可)" になります。  
  
-   ゾンビ サービス インスタンスとは、メッセージ ボックスからオーケストレーション インスタンスに回送されたメッセージがまだ "インフライト" であったときに終了したオーケストレーション インスタンスのことです。 オーケストレーション インスタンスが既に終了しているため、"インフライト" メッセージは処理されません。そのため、メッセージが中断され、メッセージの ServiceInstance/状態値が "中断 (再開不可)" になります。  
  
## <a name="typical-causes"></a>一般的な原因
ゾンビの発生は一般的に、次のカテゴリのいずれかに分類されます。  
  
1. **終了コントロール メッセージ**– オーケストレーション エンジンは、特定のオーケストレーション インスタンスで現在実行されているすべての処理を取り消すコントロール メッセージの使用を許可します。 コントロール メッセージを使用すると、実行中のオーケストレーションが直ちに終了するため、ゾンビ インスタンスが発生する可能性があります。 このメカニズムは、ヒューマン ワークフロー関連の設計で頻繁に使用される傾向があります。また、その他の設計でも使用される場合があります。  
  
2. **並列待機受信**– n 個のメッセージの 1 のこのシナリオでは、サービス インスタンスが待機して特定のメッセージを受信したときに何らかの処理を終了します。 サービス インスタンスの終了時に並列分岐でメッセージが受信された場合、ゾンビが発生します。  
  
3. **非確定的なエンドポイントを持つシーケンシャルなコンボイ**– 何らかの種類のシステム設計要件を満たすために、特定の種類のすべてのメッセージを処理するために、このシナリオではマスター オーケストレーション スケジュールが設計されています。 こうした設計要件の例として、順次配送、リソース ディスペンサー、バッチ処理などがあります。 このシナリオでは、傾向、しばらくを定義するが、受信、およびその他の後に一部のコンストラクトを while ループをことを示すためにいくつかの変数を設定する遅延図形を持つ 1 つの分岐で、リッスンを囲むループを停止する必要があります。 これは非決定的です。なぜなら、メッセージが配信可能な場合でも遅延が発生する可能性があるからです。 このような非決定的なエンドポイントでは、ゾンビが発生する可能性が高くなります。  
  
   ゾンビ サービス インスタンスが中断されると、次のエラー メッセージが生成されます。  
  
`0xC0C01B4C The instance completed without consuming all of its messages. The instance and its unconsumed messages have been suspended.`  
  
 使用することができます、 [BizTalk 終端記号](https://www.microsoft.com/download/details.aspx?id=2846)ゾンビを削除します。  
  
## <a name="see-also"></a>参照  
 **中断されたサービス インスタンスを削除します。** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]