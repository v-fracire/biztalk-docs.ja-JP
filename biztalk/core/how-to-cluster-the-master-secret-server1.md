---
title: "マスター シークレット Server1 をクラスター化する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Master Secret server, second node
- Master Secret server, restoring
- clustering, Master Secret server
- Master Secret server, clustering
ms.assetid: ef817fa4-e43d-4e3d-8686-5bd675708001
caps.latest.revision: "47"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3c9fc06d9c735a59fe59499bf9ed0ac62aab0408
ms.sourcegitcommit: 5355a25d120d094778fb8f68ea14cab55c68d292
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2017
---
# <a name="how-to-cluster-the-master-secret-server"></a>マスター シークレット サーバーをクラスター化する方法
マスター シークレット サーバーのエンタープライズ シングル サインオン (SSO) サービスを正常にクラスター化するには、このセクションに記載されている指示に従うことをお勧めします。  
  
 マスター シークレット サーバーをクラスター化した場合、シングル サインオン サーバーでは、マスター シークレット サーバーのアクティブなクラスター化インスタンスとの通信が行われます。 同様に、マスター シークレット サーバーのアクティブなクラスター化インスタンスでは、SSO データベースとの通信が行われます。  
  
 ここで示す手順を実行するには、SSO 管理者である必要があります。  
  
> [!CAUTION]
>  ネットワーク負荷分散 (NLB) クラスターにマスター シークレット サーバーをインストールすることはできません。  
  
### <a name="to-install-and-configure-enterprise-sso-on-the-cluster-nodes"></a>クラスタ ノードにエンタープライズ SSO をインストールおよび構成するには  
  
1.  各クラスター ノードに [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] をインストールします。 **コンポーネントのインストール****エンタープライズ シングル サインオン管理モジュール**と**エンタープライズ シングル サインオン マスター シークレット サーバー**です。 インストールが正常に完了した後は**いない**実行、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]構成します。  
  
2.  作成**SSO 管理者**と**SSO 関連管理者**ドメイン グループです。 エンタープライズ SSO サービスのクラスター化インスタンスを作成するのには、これらのグループをドメイン グループとして作成する必要があります。  
  
3.  作成またはのメンバーであるドメイン アカウントを指定、 **SSO 管理者**ドメイン グループです。 各ノードのエンタープライズ SSO サービスは、このドメイン アカウントとしてログオンするように構成されます。 このアカウントが必要、**サービスとしてログオン**クラスター内の各ノードを右にします。  
  
4.  ドメインに、構成プロセス中にログオンに使用しているアカウントを追加**SSO 管理者**グループ。  
  
    > [!IMPORTANT]
    >  手順 3. および手順 4. を完了しないと、エンタープライズ SSO サービスの構成が失敗します。  
  
5.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] の構成を起動します。  
  
6.  選択**カスタム構成**オプションおよび入力、**データベース サーバー名**、**ユーザー名**、および**パスワード**値。 選択**構成**を続行します。  
  
    > [!NOTE]
    >  必ずためこの時点で、エンタープライズ SSO サービスを構成できますだけ、ドメイン アカウントを入力する前に作成したは、ここです。  
  
7.  選択、**エンタープライズ SSO**左側のペインからオプションを選択し、エンタープライズ SSO 機能の次のオプションを設定します。  
  
    1.  選択、**を有効にするエンタープライズ シングル サインオンこのコンピューターに**チェック ボックスをオンします。  
  
    2.  選択**新しい SSO システムを作成する**です。  
  
    3.  入力、**データ ストア**の**サーバー名**と**データベース名**値。  
  
    4.  先ほど作成したドメイン アカウントが、エンタープライズ SSO サービスに関連付けられたアカウントになっていることを確認します。  
  
    5.  SSO 管理者ロールに関連付けられたグループとして、先ほど作成したドメイン SSO 管理者グループを入力します。  
  
    6.  SSO 関連管理者ロールに関連付けられたグループとして、先ほど作成したドメイン SSO 関連管理者グループを入力します。  
  
8.  選択、**エンタープライズ SSO シークレットのバックアップ**左側のペインからオプションを選択し、エンタープライズ SSO シークレットをバックアップするための適切なパラメーターを提供します。 既定では、エンタープライズ SSO シークレットがバックアップされる*\<ドライブ >*: \program files \common files \enterprise シングル サインオン\\*SSOxxxx*.bak です。  
  
9. クリックして、**構成の適用**概要を確認します。  
  
10. をクリックして**次**構成を適用します。  
  
11. をクリックして**完了**構成ウィザードを閉じます。  
  
12. [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] の構成を閉じます。  
  
13. パッシブ クラスター ノードにログオンし、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] の構成を起動します。  
  
