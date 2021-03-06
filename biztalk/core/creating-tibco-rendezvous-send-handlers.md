---
title: TIBCO Rendezvous アダプターの送信の成果物を作成 |Microsoft ドキュメント
description: 送信ポートを作成、メッセージを TIBCO Rendezvous を BizTalk から送信するトランスポートのプロパティを構成します。
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ad996c4f-e6ed-4582-a768-0cb1ad25b1d8
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ed6d03885423582c2657c9cb624c63f26ce1c6f3
ms.sourcegitcommit: dd7c54feab783ae2f8fe75873363fe9ffc77cd66
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2017
ms.locfileid: "24014353"
---
# <a name="create-tibco-rendezvous-send-handlers"></a>TIBCO Rendezvous 送信ハンドラーを作成します。
このセクションでは、スキーマを作成して BizTalk Server のオーケストレーションで TIBCO Rendezvous を使用する方法について説明します。  
  
## <a name="create-a-send-port"></a>送信ポートを作成します。
  
1.  **BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**、し、アプリケーションを展開します。  
  
2.  右クリック**送信ポート**、 をポイント**新規**、クリックして**静的な送信請求-応答送信ポート**です。  
  
3.  **送信ポートのプロパティ** ダイアログ ボックスで、次の操作します。  
  
    1.  たとえば、送信ポートの名前を入力`SendToTIBCORV`です。  
  
    2.  **型**ドロップダウン リストで、 **TIBCO Rendezvous**です。  
  
    3.  **送信ハンドラー**ドロップダウン リストで、URI を選択します。  
  
    4.  送信パイプラインのドロップダウン リストから選択 **[microsoft.biztalk.defaultpipelines.xmltransmit]** です。  **受信パイプライン**ドロップダウン リストで、 **[microsoft.biztalk.defaultpiplelines.xmlreceive]** です。  

        > [!NOTE]
        > Microsoft BizTalk Adapter for TIBCO Rendezvous では、送信、XMLTransmit パイプラインと受信の XMLReceive パイプラインを選択することが必要です。
        
    6.  をクリックして**構成**送信ポートを構成します。  
  
4.  **TIBCO Rendezvous トランスポートのプロパティ** ダイアログ ボックスで、次の操作します。  
  
    1.  プロパティを入力します。  
  
         ログオン情報を設定する必要はありません。  
  
    2.  一覧で、TIBCO Rendezvous システムを表すように作成した SSO 関連アプリケーションを選択します。  
  
    3.  **SSO を使用する****はい**です。  
  
    4.  **[OK]** をクリックします。  
  
5.  **[OK]** をクリックします。  

## <a name="set-the-transport-properties"></a>トランスポートのプロパティを設定します。
TIBCO Rendezvous トランスポートのプロパティは、実行時に使用されます。 **トランスポートのプロパティ**、生成されたメッセージを公開する TIBCO Rendezvous ドメインを識別する接続パラメーターを設定します。  
  
 
1.  **TIBCO Rendezvous トランスポートのプロパティ**画面で、展開**証明された送信者プロパティ**し、次の情報を入力します。  
  
     ![](../core/media/sadp-tibcoren-transs.gif "SAdp_TibcoRen_Transs")  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**元帳の名前**|既定値は空白です。 永続的な認証されたメッセージ配信に使用する台帳ファイル名。 ローカル ドライブのみを使用します。|  
    |**再利用可能名**|既定値は空白です。 認証されたメッセージ配信に使用する再利用可能な送信者名です。 この名前は、ネットワーク上のすべての認証されたメッセージの送信者名の中で一意である必要があります。|  
  
2.  展開**資格情報**し、サーバーに接続に関する次の情報を入力します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**Password**|既定値は空白です。 Tibco Rendezvous デーモンにログインするためのパスワードです。|  
    |**ユーザー名**|既定値は空白です。 Tibco Rendezvous デーモンで使用するユーザー名です。|  
  
