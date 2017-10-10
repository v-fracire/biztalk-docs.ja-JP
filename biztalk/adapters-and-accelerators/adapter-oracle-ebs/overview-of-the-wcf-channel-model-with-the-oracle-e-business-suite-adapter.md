---
title: "Oracle E-business Suite アダプターで WCF チャネル モデルの概要 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3afd2a97-5734-4c25-87a3-702d8461898b
caps.latest.revision: "8"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d59965b4fe5a94ae29ac8459ef8b8d80999c1dc5
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="overview-of-the-wcf-channel-model-with-the-oracle-e-business-suite-adapter"></a>Oracle E-business Suite アダプターで WCF チャネル モデルの概要
操作の呼び出しに、[!INCLUDE[adapteroracleebusinesslong](../../includes/adapteroracleebusinesslong-md.md)]コードが WCF クライアントとして機能し、アダプターに送信操作を送信します。 WCF チャネル モデルでは、コードは、チャネル経由で要求メッセージを送信することによって、アダプターでの操作を呼び出します。  
  
 ポーリングに基づくデータ変更を使用してメッセージの受信などの受信操作の呼び出しに、**ポーリング**操作は、コードが WCF サービスとして機能し、アダプターからの受信操作の受信アダプターによって提供されます。 言い換えると、コードは、チャネル経由で、アダプターから要求メッセージを受信します。  
  
 このセクションのトピックを使用しての概要を説明する、 [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] WCF チャネル モデルとします。  
  
## <a name="wcf-channel-model-overview"></a>WCF チャネル モデルの概要  
 クライアントとサービスは、SOAP メッセージを交換して通信します。 WCF チャネル モデルは、このメッセージ交換の低レベルの抽象化です。 インターフェイスとすると、チャネル スタックと呼ばれる階層状のプロトコル スタックを使用してメッセージを送受信できるようにする型を提供します。 スタックの各層は、チャネルから成るされ、WCF バインドから各チャネルが作成されます。 最下位の層で、トランスポート チャネルです。 トランスポート チャネルがサービスとクライアント間の基になるトランスポート機構を実装し、として上の層 (と最終的に処理を行うアプリケーション) を各メッセージを表示、 **System.ServiceModel.Message**です。 WCF**メッセージ**クラスは、SOAP メッセージの抽象化します。 WCF には、基本的な SOAP メッセージ交換パターンをモデルなどの要求/応答または一方向チャネル形状と呼ばれるいくつかのチャネル インターフェイスが用意されています。 WCF トランスポート バインディングは、1 つの実装を提供またはレイヤーの高い複数のチャネル形状がメッセージの送受信に使用できます。 WCF チャネル モデルの詳細についてを参照してください「チャネル モデルの概要」 [http://go.microsoft.com/fwlink/?LinkId=82614](http://go.microsoft.com/fwlink/?LinkId=82614)です。  
  
 [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]は、WCF サービスとして Oracle E-business Suite 成果物を公開する WCF カスタム トランスポート バインディングです。  
  
## <a name="supported-channel-shapes-for-the-oracle-e-business-suite-adapter"></a>Oracle E-business Suite アダプターのチャネル形状をサポート  
 アダプターでは、次の WCF チャネル形状を実装します。  
  
-   **IRequestChannel** (**System.ServiceModel.Channels.IRequestChannel**)。 **IRequestChannel**インターフェイスは、クライアント側の要求/応答メッセージ交換を実装します。 使用することができます、 **IRequestChannel**応答を消費する操作を実行するには、たとえば、SELECT を実行するためにクエリを実行インターフェイス テーブル。  
  
-   **IOutputChannel** (**System.ServiceModel.Channels.IOutputChannel**)。 この図形では、クライアント側の一方向メッセージ交換を実装します。 使用することができます、 **IOutputChannel**を OUT パラメーターを持たないプロシージャを呼び出す例については、応答を使用する必要のない、操作を呼び出します。  
  
    > [!IMPORTANT]
    >  Oracle クライアントにアダプターによってすべての基になる呼び出しは同期的です。 経由で呼び出された操作の結果は、Oracle クライアントへの呼び出しが含まれます、 **IOutputChannel**です。 使用すると、 **IOutputChannel**アダプターは、Oracle クライアントから受信した応答を破棄します。  
  
-   **IInputChannel** (**System.ServiceModel.Channels.IInputChannel**)。 この図形では、一方向メッセージ交換のサービス側を実装します。 使用する、 **IInputChannel**アダプターから受信メッセージを受信します。  
  
 任意の WCF バインドと同様に、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]ファクトリ パターンを使用してアプリケーション コードへのチャネルを提供します。 使用する、 **Microsoft.Adapters.OracleEBSBinding**オブジェクトのインスタンスを作成します。  
  