14. 選択、**カスタム構成**オプションし、同じ値を入力、**データベース サーバー名**、**ユーザー名**、および**パスワード**です最初のクラスター ノードを構成するときに入力されました。 これらの値を入力すると、をクリックして**構成**を続行します。  
  
15. 選択、**エンタープライズ SSO**左側のペインからオプションを選択し、エンタープライズ SSO 機能の次のオプションを設定します。  
  
    1.  選択、**を有効にするエンタープライズ シングル サインオンこのコンピューターに**オプション。  
  
    2.  選択**既存の SSO システムに参加**です。  
  
    3.  SSO データベースに同じ値を入力**サーバー名**と**データベース名**最初のクラスター ノードを構成するときに入力しました。  
  
    4.  ドメイン アカウントに、最初のクラスター ノードを構成したときと同じ値を入力します。  
  
16. 選択**構成の適用**概要を表示します。  
  
17. 選択**次**構成を適用します。  
  
18. 選択**完了**構成ウィザードを閉じます。  
  
19. 閉じる、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]構成します。  
  
### <a name="to-update-the-master-secret-server-name-in-the-sso-database"></a>SSO データベースのマスター シークレット サーバー名を更新するには  
  
1.  アクティブなクラスター ノードのコマンド プロンプトで次のコマンドを入力して、エンタープライズ SSO サービスを停止および再開します。  
  
    ```  
    net stop entsso  
    ```  
  
     クエリと  
  
    ```  
    net start entsso  
    ```  
  
2.  次の手順を実行して、SSO データベースのマスター シークレット サーバー名をクラスター名に変更します。  
  
    > [!NOTE]
    >  このクラスター名は、クラスター化されたエンタープライズ SSO サービスを含むクラスター グループ/クラスター化されたサービスまたはアプリケーションで作成したネットワーク名リソース用に定義された名前です。 たとえば、名前があります*BIZTALKCLUSTER*です。  
  
    1.  テキスト エディターに次のコードを貼り付けます。  
  
        ```  
        <sso>  
          <globalInfo>  
            <secretServer>BIZTALKCLUSTER</secretServer>  
          </globalInfo>  
        </sso>  
        ```  
  
        > [!NOTE]
        >  *BIZTALKCLUSTER*クラスターで作成される実際のネットワーク名リソースのプレース ホルダーは、グループ/クラスター化されたサービスまたはアプリケーションです。  
  
    2.  ファイルを .xml ファイルとして保存します。 たとえば、SSOCLUSTER.xml という名前で保存します。  
  
    3.  コマンド プロンプトで、エンタープライズ SSO のインストール フォルダーに移動します。 インストール フォルダーは、既定では、 *\<ドライブ >*: \program files \common files \enterprise シングル サインオンします。  
  
    4.  コマンド プロンプトで次のコマンドを入力して、データベース内のマスター シークレット サーバー名を更新します。  
  
        ```  
        ssomanage -updatedb XMLFile  
        ```  
  
        > [!NOTE]
        >  *XMLFile*以前に保存した .xml ファイルの名前のプレース ホルダーです。  
  
### <a name="to-create-the-clustered-enterprise-sso-resource"></a>クラスタ化されたエンタープライズ SSO リソースを作成するには  
  
