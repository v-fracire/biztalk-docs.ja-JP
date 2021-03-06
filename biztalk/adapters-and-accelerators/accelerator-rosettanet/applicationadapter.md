---
title: ApplicationAdapter |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2f9b876b-cd37-4e24-a476-186adc155ac0
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8b7a754b044fb12bf7cec9fed0e5455e6192c072
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36974931"
---
# <a name="applicationadapter"></a>ApplicationAdapter
ApplicationAdapter サンプルは、メッセージの受信時にパブリック プロセスとプライベート プロセス (応答側または開始側) から通知を送信する方法を示します。 このサンプルには、必要に応じて新しい機能を追加できます。  
  
 ApplicationAdapter サンプルは、`IApplicationAdapter` インターフェイスを `ApplicationAdapter1` クラスに実装する方法を示します。 このクラスには、`BeginNotify` と `Notify` という 2 つのメソッドが含まれます。 各クラスのパラメーターは、メッセージ カテゴリ、送信元パーティ名、送信先パーティ名、PIP (Partner Interface Process) コード、PIP インスタンス ID、および PIP バージョンです。  
  
 アセンブリ名とクラス名を入力して、アグリーメントの ApplicationAdapter を設定する、**全般**Microsoft® でアグリーメントのタブ[!INCLUDE[btaBTARNNoVersion](../../includes/btabtarnnoversion-md.md)]([!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)]) 管理コンソール。 アプリケーション アダプタの .dll ファイルが BizTalk ホスト サービスと同じ資格情報を使用して実行されます。  
  
 ApplicationAdapter サンプルまたは関連するいずれかの外部環境変数を変更した場合は、[!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] のパブリック プロセスをホストする BizTalk ホスト サービスを再起動します。  
  
 ApplicationAdapter サンプル コードは\<*ドライブ*\>: \Program Files\ BizTalk\<バージョン\>Accelerator RosettaNet\SDK\ApplicationAdapterfor\\.  
  
## <a name="demonstrates"></a>使用例  
 ApplicationAdapter サンプルは、パブリック プロセスがメッセージを受信したことを応答側プライベート プロセスに通知する方法を示します。 通知には、メッセージ カテゴリ、送信元パーティ名、送信先パーティ名、PIP コード、PIP バージョン、および PIP インスタンス ID が示されます。 この通知は、アクション メッセージと応答メッセージのいずれに関しても送信できます。  
  
 `BeginNotify` メソッドと `Notify` メソッドは次のように機能します。  
  
1.  応答側パブリック プロセスがメッセージを受信します。  
  
    > [!NOTE]
    >  次の手順は、パブリック開始側が応答側から応答メッセージを受信する状況にも当てはまります。  
  
2.  受信パイプラインとパブリック プロセス、および場合によって検証アダプターによる検証が正しく行われると、応答側パブリック プロセスは、`BeginNotify` クラスの `ApplicationAdapter` メソッドを呼び出します。 このメソッドは、パブリック プロセスが新しいメッセージを受信し、そのメッセージを MessageBox データベースに保存したことを、応答側プライベート プロセスに通知します。  
  
3.  応答側パブリック プロセスがシグナル メッセージを開始側に戻します。  
  
4.  応答側パブリック プロセスがメッセージの Service Content を応答側プライベート プロセスに送信します。  
  
5.  応答側プライベート プロセスが BTARNDATA データベースの MessagesToLOB テーブルにメッセージを格納します。  
  
6.  応答側プライベート プロセスが `Notify` クラスの `ApplicationAdapter` メソッドを呼び出して、End Notify メッセージを応答側パブリック プロセスに戻します。 応答側パブリック プロセスが正しく実行されるには、End Notify メッセージを受信する必要があります。 受信しなかった場合、メッセージは保留されます。  
  
> [!NOTE]
>  `Notify` メッセージを使用すると、MessagesToLOB テーブルでメッセージが待機しているというシグナルを基幹業務 (LOB) アプリケーションに送ることができます。 LOB アプリケーションは、システムから警告を受けるとすぐにテーブルからメッセージを取得できます。  
  
## <a name="to-implement-this-sample"></a>サンプルの実装  
 ApplicationAdapter サンプルを実装するには、アプリケーション アダプタをアグリーメントに追加する必要があります。  
  
#### <a name="to-add-the-application-adapter-to-an-agreement"></a>アプリケーション アダプターをアグリーメントに追加するには  
  
1. クリックして**開始**、 をポイント**すべてのプログラム**、microsoft **BizTalk\<バージョン\>Accelerator for RosettaNet**順にクリックします[!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]**管理コンソール**します。  
  
2. [!INCLUDE[btaBTARNNoVersion](../../includes/btabtarnnoversion-md.md)]管理コンソールで、展開[!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]、 をクリック**契約**します。  
  
3. アプリケーション アダプターを追加するアグリーメントをダブルクリックします。  
  
4. **アプリケーション アダプター**ボックスで、省略記号ボタンをクリックします (**.**) ボタンの右側に**アセンブリ名**、アプリケーション アダプターのアセンブリを格納している場所に移動、適切な .dll ファイルを選択およびクリックして**オープン**します。  
  
5. 下矢印をクリックして**クラス名**アプリケーション アダプター クラスを選択し、クリックして**OK**。  
  
## <a name="see-also"></a>参照  
 [アダプター サンプル](../../adapters-and-accelerators/accelerator-rosettanet/adapter-samples.md)