---
title: 送信ポートのインスタンス情報を表示する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- send ports, viewing
- managing [send ports], viewing
- viewing, send ports
ms.assetid: 37cf6561-5341-4a05-b531-33ab0334966e
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5dc1ae4401303845f92b95e6cdf7f4903c165b07
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36975147"
---
# <a name="how-to-view-instance-information-for-a-send-port"></a>送信ポートのインスタンス情報を表示する方法
このトピックでは、BizTalk Server 管理コンソールを使用して、送信ポートの実行中のサービス インスタンスを一覧表示する方法について説明します。 サービス インスタンスとは、メッセージが送信ポートに送信されたときに作成される、送信ポート サービスのインスタンスです。 このトピックの手順を実行すると、送信ポートのグループ概要ページにインスタンス情報が表示されます。  
  
## <a name="prerequisites"></a>前提条件  
 このトピックの手順を実行するには、BizTalk Server 管理者グループまたは BizTalk Server Operators グループのメンバー アカウントでログオンする必要があります。 詳細なアクセス許可についてを参照してください。[を展開すると、BizTalk アプリケーションの管理に必要なアクセス許可](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)します。  
  
### <a name="to-view-instance-information-for-a-send-port"></a>送信ポートのインスタンス情報を表示するには  
  
1. クリックして**開始**、 をクリックして**すべてのプログラム**、 をクリックして[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]、順にクリックします**BizTalk Server 管理**します。  
  
2. コンソール ツリーで、BizTalk グループを展開し、送信ポートのサービス インスタンス情報を表示する BizTalk アプリケーションを展開します。  
  
3. をクリックして**送信ポート**、送信ポートを右クリックし、 をポイント**ビュー**、 をクリックし、**インスタンス情報**します。  
  
    ページ下部のクエリ結果パネルに、送信ポートの実行中のインスタンスがすべて表示されます。  
  
4. クエリを絞り込むし、送信ポートの別のサービス インスタンスの情報を表示、下にあるボックスをクリックします。**値**、検索対象フィールドの表示、およびクリックするインスタンスの種類を選択します。**クエリの実行**します。 クエリの作成の詳細については、「関連項目」で検索に関するトピックを選んで参照してください。  
  
## <a name="see-also"></a>参照  
 [作成と送信ポートの構成](../core/creating-and-configuring-send-ports.md)   
 [実行中のサービス インスタンスを検索する方法](../core/how-to-search-for-running-service-instances.md)   
 [中断されたサービス インスタンスを検索する方法](../core/how-to-search-for-suspended-service-instances.md)   
 [メッセージを検索する方法](../core/how-to-search-for-messages.md)   
 [サブスクリプションを検索する方法](../core/how-to-search-for-subscriptions.md)