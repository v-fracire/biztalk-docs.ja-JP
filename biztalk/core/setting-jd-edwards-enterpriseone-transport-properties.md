---
title: "JD Edwards EnterpriseOne トランスポートのプロパティを設定 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Max Concurrent Calls parameter
- JD Edwards EnterpriseOne adapters, transport properties
- transport properties, configuring [JD Edwards EnterpriseOne adapters]
- adapters [JD Edwards EnterpriseOne adapters], transport properties
- Bootstrap Data Source properties
ms.assetid: 7d258ee6-1cb3-4b88-ac41-49e639833574
caps.latest.revision: "17"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4ed3118230f2e4ae48676b297ac444da9c392221
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="setting-jd-edwards-enterpriseone-transport-properties"></a>JD Edwards EnterpriseOne トランスポートのプロパティの設定
JD Edwards EnterpriseOne トランスポートのプロパティは、デザイン時および実行時に使用されます。 **トランスポートのプロパティ**ダイアログ ボックスで、パラメーターを設定する接続と資格情報を特定サーバーのシステムおよびアクセスしようとしているオブジェクトにします。  
  
 接続パラメーターの設定後、JD Edwards EnterpriseOne システムのテーブル、ビュー、およびプロシージャをアダプター ウィザードで表示できます。  
  
 JD Edwards EnterpriseOne に接続すると、パラメーターが接続オブジェクトに渡されます (ユーザー、パスワード、環境)。 これにより、JD Edwards EnterpriseOne アプリケーション ビジネス関数のインスタンスが返されます。 資格情報には、さらにエンタープライズ サーバーまたはアプリケーション サーバーの名前と、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] がリッスンする定義済みの TCP/IP ポートが含まれます。  
  
> [!NOTE]
>  エンタープライズ サーバー名およびポートの既定値は、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] で構成されています。 また、jdeinterop.ini というファイルからも読み込まれます。 ログオン エラーが発生した場合は、資格情報と値を確認してください。  
  
### <a name="to-specify-transport-properties"></a>トランスポートのプロパティを指定するには  
  
1.  BizTalk Server 管理コンソールで、展開**BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**アプリケーション**、し、必要な展開アプリケーション。  
  
2.  右クリック**送信ポート**、 をポイント**新規**、クリックして**静的な一方向送信ポート**です。  
  
3.  **送信ポートのプロパティ** ダイアログ ボックス内をクリックして、**名前**ボックスし、このポートの名前を入力 (たとえば、 `JDEEnterpriseOneSend`)。  
  
4.  **全般**で、**トランスポートの種類**ボックスで、 **JDE EnterpriseOne**ドロップダウン リストでします。  
  
5.  **アドレス (URI)**プロパティ、省略記号ボタン (**.**).  
  
     **JDE EnterpriseOne トランスポートのプロパティ** ダイアログ ボックスが表示されます。  
  
     ![](../core/media/jdeenterprise-trans.gif "JDEEnterprise_Trans")  
  
