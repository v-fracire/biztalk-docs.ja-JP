---
title: "BizTalk アプリケーション開始および停止する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- starting
- starting, applications
- managing [applications], starting
- managing [applications], stopping
- applications, starting
- stopping, applications
- applications, stopping
- stopping
ms.assetid: f9f83e99-a1e2-4dfd-b3be-60d3ec2cbcc4
caps.latest.revision: "20"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: faacb2561b63d0e946c3408810db146e083f3e13
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-start-and-stop-a-biztalk-application"></a>BizTalk アプリケーションを開始および停止する方法
このトピックでは、BizTalk Server 管理コンソールを使用して、BizTalk アプリケーションを開始および停止する方法について説明します。  
  
 それに含まれるすべてのオーケストレーションのバインドを構成する必要があります、アプリケーションを開始する前に」の説明に従って[オーケストレーションのバインドを構成する方法](../core/how-to-configure-bindings-for-an-orchestration.md)です。  
  
 アプリケーションを開始するとき、次のオプションを 1 つ以上選択できます。  
  
-   [すべてのオーケストレーションを参加させて開始する]  
  
-   [すべての送信ポートを参加させて開始する]  
  
-   [すべての送信ポート グループを参加させて開始する]  
  
-   [すべての受信場所を有効にする]  
  
-   [関連するすべてのホスト インスタンスを開始する]  
  
-   [中断したインスタンスを再開する]  
  
-   すべてのポリシーを展開します。  
  
> [!NOTE]
>  自動的に展開されるのは、アプリケーションの公開済みポリシーのみです。 公開されていないポリシーは展開されません。  
  
 アプリケーションを停止するとき、次のいずれかのオプションを選択できます。  
  
-   **部分停止 - 実行中のインスタンスを続行します。** このオプションを選択すると、アプリケーションの受信場所はすべて無効になりますが、その他のアイテムはすべて以前の状態のままになります。 これにより、実行中のインスタンスは現在システム内にあるメッセージの処理を完了できます。 このオプションを使用する場合、複数の入力を必要とするメッセージ トランザクションは完了できない可能性があることに注意してください。  
  
-   **部分停止 - 実行中のインスタンスを中断します。** このオプションを選択すると、アプリケーションの受信場所がすべて無効になり、オーケストレーションと送信ポートがすべて停止されます。 アイテムの参加解除や展開解除は行われません。 このオプションは、アプリケーションを一時的に停止する場合に使用します。  
  
-   **完全停止 - インスタンスを終了します。** このオプションを選択すると、アプリケーションの受信場所がすべて無効になり、オーケストレーションと送信ポートがすべて停止されて参加解除され、ポリシーもすべて展開解除されます。 このオプションは、アプリケーションを完全に展開解除する場合に使用します。 まだメッセージを処理している実行中のインスタンスがある場合、そのインスタンスの処理は完了しません。 詳細については、次を参照してください。 [BizTalk アプリケーションを展開解除](../core/undeploying-biztalk-applications.md)です。  
  
## <a name="prerequisites"></a>前提条件  
 このトピックの手順を実行するには、BizTalk Server 管理者グループのメンバーであるアカウントを使用してログオンする必要があります。 BizTalk Operators は、部分停止は実行できますが完全停止は実行できません。 また、BizTalk Operators は、すべてのアイテムが参加している場合にはアプリケーションを開始できます。 詳細なアクセス許可についてを参照してください。[を展開すると、BizTalk アプリケーションの管理に必要なアクセス許可](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)です。  
  
### <a name="to-start-or-stop-a-biztalk-application"></a>BizTalk アプリケーションを開始または停止するには  
  
1.  をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]、順にクリック**BizTalk Server 管理コンソール**です。  
  
2.  コンソール ツリーで  **BizTalk Server 管理コンソール**BizTalk グループを展開し、展開、**アプリケーション**です。  
  
3.  開始または停止、およびをクリックする BizTalk アプリケーションを右クリックして**開始**または**停止**です。  
  
4.  開始を選択するか、停止のオプションをクリックしします**開始**または**停止**です。  
  
## <a name="see-also"></a>参照  
 [展開して、BizTalk アプリケーションの管理](../core/deploying-and-managing-biztalk-applications.md)   
 [BizTalk アプリケーションの更新](../core/updating-biztalk-applications.md)