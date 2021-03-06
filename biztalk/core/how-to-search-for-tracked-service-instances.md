---
title: 追跡サービス インスタンスを検索する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b6337df9-8c2e-4d4a-a64b-cc040f83bd91
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3770e871e7be022ff7f4597b8d3eb4d8f307cc37
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36966515"
---
# <a name="how-to-search-for-tracked-service-instances"></a>追跡対象サービス インスタンスを検索する方法
使用することができます、**クエリ** タブで、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールのすべての追跡サービス インスタンスを検索します。 サービス インスタンスを検索するには、アセンブリの名前とバージョン、有効期間の開始時刻と終了時刻、サービス クラスの名前またはインスタンス ID、ホスト名、エラー コード、サービス インスタンスの状態に基づいて検索できます。  

## <a name="prerequisites"></a>前提条件  
 ここで示す手順を実行するには、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Operators グループのメンバーとしてログオンする必要があります。  

### <a name="to-search-for-tracked-service-instances"></a>追跡対象サービス インスタンスを検索するには  

1. クリックして**開始**、 をクリックして**プログラム**、 をクリックして[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]、順にクリックします[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]します。  

2. コンソール ツリーで、展開**BizTalk Server 管理**、し、[BizTalk グループ] をクリックします。  

3. 詳細ウィンドウでをクリックして、**新しいクエリ**タブ。  

4. **クエリ式**グループに、**値**列で、**追跡サービス インスタンス**ドロップダウン リスト ボックスから。  

5. **フィールド名**列のアスタリスクの横にある空のドロップダウン リスト ボックスで、(* *\\* * *)、次の 1 つ以上選択します。  


   |          アイテム           |                     説明                      |
   |-------------------------|------------------------------------------------------|
   |    **アセンブリ名**    |    サービス インスタンスのアセンブリの名前。    |
   |  **アセンブリのバージョン**   |           サービス インスタンスのバージョン。           |
   |      **[終了時刻]**       |          サービス インスタンスの終了時刻。           |
   |     **エラー コード**      | サービス インスタンスに関連付けられているエラー コード。 |
   |      **Host Name**      |        サービス インスタンスのホスト名。        |
   |   **最大一致数**   |          一致項目の表示数を指定します。           |
   |    **サービス クラス**    |          サービス インスタンスのクラス。          |
   | **サービス インスタンス ID** |               サービス インスタンス ID。               |
   |    **[サービス名]**     |          サービス インスタンスの名前。           |
   |     **Start Time**      |       サービス インスタンスの開始時刻。        |
   |        **State**        |          サービス インスタンスの状態。          |


6. 完了、**値**で行った選択の適切な列、**フィールド名**列。  

7. 適切なクエリを実行して行を追加、**フィールド名**、**演算子**、および**値**列、およびクリック**実行クエリ**します。  

## <a name="see-also"></a>参照  
 [管理コンソールの [クエリ] タブの使用](../core/using-the-administration-console-query-tab.md)