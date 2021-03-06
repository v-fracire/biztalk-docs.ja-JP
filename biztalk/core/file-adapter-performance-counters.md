---
title: ファイル アダプターのパフォーマンス カウンター |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 343465b4-6b20-4a24-b4b1-138548c572cc
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8d48cf2cf203ed001611bb30e3c9f1d5746a903e
ms.sourcegitcommit: 5abd0ed3f9e4858ffaaec5481bfa8878595e95f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2017
ms.locfileid: "25968792"
---
# <a name="file-adapter-performance-counters"></a>ファイル アダプターのパフォーマンス カウンター
パフォーマンス カウンターを使用すると、サービスによってサイトまたはシステムで実行されている作業の具体的な側面を監視できます。 パフォーマンス カウンターは、サーバー パフォーマンスに関する問題を特定してトラブルシューティングする際に役立ちます。  
  
 次のパフォーマンス カウンターは各ホスト インスタンスにアクセスできる、 **biztalk: ファイル受信アダプター**と**biztalk: ファイル送信アダプター**パフォーマンス オブジェクト カテゴリ。  
  
|**カテゴリ**|**カウンター**|**Description**|  
|------------------|-----------------|---------------------|  
|BizTalk:ファイル受信アダプター|Bytes received|ファイル受信アダプターによって受信された合計バイト数。 このカウンターは、アダプターがファイル システムからメッセージを完全に読み取った後で増やされます。|  
||Byte received/Sec|ファイル受信アダプターが 1 秒あたりに受信したバイト数。 このカウンターの対象となるのは、ファイル アダプターがファイル システムから完全に読み取ったメッセージだけです。|  
||Delete retries|ファイル受信アダプターが、読み取ったファイルの削除を試みた回数。|  
||Lock failures|ファイル受信アダプターがファイルのロックに失敗した回数。|  
||Lock failures/sec|ファイル受信アダプターがファイルのロックに失敗した 1 秒あたりの回数。|  
||Messages received|ファイル受信アダプターが受信したメッセージの総数。 このカウンターは、ファイル受信アダプターがファイル システムからメッセージを完全に読み取った後で増やされます。|  
||Messages received/Sec|ファイル受信アダプターが 1 秒あたりに受信したメッセージ数。 このカウンターの対象となるのは、ファイル受信アダプターがファイル システムから完全に読み取ったメッセージだけです。|  
||Time to build batch|ファイル受信アダプターがバッチの作成に要した平均時間。|  
|BizTalk:ファイル送信アダプター|Bytes sent|ファイル送信アダプターによって送信された合計バイト数。 カウンターは、メッセージがファイル システムに完全に書き込まれた場合にのみ増やされます。|  
||Bytes sent/Sec|ファイル送信アダプターによって送信された 1 秒あたりのバイト数。 このカウンターの対象となるのは、ファイル システムに完全に書き込まれたメッセージだけです。|  
||Messages sent|ファイル送信アダプターによって送信されたメッセージの総数。 カウンターは、メッセージがファイル システムに完全に書き込まれた場合にのみ増やされます。|  
||Messages Sent/sec|ファイル送信アダプターによって送信された 1 秒あたりのメッセージ数。 このカウンターの対象となるのは、ファイル システムに完全に書き込まれたメッセージだけです。|  
  
## <a name="to-access-performance-counters"></a>パフォーマンス カウンターにアクセスするには  
 パフォーマンス カウンターにアクセスするには、次の手順を実行します。  
  
#### <a name="if-you-are-using-windows-2008"></a>Windows 2008 を使用している場合  
  
1.  をクリックして**開始**、 をポイント**管理ツール**、順にクリック**パフォーマンス モニター**です。  
  
2.  **パフォーマンス モニター** ] ダイアログ ボックスで、展開**の監視ツールを**[**パフォーマンス モニター**、順にクリック**追加**です。  
  
3.  **カウンターの追加** ダイアログ ボックスから、**使用可能なカウンター**一覧で、展開、 **biztalk: ファイル**パフォーマンス カウンター オブジェクトおよび監視するカウンターの選択  
  
4.  **インスタンスの選択したオブジェクト**一覧をクリックして、選択したカウンターを監視する特定のインスタンスを選択**追加**です。  使用可能なカウンターのすべてのインスタンスを選択するには、次のように選択します。 \<**すべてのインスタンス**\>です。  
  
5.  カウンターを追加すると、をクリックして**OK**です。  
  
     選択したパフォーマンス カウンターが表示されます、**パフォーマンス モニター**画面。  
  
## <a name="see-also"></a>参照  
 [パフォーマンス維持の計画](../core/planning-for-sustained-performance.md)