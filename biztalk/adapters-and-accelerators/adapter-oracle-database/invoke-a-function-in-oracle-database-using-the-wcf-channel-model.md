---
title: "WCF チャネル モデルを使用して Oracle データベース内の関数を呼び出す |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- channel programming, executing a function
- WCF channel model, invoking a function
- how to, execute a function using a channel
- executing a function, using a channel
ms.assetid: 6c15c352-3086-44f6-b265-4c7a7aee47ff
caps.latest.revision: "3"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: bc38e0ce4dc1f6ae184b51ee157fb4461364a85e
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="invoke-a-function-in-oracle-database-using-the-wcf-channel-model"></a>WCF チャネル モデルを使用して Oracle データベース内の関数を呼び出す
このセクションでは、関数で作成されたチャネルを使用して Oracle データベースで実行する方法を示します[Oracle データベースを使用して、チャネルの作成](../../adapters-and-accelerators/adapter-oracle-database/create-a-channel-using-oracle-database.md)です。  
  
## <a name="executing-a-function-using-the-channel"></a>チャネルを使用して関数を実行します。  
 Oracle データベースで関数を実行するには、XML メッセージを渡すことによって[!INCLUDE[adapteroracle](../../includes/adapteroracle-md.md)]です。 入力 XML には、次のようになります。  
  
```  
\<CREATE_ACCOUNT xmlns="http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Package/ACCOUNT_PKG" xmlns:ns0="http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Package/ACCOUNT_PKG/CREATE_ACCOUNT">  
  <REC xmlns="http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Package/ACCOUNT_PKG">  
    \<ns0:ID>1\</ns0:ID>  
    \<ns0:NAME>Scott\</ns0:NAME>  
    \<ns0:BANKNAME>CitiBank\</ns0:BANKNAME>  
    \<ns0:BRANCH>NY\</ns0:BRANCH>  
    \<ns0:ENABLED>Y\</ns0:ENABLED>  
  </REC>  
</CREATE_ACCOUNT>  
```  
  
 次のコードの抜粋では、チャネルを使用して Oracle データベースで関数を実行する方法を示します。  
  
```  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Xml;  
  
using System.ServiceModel;  
using System.ServiceModel.Channels;  
  
using Microsoft.ServiceModel.Adapters;  
using Microsoft.Adapters.OracleDB;  
  
namespace OraclePackageChannel  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            // Create Endpoint  
            EndpointAddress address = new EndpointAddress("oracledb:// ADAPTER");  
  
            // Create Binding  
            OracleDBBinding binding = new OracleDBBinding();  
  
            // Create Channel Factory  
            ChannelFactory<IRequestChannel> factory = new ChannelFactory<IRequestChannel>(binding, address);  
            factory.Credentials.UserName.UserName = "SCOTT";  
            factory.Credentials.UserName.Password = "TIGER";  
            factory.Open();  
  
            // Create Request Channel  
            IRequestChannel channel = factory.CreateChannel();  
            channel.Open();  
  
            // Send Request  
            System.Xml.XmlReader readerIn = System.Xml.XmlReader.Create("Create_Account.xml");  
  
            Message messageIn = Message.CreateMessage(MessageVersion.Default, "http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Package/ACCOUNT_PKG/CREATE_ACCOUNT", readerIn);  
            Message messageOut = channel.Request(messageIn);  
  
            // Get Response XML  
            XmlReader readerOut = messageOut.GetReaderAtBodyContents();  
  
            // Get Employee ID  
            XmlDocument doc = new XmlDocument();  
            doc.Load(readerOut);  
            doc.Save("d:\\out.xml");  
  
            messageOut.Close();  
            channel.Close();  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>参照  
 [WCF チャネル モデルを使用して Oracle データベース アプリケーションを開発します。](../../adapters-and-accelerators/adapter-oracle-database/develop-oracle-database-applications-using-the-wcf-channel-model.md)   
 [WCF チャネル モデルを使用して Oracle データベースで挿入操作を実行します。](../../adapters-and-accelerators/adapter-oracle-database/run-an-insert-operation-in-oracle-database-using-the-wcf-channel-model.md)   
 [WCF チャネル モデルを使用して、SQLEXECUTE 操作を実行します。](../../adapters-and-accelerators/adapter-oracle-database/run-a-sqlexecute-operation-in-oracle-database-using-the-wcf-channel-model.md)