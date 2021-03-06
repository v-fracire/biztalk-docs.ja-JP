---
title: ログ配布用に送信先システムを構成する方法 |Microsoft Docs
ms.custom: ''
ms.date: 2015-12-03
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- backing up, log shipping
- system failures, preventing
- log shipping
- databases, backing up
- backing up, databases
- system failures, backing up
- backing up, system failures
ms.assetid: 7b4425f5-b105-4fb2-a503-94ca1e75ad55
caps.latest.revision: 54
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9ee5c7a5d59ce60923fa4ad3ba015f60bc30a0c8
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36971467"
---
# <a name="how-to-configure-the-destination-system-for-log-shipping"></a>ログ配布用に送信先システムを構成する方法
ログ配布は、システム障害時のダウンタイムを短縮することを目的とした、スタンバイ サーバーの機能です。 ログ配布を使用すると、送信元システムのトランザクション ログを送信先システムに自動的に送信できます。 送信先システムでトランザクション ログの復元、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]データベース; ソース データベースと密接に同期を維持することです。  
  
 ログ配布は、単一サーバー環境および分散型サーバー環境の両方で動作します。 ライブ データが格納されたサーバーまたはサーバーのグループを、送信元 (プライマリ) システムと呼びます。 送信元 (プライマリ) システムによって生成されたデータベース バックアップの復元先として使用するサーバーまたはサーバーのグループを、送信先 (セカンダリ) システムと呼びます。  
  
 [ログ配布について](https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server)ドキュメントを sql には、特定の詳細情報を提供します。  
  
 次の手順を使用すれば、1 つの送信元システムに対する 1 サーバーの送信先システムを作成できます。 送信先システムに複数のサーバーが含まれる場合は、各送信先サーバーに対してこの手順を繰り返してください。  
  
> [!IMPORTANT]
>  バックアップ ファイルのコピーは、常に安全な場所に保管してください。 ログ バックアップがあっても、バックアップ ファイルがなければデータベースを復元することはできません。  
  
## <a name="prerequisites"></a>前提条件  
* メンバーとしてサインイン、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理者グループ。  
  
* 送信元と送信先システムで同じバージョンの SQL Server を使用します。 SQL Server は、元とコピー先のシステムで、同じ相対的場所にインストールする必要があります。  
  
* 送信先システムにも、送信元システムの SQL トランザクション ログ (.LDF ファイル) のディレクトリが存在している必要があります。 このディレクトリが送信先システムにない場合は、送信元システムと同じ名前およびアクセス許可を持つディレクトリを作成します。  
  
### <a name="configure-the-destination-system-for-log-shipping"></a>ログ配布用に送信先システムを構成します。  
  
1. 送信先システムで開く**SQL Server Management Studio**、し、SQL Server に接続します。 選択**マスター**から利用可能なデータベースです。  
  
