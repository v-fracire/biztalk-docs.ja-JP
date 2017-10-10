---
title: "送信 Port2 を作成する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: bts10.admin.procedure.createsendport
helpviewer_keywords:
- managing [send ports], creating
- creating, send ports
- send ports, creating
ms.assetid: 7f0d07b8-1ac5-4032-bb08-2f7e05185f86
caps.latest.revision: "24"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 796ba5da53257d0f198e4b8bf13ee81835efcf4e
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-create-a-send-port"></a>送信ポートを作成する方法
このトピックでは、BizTalk Server 管理コンソールを使用して、送信ポートを作成する方法について説明します。 送信ポートを作成する場合、次のような送信ポートの種類を選択する必要があります。  
  
-   静的な一方向 : 送信のみのポート。  
  
-   静的な送信請求 - 応答 : 送信先からの応答を待つ送信ポート。  
  
-   動的な一方向 : 実行時にメッセージ プロパティに基づいてプロトコルおよび場所にバインドできる送信のみのポート。  
  
-   動的な送信請求 - 応答 : 応答を待つ送信ポート。実行時にメッセージ プロパティに基づいてプロトコルおよび場所にバインドできます。  
  
 送信ポートを作成した後で、次の追加のステップを実行することにより構成を完了できます。  
  
-   構成の詳細」の説明に従って、メッセージのエラーや、ポートのサービス ウィンドウ スケジュールでのメッセージの送信を再試行する回数などのトランスポート オプション[トランスポート高度なオプションの構成、送信ポートの方法](../core/how-to-configure-transport-advanced-options-for-a-send-port.md)です。  
  
-   バックアップ トランスポートを構成する」の説明に従って、機能するために、主要なトランスポートが失敗した場合に備えて[送信ポートに対してバックアップ トランスポートのオプションを構成する方法](../core/how-to-configure-backup-transport-options-for-a-send-port.md)です。  
  
-   」の説明に従って、メッセージ ボックスから、この送信ポートにルーティングするメッセージを決定するフィルターを構成する[送信ポートのフィルターを構成する方法](../core/how-to-configure-filters-for-a-send-port.md)です。  
  
-   セキュリティ証明書を暗号化または」の説明に従って、送信ポートによって処理されるドキュメントに署名する送信ポートに割り当てる[送信ポートに証明書を割り当てる方法](../core/how-to-assign-a-certificate-to-a-send-port.md)です。  
  
-   送信ポートによって処理されるメッセージの追跡オプションを構成する」の説明に従って[送信ポートの追跡を構成する方法](../core/how-to-configure-tracking-for-a-send-port.md)です。  
  
## <a name="prerequisites"></a>前提条件  
 このトピックの手順を実行するには、BizTalk Server 管理者グループのメンバーであるアカウントを使用してログオンする必要があります。 詳細なアクセス許可についてを参照してください。[を展開すると、BizTalk アプリケーションの管理に必要なアクセス許可](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)です。 さらに、エンタープライズ シングル サインオン (SSO) データベースに対して SSO 関連の管理者権限が必要です。 詳細については、次を参照してください。 [SSO ユーザー グループ](../core/sso-user-groups.md)です。  
  
### <a name="to-create-a-send-port"></a>送信ポートを作成するには  
  
1.  をクリックして**開始**、 をクリックして**すべてのプログラム**、 をクリックして[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]、順にクリック**BizTalk Server 管理コンソール**です。  
  
2.  コンソール ツリーで、BizTalk グループを展開し、送信ポートを作成する BizTalk アプリケーションを展開します。  
  
3.  右クリック**送信ポート**、 をポイント**新規**、しを作成するポートの種類をクリックします。  
  
4.  **送信ポート プロパティ** ウィンドウで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**名前**|新しい送信ポートの名前を入力します。 この名前は、BizTalk グループ内で一意にする必要があります。|  
    |**トランスポートの種類**|ドロップダウン リストから、適切なトランスポートの種類またはトランスポート プロトコルを選択します。 送信請求 - 応答のポートの場合、ドロップダウン リストでは、送信請求 - 応答をサポートするアダプターのみを選択できます。 このプロパティは、静的ポートに対してのみ表示されます。|  
    |**構成**|トランスポートの種類を選択してクリックして**構成**を表示する、**トランスポートのプロパティ** ダイアログ ボックスは、トランスポート固有の構成オプションを提供します。 このプロパティは、静的ポートに対してのみ表示されます。 をクリックして**ヘルプ**の構成手順のダイアログ ボックスでします。|  
    |**送信ハンドラー**|ドロップダウン リストから、送信アダプターが動作しているホスト インスタンスを選択します。 このプロパティは、静的ポートに対してのみ表示されます。|  
    |**送信パイプライン**|ドロップダウン リストから、このポートの送信メッセージを処理するパイプラインを選択します。 パイプラインを選択した後、横の省略記号をクリックすることができます (**.**) を表示するボタン、**パイプラインの構成**ダイアログ ボックスで、この特定のポートのインスタンスごとのパイプライン プロパティを構成します。 をクリックして**ヘルプ**の構成手順のダイアログ ボックスでします。|  
    |**受信パイプライン**|ドロップダウン リストから、このポートの受信メッセージを処理するパイプラインを選択します。 このパイプラインでは、このパイプラインの受信メッセージに対する応答も送信されます。 パイプラインを選択した後、横の省略記号をクリックすることができます (**.**) を表示するボタン、**パイプラインの構成**ダイアログ ボックスで、この特定のポートのインスタンスごとのパイプライン プロパティを構成します。 このプロパティは、送信請求 - 応答のポートに対してのみ表示されます。|  
  
5.  左側のウィンドウで、送信請求-応答送信ポートを作成する場合にクリックして**受信マップ**とは、次の必要なかどうかを追加する複数のマップを繰り返します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**ソース ドキュメント**|ドロップダウン リストから、受信マップの送信元ドキュメントを選択します。 送信ポートには複数のマップを指定できますが、各マップには一意の送信元ドキュメントが必要です。|  
    |**マップ**|ドロップダウン リストから、送信元ドキュメントと送信先ドキュメントに関連付けられているマップを選択します。|  
    |**対象のドキュメント**|ドロップダウン リストから、受信マップの送信先ドキュメントを選択します。|  
  
6.  左側のウィンドウでをクリックして**送信マップ**とは、次の必要なかどうかを追加する複数のマップを繰り返します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**ソース ドキュメント**|ドロップダウン リストから、送信マップの送信元ドキュメントを選択します。|  
    |**マップ**|ドロップダウン リストから、送信元ドキュメントと送信先ドキュメントに関連付けられているマップを選択します。|  
    |**対象のドキュメント**|ドロップダウン リストから、送信マップの送信先ドキュメントを選択します。|  
  
7.  送信ポートの構成が完了、 **OK**です。  
  
## <a name="see-also"></a>参照  
 [作成して、送信ポートの構成](../core/creating-and-configuring-send-ports.md)   
 [パイプラインの管理](../core/managing-pipelines.md)   
 [マップを管理します。](../core/managing-maps.md)