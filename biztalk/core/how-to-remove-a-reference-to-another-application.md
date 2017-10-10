---
title: "別のアプリケーションへの参照を削除する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: applications, references
ms.assetid: cc867706-7c56-4386-b7ec-9fd7cf6c83a4
caps.latest.revision: "11"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: de51adb1a9c42874025527ad458ecb6e3c311b3f
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-remove-a-reference-to-another-application"></a>他のアプリケーションへの参照を削除する方法
このトピックでは、BizTalk Server 管理コンソールを使用して、1 つのアプリケーションから別のアプリケーションへの参照を削除する方法について説明します。 同じ BizTalk グループの別のアプリケーション内に存在するアイテムを、現在のアプリケーションで使用する必要がなくなった場合は、参照を削除します。 参照の追加の詳細については、次を参照してください。[を別のアプリケーションへの参照を追加する方法](../core/how-to-add-a-reference-to-another-application.md)です。  
  
 参照先アプリケーションのアイテムが、現在のアプリケーションのアイテムによって引き続き使用されている場合、参照を削除する操作は失敗します。  
  
> [!CAUTION]
>  BizTalk Server のすべてのアプリケーションには自動的に BizTalk.System アプリケーションへの参照が含まれます。 これは、BizTalk.System に含まれるアイテムが、すべての BizTalk アプリケーションで使用されるためです。 BizTalk.System アプリケーションへの参照は削除しないでください。 削除すると、アプリケーションが正しく機能しなくなる可能性があります。  
  
## <a name="prerequisites"></a>前提条件  
 このトピックの手順を実行するには、BizTalk Server 管理者グループのメンバーであるアカウントを使用してログオンする必要があります。 詳細なアクセス許可についてを参照してください。[を展開すると、BizTalk アプリケーションの管理に必要なアクセス許可](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)です。  
  
### <a name="to-remove-a-reference-to-another-application"></a>他のアプリケーションへの参照を削除するには  
  
1.  をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]、順にクリック**BizTalk Server 管理コンソール**です。  
  
2.  コンソール ツリーで  **BizTalk Server 管理コンソール**(別のアプリケーションを参照するもの) の参照を削除するアプリケーションを右クリックし、クリックして**プロパティ**.  
  
3.  [プロパティ] ページの左側のウィンドウでをクリックして**参照**です。  
  
4.  右側のウィンドウでこのアプリケーションからの参照 をクリックする必要がなくなったアプリケーションをクリックして**削除**、順にクリック**OK**です。  
  
## <a name="see-also"></a>参照  
 [作成して、BizTalk アプリケーションの変更](../core/creating-and-modifying-biztalk-applications.md)