2. **ファイル**] メニューの [**オープン**次の SQL スクリプト。  
  
   ```    
   %SystemDrive%\Program Files\Microsoft BizTalk Server <version>\Schema\LogShipping_Destination_Schema.sql  
   ```  
  
3. **クエリ**メニューの  **Execute**します。  
  
    *LogShipping_Destination_Schema*され、送信先システムでソース データベースの復元に使用するテーブルを再作成します。 これには、復元対象のデータベースの一覧を格納するテーブル、送信元システムの BizTalkMgmtDb データベースからインポートされたバックアップ履歴のコピー、および送信元データベースに対して実行するように構成されている SQL Server エージェント ジョブについての情報が含まれます。  
  
4. **ファイル**] メニューの [**オープン**次の SQL スクリプト。  
  
   ```    
   %SystemDrive%\Program Files\Microsoft BizTalk Server <version>\Schema\LogShipping_Destination_Logic.sql  
   ```  
  
5. **クエリ**メニューの  **Execute**します。  
  
6. 送信先システムとして指定したコンピューターまたはコンピューターで開く**SQL Server Management Studio**し、SQL Server に接続します。  
  
7. 選択**新しいクエリ**します。 クエリ ウィンドウに、次のコマンドを貼り付けます。  
  
   ```  
   exec bts_ConfigureBizTalkLogShipping @nvcDescription = '<MyLogShippingSolution>',  
   @nvcMgmtDatabaseName = '<BizTalkServerManagementDatabaseName>',  
   @nvcMgmtServerName = '<BizTalkServerManagementDatabaseServer>',  
   @SourceServerName = null, -- null indicates that this destination server restores all databases  
   @fLinkServers = 1 -- 1 automatically links the server to the management database  
   ```  
  
    そうしたら：  
  
   1.  送信先システムで有効にする **[Ad Hoc Distributed Queries](https://docs.microsoft.com/sql/database-engine/configure-windows/server-configuration-options-sql-server)** します。  
  
   2.  クエリ ウィンドウに、 *\<MyLogShippingSolution\>* わかりやすい説明を単一引用符で囲みます。  
  
   3.  クエリ ウィンドウに、 *\<BizTalkServerManagementDatabaseName\>* と*\<BizTalkServerManagementDatabaseServer\>* で名前と、単一引用符で囲まれたソース BizTalk 管理データベースの場所。  
  
   > [!NOTE]
   >  複数の送信元サーバーがある場合は、各送信元サーバーをそれぞれ独自の送信先サーバーに復元できます。 各送信先サーバーでの **@SourceServerName = null**パラメーター、置換*null*適切なソース サーバーの名前を単一引用符で囲みます (たとえば、  **@SourceServerName = 'MySourceServer'**)。  
  
8. **クエリ**メニューの  **Execute**します。  
  
   > [!IMPORTANT]
   >  クエリが失敗した場合は、クエリの問題を修正した後で、この手順の手順 1. から開始して、送信先システムを再構成する必要があります。  
  
   > [!NOTE]
   >  送信先システムでの復元ジョブは、復元された各データベースに対するログ ファイルおよびデータ ファイルを、送信元データベース サーバーに格納されていたときと同じ場所に再作成しようとします。  
  
9. 送信先システムで**SQL Server Management Studio**、展開**SQL Server エージェント**、展開と**ジョブ**します。  
  
     詳細ウィンドウに、次の 3 つの新しいジョブが表示されます。  
  
   - **BTS ログの配布のバックアップ履歴の取得**  
  
      この BizTalk ジョブでは、送信元のバックアップ履歴レコードを送信先に移動します。 既定では、ジョブを 1 分おきに実行するスケジュールになります。 このジョブは、履歴レコードを送信元から送信先に移動するために、可能な限り頻繁に実行されます。 送信元システムでシステム障害が発生しても、送信先システムとして指定したサーバーでは、インポート済みの履歴レコードの処理が続行します。  
  
   - **BTS Server のログ配布データベースの復元**  
  
      この BizTalk ジョブは、移行元の指定されたデータベースのバックアップ ファイルを移行先サーバーに復元します。 既定では、ジョブを 1 分おきに実行するスケジュールになります。 このジョブは、復元するバックアップ ファイルがある限り、完了することなく続行されます。 用心のために、このジョブを 1 回だけ多く実行してジョブが完了していることを確認できます。  
  
   - **BTS ログのマークまで復元の配布**  
  
      この BizTalk ジョブは、すべてのデータベースを最新のログ バックアップ内のマークまで復元します。 これにより、すべてのデータベースでトランザクションの状態の一貫性が確保されます。 さらに、このジョブでは、送信元システムに存在したすべての SQL Server エージェント ジョブが送信先システムに再作成されます。  
  
     > [!IMPORTANT]
     >  これらのジョブが失敗しないように監視する必要があります。  
  
10. [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] で、次のフォルダーを開きます。  
  
     32 ビット コンピューター: %SystemDrive%\Program files \microsoft BizTalk Server\<バージョン\>\Schema\Restore  
  
     64 ビット コンピューター: %SystemDrive%\Program Files (x86) \Microsoft BizTalk Server\<バージョン\>\Bins32\Schema\Restore  
  
11. 右クリック**SampleUpdateInfo.xml**、選び**編集**します。 次の操作を行います。  
  
    -   すべてのインスタンスを置き換える **"SourceServer"** ソース システムの名前に置き換えます。  
  
    -   すべてのインスタンスを置き換える **"DestinationServer"** 送信先システムの名前に置き換えます。  
  
    > [!IMPORTANT]
    >  送信元システムおよび送信先システムの名前は、引用符で囲んでください。  
    > 
    > [!NOTE]
    >  いずれかの [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] データベースの名前を変更した場合、XML ファイル内のデータベース名も更新する必要があります。  
    > 
    > [!NOTE]
    >  BAM を構成している場合は、次の行を追加する必要があります、 **OtherDatabases**のセクション、 **SampleUpdateInfo.xml** BAMAlertsApplication、BAMAlertsNSMain データベースのファイル。   
    > `<Database Name="BAM Alerts Application DB" oldDBName="BAMAlertsApplication" oldDBServer="SourceServer" newDBName=" BAMAlertsApplication" newDBServer="DestinationServer"/>`  
    > `<Database Name="BAM Alerts Instance DB" oldDBName="BAMAlertsNSMain" oldDBServer="SourceServer" newDBName="BAMAlertsNSMain" newDBServer="DestinationServer"/>`  
    > 
    >  これら 2 つのデータベースの既定の名前を変更した場合は、実際のデータベース名を使用してください。  
  
12. 複数のメッセージ ボックス データベースがある場合、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]システムは、リストに別の MessageBoxDB 行を追加し、設定**IsMaster =「0」** マスター以外のデータベースにします。  
  
13. BAM またはルール エンジンを使用する場合は、必要に応じてこれらの行をコメント解除してください。  
  
14. すべてのカスタム データベースがあれば、下に追加、 **\<OtherDatabases\>** セクション。 参照してください[カスタム データベースをバックアップする方法](../core/how-to-back-up-custom-databases.md)します。  
  
15. ファイルの編集を終了したら、ファイルを保存して閉じます。  
  
## <a name="next-steps"></a>次の手順  
 [データベースを復元する方法](../core/how-to-restore-your-databases.md)  
  
## <a name="see-also"></a>参照  
 [バックアップ BizTalk Server ジョブを構成する方法](../core/how-to-configure-the-backup-biztalk-server-job.md)   
 [バックアップ BizTalk Server のジョブをスケジュールする方法](../core/how-to-schedule-the-backup-biztalk-server-job.md)   
 [カスタム データベースをバックアップする方法](../core/how-to-back-up-custom-databases.md)