3.  展開**全般設定**と TIBCO Rendezvous サーバーに接続に関する次の情報を入力します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**コード ページ番号**|既定値は 65001 (UTF-8 エンコーディングのコード ページ) です。 これは、TIBCO Rendezvous SDK が文字列のエンコーディングに使用するコード ページです。|  
    |**既定のサブジェクト名**|既定では空になっています。 サブジェクト名はオーケストレーションで設定されます。 1 つの種類のメッセージに 1 つのポートを使用する場合、既定のサブジェクト名を指定でき、サブジェクト名プロパティを設定する必要をなくしてオーケストレーションを単純化できます。|  
    |**タイム バッチを有効にします。**|既定値は False です。 TIBCO Rendezvous のタイム バッチ機能を有効または無効にします。|  
    |**サポートされていない型を文字列に対応付け**|既定値は True です。 True の場合、サポートされていない型はすべて文字列型にマップされます。 False の場合、実行時エラーが生成されます。|  
    |**TIBCO Rendezvous アセンブリなど、バイナリ ファイルへのパス**|PATH 環境変数でまだ設定されていない場合は、この情報を指定します。|  
    |**順序の保持**|既定値は True です。 ロジックで、メッセージを BizTalk Server から受信したときと同じ順序で TIBCO Rendezvous に送信できます。 このパラメーターにより、同じ順序での公開が強制されますが、サブスクライバーが同じ順序で受信するということではありません。|  
    |**送信ポートの識別子**|この識別子は、このポートに関連付けられているログ メッセージに表示されます。 これは、便宜上指定します。|  
  
4.  展開**Rendezvous トランスポート**TIBCO Rendezvous サーバーへの接続情報を入力し、**適用**、クリックして **[ok]** です。  
  
     Microsoft BizTalk Adapter for TIBCO Rendezvous が TIBCO Rendezvous にアクセスできるようにするために接続パラメーターを設定する必要があります。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**デーモン**|既定では空になっています。<br /><br /> Rendezvous トランスポート デーモン パラメーター。|  
    |**ネットワーク**|既定では空になっています。<br /><br /> Rendezvous トランスポート ネットワーク パラメーター。|  
    |**サービス**|既定では空になっています。<br /><br /> Rendezvous トランスポート サービス パラメーター。|  
  
5.  シングル サインオン (SSO) を使用する資格情報を指定します。  
  
     TIBCO Rendezvous システムにアクセスする方法は 2 つあります。 1 つは資格情報 ([ユーザー名] パラメーターと [パスワード] パラメーター) を使用する方法で、もう 1 つはシングル サインオン (SSO) を使用する方法です。  
  
    1.  選択**はい**で、 **SSO を使用する**でのシングル サインオンを使用します。  
  
        > [!NOTE]
        >  参照してください[セキュリティ](../core/security-in-biztalk-adapter-for-tibco-rendezvous.md)SSO をセットアップする方法についてはします。  
  
    2.  一覧から関連アプリケーションを選択します。  
  
         エンタープライズ シングル サインオン ツールで作成された関連アプリケーションは TIBCO Rendezvous などのアプリケーションを表します。 Microsoft BizTalk Adapter for TIBCO Rendezvous では、アプリケーション ユーザーの資格情報が使用されます。 これらの資格情報は、指定された関連アプリケーションのサーバー システムの SSO データベースから取得されます。  
  
        > [!NOTE]
        >  関連アプリケーションを作成する方法については、次を参照してください。[関連アプリケーションの作成](../core/creating-affiliate-applications1.md)です。  
  
6.  をクリックして**適用**、クリックして **[ok]** 接続情報を受け入れるように必要なすべての情報を提供するとします。  
  
     BizTalk Adapter for TIBCO Rendezvous にアクセスする TIBCO Rendezvous の接続パラメーターを設定する必要があります。  


## <a name="next-steps"></a>次の手順
  
-   [BizTalk Server からの TIBCO Rendezvous 送信ポートの使用](../core/using-tibco-rendezvous-send-ports-from-biztalk-server.md)  
  
-   [TIBCO Rendezvous での送信ハンドラーのデータ型マッピング](../core/data-type-mapping-for-send-handlers-in-tibco-rendezvous.md)  
  
-   [BizTalk Server のメッセージ コンテキストのプロパティ (送信ハンドラー)](../core/biztalk-server-message-context-properties-send-handlers.md)