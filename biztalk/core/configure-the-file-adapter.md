---
title: "ファイル アダプターの構成 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- File adapters, configuring
- configuring [File adapters], about configuring File adapters
- configuring [File adapters]
ms.assetid: 1e0c7e20-80f8-469b-b423-34a2b90f9ec3
caps.latest.revision: "13"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e445bc1d2fb4dcea719c33a336eec88554e20962
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="configure-the-file-adapter"></a>ファイル アダプターを構成します。
ファイル アダプターの構成、セキュリティに関する推奨事項を読み取り、および必要なアクセス許可を表示する方法。

受信場所を作成して送信ポートを使用して[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]、またはプログラム。 このトピックのねらいで、[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]コンソールです。 移動する手順については、プログラムによる、[受信場所を作成または送信ポートをプログラムで](../core/create-the-receive-location-and-send-port-programmatically.md)です。

> [!IMPORTANT]
> **以降で[!INCLUDE[bts2016_md](../includes/bts2016-md.md)]** 、ファイル アダプターを使用して、Azure のファイル共有に接続することができます。 Azure のストレージ アカウントは、BizTalk Server にマウントする必要があります。 [Windows で Azure File storage の概要](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files#mount-the-file-share)取り付け手順について説明します。

## <a name="security-recommendations"></a>セキュリティに関する推奨事項

ファイル アダプタを使用すると、BizTalk Server とディレクトリの間でファイルを入出力できます。 ファイル アダプタをセキュリティで保護して環境に展開するには、次のガイドラインに従うことをお勧めします。  
  
-   境界ネットワーク内のファイル共有に接続するポートを開かないでください。 ファイル アダプタは、イントラネットなど、高い信頼レベルの環境で使用する必要があります。 
  
-   受信場所のドロップ ディレクトリで強力な随意アクセス制御リスト (DACL) を設定します。 たとえば、ファイルの受信場所で取得するメッセージが存在するディレクトリに対してファイルに読み取り、書き込み、削除のアクセス許可を設定し、サブフォルダとファイルに削除のアクセス許可を設定して、認証されたユーザーだけがこの場所にメッセージをドロップできるようにする必要があります。  
  
-   ファイル アダプタを使用して重要なデータを取得する場合は、インターネット プロトコル セキュリティ (IPSec) を使用することをお勧めします。  
  
## <a name="required-permissions"></a>必要な権限

アダプター ハンドラーは、アダプター ハンドラーの選択したホスト インスタンスのセキュリティ コンテキストで実行されます。 ホスト インスタンスを使用して、`Logon`プロパティに、 ***ホスト名*-ホスト インスタンスのプロパティ**BizTalk 管理コンソールでします。 これは、`Logon`任意のフォルダーやファイル アダプターによって使用される共有リソースに対する特定の権限が必要です。

ハンドラーが使用するホスト インスタンスのユーザー アカウントには、次のアクセス許可が必要です。 ✔ では、アクセス許可が必要なことを意味します。 空のエントリは、アクセス許可は必要ありませんを意味します。

| Permissions | [受信ハンドラー] | 送信ハンドラー |
| --- | --- | --- |
| フル コントロール | ✔ <br/> (ファイル共有にアクセスする) 場合は、共有レベルで |  | 
| フォルダーのスキャンとファイルの実行 |  | ✔ <br/> ファイル レベル | 
| フォルダーの一覧とデータの読み取り | ✔ <br/> ファイル レベル | ✔ <br/> ファイル レベル | 
| 属性の読み取り | | ✔ <br/> ファイル レベル | 
| 拡張属性の読み取り | | ✔ <br/> ファイル レベル | 
| ファイルの作成とデータの書き込み | | ✔ <br/> ファイル レベル | 
| フォルダーの作成とデータの追加 | | ✔ <br/> ファイル レベル | 
| サブフォルダーとファイルの削除 | ✔ <br/> ファイル レベル | ✔ <br/> ファイル レベル | 
| アクセス許可の読み取り | | ✔ <br/> ファイル レベル | 
| 変更 | | ✔ <br/> (ファイル共有にアクセスする) 場合は、共有レベルで |

> [!TIP] 
> ファイル レベルでは、開く、**アクセス許可を高度な**のファイルまたはフォルダーをこれらのアクセス許可を参照してください。

> [!NOTE] 
> 各ホストに関連付けられる受信ハンドラーは 1 つだけです。  

## <a name="configure-the-receive-location"></a>受信場所を構成します。
  
> [!NOTE]
>  次の手順を完了する前にする必要がありますが既に追加して、一方向受信ポート。 参照してください[を作成する方法、受信ポート](../core/how-to-create-a-receive-port.md)です。  
  
1.  BizTalk Server 管理コンソールで、 [!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]、展開**BizTalk グループ**、展開**アプリケーション**アプリケーションを展開し、受信場所を作成する です。  
  
2.  左側のウィンドウでをクリックして、**受信ポート**ノード。 次に右ウィンドウで、既存の受信場所に関連付けられているか、新しい受信場所に関連付ける受信ポートを右クリックし、[ **プロパティ**] をクリックします。  
  
3.  左側のウィンドウで、**受信ポートのプロパティ**ダイアログ ボックスで、**受信場所**で、右側のペインをダブルクリックする受信場所またはをクリックして、既存**新規**に新しい受信場所。  
  
4.  **受信場所のプロパティ** ダイアログ ボックスで、**トランスポート**セクションで、**ファイル**ドロップダウン リストから入力して、クリックして**構成**を受信場所のトランスポートのプロパティを構成します。  
  
5.  **全般** タブで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**受信フォルダー**|必須。 ファイル システム、ネットワーク共有上のフォルダーにパスを入力するか、ファイル受信ハンドラー、Azure のファイル共有がファイルを読み取る。 直接のパスを入力することができます、**受信フォルダー**テキスト ボックス、またはファイル システムを使用して、選択、**参照**ボタンをクリックします。 フォルダーの参照をするときに作成することも、フォルダーを使用して新しい**新しいフォルダーの作成**です。<br /><br /> Azure ファイル記憶域共有を使用する場合は、入力`\\yourfilestoragename.file.core.windows.net\yourfilesharename`です。 <br /><br />**型:**文字列 <br/><br/>**注:**を設定しないでください、**受信フォルダー**プロパティ シンボリック リンクを使用して NT の分散ファイル システムを使用するフォルダーをします。 NT の分散ファイル システムを使用している場合は、直接的なファイル アダプターのネットワーク パスのフォルダーを使用する受信場所のみをできます。 <br /><br /> このプロパティの制限については、次を参照してください。[ファイル アダプタ構成時の制限事項](../core/restrictions-when-configuring-the-file-adapter.md)です。 <br/><br/>**注:**の URI を送信ポートまたは受信場所は、256 文字を超えることはできません。|  
    |**ファイル マスク**|必須。 ファイルのマスクを指定します。 このマスクは、標準のワイルドカード文字を含めることができます"\*"です。<br /><br /> **既定値:** \*.xml<br /><br /> **型:**文字列<br /><br /> このプロパティの制限については、次を参照してください。[ファイル アダプタ構成時の制限事項](../core/restrictions-when-configuring-the-file-adapter.md)です。|  
    |**パブリック アドレス**|この場所のパブリック アドレスを指定します。 このアドレスは、外部のパートナーに公開されます。<br /><br /> このプロパティの値が指定されていない場合、ランタイム エンジンで次のように置き換えられます。<br /><br /> file://\<*受信フォルダー*>/\<*ファイル マスク*><br /><br /> このプロパティの値にはアダプター プレフィックスが必要です。<br /><br /> **型:**文字列<br /><br /> **最小の長さ:** 0<br /><br /> **最大長:** 256|  
    |**再試行の回数**|ネットワーク共有上の受信場所が一時的に使用できない場合に、アクセスを試行する回数を指定します。<br /><br /> **既定値:** 5<br /><br /> **型:**長<br /><br /> **最小値:** 0<br /><br /> **最大値:** MAX_LONG|  
    |**再試行の間隔 (分)**|ネットワーク共有上の受信場所が一時的に使用できない場合に、アクセスを再試行する時間間隔を分単位で指定します。<br /><br /> **既定値:** 5 分<br /><br /> **型:**長<br /><br /> **最小値:** 0<br /><br /> **最大値:** MAX_LONG|  
  
6.  **認証** タブで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**ホストにネットワーク共有へのアクセスがあるない場合に、これらの資格情報を使用します。**| ネットワーク共有、または、Azure のファイル共有を使用する場合にのみ必要です。 <br /><br /> **既定値:** False<br /><br /> **型:**ブール|  
    |**ユーザー名**|ネットワーク共有を使用する場合は、共有へのアクセスを持っているユーザー名を入力します。 <br /><br />  Azure のファイル ストレージを使用して共有する場合は、ストレージ アカウントの名前を入力します。<br/><br/>**型:**文字列 <br /><br />**注:**同じネットワーク共有にマップされている複数の受信場所が代替の資格情報で構成されているかどうかは、すべての受信場所と同じ資格情報を使用する必要があります。 Windows では、1 台のコンピューターから、共有ネットワーク サーバーに、複数の資格情報を使用して複数の接続を確立することはできません。|  
    |**Password**|ネットワーク共有を使用する場合は、ネットワーク共有へのアクセス権を持つアカウントのパスワードを入力します。<br /><br />  共有ファイルを Azure ストレージを使用した場合は、ストレージ アカウント アクセス キーです。 を入力します。Azure ポータルに表示されます。<br /><br /> **型:**文字列|  
  
7.  **バッチ処理** タブで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**バッチ内のメッセージの数**|バッチ送信するメッセージの最大数を指定します。<br /><br /> **既定値:** 5<br /><br /> **型:** Int<br /><br /> **最小値:** 1<br /><br /> **最大値:** 256|  
    |**最大バッチ サイズ (バイト単位)**|バッチの合計バイト数の最大値を指定します。<br /><br /> **既定値:** 102400<br /><br /> **型:** Int<br /><br /> **最小値:** 1024<br /><br /> **最大値:** MAX_LONG|  
  
     ファイル アダプターは、メッセージが最大数または最大サイズ (バイト単位) のどちらかに到達したときにバッチを制限します。  
  
9. [ **OK**] を選択します。  
  
10. 適切な値を入力、**受信場所のプロパティ** ダイアログ ボックスで、受信場所の構成を完了し、をクリックして**OK**設定を保存します。 については、**受信場所のプロパティ**ダイアログ ボックスを参照してください[受信場所を作成する方法](../core/how-to-create-a-receive-location.md)です。  

## <a name="configure-the-send-port"></a>送信ポートを構成します。

1.  BizTalk Server 管理コンソールで、新しい送信ポートを作成または変更する既存の送信ポートをダブルクリックします。 参照してください[送信ポートを作成する方法](../core/how-to-create-a-send-port2.md)です。 すべての送信ポートのオプションを構成し、指定**ファイル**の**型**オプション、**トランスポート**のセクションで、**全般**タブです。  
  
2.  選択、**構成**横に**型**です。  
  
3.  **全般** タブで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**移行先の場所**|必須。 ファイル システム、パブリック共有、または出力メッセージを書き込むための Azure のファイル共有上の場所にパスを入力します。 直接のパスを入力することができます、**先**、か、またはファイル システムを使用して、、**参照**ボタンをクリックします。 フォルダーを参照するとき、**フォルダーの参照**ダイアログ ボックスで、作成することも、新しいフォルダーをクリックして**新しいフォルダーの作成**です。<br /><br /> Azure ファイル記憶域共有を使用する場合は、入力`\\yourfilestoragename.file.core.windows.net\yourfilesharename`です。<br /><br /> **型:**文字列 <br /><br />**注:**の URI を送信ポートまたは受信場所は、256 文字を超えることはできません。|  
    |**ファイル名**|ファイル送信ハンドラがメッセージを書き込むファイルの名前を指定します。<br /><br /> このプロパティの制限についてを含む、ファイル名にマクロを使用して参照してください[ファイル アダプタ構成時の制限事項](../core/restrictions-when-configuring-the-file-adapter.md)です。|  
    |**[コピー モード]**|ファイルにメッセージを書き込むときに使用するコピー モードを定義します。 有効な値は、<br /><br /> **追加します。** ファイルが存在する場合は、ファイル送信ハンドラがファイルを開き、ファイルの末尾にメッセージを追加します。 ファイルが存在しない場合は、ファイル送信ハンドラが新しいファイルを作成します。<br /><br /> **上書き**です。 ファイルが存在する場合は、ファイル送信ハンドラがファイルを開き、ファイルの内容を上書きします。 ファイルが存在しない場合は、ファイル送信ハンドラが新しいファイルを作成します。<br /><br /> **新規作成**です。 ファイルが存在しない場合は、ファイル送信ハンドラが新しいファイルを作成し、そのファイルにメッセージを書き込みます。 ファイルが存在する場合は、ファイル送信ハンドラがエラーを報告し、送信ポートの通常のアダプタ再試行ロジックに従ってメッセージを処理します。 これはファイル送信ハンドラの既定のコピー モードです。|  
    |**書き込みキャッシュを許可します。**|ファイルにメッセージを書き込む際にファイル システム キャッシュを使用するかどうかを定義します。<br /><br /> 有効なオプションを次に示します。<br /><br /> **False**ファイル システム キャッシュを使用しないでください。<br /><br /> **True**ファイル システム キャッシュを使用します。<br /><br /> **既定値:** False**重要:**このプロパティを設定**True**停電がある場合に、潜在的なデータが失われる、ファイル アダプターのパフォーマンスを向上させることができますおよび notすべてのデータが書き込まれるディスクにします。|  
    |**書き込み中に一時ファイルを使用します。**|最初に一時ファイルに出力ファイルを書き込み、この書き込み操作が完了した後でファイル名を変更するかどうかを定義します。 このオプションが有効になっているかどうかは、拡張子を持つ一時ファイルを作成、 **BTS-WIP**です。<br /><br /> 有効なオプションは次のとおりです。<br /><br /> **True** : ファイル アダプタはターゲット フォルダに書き込むときに一時ファイルを作成します。<br /><br /> **False** : ファイル アダプタはターゲット フォルダに書き込むときに一時ファイルを作成できません。<br /><br /> **既定値:** False**注:**ときにこのオプションは利用できるのみ、 **CopyMode**の値に設定されて**新規作成**|  
  
4.  **認証** タブで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**ホストにネットワーク共有へのアクセスがあるない場合に、これらの資格情報を使用します。**| ネットワーク共有、または、Azure のファイル共有を使用する場合にのみ必要です。 <br /><br /> **既定値:** False<br /><br /> **型:**ブール|  
    |**ユーザー名**|ネットワーク共有を使用する場合は、共有へのアクセスを持っているユーザー名を入力します。 <br /><br />  Azure のファイル ストレージを使用して共有する場合は、ストレージ アカウントの名前を入力します。<br /><br /> **型:**文字列|  
    |**Password**|ネットワーク共有を使用する場合は、ネットワーク共有へのアクセス権を持つアカウントのパスワードを入力します。<br /><br />  共有ファイルを Azure ストレージを使用した場合は、ストレージ アカウント アクセス キーです。 を入力します。Azure ポータルに表示されます。<br /><br /> **型:**文字列|  
  
5.  選択**OK**設定を保存します。  

## <a name="set-the-properties-for-a-dynamic-send-port"></a>動的送信ポートのプロパティを設定します。
  
 動的送信ポートには、BizTalk Server 管理コンソールのトランスポート構成オプションが用意されていません。これは、これらのプロパティがメッセージに関連付けられたコンテキスト プロパティで提供されることが前提となっているためです。 これらのプロパティは、カスタム パイプラインまたはオーケストレーションで設定できます。 オーケストレーションでメッセージ構成プロパティを設定するには、次の操作を行うことができます。  
  
-   追加、**メッセージの構築**図形をオーケストレーションにします。  
  
-   構成、**メッセージの構築**新しいメッセージの構築図形。 (例、Message_2)。  
  
-   追加、**メッセージの割り当て**図形を**メッセージの構築**図形です。  
  
-   コードを追加して、**メッセージの割り当て**図形を構築するメッセージを初期化し、メッセージの適切な構成プロパティを設定します。 次のコードで構築された Message_2 というメッセージの初期化、**メッセージの構築**図形し、メッセージの 2 つの構成プロパティを設定します。 このシナリオでは、Message_1 が最初にオーケストレーションで受信されました。  
  
    ```  
    Message_2=Message_1;  
    Message_2(FILE.CopyMode)= 0; //0=Append  
    Message_2(FILE.AllowCacheOnWrite)= true;  
    Message_2(FILE.UseTempFileOnWrite)= true;  
    ```  
 
  
## <a name="configure-the-receive-or-send-handler"></a>受信を構成するか、送信ハンドラー
  
1.  BizTalk Server 管理コンソールで、展開**BizTalk Server 管理コンソール**、展開**BizTalk グループ**、展開**プラットフォームの設定**をクリックして**アダプター**です。  
  
2.  アダプターの一覧を展開でクリックして**ファイル**右側のウィンドウで、受信を右クリックし、または送信ハンドラーを構成します。 選択**プロパティ**です。  
  
3.  **ホスト名**一覧で、ハンドラーを実行するホストを選択します。  
  
4.  **[OK]**をクリックします。  

## <a name="more-topics-in-this-section"></a>このセクションのトピック

[ファイルを作成する受信場所または送信ポートをプログラムで](../core/create-the-receive-location-and-send-port-programmatically.md)

[ファイル アダプタ プロパティ スキーマおよびプロパティ](../core/file-adapter-property-schema-and-properties.md)

[ファイル アダプタ構成時の制限事項](../core/restrictions-when-configuring-the-file-adapter.md)

## <a name="see-also"></a>参照

 [受信と送信サーバーのポート](../core/ports-for-the-receive-and-send-servers.md)   
 [セキュリティの最小ユーザー権限](../core/minimum-security-user-rights.md)