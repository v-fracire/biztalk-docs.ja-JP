---
title: ストアド プロシージャを使用してポーリング Oracle E-business Suite |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e9e89dfe-f33a-436b-94c6-be78e84d5efd
caps.latest.revision: 21
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b0301a571fba8e768052fa9caaf1465abd8aa162
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36990915"
---
# <a name="poll-oracle-e-business-suite-using-stored-procedures"></a>ストアド プロシージャを使用してポーリング Oracle E-business Suite
構成することができます、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]継続的に、Oracle データベースをポーリングするストアド プロシージャを使用して、定期的なデータ変更メッセージを受信します。 ストアド プロシージャは、Oracle データベースをポーリングするアダプターを定期的に実行するポーリング ステートメントとして指定できます。  

 ポーリングを有効にするには、Wcf-custom または Wcf-oracleebs 特定のバインド プロパティの受信ポートを指定する必要があります。  アダプターがポーリングをサポートする方法の詳細については、次を参照してください。[受信呼び出しのポーリングを使用してサポート](../../adapters-and-accelerators/adapter-oracle-ebs/support-for-inbound-calls-using-polling.md)します。 ポーリング操作用の SOAP メッセージの構造については、次を参照してください。[ポーリング操作のメッセージ スキーマ](../../adapters-and-accelerators/adapter-oracle-ebs/message-schemas-for-the-polling-operations1.md)します。  

## <a name="configuring-a-polling-operation-with-oracle-e-business-adapter-binding-properties"></a>Oracle E-business アダプターのバインドのプロパティをポーリング操作を構成します。  
 次の表にまとめたものです、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]バインドのプロパティのデータ変更メッセージを受信するアダプターを構成するために使用します。 Wcf-custom または Wcf-oracleebs を構成するときにこれらのバインド プロパティの受信のポートを指定する必要があります、[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理コンソール。  


|         プロパティのバインド         |                                                                                                                                                                                                                                                                       説明                                                                                                                                                                                                                                                                       |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     **InboundOperationType**     |                                                                                                                                                                                                                   実行するかどうかを指定します、**ポーリング**または**通知**操作を受信します。 既定値は**ポーリング**します。                                                                                                                                                                                                                    |
| **PolledDataAvailableStatement** |                                                                                                                                                       すべてのデータがポーリングに使用できるかどうかを判断するアダプターを実行する SQL ステートメントを指定します。 指定したストアド プロシージャのレコードを使用できる場合にのみ、 **PollingInput**プロパティのバインドが実行されます。                                                                                                                                                       |
|       **PollingInterval**        |                                           秒単位で間隔を指定、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]に指定されたステートメントが実行される、 **PolledDataAvailableStatement**プロパティをバインドします。 既定値は 30 秒です。 ポーリング間隔は、連続するポーリングの間隔を決定します。 ステートメントは、指定した期間内で実行される、アダプターが間隔内の残りの時間の間スリープします。                                            |
|         **PollingInput**         | ポーリング ステートメントを指定します。 ストアド プロシージャを使用してポーリングする、このバインドのプロパティの全体の要求メッセージを指定する必要があります。 要求メッセージは、送信操作としてストアド プロシージャを呼び出すため、アダプターに送信すると、同じである必要があります。 既定値は null です。<br /><br /> 値を指定する必要があります**PollingInput**ポーリングを有効にするプロパティをバインドします。 ポーリング ステートメントの実行によって決定される、ポーリングに使用できるデータが場合にのみ、 **PolledDataAvailableStatement**プロパティをバインドします。 |
|        **PollingAction**         |                                                                                                                                               ポーリング操作のアクションを指定します。 特定の操作を使用して、操作を生成するメタデータからのポーリング アクションを決定することができます、[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]します。                                                                                                                                               |
|      **PostPollStatement**       |                                                                                                                                                                                                            指定されたステートメントの後に実行されるステートメント ブロックを指定します、 **PollingInput**プロパティのバインドを実行します。                                                                                                                                                                                                             |
|      **PollWhileDataFound**      |                                                                               指定するかどうか、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]ポーリング間隔を無視し、継続的にデータがポーリングされるテーブルで使用できる場合に、ポーリング ステートメントを実行します。 テーブルのデータがない場合は、アダプターは、指定されたポーリング間隔でポーリング ステートメントを実行する元に戻します。 既定値は false です。                                                                               |

 これらのプロパティの詳細については、次を参照してください。 [for Oracle E-business Suite バインド プロパティの BizTalk アダプターについて](../../adapters-and-accelerators/adapter-oracle-ebs/read-about-the-biztalk-adapter-for-oracle-e-business-suite-binding-properties.md)します。 使用する方法の詳細については、 [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)] Oracle データベースをポーリングするには、次のセクションを参照しています。  