6.  **JDE EnterpriseOne トランスポートのプロパティ** ダイアログ ボックスで、展開、**アダプターの必要なプロパティ**、JD Edwards EnterpriseOne サーバーに接続に必要なすべての情報を入力します。  
  
     次のガイドラインに従ってトランスポートのプロパティを設定してください。  
  
    |これを使用してください。|これを行う|  
    |--------------|----------------|  
    |**アダプタに必要なプロパティ**||  
    |Host|ホスト サーバー コンピューターの名前<br /><br /> `actsvr1`)<br /><br /> - または--<br /><br /> コンピューターの IP アドレス<br /><br /> `123.456.0.789`)|  
    |JAVA_HOME|JDK インストールへの完全なパスを入力します (たとえば、<br /><br /> `C:\jdk1sdk1.4.2_07`)|  
    |JDEdwards 環境|JD Edwards EnterpriseOne の環境の名前を入力 (たとえば、 `DV7333`)。<br /><br /> DV7333 は開発環境の一般名、PY7333 はプロトタイプ環境の一般名、PD7333 は実稼働環境の一般名です。|  
    |JDEdwards JAR ファイル|各 JAR ファイルの完全パスとファイル名を入力します。<br /><br /> -C:\JDEOWJars\Connector.jar<br />-C:\JDEOWJars\Kernel.jar<br />-\Microsoft BizTalk Adapters を program for Enterprise applications \j.d. です。 Edwards EnterpriseOne(r)\Classes\JDEDynAccess.jar<br /><br /> 各 jar ファイルは、次に示すようにセミコロン (;) で区切り、スペースは挿入しません。<br /><br /> `<c:>\Connector.jar;<c:>\Kernel.jar;`)|  
    |Password|ユーザーのパスワードを入力します。 シングル サインオン (SSO) を使用しない場合、サーバー システムにアクセスするには BizTalk Adapter for JD Edwards EnterpriseOne の資格情報関連のパラメーターを設定する必要があります。 このパスワードは、ユーザー名に対応しています。このパスワードに基づいて、データベースにアクセスしたときに付与される特権が決定されます。|  
    |ポート|入力した数値識別子、送信ポートまたは受信ポート (たとえば、 `6009`)。|  
    |[ユーザー名]|ユーザーの名前を入力し、クリックして**OK**です。|  
    |**Bootstrap Data Source に必要なプロパティ\*\***||  
    |Data Source Name|データ ソースの名前を入力します。 この名前はすべてのデータの種類に必須です。|  
    |データベースの所有者|データベースの所有者の名前を入力します。|  
    |データベース サーバー名|データベース サーバーの名前を入力します。|  
    |データベース サーバー ポート|データベース サーバー ポートの識別用の番号を入力します。|  
    |データベースの種類|データベースの種類を示す単一の文字を入力します。 例:<br /><br /> **I** -iSeries<br /><br /> **O** -Oracle<br /><br /> **S** -SQL Server<br /><br /> **L** -SQL Server OLEDB<br /><br /> **W** -UDB|  
    |物理データベース名|物理データベースの名前を入力します。 この名前はすべてのデータベースの種類に必須です。|  
    |**同時実行制御**||  
    |最大同時呼び出し数|数値の値を入力、 **Max Concurrent Calls**です。 この番号がなど、同時呼び出しの最大数を表す`10`です。<br /><br /> このフィールドの既定値は 5 です。|  
    |**エージェントを更新します。**||  
    |エージェントの更新|選択**はい**の**エージェントの更新**runtimeagent.exe および browsingagent.exe の処理を必要時に自動的に再起動を強制します。<br /><br /> たとえば、サーバーとの接続が失われた場合や、サーバーに追加したものが Microsoft アダプター ウィザードに表示されない場合に、処理を自動的に再起動することができます。|  
    |**セキュリティ サーバー**||  
    |セキュリティ サーバー名|セキュリティ サーバーの名前を入力します。 このフィールドは省略可能で、既定値は JD Edwards サーバー ホストです。|  
    |サービス名接続|セキュリティ サーバーとオブジェクト構成マッピング (OCM) で使用されるポート番号を入力します。 既定値は JD Edwards サーバー ポートです。|  
    |**シングル サインオン**||  
    |[関連アプリケーション]|一覧から関連アプリケーションを選択します (SSO を使用している場合のみ)。|  
    |SSO の使用|選択**はい**SSO; を使用している場合、パスワードは必要ありませんここでします。|  
  
7.  をクリックして**OK**をすべてのプロパティを受け入れるようにします。  
  
## <a name="bootstrap-data-source-required-properties"></a>Bootstrap Data Source に必要なプロパティ  
 Bootstrap セクションは、サインオンでシステム テーブルにアクセスするために使用されます。 Bootstrap Data Source の情報によって、OCM が存在するデータ ソースが定義されます。  
  
 Bootstrap Data Source のパラメーターには、プラットフォームによっては設定する必要がない項目もあります。 一般的でないデータベースを使用している場合は、[JDBJ-JDBC DRIVERS] セクションを更新する必要があります**jdeinterop.ini** JDBC ドライバーを宣言します。 プラットフォームごとに、必要な設定を次に示します。  
  
-   **iSeries**です。 [データ ソース名]、[データベースの種類]、[データベース サーバー名]、[物理データベース名]  
  
-   **Oracle**です。 データ ソース名、データベースの種類、物理データベース名、データベースの所有者  
  
-   **SQL Server**です。 [データ ソース名]、[データベースの種類]、[データベース サーバー名]、[データベース サーバー ポート]、[物理データベース名]、[データベース所有者]  
  
