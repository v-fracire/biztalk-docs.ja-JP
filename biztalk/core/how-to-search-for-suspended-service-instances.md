---
title: "中断されたサービス インスタンスを検索する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- service instances, viewing
- service instances, Query tab [Administration Console]
- Query tab [Administration Console], service instances
- service instances, suspended
- Query tab [Administration Console], searching
- instances, suspended
- instances, services
ms.assetid: f91b1151-d879-4aa7-afc8-4cf13d928158
caps.latest.revision: "19"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 52c0d3ad192ad2cc8f4429f78cfa38ddc97ac837
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-search-for-suspended-service-instances"></a>中断されたサービス インスタンスを検索する方法
使用することができます、**クエリ** タブで、BizTalk Server 管理コンソールの中断されたサービス インスタンスを検索します。 メッセージの特定のサブセットを検索して、サービス名、種類、ホストなどに関連付けられた特定のメッセージを見つけることができます。  
  
> [!NOTE]
>  終了 (メッセージ未消費) インスタンスは、該当する中断されたサービス インスタンスにエラー コード ("終了 (メッセージ未消費)") として表示されます。 これらのインスタンスは再開できません。  
  
> [!NOTE]
>  URI またはエラー アダプター名によるグループ化とフィルター選択を行うと、検索結果には送信ポートと受信ポートのみが表示されます。 URI によるグループ化とフィルター選択はオーケストレーションには使用できないので、表示される結果にオーケストレーションは含まれません。  
  
## <a name="prerequisites"></a>前提条件  
 ここで示す手順を実行するには、BizTalk Server Operators グループのメンバーとしてログオンする必要があります。  
  
### <a name="to-search-for-suspended-service-instances"></a>中断されたサービス インスタンスを検索するには  
  
1.  をクリックして**開始**、 をクリックして**すべてのプログラム**、 をクリックして**Microsoft**[!INCLUDE[btsBizTalkServer2006r3ui](../includes/btsbiztalkserver2006r3ui-md.md)]、順にクリック**BizTalk Server 管理コンソール**です。  
  
2.  コンソール ツリーで  **BizTalk Server 管理コンソール**、し、BizTalk グループ をクリックします。  
  
3.  詳細ウィンドウで、をクリックして、**新しいクエリ**タブです。  
  
4.  **クエリ式**グループにおいて、**値**列で、選択**中断サービス インスタンスの**ドロップダウン リスト ボックスからです。  
  
5.  **フィールド名**列のアスタリスクの横にある空のドロップダウン リスト ボックスで、(**\***)、次の 1 つ以上選択します。  
  
    |アイテム|Description|  
    |----------|-----------------|  
    |**Application Name**|BizTalk Server アプリケーションの名前です。|  
    |**作成日時**|中断されたサービス インスタンスの中で、指定した日付の前または後に作成されたインスタンスを検索します。|  
    |**エラー アダプター**|中断されたサービス インスタンスをアダプターの種類でグループ化またはフィルター選択できます。 例: ファイル、FTP、HTTP、MQSeries、MSMQ、POP3、SMTP、SOAP、または Windows SharePoint Services です。 **注:**クエリの結果に指定したアダプターの使用中にエラーが発生、BizTalk Server ランタイムの実行時にアダプター フィールドは設定のみです。 ランタイムでアダプターのエラーが検出されなかった場合、クエリ結果の "エラー アダプター" フィールドは空になります。|  
    |**エラー コード**|中断されたサービス インスタンスをエラー コードでグループ化またはフィルター選択して、そのエラー コードで中断されたすべてのサービス インスタンスを表示できます。|  
    |**エラーの説明**|中断されたサービス インスタンスを、指定したエラーの説明でグループ化またはフィルター選択できます。|  
    |**結果をグループ化**|アダプター、アプリケーション、エラー コード、エラーの説明、ホスト名、サービス クラス、サービス インスタンスの状態、サービス名、または URI で結果をグループ化またはフィルター選択できます。|  
    |**Host Name**|中断されたサービス インスタンスをホスト名でグループ化またはフィルター選択します。|  
    |**インスタンスの状態**|中断されたインスタンスの中で再開できないインスタンスまたは再開できるインスタンスを検索できます。|  
    |**最大一致数**|一致項目の表示数を指定します。|  
    |**サービス クラス**|[分離アダプター]、[メッセージング]、[メッセージング、分離アダプター]、[MSMQT]、[オーケストレーション]、または [ルーティング エラー報告] を指定して検索できます。|  
    |**サービス名**|中断されたサービス インスタンスをサービス名でグループ化またはフィルター選択できます。|  
    |**サービスの種類 ID**|中断されたサービス インスタンスをサービスの種類 ID でグループ化またはフィルター選択できます。|  
    |**[中断時間]**|指定した日付の前または後に中断されたサービス インスタンスをグループ化またはフィルター選択できます。|  
    |**URI**|中断されたサービス インスタンスを URI でグループ化またはフィルター選択できます。 **注:**クエリの結果に URI にのみ設定されます指定 URI に送信中にエラーが発生、BizTalk Server ランタイムを実行するとします。 URI への送信中にランタイムでエラーが検出されなかった場合、クエリ結果の "URI" フィールドは空になるか、または URI が利用できないことが表示されます。|  
  
6.  完了、**値**で行う選択範囲の適切な列、**フィールド名**列です。  
  
7.  実行し、必要に応じて、クエリに行を追加、**フィールド名**、**演算子**、および**値**列、およびクリック**実行クエリ**です。  
  
## <a name="see-also"></a>参照  
 [管理コンソールの [クエリ] タブを使用します。](../core/using-the-administration-console-query-tab.md)