## <a name="how-this-topic-demonstrates-polling"></a>このトピックでポーリングしていますか  
 示すために、このトピックでどのように[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]データの受信をサポート ストアド プロシージャを使用してメッセージを変更する BizTalk プロジェクトを作成し、Oracle データベースにポーリングを使用するストアド プロシージャのスキーマを生成します。 このトピックでは、ACCOUNTACTIVITY テーブルをポーリングするのに GET_ACTIVITYS ストアド プロシージャを使用します。 このストアド プロシージャは ACCOUNT_PKG パッケージで使用できます。 データベースでこれらのオブジェクトを作成するサンプルに付属の SQL スクリプトを実行することができます。  

> [!NOTE]
>  このトピックでポーリングをベース データベース テーブルは、サンプルで提供されるスクリプトを実行してこれを作成、ACCOUNTACTIVITY がテーブルでのオーケストレーションです。 インターフェイス テーブルなど、他のテーブルをポーリングするには、このトピックの説明に従って、同じような手順を実行する必要があります。  

 ポーリング操作を説明するために、次の項目行います。  

-   SELECT ステートメントを指定、 **PolledDataAvailableStatement**データがある、テーブルの中にポーリングされます (ACCOUNTACTIVITY) を決定するプロパティをバインドします。 この例では、としては、このバインド プロパティを設定できます。  

    ```  
    SELECT COUNT (*) FROM ACCOUNTACTIVITY  
    ```  

     これにより、ACCOUNTACTIVITY テーブルにいくつかのレコードがある場合にのみ、アダプターがポーリング ステートメントを実行します。  

-   一部として、要求メッセージを提供することで、GET_ACTIVITYS、ストアド プロシージャを実行、 **PollingInput**プロパティをバインドします。 このストアド プロシージャは ACCOUNTACTIVITY テーブル内のすべての行を取得し、アダプターから応答メッセージが表示されます。  

-   ブロックを実行する PL/SQL の一部として、 **PostPollStatement**プロパティをバインドします。 このステートメントは、ACCOUNTACTIVITY テーブルからのすべてのデータをデータベース内の別のテーブルに移動されます。 これは、次の時間と**PollingInput**は実行すると、それをフェッチできませんすべてのデータとその GET_ACTIVITYS ストアド プロシージャは空の応答メッセージを返します。  

-   多くのデータは ACCOUNTACTIVITY テーブルに追加されるまで空の応答メッセージを取得する続けます。 そのため、新しいレコードを含む ACCOUNTACTIVITY テーブルを再作成する必要があります。 サンプルで提供される more_activity_data.sql スクリプトを実行して行うことができます。 このスクリプトを実行した後、次のポーリング操作によって新しいレコードをテーブルに挿入がフェッチされます。  