-   **System.ServiceModel.ChannelFactory\<IRequestChannel >**を提供する**IRequestChannel**チャネル アダプターの要求-応答操作の呼び出しに使用することができます。  
  
-   **System.ServiceModel.ChannelFactory\<IOutputChannel >**を提供する**IOutputChannel**チャネル アダプターの一方向の操作の呼び出しに使用することができます。  
  
-   **System.ServiceModel.IChannelListener\<IInputChannel >**を提供する**IInputChannel**チャネルがメッセージを受信する受信アダプターから行うこともできます。  
  
### <a name="creating-messages-for-the-oracle-enterprise-business-solution-in-the-wcf-channel-model"></a>WCF チャネル モデルの Oracle Enterprise ビジネス ソリューションのメッセージを作成  
 WCF では、 **System.ServiceModel.Channels.Message**クラスは、メモリに SOAP メッセージの表現。 作成する、**メッセージ**、静的なを呼び出すことによってインスタンス**Message.Create**メソッドです。  
  
 必要がありますを指定することを作成する場合、SOAP メッセージに 2 つの重要な部分、**メッセージ**インスタンスに送信する、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]です。  
  
-   メッセージのアクションは、SOAP メッセージ ヘッダーの一部である文字列です。 メッセージのアクションでは、Oracle E-business Suite で呼び出される操作を識別します。 呼び出しに指定されたメッセージのアクションを次に示します、**顧客インターフェイス**同時実行プログラム、**債権**Oracle E-business suite アプリケーション:`ConcurrentPrograms/AR/RACUST`です。  
  
-   メッセージの本文には、操作のパラメーターのデータが含まれています。 メッセージ本文がによって予期されるメッセージ スキーマに対応する整形式 xml で構成される、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]要求された操作にします。 次のメッセージ本文を呼び出すための要求メッセージを指定する、**顧客インターフェイス**同時実行プログラムです。  
  
    ```  
    <RACUST xmlns="http://schemas.microsoft.com/OracleEBS/2008/05/ConcurrentPrograms/AR">  
      <Description>Customer Interface Program</Description>  
      <StartTime></StartTime>  
      <CREATE_RECIPROCAL_CUSTOMER>Yes</CREATE_RECIPROCAL_CUSTOMER>  
      <ORG_ID>203</ORG_ID>  
    </RACUST>  
  
    ```  
  
 については、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]メッセージ スキーマと操作のアクションのメッセージを参照してください[メッセージと BizTalk Adapter for Oracle E-business Suite のメッセージ スキーマを](../../adapters-and-accelerators/adapter-oracle-ebs/messages-and-message-schemas-for-biztalk-adapter-for-oracle-e-business-suite.md)です。  
  
 **作成**メソッドはオーバー ロードされ、メッセージ本文を提供するためのさまざまなオプションを提供します。 次のコードを作成する方法を示しています、**メッセージ**インスタンスを使用して、 **XmlReader**をメッセージ本文を指定します。 このコードでは、メッセージの本文をファイルから読み取られます。  
  
```  
XmlReader readerIn = XmlReader.Create("ConcProgRequest.xml");  
Message messageIn = Message.CreateMessage(MessageVersion.Default,  
    "ConcurrentPrograms/AR/RACUST",  
    readerIn);  
```  
  
 ここで、ConProgRequest.xml には、要求メッセージが含まれています。  
  
> [!IMPORTANT]
>  メッセージのアクションを指定する必要があります、**メッセージ**インスタンス。 通常、これを行うときに、**メッセージ**インスタンスを作成します。  
  
## <a name="see-also"></a>参照  
 [WCF チャネル モデルを使用して Oracle E-business Suite アプリケーションを開発します。](../../adapters-and-accelerators/adapter-oracle-ebs/develop-oracle-e-business-suite-applications-using-the-wcf-channel-model.md)