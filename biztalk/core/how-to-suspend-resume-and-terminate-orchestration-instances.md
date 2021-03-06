---
title: 中断、再開、およびオーケストレーションのインスタンスを終了する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- managing [orchestrations], resuming
- orchestrations, terminating
- managing [orchestrations], suspending
- orchestrations, resuming
- orchestrations, suspending
- managing [orchestrations], terminating
ms.assetid: 7b373dad-57d5-4696-9b29-a6c351d44fa8
caps.latest.revision: 17
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 88ad7a5b278f8f972a518af40d527ff312d0d237
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36980395"
---
# <a name="how-to-suspend-resume-and-terminate-orchestration-instances"></a>オーケストレーション インスタンスを中断、再開、および終了する方法
このトピックでは、BizTalk Server 管理コンソールを使用して、実行中の 1 つ以上のオーケストレーションのサービス インスタンスを中断、再開、および終了する方法について説明します。 サービスのインスタンスとは、後続の処理や追跡を目的に BizTalk Server が処理しているオーケストレーションのインスタンス、または、メッセージ ボックスにシリアル化されたオーケストレーションのインスタンスを指します。  
  
 以下に、これら 3 つの操作の効果について説明します。  
  
-   **中断します。** サービス インスタンスを一時停止します。 インプロセス メッセージは最後まで実行されます。 メッセージは依然として回送されますが、処理されません。  
  
-   **再開します。** 中断したインスタンスの処理を再開します。  
  
> [!NOTE]
>  ブレークポイント状態のインスタンスは再開できません。 このようなインスタンスを再開すると、"保留中" という状態が表示されることがあります。ただし、このインスタンスは最終的に失敗します。  
  
-   **終了します。** メッセージ処理をすべて終了します。 サービス インスタンスは、BizTalk Server データベースから削除されます。 サービス インスタンスが処理しているメッセージも削除されます。ただし、終了しないサービス インスタンスによって参照されているメッセージは削除されません。  
  
## <a name="prerequisites"></a>前提条件  
 このトピックの手順を実行するには、BizTalk Server Operators グループまたは BizTalk Server 管理者グループのメンバーとしてログオンする必要があります。 詳細なアクセス許可についてを参照してください。[を展開すると、BizTalk アプリケーションの管理に必要なアクセス許可](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)します。  
  
### <a name="to-view-start-stop-or-terminate-an-instance-of-an-orchestration"></a>オーケストレーションのインスタンスを開始、停止、または終了するには  
  
1. クリックして**開始**、 をクリックして**すべてのプログラム**、 をクリックして[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]、順にクリックします**BizTalk Server 管理**します。  
  
2. [グループ ハブ] ページを表示する BizTalk グループを選択します。  
  
3. [**進行中の作業**、] をクリックして**サービス インスタンスを実行している**します。  
  
    ページ下部のクエリ結果パネルに、オーケストレーションのすべてのインスタンスが表示されます。  
  
4. クエリを変更して、オーケストレーションの別のインスタンスを表示、下にあるボックスをクリックします**値**の、**検索の**フィールドで、表示する をクリックし、インスタンスの種類を選択します。**クエリの実行。**. クエリの作成の詳細については、「関連項目」で検索に関するトピックを選んで参照してください。  
  
5. をクリックしてインスタンスを右クリックして**Suspend**、**再開**、または**Terminate**します。 この機能を使用すると、再開するインスタンスを選択できます。  
  
   > [!NOTE]
   >  複数のインスタンスに対して操作を実行するには、CTRL キーを押しながら目的のインスタンスをクリックします。 次にインスタンスを右クリックし、をクリックして**Suspend**、**再開**、または**Terminate**します。  
  
    [サービス インスタンスの状態](../core/service-instance-states.md)中断状態について詳しく説明します。  
  
## <a name="see-also"></a>参照  
 [オーケストレーションの管理](../core/managing-orchestrations.md)   
 [実行中のサービス インスタンスを検索する方法](../core/how-to-search-for-running-service-instances.md)   
 [中断されたサービス インスタンスを検索する方法](../core/how-to-search-for-suspended-service-instances.md)