## <a name="how-to-receive-data-change-messages-from-oracle"></a>Oracle からのデータ変更メッセージを受信する方法  
 使用して Oracle データベースでの操作を実行する[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]で[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]で説明されている次の手順のタスクが含まれます[Oracle E-business Suite 学ぶことのできるを作成する構成要素](../../adapters-and-accelerators/adapter-oracle-ebs/building-blocks-to-create-oracle-e-business-suite-applications.md)します。 これらのタスクは、ストアド プロシージャを使用して Oracle データベースをポーリングするアダプターを構成するには。  

1. BizTalk プロジェクトを作成し、ポーリングに使用するストアド プロシージャのスキーマを生成します。  

2. Oracle データベースからメッセージを受信するための BizTalk プロジェクトでは、メッセージを作成します。  

3. Oracle データベースからメッセージを受信し、フォルダーに保存するためのオーケストレーションを作成します。  

4. ビルドし、BizTalk プロジェクトを配置します。  

5. BizTalk 物理を作成してアプリケーションの送信および受信ポートを構成します。  

   > [!IMPORTANT]
   >  常に設定する必要があります、ポーリングの受信シナリオの一方向の受信ポート。 双方向受信ポートは受信操作のサポートされていません。  

6. BizTalk アプリケーションを起動します。  

   このトピックでは、これらのタスクを実行する手順を説明します。  

## <a name="sample-based-on-this-topic"></a>このトピックに基づくサンプル  
 サンプル PollingUsingStoredProc、ベースのこのトピックでは、BizTalk Adapter Pack 付きも提供されます。 詳細については、次を参照してください。[サンプル](../../adapters-and-accelerators/adapter-oracle-ebs/samples-for-the-oracle-ebs-adapter.md)します。  

## <a name="generating-schema"></a>スキーマを生成します。  
 GET_ACTIVITYS 操作用のスキーマを生成する必要があります。 使用して、スキーマの生成中に、次のタスクを実行、[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]します。  

- コントラクトの種類を選択します。**サービス (受信操作)** します。  

- スキーマの生成、 **GET_ACTIVITYS**プロシージャ。  

  スキーマを生成する方法の詳細については、次を参照してください。[参照、検索、および Oracle E-business 操作のメタデータを取得](../../adapters-and-accelerators/adapter-oracle-ebs/browse-search-and-get-metadata-for-oracle-e-business-suite-operations.md)します。  

## <a name="defining-messages-and-message-types"></a>メッセージおよびメッセージの種類を定義します。  
 以前に生成したスキーマには、オーケストレーション内のメッセージに必要な「型」について説明します。 メッセージは、通常、対象の型が、対応するスキーマで定義されている、変数です。 スキーマが生成されるは、BizTalk プロジェクトのオーケストレーションからメッセージをリンクする必要があります。  

 このトピックでは、Oracle からメッセージを受信する 1 つのメッセージを作成する必要があります。  

 メッセージを作成し、スキーマにリンクするには、次の手順を実行します。  

#### <a name="to-create-messages-and-link-to-schema"></a>メッセージを作成し、スキーマにリンクするには  

1. オーケストレーションを BizTalk プロジェクトに追加します。 ソリューション エクスプ ローラーで、BizTalk プロジェクト名を右クリックして**追加**、 をクリックし、**新しい項目の**します。 BizTalk オーケストレーションの名前を入力し、クリックして**追加**します。  

2. 開いていない場合は、BizTalk プロジェクトのオーケストレーション ビュー ウィンドウを開きます。 をクリックして**ビュー**、 をポイント**その他の Windows**、順にクリックします**オーケストレーション**します。  

3. **オーケストレーション**、右クリック**メッセージ**、順にクリックします**新しいメッセージ**します。  

4. 新しく作成されたメッセージを右クリックし、**プロパティ ウィンドウ**します。  

