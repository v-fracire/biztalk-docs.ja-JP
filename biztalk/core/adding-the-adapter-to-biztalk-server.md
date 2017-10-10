---
title: "BizTalk Server にアダプターを追加する |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adapters [JD Edwards OneWorld adapters], installing
- installing, JD Edwards OneWorld adapters
- JD Edwards OneWorld adapters, installing
ms.assetid: e2018856-1943-48e9-b43f-7d527880e4bd
caps.latest.revision: "12"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 63de8824112c9891c6d67eee424a84dd4968976c
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="adding-the-adapter-to-biztalk-server"></a>BizTalk Server にアダプターを追加します。
Microsoft BizTalk Adapter for JD Edwards OneWorld には、受信ハンドラーと送信ハンドラーの両方のフォルダーが含まれています。 送信ハンドラー フォルダーには、BizTalkServerApplication が含まれています。 BizTalk Adapter for JD Edwards OneWorld は作成可能です。BizTalk Server とインプロセスで実行され、分離されたホスト プロセスでは実行されません。  
  
 BizTalk Server にアダプターを追加するには、次の手順を実行します。  
  
### <a name="to-add-biztalk-adapter-for-jd-edwards-oneworld"></a>BizTalk Adapter for JD Edwards OneWorld を追加するには  
  
1.  **開始** メニューのをポイント**Program Files**、 をポイント[!INCLUDE[btsBizTalkServer2006r3ui](../includes/btsbiztalkserver2006r3ui-md.md)]、順にクリック**BizTalk Server 管理コンソール**を開始する、 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールです。  
  
2.  展開**BizTalk Server 管理コンソール**、展開**BizTalk グループ**、順に展開**プラットフォームの設定**です。  
  
3.  右クリック**アダプター**、指す**新規**、 をクリック**アダプター**です。  
  
4.  **アダプター プロパティ**ダイアログ ボックスで、アダプターの名前を入力します。 たとえば、JDEdwards です。  
  
5.  選択**[jdeoneworld]**から、**アダプター**一覧をクリックして**OK**です。  
  
## <a name="verifying-the-adapter"></a>アダプターの確認  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、できることを確認するを確認して、アダプターが正しく機能している、**論理システム**ウィンドウです。 初回のインストレーションでは、このウィンドウは空です。これは、サーバー システムへの接続が未確立で、論理システムが作成されていないからです。  
  
#### <a name="to-verify-that-the-adapter-is-running-correctly"></a>アダプターが正常に動作していることを確認するには  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、 **BizTalk グループ**、展開**プラットフォームの設定**、展開**アダプター**、し、 **[Jdeoneworld]**です。  
  
2.  詳細ウィンドウで右クリック**BizTalkServerApplication**を選択して**プロパティ**です。  
  
3.  **[プロパティ]** タブをクリックします。  
  
4.  SQL 接続パラメーターを設定します。  
  
    -   **SQL データベース パラメーターを定義する**SQL Server 名とデータベースがインストール時に設定します。 これは、テキスト領域がサーバーと、このアダプターのデータベースを再定義できることです。  
  
5.  をクリックして**閉じる**を終了する、**論理システム**ウィンドウです。  
  
     次のステップでは、[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] を使用して論理システムを追加します。  
  
## <a name="see-also"></a>参照  
 [計画とアーキテクチャ](../core/planning-and-architecture17.md)   
 [BizTalk Adapter for JD Edwards OneWorld のセキュリティ](../core/security-in-biztalk-adapter-for-jd-edwards-oneworld.md)   
 [追加の BizTalk Adapter for JD Edwards OneWorld](../core/adding-biztalk-adapter-for-jd-edwards-oneworld.md)