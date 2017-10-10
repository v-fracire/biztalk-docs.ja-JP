---
title: "サーバー スナップインを使用する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4f520692-9606-41f5-98ed-5a4962bd1f09
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 12eb72323a6dcd1132f03febc9b4d9bd75316c84
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-use-the-servers-snap-in"></a>サーバー スナップインの使用方法
このバージョンのエンタープライズ シングル サインオン (SSO) には、ENTSSO サーバー スナップインが含まれています。これにより、Windows インターフェイスを使用して ENTSSO サーバー上で、特定のアクションを表示、監視、および実行できます。  
  
> [!NOTE]
>  システムにファイアウォールがあり、サーバー名に FQDN 形式が使用されている場合、サーバーに接続できないことがあります。 代わりに、NetBIOS 名または関連する IP アドレスを指定する必要があります。  
  
### <a name="to-use-the-entsso-servers-snap-in"></a>ENTSSO サーバー スナップインを使用するには  
  
1.  エンタープライズ シングル サインオンを開きます。  
  
2.  スコープ ペインで、をクリックして、**サーバー**ノード。  
  
     結果ペインに次の情報が表示されます。  
  
    -   **名前**: 指定された名前です。  
  
    -   **ステータス**: (オンライン、オフライン、保留中の開始、停止、開始待ち、停止待ち)、ENTSSO サービスの状態。  
  
    -   **日付**: 情報が取得した日付。  
  
    -   **時間**: 情報が取得された時刻。  
  
    -   **SSO サーバー**: サーバーの完全修飾名。  
  
    -   **サービス アカウント**: ENTSSO サービス アカウント。  
  
    -   **SSO データベース**: このサーバーと通信している ENTSSO データベースです。  
  
    -   **シークレット サーバー**: シークレット サーバー モジュールが実行されているかどうかを示します。  
  
    -   **パスワード同期**: パスワード同期がインストールされているかどうかを示します。  
  
    -   **コンピューター**: コンピューターの NETBIOS 名。  
  
    -   **イベントはカウント**: 情報/警告/エラー イベントの数。 リセットすると、カウンタは 0 から開始されます。  
  
    -   **インストールされている SSO のバージョン**: ENTSSO.exe のバージョン番号。 また、これが 32 ビット (x86) か 64 ビット (x64) かも示します。  
  
### <a name="to-start-or-stop-the-server-service"></a>サーバー サービスを開始または停止するには  
  
-   ENTSSO サーバー スナップインで、サーバーを右クリックし、をクリックして**開始**または**停止**です。  
  
### <a name="to-display-information-for-one-server"></a>1 台のサーバーの情報を表示するには  
  
-   サーバー ツリーでサーバーをクリックします。  
  
     結果ペインに情報が表示されます。  
  
### <a name="to-add-a-server"></a>サーバーの追加  
  
-   スコープ ペインで右クリックし、をクリックして**サーバーの追加**です。  
  
     **サーバーの追加** ダイアログ ボックスが表示されます。 追加するサーバーを入力または参照します。  
  
> [!NOTE]
>  クリックすると、特定のワークグループ環境で、**参照**ボタンをクリックすると、このダイアログ ボックスを閉じます。 使用する代わりに、**参照**ボタン、単にボックスに、サーバー名を入力します。  
  
### <a name="to-view-or-change-server-properties"></a>サーバーのプロパティを表示または変更するには  
  
-   サーバー ツリーで、サーバーを右クリックし、をクリックして**プロパティ**です。  
  
     **サーバー プロパティ** ダイアログ ボックスが表示されます。 次のタブで情報を表示または変更できます。  
  
    -   **監査レベル**  
  
    -   **SSO データベース**  
  
    -   **SSO サービス**  
  
    -   **パスワード同期**  
  
    -   **[詳細設定]**