5. **プロパティ**ウィンドウ **[message_1]** 次の操作を行います。  

   |プロパティ|目的|  
   |--------------|----------------|  
   |[Identifier]|型**受信**します。|  
   |メッセージ型|ドロップダウン リストから展開**スキーマ**、選択と*Polling.OracleEBSBindingSchema*ここで、*ポーリング*BizTalk プロジェクトの名前を指定します。 *OracleEBSBindingSchema*に対して生成される応答スキーマには、 **GET_ACTIVITYS**ストアド プロシージャ。<br /><br /> **重要:** ポーリングは、一方向の操作で、アダプターによって生成されたスキーマに、応答のノードが含まれていないスキーマには 1 つだけのルート ノードがない、したがってためです。 このようなスキーマのメッセージの種類を使用する場合、生成されたスキーマのファイル名でスキーマを識別する必要があります。<br /><br /> たとえば、双方向の操作のスキーマを作成する場合、スキーマ内のノード ファイルの名前を持つ`OracleEBSBindingSchema`「要求」と「応答」のようになります。 要求スキーマにマップするオーケストレーションでメッセージを作成する場合を探すことによって、リスト内のスキーマを識別できます`OracleEBSBindingSchema.Request`します。 ただし、ポーリング操作の場合、唯一のノードが「ポーリング」であるため簡単ではありませんの 1 つのノードのスキーマとしてリストされていないためにマップするスキーマを識別するために\<schemafilename\>.\<rootnodename\>します。 代わりに、このようなスキーマ ファイル名のみが表示されます。 このような場合は、スキーマ ファイル名、たとえば、OracleEBSBindingSchema では、スキーマを識別するしかありません。|  

    [!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)] GET_ACTIVITYS の受信と送信の両方の操作のストアド プロシージャでは、スキーマを生成します。 操作が受信するスキーマを使用する必要があります。  

   - オーケストレーションの一部として作成されたメッセージをマップします。  

   - 指定する必要がありますアクションを取得する、 **PollingAction**実行時にプロパティをバインドします。  

     送信操作のスキーマを使用して、一部として指定する必要があります、要求メッセージを取得する必要があります、 **PollingInput**プロパティをバインドします。  

## <a name="setting-up-the-orchestration"></a>オーケストレーションのセットアップ  
 使用する BizTalk オーケストレーションを作成する必要があります[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]Oracle からのポーリング ベースのデータ変更メッセージを受信するためです。 このオーケストレーションでアダプターがの一部として、要求メッセージを指定したストアド プロシージャを実行して、応答を受信、 **PollingInput**プロパティをバインドします。 ストアド プロシージャの応答メッセージは、ファイルの場所に保存されます。 Oracle データベースをポーリングするための一般的なオーケストレーションが含まれます。  

- 受信図形と送信図形を Oracle からメッセージを受信し、それぞれ、ファイルのポートに送信します。  

- 一方向の受信ポートの Oracle データベースからメッセージを受信します。  

  > [!IMPORTANT]
  >  常に設定する必要があります、ポーリングの受信シナリオの一方向の受信ポート。 双方向受信ポートは受信操作のサポートされていません。  

- Oracle データベースからポーリング応答を送信する一方向の送信ポート。  

  サンプル オーケストレーションでは、次の項目に似ています。  

  ![Oracle のポーリング クエリのオーケストレーション](../../adapters-and-accelerators/adapter-oracle-database/media/6eddfe32-bfd0-4bd9-9e2a-fb4a7d0b53e3.gif "6eddfe32-bfd0-4bd9-9e2a-fb4a7d0b53e3")  

### <a name="adding-message-shapes"></a>メッセージの構築図形を追加します。  
 メッセージの構築図形のごとに、次のプロパティを指定することを確認します。 図形の列に示した名前は、単に説明したオーケストレーションに表示されるメッセージの構築図形の名前です。  

|図形|図形の種類|[プロパティ]|  
|-----------|----------------|----------------|  
|ReceiveMessage|Receive|-設定**名前**に*ReceiveMessage*<br /><br /> -設定**アクティブ**に*は True。*|  
|SaveMessage|Send|-設定**名前**に*SaveMessage*|  