1.  クラスター化された分散トランザクション コーディネーター (MSDTC) リソース クラスターが構成されていない場合、手順「を向上させるフォールト トレランス BizTalk サーバーでを使用して、Windows Server クラスターで」ホワイト ペーパー 『 [http://go.microsoft.com/fwlink/ しますか。LinkId = 69207](http://go.microsoft.com/fwlink/?LinkId=69207)をクラスター化された MSDTC リソースを作成します。  
  
2.  をクリックして**開始**、**プログラム**、**管理ツール**、し**フェイル オーバー クラスター管理**フェールオーバー クラスターを起動するには管理のプログラムです。  
  
3.  左側のウィンドウで右クリック**フェイル オーバー クラスター管理** をクリック**クラスターを管理**です。  
  
4.  **を管理するクラスターの選択** ダイアログ ボックスで、クラスターを管理できをクリックして入力**ok**です。  
  
5.  左側のウィンドウで、IP アドレスおよびネットワーク名リソースが入ったクラスター化されたサービスかアプリケーションをクリックして選択します。 手順に従います[ディスク、IP アドレス名リソースとクラスター グループを作成する方法](../core/how-to-create-a-cluster-group-with-a-disk-ip-address-and-name-resource1.md)が既に存在しない場合、IP アドレスおよびネットワーク名リソースとグループを作成します。  
  
    > [!NOTE]
    >  クラスター化されたエンタープライズ SSO サービスでは、同じグループ内でクラスター化された物理ディスク リソースの使用は明示的に要求されません。  
  
6.  クラスター化されたサービスまたはアプリケーションを右クリックし、[**リソースを追加**、] をクリック**汎用サービス**を表示する、**新しいリソース ウィザード**ダイアログ。  
  
    > [!IMPORTANT]
    >  **汎用サービス パラメーター**ダイアログ ボックスで、選択をクリックしない場合、**コンピューター名のネットワーク名を使用** チェック ボックス SSO クライアント コンピューターは、次のようなエラーを生成時に、エンタープライズ SSO サービスのクラスター化されたこのインスタンスに接続しようとしてください。  
    >   
    >  マスター シークレットを取得できませんでした。  
    >   
    >  マスター シークレット サーバー名が正しいこと、および利用可能であることを確認してください。 シークレット サーバー名: ENTSSO エラー コード: 0x800706D9、エンドポイント マッパーから使用できるエンドポイントはこれ以上ありません。  
  
7.  **サービスの選択**のページ、**新しいリソース ウィザード**をクリックして選択**エンタープライズ シングル サインオン サービス** をクリック**次**です。  
  
8.  **確認**ページをクリックして**次**です。  
  
9. **概要**ページをクリックして**完了**です。 エンタープライズ シングル サインオン サービスのクラスター化されたインスタンスに表示されます**その他のリソース**の中央のペインで、**フェイル オーバー クラスター管理**インターフェイスです。  
  
10. エンタープライズ シングル サインオン サービスのクラスター化されたインスタンスを右クリックし [**プロパティ**を表示する、**エンタープライズ シングル サインオン サービスのプロパティ**] ダイアログ ボックス。  
  
11. クリックして、**の依存関係** タブをクリックして、プロパティ ダイアログ ボックスの**挿入**です。  
  
12. 下のボックスのドロップダウンをクリックして**リソース**を選択、**名前:**リソースをクリック**OK**です。  
  
### <a name="to-restore-the-master-secret-on-the-second-cluster-node"></a>2 番目のクラスタ ノードでマスタ シークレットを復元するには  
  
1.  フェールオーバー クラスター管理では、クラスター化されたサービスまたはクラスター化されたエンタープライズ シングル サインオン サービスを含むアプリケーションを右クリックし、をクリックして**このサービスまたはアプリケーションをオンライン**内のリソースのすべてを開始するにはクラスター化されたサービスまたはアプリケーションです。  
  
2.  クラスター化されたサービスまたはアプリケーションを右クリックし、**このサービスまたはアプリケーションを別のノードに移動**、2 番目のノードをクリックします。 この手順では、クラスター化されたエンタープライズ シングル サインオン サービスが入ったクラスター化されたサービスまたはアプリケーションを最初のノードから 2 番目のノードに移動します。  
  
3.  クラスター化されたエンタープライズ シングル サインオン サービスを右クリックし、をクリックして**このサービスまたはアプリケーションをオフラインに**、エンタープライズ SSO サービスのクラスター化されたインスタンスを右クリックしてをクリックして**このサービスまたはアプリケーションをオンライン**です。  
  
    > [!NOTE]
    >  この手順を省略すると、マスター シークレットの復元に失敗する場合があります。  
  
4.  最初のノードのマスター シークレットのバックアップ ファイルを、2 番目のノードの \Enterprise Single Sign-On インストール フォルダーにコピーします。 インストール フォルダーは、既定では、 *\<ドライブ >*: \program files \common files \enterprise シングル サインオンします。  
  
5.  2 番目のノードにログオンし、コマンド プロンプトで、エンタープライズ SSO のインストール フォルダーに移動します。  
  
6.  コマンド プロンプトで次のコマンドを入力し、マスター シークレットを 2 番目のノードに復元します。  
  
    ```  
    ssoconfig -restoresecret RestoreFile  
    ```  
  
    > [!NOTE]
    >  置き換える*RestoreFile*のパスと、マスター シークレットを含むバックアップ ファイルの名前を使用します。  
  
     マスター シークレットがレジストリの次の場所に保存されます。  
  
     HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ENTSSO\SSOSS  
  
7.  このクラスター ノードから他のクラスター ノードに、クラスター化されたエンタープライズ シングル サインオン サービスを含むクラスター化されたサービスまたはアプリケーションを移動して、フェールオーバー機能を確認します。 次に、クラスター グループを元に戻して、フェールバック機能を検証します。  
  
## <a name="see-also"></a>参照  
 [ディスク、IP アドレス名リソースとクラスター グループを作成する方法](../core/how-to-create-a-cluster-group-with-a-disk-ip-address-and-name-resource1.md)