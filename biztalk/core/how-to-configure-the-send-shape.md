---
title: 送信図形を構成する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Send shape [Orchestration Designer], delivery notification
- send ports, delivery notifications
- configuring [Orchestration Designer], Send shapes
- Send shape [Orchestration Designer], configuring
- delivery notification
- messages, delivery notification
ms.assetid: 2cf4755b-1cfc-484e-bd9c-c9f3855af556
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: bbfedd5067be1de443c20ce522cbe30f27395db1
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36989963"
---
# <a name="how-to-configure-the-send-shape"></a>送信図形を構成する方法
![](../core/media/ebiz-orch-send.gif "ebiz_orch_send")  
送信図形  
  
 送信したメッセージへの応答を間接的または非同期的に受信する (要求 - 応答ポートを使用しないで受信する) 場合は、応答者が適切なインスタンスに応答できるように、送信したメッセージを現在実行中のオーケストレーションのインスタンスに関連付ける必要があります。 フォロー関連付けセット適用することができます、**送信**既にイニシャライズするかの図形にイニシャライズ関連付けセットを適用できます。 詳細については、次を参照してください。[オーケストレーションでの相関関係を使用して](../core/using-correlations-in-orchestrations.md)します。  
  
### <a name="to-configure-a-send-shape"></a>送信図形を構成するには  
  
1.  メッセージとポート操作を設定します。  
  
    1.  [オーケストレーションの種類] ウィンドウで、送信するマルチパート メッセージの種類に対して定義されているメッセージとポート操作の両方がオーケストレーションにあることを確認します。  
  
    2.  [プロパティ] ウィンドウで選択から送信されるメッセージを**メッセージ**プロパティ ボックスの一覧。  
  
    3.  [プロパティ] ウィンドウ内からメッセージを送信するポート操作を選択、**ポート操作**ドロップダウン リスト。  
  
         - または -  
  
         送信コネクタをドラッグして、**送信**図形にメッセージを送信するポート ソケットにします。  
  
2.  関連付けはメッセージを制限するセットを指定、**送信**図形が送信または関連付けセット内の値を初期化します。  
  
    1.  各関連付けセットを使用する、関連付けのドロップダウン リストからセットを確認してください、**フォロー関連付けセット**プロパティ。  
  
    2.  各関連付けセットを初期化することは、ドロップダウン リストから 相関関係を確認してください。、**イニシャライズ関連付けセット**プロパティ。  
  
## <a name="delivery-notification"></a>[配信通知]  
 送信ポートでメッセージが正常に送信されたかどうかをテストするには、次の手順を実行します。  
  
1. トランザクション以外のスコープ、長時間のスコープ、またはアトミックのスコープ内に送信図形を配置します。  
  
2. DeliveryNotification プロパティを設定、送信ポートで**送信**します。  
  
3. DeliveryFailureException を処理するスコープに catch ハンドラーを追加します。  
  
   > [!NOTE]
   >  送信図形は、アトミックのスコープ内に含まれる、DeliveryFailureException を引き続きキャッチできますが、外側のスコープ図形を追加する、トランザクションの種類の設定が必要になります**長時間**または**None**. アトミックのスコープは、直接例外をキャッチすることはできません。  
  
   オーケストレーションは、囲んでいる非アトミックなスコープの最後、またはオーケストレーションの最後に、受信確認応答を受信するために待機します。  
  
> [!NOTE]
>  これは一方向の処理のみに適用され、SoapException の双方向 (要求 - 応答) の処理 (否定受信確認) は、ポート属性が設定されていない場合でもエラーとなります。  
  
> [!NOTE]
>  配信通知では、直接バインドはサポートされません。  
  
## <a name="see-also"></a>参照  
 [エラー処理](../core/error-handling.md)