### <a name="adding-ports"></a>ポートの追加  
 論理ポートごとに、次のプロパティを指定することを確認します。 ポート列に示した名前は、オーケストレーションで表示されているポートの名前です。  

|Port|[プロパティ]|  
|----------|----------------|  
|OracleReceivePort|-設定**識別子**に*OracleReceivePort*<br /><br /> -設定**型**に*OracleReceivePortType*<br /><br /> -設定**通信パターン**に*一方向*<br /><br /> -設定**通信方向**に*受信*|  
|SaveMessagePort|-設定**識別子**に*SaveMessagePort*<br /><br /> -設定**型**に*SaveMessagePortType*<br /><br /> -設定**通信パターン**に*一方向*<br /><br /> -設定**通信方向**に*送信*|  

### <a name="specify-messages-for-action-shapes-and-connect-to-ports"></a>アクション図形のメッセージを指定し、ポートに接続  
 次の表では、プロパティとアクション図形のメッセージを指定して、メッセージ ポートにリンクを設定する必要があります、値を指定します。 図形の列に示した名前は、前に説明したオーケストレーションに表示されるメッセージの構築図形の名前です。  

|図形|[プロパティ]|  
|-----------|----------------|  
|ReceiveMessage|-設定**メッセージ**に*受信*<br /><br /> -設定**操作**に*OracleReceivePort.Polling.Request*|  
|SaveMessage|-設定**メッセージ**に*受信*<br /><br /> -設定**操作**に*SaveMessagePort.Polling.Request*|  

 これらのプロパティを指定したら、メッセージの構築図形とポートが接続されているし、オーケストレーションが完了します。  

 ここで、BizTalk ソリューションをビルドしに配置する必要があります、[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]します。 詳細については、次を参照してください。[を実行しているオーケストレーションのビルドと](../../core/building-and-running-orchestrations.md)します。

## <a name="configuring-the-biztalk-application"></a>BizTalk アプリケーションを構成します。  
 先ほど作成したオーケストレーションが 下にある BizTalk プロジェクトを配置した後、**オーケストレーション**BizTalk Server 管理コンソール ウィンドウ。 BizTalk Server 管理コンソールを使用して、アプリケーションを構成する必要があります。 チュートリアルについては、次を参照してください。[チュートリアル: 基本的な BizTalk アプリケーションの展開](Walkthrough:%20Deploying%20a%20Basic%20BizTalk%20Application.md)します。

 アプリケーションを構成する必要があります。  

- アプリケーションのホストを選択します。  

