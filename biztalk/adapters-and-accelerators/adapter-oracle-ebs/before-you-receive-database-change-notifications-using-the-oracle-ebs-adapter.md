---
title: Oracle E-business Suite アダプターを使用して通知を変更するデータベースを受信するための考慮事項 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 95bbb19e-8d31-4b27-8cfe-6760e4bb0808
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 07bdb873875d147911f2eb8cb2fd7a80ba01f67e
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36991355"
---
# <a name="considerations-for-receiving-database-change-notifications-using-the-oracle-e-business-suite-adapter"></a>受信側のデータベースに関する考慮事項は、Oracle E-business Suite アダプターを使用して通知を変更します。
このトピックではいくつかの考慮事項とベスト プラクティスを使用しているときに点に注意する必要があります[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]Oracle データベースからデータベースの通知を受け取ります。  
  
## <a name="considerations-while-using-the-adapter-to-receive-notifications"></a>アダプターを使用して通知を受信する場合の考慮事項  
 使用しているときに、次を考慮する必要があります、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]クエリ通知を受信します。  
  
- [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]アダプター クライアントに、Oracle データベースから受信すると、通知を渡すだけです。 アダプターは区別されません、さまざまな操作の通知など、挿入操作または更新操作の特定の通知があるのか、アダプターはすべての情報をありません。  
  
- 操作の通知メッセージは、その操作によって影響を受けたレコードの数の影響を受けません。 たとえば、アダプター クライアントで、Oracle データベース テーブルに挿入されたレコードの数に関係なく 1 つだけの通知メッセージが表示されます。  
  
- アダプターのクライアント アプリケーションが Oracle データベースから受信した通知の種類を解釈するためのロジックを含めることをお勧めします。 アダプターのクライアント アプリケーションを内の情報を抽出することによって行うことができます、 **\<情報\>** 受信した通知メッセージの要素。 挿入操作では受信した通知メッセージの例を次に示します。  
  
  ```  
  <?xml version="1.0" encoding="utf-8" ?>   
  <Notification xmlns="http://schemas.microsoft.com/OracleEBS/2008/05/Notification/">  
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
  
   内の値に注意してください、 **\<情報\>** 要素。 この値は、通知メッセージを受信した操作について説明します。 アプリケーション内で値を抽出するための機能があります、 **\<情報\>** 要素し、値に基づき、後続のタスクを実行します。 トピック[Oracle E-business Suite で特定のタスクを実行するプロセスの通知メッセージ](../../adapters-and-accelerators/adapter-oracle-ebs/process-notification-messages-to-complete-specific-tasks-in-oracle-ebs.md)が内の値を抽出する方法について説明されています、 **\<情報\>** 要素.  
  
- 理想的には、クライアント アプリケーションが通知を受信した後を同じレコードの後続の通知がないように、通知を受け取る既にレコードを更新する必要があります。 たとえば、 **ACCOUNTACTIVITY**を持つテーブルを**処理**列。 すべての新しいレコードに挿入されるため、 **ACCOUNTACTIVITY**テーブル内の値、**処理**列は常に ' n '。 内のレコード挿入操作の後など、 **ACCOUNTACTIVITY**テーブルは、次のようになります。  
  
  |アカウントのトランザクション ID|処理済み|  
  |----------------------------|---------------|  
  |10001|n|  
  
   アダプターのクライアントを設定する、新しく挿入されたレコードの通知を受信する、 **NotificaitonStatement**としてプロパティをバインドします。  
  
  ```  
  SELECT * FROM SCOTT.ACCOUNTACTIVITY WHERE PROCESSED = ‘n’  
  ```  
  
   その後、通知を受信するには、クライアント アプリケーションする必要がありますの値を設定、**処理**'y' の列が既にの通知を受け取ったレコードでは、notification ステートメントが動作しないようにします。 そのため、これを実現する、クライアント アプリケーションする必要があります、更新操作を実行で、 **ACCOUNTACTIVITY**テーブル。 更新操作の後で同じ記録、 **ACCOUNTACTIVITY**テーブルは、次のようになります。  
  
  |アカウントのトランザクション ID|処理済み|  
  |----------------------------|---------------|  
  |10001|y|  
  
   興味深いことに、更新操作では、通知をアダプターのクライアントに送信もう一度と、プロセス全体がもう一度繰り返されます。 そのため、クライアント アプリケーションには、このような不要な通知を破棄する必要なロジックが必要です。  
  
- 場合、 **NotifyOnListenerStart**プロパティのバインドは、アダプターは通知を送信アダプターのクライアントに受信場所を開始するたびにします。 バインド プロパティを使用し、通知メッセージを解釈する方法の詳細については、次を参照してください。[受信 Oracle E-business Suite データベース変更通知した後、受信場所のブレーク ダウン](../../adapters-and-accelerators/adapter-oracle-ebs/receive-oracle-ebs-database-change-notifications-after-a-receive-location-stops.md)します。  
  
## <a name="typical-orchestration-for-receiving-notifications"></a>通知を受信するための一般的なオーケストレーション  
 このセクションを使用して通知を受信するための一般的なオーケストレーション フローの概要、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]します。  
  
1. オーケストレーションを行う必要があります最初に行うことでは、受信した通知の種類を確認します。 確認事項は次のとおりです。  
  
   - かどうか、通知を受信場所の再起動を受信しました。  
  
   - Insert などのデータベース テーブルで操作の通知を受信したかどうかは、更新、または削除します。  
  
     オーケストレーションを含める必要があります、**式**図形内でメッセージの種類を決定する、xpath クエリを受信したとします。  
  
2. 通知の種類を使用した後、オーケストレーションは受信した通知の種類に基づいて特定のアクションを実行するための判断ブロックを含める必要があります。 これを実現するオーケストレーションを含める必要があります、**判断**図形。 **判断**図形から成る、**ルール**ブロックと**Else**ブロックします。 内で、**ルール**ブロックする条件を指定して、条件が満たされる場合は、特定の操作を実行するオーケストレーション図形を含める必要があります。 内で、 **Else**ブロック、条件の場合は、特定の操作を実行するオーケストレーション図形を含める必要があります*いない*満たします。  
  
   前述の推奨事項がで詳しく説明されている[Oracle E-business Suite で特定のタスクを実行するプロセスの通知メッセージ](../../adapters-and-accelerators/adapter-oracle-ebs/process-notification-messages-to-complete-specific-tasks-in-oracle-ebs.md)します。  
  
## <a name="see-also"></a>参照  
 [Oracle E-business Suite データベース変更通知 BizTalk Server を使用しての受信します。](../../adapters-and-accelerators/adapter-oracle-ebs/receive-oracle-ebs-database-change-notifications-using-biztalk-server.md)