-   **SQL Server OLEDB**です。 [データ ソース名]、[データベースの種類]、[データベース サーバー名]、[データベース サーバー ポート]、[物理データベース名]、[データベース所有者]  
  
-   **UDB**です。 データ ソース名、データベースの種類、物理データベース名、データベースの所有者  
  
## <a name="optimization-configuration"></a>構成の最適化  
 BizTalk Adapter for JD Edwards EnterpriseOne の構成を最適化するのに役立つ情報を次に示します。  
  
### <a name="max-concurrent-calls-parameter"></a>[最大同時呼び出し数] パラメーター  
 `Max Concurrent Calls` パラメーターは、スループットがバックエンドの処理機能を上回るインスタンスで使用できます。 内のアダプターにパラメーターを追加する、**送信ポートのトランスポート プロパティ**メッセージ オーバー ロードの保護をアクティブ化するページ。 既定値は -1 です。これは呼び出しが制限されないことを意味します。  
  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は、送信アダプターに対してメッセージを送信するとき、まずアダプターからバッチを受け取り、そのバッチについて `TransmitMessage()` を呼び出して各メッセージを転送します。 この処理が完了すると、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] はバッチで `Done()` を呼び出し、アダプターがバックエンドに対するメッセージ送信を開始します。  
  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] が `Done` を呼び出す前に複数のバッチを取得した場合、`Done` コマンドは実行されないことがあります。 バッチ内に含めるメッセージの最大数を設定することで、バックエンドに送信するメッセージを制御できます。  
  
 このパラメーターに加えた変更は、1 分以内に有効になります。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は、SQL データベースに保存されているアダプター構成に対する変更を取得する必要があります。  
  
### <a name="refresh-agent"></a>エージェントの更新  
 選択すると**はい**の**エージェントの更新**、runtimeagent.exe および browsingagent.exe の処理を必要時に自動的に再起動を強制します。  
  
 たとえば、プロセス サーバーとの接続を失ったまたは何かがサーバーに追加すると、Microsoft アダプター ウィザードの選択のためには表示されませんが自動的に再起動をします。  
  
 エージェントの更新パラメーターは、[トランスポートのプロパティ] ウィンドウで設定します。参照エージェントとランタイム エージェントの両方を更新します。 runtimeagent.exe は 1 分の遅延後または次の送信呼び出し時に更新されます。  
  
> [!NOTE]
>  browsingagent.exe は、現在の参照セッションを終了するまで更新されません。 "Add generated item..."を終了する必要があります、 セッションと、browsingagent.exe を更新するを再入力を参照しています。  
  
### <a name="single-sign-on"></a>シングル サインオン  
 JD Edwards EnterpriseOne システムへのアクセスには、2 つの方法を使用できます。 1 つはログイン資格情報 (トランスポートのプロパティのログイン パラメーター) を使用する方法で、もう 1 つはシングル サインオン (SSO) を使用する方法です。 選択**はい**で、 **SSO を使用する**でのシングル サインオンを使用するフィールドです。  
  
 詳細および基本的な手順をシングル サインオンの設定については、「[シングル サインオンを使用して](../core/using-single-sign-on1.md)です。  
  
 さらに、一覧から関連アプリケーションを選択する必要があります。 エンタープライズ シングル サインオン ツールで作成される関連アプリケーションは、JD Edwards EnterpriseOne などのアプリケーションを表します。 BizTalk Adapter for JD Edwards EnterpriseOne は、アプリケーション ユーザーの資格情報を使用します。  
  
 これらの資格情報は、指定された関連アプリケーションのサーバー システムの SSO データベースから取得されます。 取得される資格情報は、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] プロジェクトを起動したユーザー (アプリケーション ユーザー) の資格情報です。  
  
 関連アプリケーションを作成する方法の詳細については、次を参照してください。[関連アプリケーションの作成](../core/creating-affiliate-applications4.md)です。 また、Microsoft [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] オンライン ヘルプでも参照できます。  
  
## <a name="see-also"></a>参照  
 [シングル サインオンと BizTalk Adapter JD Edwards EnterpriseOne for](../core/single-sign-on-and-biztalk-adapter-for-jd-edwards-enterpriseone.md)   
 [JD Edwards EnterpriseOne 送信ハンドラーの作成](../core/creating-jd-edwards-enterpriseone-send-handlers.md)