- BizTalk Server 管理コンソールで物理ポートにオーケストレーションで作成したポートをマッピングします。 このオーケストレーションの次の操作を行う必要があります。  

  - ハード ディスクと、対応するファイル ポートを BizTalk オーケストレーション Oracle からのメッセージをドロップできる場所での場所を定義します。 これらのメッセージは、受信ポートの指定したポーリング ステートメントへの応答になります。  

  - Wcf-oracleebs 一方向受信ポートまたは物理 Wcf-custom を定義します。 このポートは、Oracle データベースをポーリングします。 受信ポートを作成する方法についてを参照してください[、Oracle E-business アダプターを物理ポート バインドを手動で構成](../../adapters-and-accelerators/adapter-oracle-ebs/manually-configure-a-physical-port-binding-to-the-oracle-e-business-adapter.md)します。 受信ポートのバインドのプロパティを指定することを確認します。  


    |         プロパティのバインド         |                                                                                                                                                                                                                                                                                                                                                  値                                                                                                                                                                                                                                                                                                                                                   |
    |----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    |     **InboundOperationType**     |                                                                                                                                                                                                                                                                                                                                         これを設定**ポーリング**します。                                                                                                                                                                                                                                                                                                                                         |
    | **PolledDataAvailableStatement** |                                                                                                                                                                                                                                    この例このバインドのプロパティを設定します。<br /><br /> `SELECT COUNT (*) FROM ACCOUNTACTIVITY`<br /><br /> これにより、ACCOUNTACTIVITY テーブルにいくつかのレコードがある場合にのみ、アダプターがポーリング ステートメントを実行します。                                                                                                                                                                                                                                    |
    |        **PollingAction**         |                                                                                                                                                                                                                                           GET_ACTIVITYS 手順については、受信メッセージの生成スキーマからポーリング アクションを取得します。 この例でこのバインドのプロパティを設定**PollingPackageApis/アプリ/ACCOUNT_PKG/GET_ACTIVITYS**します。                                                                                                                                                                                                                                           |
    |         **PollingInput**         | このバインドのプロパティでは、ストアド プロシージャを呼び出す、GET_ACTIVITYS 要求メッセージを指定します。 によって生成された送信操作のスキーマから要求メッセージを取得できます、[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]します。 このバインドのプロパティの入力として全体の XML メッセージを指定する必要があります。 この例このバインドのプロパティを設定します。<br /><br /> `<GET_ACTIVITYS xmlns="http://schemas.microsoft.com/OracleEBS/2008/05/PackageApis/APPS/ACCOUNT_PKG">   <INRECS>OPEN ? FOR SELECT * FROM ACCOUNTACTIVITY</INRECS> </GET_ACTIVITYS>`<br /><br /> GET_ACTIVITYS は、プロシージャは入力の REF CURSOR をパラメーターとして格納されます。 |
    |      **PostPollStatement**       |                                                                                                                                                                                                                                                  ACCOUNTACTIVITY テーブルから別のテーブルにすべてのデータを移動するポスト ポーリング ステートメントを指定します。 この例このバインドのプロパティを設定します。<br /><br /> `BEGIN ACCOUNT_PKG.PROCESS_ACTIVITY(); END;`                                                                                                                                                                                                                                                  |

     異なるバインディング プロパティの詳細については、次を参照してください。[については、BizTalk Adapter for Oracle E-business Suite バインド プロパティを読み取る](../../adapters-and-accelerators/adapter-oracle-ebs/read-about-the-biztalk-adapter-for-oracle-e-business-suite-binding-properties.md)します。  

    > [!IMPORTANT]
    >  インターフェイス テーブルをポーリングする場合は、必要なバインドのプロパティを指定することで、アプリケーションのコンテキストを設定する必要があります。 アプリケーション コンテキストの設定の詳細については、次を参照してください。[アプリケーション コンテキストの設定](../../adapters-and-accelerators/adapter-oracle-ebs/set-application-context.md)します。  
    > 
    > [!NOTE]
    >  使用して受信操作の実行中に、トランザクション分離レベルとトランザクションのタイムアウトを構成することをお勧めします。、[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]します。 WCF カスタムを構成するときに、サービスの動作を追加することで行うことができますか、Wcf-oracleebs 受信ポート。 サービスの動作を追加する方法については、次を参照してください。[トランザクション分離レベルの構成と Oracle E-business Suite でのトランザクション タイムアウト](../../adapters-and-accelerators/adapter-oracle-ebs/configure-transaction-isolation-level-and-transaction-timeout-with-oracle-ebs.md)します。  

## <a name="starting-the-application"></a>アプリケーションの起動  
 Oracle データベースをポーリングするための BizTalk アプリケーションを起動する必要があります。 BizTalk アプリケーションを開始する手順については、次を参照してください。[オーケストレーションを開始する方法](../../core/how-to-start-an-orchestration.md)します。

 この段階で、ことを確認します。  

-   Wcf-custom または Wcf-oracleebs 一方向受信ポートで、指定されたストアド プロシージャを使用して Oracle のポーリング、 **PollingInput**プロパティ、バインドが実行されています。  

-   、Oracle データベースからメッセージを受信する FILE 送信ポートが実行されています。  

-   操作の BizTalk オーケストレーションが実行されています。  

