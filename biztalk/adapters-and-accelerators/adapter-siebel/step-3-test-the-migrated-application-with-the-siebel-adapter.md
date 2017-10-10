---
title: "手順 3: Siebel アダプターを使用して移行されたアプリケーションのテスト |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 651ee1b2-52da-497a-84a5-67f1436cc3e6
caps.latest.revision: "4"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9d47d4e1e63cee106c3e00053ff6718ea0606516
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="step-3-test-the-migrated-application-with-the-siebel-adapter"></a>手順 3: Siebel アダプターを使用して移行されたアプリケーションをテストします。
![手順 3 3](../../adapters-and-accelerators/adapter-oracle-database/media/step-3of3.gif "Step_3of3")  
  
 **所要時間:** 5 分  
  
 **目標:**この手順では、アカウントのビジネス コンポーネントで挿入操作を実行することによって移行済みのアプリケーションをテストします。 これを行うには、vPrev Siebel アダプターを使用して生成されたスキーマに準拠している要求メッセージをドロップします。  
  
## <a name="prerequisites"></a>前提条件  
  
-   BizTalk Server 管理コンソールで物理ポートを BizTalk オーケストレーションの論理ポートにマップして、BizTalk アプリケーションを構成します。  
  
-   WCF ベースの Wcf-custom 送信ポートを使用する BizTalk アプリケーションを構成する[!INCLUDE[adaptersiebel_short](../../includes/adaptersiebel-short-md.md)]です。  
  
### <a name="to-test-the-migrated-application"></a>移行したアプリケーションをテストするには  
  
1.  Siebel_BussComp_Migration フォルダーから AccountInsert.xml 要求メッセージをコピーします。 この要求メッセージは、vPrev Siebel アダプターによって生成されたスキーマに準拠しています。 送信マップを使用して、Wcf-custom 送信ポートに変換 WCF ベースのスキーマに準拠するようにこの[!INCLUDE[adaptersiebel_short](../../includes/adaptersiebel-short-md.md)]Siebel システムに送信します。  
  
    ```  
    <Insert xmlns="http://schemas.microsoft.com/[Siebel://Business Objects/Account/Account]">  
      <AccountInsertRecordSet>  
        <AccountInsertRecord xmlns="http://schemas.microsoft.com/Business_Objects">  
          <Currency_Code>USD</Currency_Code>  
          <Customer_Account_Group>Sold-To-Party</Customer_Account_Group>  
          <Location>Location_1</Location>  
          <Main_Phone_Number>012345678</Main_Phone_Number>  
          <Name>John_Smith</Name>  
          <Party_Name>Party_Name_1</Party_Name>  
          <Primary_Address_Id></Primary_Address_Id>  
        </AccountInsertRecord>  
      </AccountInsertRecordSet>  
    </Insert>  
    ```  
  
2.  貼り付けをファイルにマップされているフォルダーに要求メッセージの受信場所。  
  
3.  オーケストレーションは、要求メッセージを使用して、Siebel システムに送信します。 WCF ベースのスキーマに準拠しているスキーマの Siebel システムからの応答が受信した[!INCLUDE[adaptersiebel_short](../../includes/adaptersiebel-short-md.md)]です。 受信マップを使用して、Wcf-custom 送信ポートに変換しますこの vPrev Siebel アダプター用のスキーマにします。 Siebel システムからの応答は、オーケストレーションの一部として定義されているその他のファイルの場所に保存されます。 上記の要求メッセージに対する応答は次のとおりです。  
  
    ```  
    \<?xml version="1.0" encoding="utf-8"?>  
    \<ns0:InsertResponse xmlns:ns0="http://schemas.microsoft.com/[Siebel://Business Objects/Account/Account]" xmlns:exposed="http://schemas.microsoft.com" xmlns:Business_Objects="http://schemas.microsoft.com/Business_Objects">  
      \<ns0:RowIDList>  
        \<exposed:String>1-8EWWZ\</exposed:String>  
      \</ns0:RowIDList>  
    \</ns0:InsertResponse>  
    ```  
  
## <a name="see-also"></a>参照  
 [チュートリアル 2: Siebel の BizTalk プロジェクトを移行します。](../../adapters-and-accelerators/adapter-siebel/tutorial-2-migrating-biztalk-projects-in-siebel.md)