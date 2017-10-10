---
title: "受信データベースの変更通知を使用して、Oracle Database アダプターに関する考慮事項 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 206439b9-0408-4fbb-80e3-cfda2f5a89a5
caps.latest.revision: "4"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 01894ab7011324d0f5a3eab84a4cea72e8186c14
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="considerations-for-receiving-database-change-notifications-using-the-oracle-database-adapter"></a>受信データベースの変更通知を使用して、Oracle Database アダプターに関する考慮事項
このトピックでは、いくつかの考慮事項とベスト プラクティスを使用しているときに点に注意する必要がある、 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)] Oracle データベースからデータベースの通知を受信します。  
  
## <a name="considerations-while-using-the-adapter-to-receive-notifications"></a>アダプターを使用して通知を受信するときの考慮事項  
 使用しているときに、次を考慮する必要があります、[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]クエリ通知を受信します。  
  
-   [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]アダプター クライアントに、Oracle データベースから受信する通知に渡します。 アダプターは区別されません、通知のさまざまな操作は、つまり、アダプター情報のない任意の挿入操作または更新操作は、特定の通知するかどうか。  
  
-   操作の通知メッセージは、その操作によって影響を受けたレコードの数の影響を受けません。 たとえば、アダプター クライアントに関係なく、Oracle データベース テーブルに挿入されるレコードの数、1 つだけの通知メッセージが表示されます。  
  
-   アダプターのクライアント アプリケーションに Oracle データベースから受信した通知の種類を解釈するためのロジックが含まれていることをお勧めします。 アダプター クライアント アプリケーションを内の情報を抽出することによって行うことができます、 **\<情報 >**通知を受信したメッセージの要素。 挿入操作用に受信した通知メッセージの例を次に示します。  
  
    ```  
    \<?xml version="1.0" encoding="utf-8" ?>   
    <Notification xmlns="http://Microsoft.LobServices.OracleDB/2007/03/Notification/">  
      <Details>  
        <NotificationDetails>  
          <ResourceName>SCOTT.ACCOUNTACTIVITY</ResourceName>   
          <Info>1</Info>   
          <QueryId>0</QueryId>   
        </NotificationDetails>  
      </Details>  
      <Info>Insert</Info>   
      <ResourceNames>  
        <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/Arrays">SCOTT.ACCOUNTACTIVITY</string>   
      </ResourceNames>  
      <Source>Data</Source>   
      <Type>Change</Type>   
    </Notification>  
  
    ```  
  
     内の値に注意してください、 **\<情報 >**要素。 この値は、通知メッセージを受信した操作について説明します。 アプリケーション内の値を抽出する機能を持つ必要があります、 **\<情報 >**要素し、値に基づいて、後続のタスクを実行します。 トピック[を Oracle データベースで特定のタスクの完了の通知メッセージの処理](../../adapters-and-accelerators/adapter-oracle-database/process-notification-messages-to-run-specific-tasks-in-oracle-db-using-biztalk.md)内の値を抽出する方法の手順を持つ、 **\<情報 >**要素。  
  
-   理想的には、クライアント アプリケーションは、通知を受信した後を通知を既に受信した同じレコードの後続の通知がされないように、レコードを更新する必要があります。 たとえば、 **ACCOUNTACTIVITY**を持つテーブル、**処理**列です。 すべての新しいレコードが挿入されるため、 **ACCOUNTACTIVITY**テーブル内の値、**処理**列は常に 'n' です。 内のレコード挿入操作の後など、 **ACCOUNTACTIVITY**テーブルは、次のようになります。  
  
    |アカウントのトランザクションの ID|処理済み|  
    |----------------------------|---------------|  
    |10001|n|  
  
     アダプターのクライアントを設定、新しく挿入したレコードの通知を受信する、 **NotificationStatement**バインディングとしてのプロパティ。  
  
    ```  
    SELECT * FROM SCOTT.ACCOUNTACTIVITY WHERE PROCESSED = ‘n’  
    ```  
  
     その後、通知を受信するには、クライアント アプリケーションする必要がありますの値を設定、**処理**'y' 列が既にの通知を受け取ったレコードでは、notification ステートメントが動作しないようにします。 そのため、これを実現する、クライアント アプリケーションする必要があります更新プログラムで操作を実行、 **ACCOUNTACTIVITY**テーブル。 内のレコード、同じ更新操作の完了後、 **ACCOUNTACTIVITY**テーブルは、次のようになります。  
  
    |アカウントのトランザクションの ID|処理済み|  
    |----------------------------|---------------|  
    |10001|y|  
  
     興味深いことに、更新操作は、アダプターのクライアントに通知を再度送信します。 および、プロセス全体はもう一度繰り返されます。 そのため、クライアント アプリケーションには、このような不要な通知を破棄する必要なロジックが必要です。  
  
-   場合、 **NotifyOnListenerStart**プロパティのバインドは、アダプターは通知を送信アダプター クライアントたびに、受信場所を開始します。 バインディング プロパティを使用し、通知メッセージを解釈する方法の詳細については、次を参照してください。[受信 Oracle データベースの変更通知した後、受信場所内訳](../../adapters-and-accelerators/adapter-oracle-database/receive-oracle-database-change-notifications-after-a-receive-location-breakdown.md)です。  
  
## <a name="typical-orchestration-for-receiving-notifications"></a>通知を受信するための一般的なオーケストレーション  
 このセクションで説明を使用して通知を受信するための一般的なオーケストレーション フロー、[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]です。  
  
1.  オーケストレーションが行う必要があります最初の手順では、受信した通知の種類を確認します。 確認事項は次のとおりです。  
  
    -   かどうか、受信場所の再起動の通知を受信しました。  
  
    -   Insert などのデータベース テーブル上の操作に対して、通知を受信したかどうかは、更新、または削除します。  
  
     オーケストレーションを含める必要があります、**式**図形、メッセージの種類を決定する、xpath クエリが受信されるとします。  
  
2.  通知の種類を使用した後、オーケストレーションは、受信した通知の種類に基づいて特定のアクションを実行する判断ブロックを含める必要があります。 そのため、オーケストレーションを含める必要があります、**判断**図形です。 **判断**図形から成る、**ルール**ブロックと**Else**ブロックします。 内で、**ルール**ブロック、条件を指定して、条件が満たされた場合、特定の操作を実行するオーケストレーション図形を含める必要があります。 内で、 **Else**ブロック、条件の場合は、特定の操作を実行するオーケストレーション図形を含める必要があります*されません*満たされています。  
  
 上記の推奨事項がで詳しく説明されている[を BizTalk Server を使用して Oracle データベースで特定のタスクの完了の通知メッセージの処理](../../adapters-and-accelerators/adapter-oracle-database/process-notification-messages-to-run-specific-tasks-in-oracle-db-using-biztalk.md)です。  
  
## <a name="see-also"></a>参照  
 [BizTalk Server を使用して Oracle データベースの変更通知を受け取る](../../adapters-and-accelerators/adapter-oracle-database/receive-oracle-database-change-notifications-using-biztalk-server.md)