## <a name="executing-the-operation"></a>操作の実行  
 アプリケーションを実行した後、次の一連のアクションに、同じシーケンスを実行します。  

-   アダプターが実行、 **PolledDataAvailableStatement**アダプターに指定されたステートメントを実行することを示す正の値を返す**PollingInput**プロパティをバインドします。  

-   アダプターの指定された GET_ACTIVITYS ストアド プロシージャを実行する、 **PollingInput** ACCOUNTACTIVITY テーブルのプロパティを返しますのすべての行をバインドします。 Oracle データベースからの応答には、次のようになります。  

    ```  
    <?xml version="1.0" encoding="utf-8" ?>   
    <GET_ACTIVITYS xmlns="http://schemas.microsoft.com/OracleEBS/2008/05/PollingPackageApis/APPS/ACCOUNT_PKG">  
      <OUTRECS>  
        <OUTRECSRecord xmlns="http://schemas.microsoft.com/OracleEBS/2008/05/ReferencedRecordTypes/APPS/ACCOUNT_PKG/GET_ACTIVITYS/APPS/GET_ACTIVITYS">  
          <TID>1</TID>   
          <ACCOUNT>100001</ACCOUNT>   
          <AMOUNT>500</AMOUNT>   
          <DESCRIPTION />   
          <TRANSDATE>2008-06-21T15:52:19</TRANSDATE>   
          <PROCESSED>n</PROCESSED>   
        </OUTRECSRecord>  
        <OUTRECSRecord xmlns="http://schemas.microsoft.com/OracleEBS/2008/05/ReferencedRecordTypes/APPS/ACCOUNT_PKG/GET_ACTIVITYS/APPS/GET_ACTIVITYS">  
          ......  
          ......   
        </OUTRECSRecord>  
        ......  
        ......  
      </OUTRECS>  
    </GET_ACTIVITYS>  
    ```  

-   アダプターは、ポーリング後ステートメントは、ACCOUNTACTIVITY テーブルからすべてのデータを別のテーブルに移動します。 これを実行します。  

-   ポーリング間隔の後、アダプターをもう一度実行します**PolledDataAvailableStatement**します。 ACCOUNTACTIVITY テーブルにはレコードがあるない、ため**PolledDataAvailableStatement**正の値を返さないため、アダプターに指定されたステートメントを実行しないと、 **PollingInput**プロパティをバインドします。 結果として、アダプターのクライアントは、ポーリング メッセージを取得できません。  

-   レコードの一部は明示的な ACCOUNTACTIVITY テーブルに挿入されるまで、アダプター クライアントは、これ以上ポーリング メッセージを取得できません。 以上のレコードを挿入するには、サンプルで提供される more_activity_data.sql スクリプトを実行することができます。 次に、このスクリプトを実行した後**PolledDataAvailableStatement**が実行すると、正の値を返します。 結果として、アダプターがポーリング ステートメントを実行し、アダプター クライアントは再度ポーリング メッセージを受信します。  

> [!NOTE]
>  [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]ポーリングからの受信ポートを明示的に無効にするまでは引き続き、[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理コンソール。  

## <a name="best-practices"></a>ベスト プラクティス  
 展開し、BizTalk プロジェクトの構成後は、バインド ファイルと呼ばれる XML ファイル構成設定をエクスポートできます。 バインド ファイルを生成すると、送信ポートを作成し、同じオーケストレーション用のポートを受信する必要はありませんように構成設定ファイルからインポートできます。 バインド ファイルの詳細については、次を参照してください。 [SQL アダプターのバインドを再利用](../../adapters-and-accelerators/adapter-sql/reuse-sql-adapter-bindings.md)します。  

## <a name="see-also"></a>参照  
 [BizTalk Server を使用してポーリング Oracle E-business Suite](../../adapters-and-accelerators/adapter-oracle-ebs/poll-oracle-e-business-suite-using-biztalk-server.md)