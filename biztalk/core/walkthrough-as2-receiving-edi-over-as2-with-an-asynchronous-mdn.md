---
title: "チュートリアル (AS2): 非同期 MDN による AS2 経由で EDI の受信 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ac3962e4-0525-4194-8cf1-b90664f1a139
caps.latest.revision: "40"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a0dd9e94ff74adb4419f95b386861376bb424fd1
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="walkthrough-as2-receiving-edi-over-as2-with-an-asynchronous-mdn"></a>チュートリアル (AS2): 非同期 MDN による AS2 経由での EDI の受信
このチュートリアルでは、AS2 トランスポート経由で EDI メッセージを受信して同期 MDN を返すソリューションを作成する、一連の手順について説明します。  
  
## <a name="prerequisites"></a>前提条件  
 このトピックの手順を実行するための前提条件を次に示します。  
  
-   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理者グループまたは [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] B2B Operators グループのメンバーとしてログオンしている必要があります。  
  
-   チュートリアルを実行するコンピューターには、インターネット インフォメーション サービス (IIS) 7 がインストールされている必要があります。  
  
-   チュートリアルを実行するコンピューターに 64 ビット版の Windows がインストールされている場合は、BizTalk ホストが 32 ビットのみとマークされていることを確認する必要があります。 IIS の [アプリケーション プールの 32 ビット アプリケーション設定を有効にする] を True に設定する必要があります。 詳細については、次を参照してください。[チュートリアル 3: AS2 チュートリアル](../core/tutorial-3-as2-tutorial.md)です。  
  
## <a name="how-the-solution-receives-an-edi-interchange-and-returns-an-asynchronous-mdn"></a>ソリューションで EDI インターチェンジを受信して非同期 MDN を返す方法  
 このソリューションは次の処理を実行します。  
  
1.  取引先から HTTP 経由で、EDI インターチェンジが含まれた AS2 メッセージを受信し、EDIINT/AS2 からインターチェンジをデコードします。  
  
    > [!NOTE]
    >  この一覧のイベントは、示されている順序で発生するとは限りません。  
  
2.  MDN 応答を生成して、MessageBox に配置します。  
  
3.  動的送信ポートによるメッセージ MDN を取得します。  
  
4.  非同期メッセージ MDN を取引先に返します。  
  
5.  インターチェンジの EDI 形式を内部 XML 形式に変換し、メッセージ ボックスに格納します。  
  
6.  PassThruTransmit パイプラインを持つ送信ポートが、メッセージ XML ファイルを MessageBox から取得します。  
  
7.  送信ポートが、EDI インターチェンジ XML ファイルを Contoso というパーティのフォルダーに送信します。  
  
 次の図では、このソリューションのアーキテクチャを示しています。  
  
 ![非同期 MDN による AS2 の受信](../core/media/bts-configuring-the-receiving-of-edi-over-as2-with-an-asynchronous-mdnc.gif "bts_Configuring_the_Receiving_of_EDI_Over_AS2_with_an_Asynchronous_MDNc")  
  
## <a name="the-functionality-in-this-solution"></a>このソリューションの機能  
 このチュートリアルの機能には、以下の条件が適用されます。  
  
-   EDI 受信確認は生成されません。 EDI 受信確認の生成はではデモンストレーション[チュートリアル (X12): EDI インターチェンジの受信と送信、受信確認をバックアップ](../core/walkthrough-x12--receive-edi-interchanges-and-send-back-an-acknowledgement.md)です。 「AS2 トランスポート経由で EDI 受信確認を送信する[チュートリアル (AS2): 非同期 MDN による AS2 経由で送信する EDI](../core/walkthrough-as2-sending-edi-over-as2-with-an-asynchronous-mdn.md)です。  
  
-   このソリューションは、EDIFACT エンコードではなく X12 エンコードを使用するインターチェンジを対象に設計されています。  
  
    > [!NOTE]
    >  EDIFACT エンコードに使用される構成は、X12 エンコードに使用される構成とよく似ています。  
  
-   EDI の種類の検証および拡張された検証は、受信インターチェンジに対して実行されます。  
  
-   AS2 レポートおよび EDI レポートが有効になり、インターチェンジの状態レポートに表示するトランザクション セットが保存されます。  
  
-   このソリューションは、否認不可データベースに署名、圧縮、暗号化、およびメッセージ ストレージを構成しません。 これらのプロパティを構成する手順については、次を参照してください。 [AS2 プロパティを設定する](../core/configuring-as2-properties.md)です。  
  
## <a name="configuring-and-testing-the-walkthrough"></a>チュートリアルの構成とテスト  
 このソリューションに必要な手順は以下のとおりです。  
  
-   必要なメッセージ スキーマを使用して BizTalk プロジェクトをビルドおよび展開し、受信したインターチェンジを [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] で処理するときにそのスキーマを利用できるようにします。  
  
-   AS2 メッセージの受信に使用する BTS ISAPI フィルターを有効にします。  
  
-   Fabrikam からの AS2 メッセージを受信する Contoso 仮想ディレクトリを、受信場所で構成したとおりに作成します。  
  
-   MDN を Contoso から受信する Fabrikam 仮想ディレクトリを作成します。  
  
-   Contoso および Fabrikam 仮想ディレクトリが、Windows SharePoint Services の管理対象から除外されるように指定します。  
  
-   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 用の静的な一方向 HTTP 受信ポートを作成し、EDI ビジネス ドキュメントを含んでいる AS2 メッセージを取引先から受信します。 受信パイプラインとして AS2EDIReceive パイプラインを構成します。  
  
-   受信した AS2 メッセージに応答して MDN を送信する [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 用の動的な一方向 HTTP 送信ポートを作成します。  
  
    > [!NOTE]
    >  この送信ポートは、EdiIntAS.IsAS2AsynchronousMDN プロパティ (AS2EdiReceive パイプラインにより True に設定されている) および関連付けトークンに基づいて、MDN をサブスクライブします。 メッセージのヘッダーにある Receipt-Delivery-Notification 行のアドレスに MDN を送信するには、送信ポートが動的になっている必要があります。  
  
-   静的な一方向 FILE 送信ポートを作成し、EDI ペイロード (XML 形式) をローカル フォルダーにルーティングします。 ローカル フォルダーを作成します。  
  
-   Fabrikam および Contoso の両方にパーティ (取引先) を作成します。  
  
-   両方の取引先に対して、それぞれビジネス プロファイルを作成します。  
  
-   Fabrikam および Contoso のビジネス プロファイル間に AS2 アグリーメントを作成します。 AS2 アグリーメントには、AS2 メッセージを送信し、その応答として非同期 MDN を受信するためのプロパティが含まれます。  
  
-   Fabrikam および Contoso のビジネス プロファイル間に、X12 メッセージを受信する X12 アグリーメントを作成します。  
  
-   AS2 チュートリアル ファイルの一部として同梱されている HTTP 送信者ユーティリティを使用して、このソリューションをテストします。 このユーティリティは、EDI インターチェンジを含むテスト用 AS2 メッセージを、AS2 トランスポートを経由して送信します。 このユーティリティは、AS2 トランスポートを経由して、EDI インターチェンジが含まれた AS2 テスト メッセージを送信します (この X12_00401_864.edi は AS2 チュートリアルにも付属しています)。 このチュートリアルに使用する HTTP 送信者とテスト メッセージは、チュートリアルに付属しているバージョンと同じです。  
  
### <a name="configuring-the-walkthrough"></a>チュートリアルの構成  
 ここでは、チュートリアルを構成する手順について説明します。  
  
##### <a name="to-deploy-the-message-schema"></a>メッセージ スキーマを展開するには  
  
1.  [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] で、[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\AS2 Tutorial\Schemas\Schemas.btproj プロジェクトを開きます。  
  
    > [!NOTE]
    >  このプロジェクトは AS2 チュートリアルに付属し、テスト メッセージと共に使用する 864 スキーマが含まれています。  
  
    > [!NOTE]
    >  このトピックは、EDI スキーマ、パイプライン、およびオーケストレーションを含む BizTalk EDI アプリケーションに別のアプリケーションから参照を既に追加していることを前提としています。 いない場合を参照してください。[を BizTalk Server EDI アプリケーションへの参照を追加する方法](http://msdn.microsoft.com/library/7af066fb-372f-4709-b566-c8d6b4a9d782)です。  
  
2.  右クリックし、**スキーマ**ソリューション エクスプ ローラーでプロジェクトをクリックして**プロパティ**です。 をクリックして、**署名**プロジェクト デザイナーのチェック タブ、**アセンブリに署名**、チェック ボックスをオンし、ドロップダウン リストから選択**新規**を作成するために必要な値を指定し、厳密な名前キー ファイルです。 変更を保存し、プロジェクトのプロパティ ウィンドウを閉じます。  
  
3.  Schemas.btproj をビルドおよび展開します。  
  
##### <a name="to-enable-the-bts-isapi-filter"></a>BTS ISAPI フィルターを有効にするには  
  
1.  をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**管理ツール**、クリックして**インターネット インフォメーション サービス (IIS) マネージャー**.  
  
    > [!TIP]
    >  オペレーティング システムによっては、管理ツールの [スタート] メニュー オプションを利用できない場合があります。 このような場合、をクリックして**開始**、 をクリックして**実行**、入力と`inetmgr`インターネット インフォメーション サービス (IIS) マネージャを開きます。  
  
2.  ルート Web サーバーのエントリを選択し、、**機能ビュー**、ダブルクリックして**ハンドラー マッピング**し、操作 ウィンドウでをクリックして**スクリプト マップの追加**です。  
  
    > [!NOTE]
    >  Web サーバー レベルでスクリプト マッピングを構成すると、すべての子 Web サイトに適用するには、このマッピングが発生します。 特定の Web サイトまたは仮想フォルダーへのマッピングを制限する場合は、ターゲット サイトまたは Web サーバーではなくフォルダーを選択します。  
  
3.  **スクリプト マップの追加** ダイアログ ボックスで、入力`BtsHttpReceive.dll`で、**要求パス**フィールドです。  
  
4.  **実行可能ファイル**フィールドで、をクリックして、**省略記号 (...)**ボタンをクリックしを参照[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]HttpReceive です。 BtsHttpReceive.dll を選択し、をクリックして**OK**です。  
  
5.  入力`BizTalk HTTP Receive`で、`Name`フィールドをクリックして**要求の制限**です。  
  
6.  要求の制限 ダイアログ ボックスで、選択、**動詞**タブをクリックし**次の動詞のいずれかの**します。 入力`POST`動詞として。  
  
7.  **アクセス** タブで **スクリプト** をクリックし、 **ok**です。  
  
8.  をクリックして**OK** ISAPI 拡張を許可するメッセージが表示されたらをクリックし、**はい**です。  
  
##### <a name="to-configure-the-contoso-web-page"></a>Contoso Web ページを構成するには  
  
1.  IIS マネージャーを右クリックして**アプリケーション プール**選択**アプリケーション プールの追加**です。  
  
2.  **アプリケーション プールの追加**] ダイアログ ボックスで、入力**BizTalkAppPool**で**名前**、し、[ **.NET Framework V4.0.30210**で、**.NET framework のバージョン**ドロップダウン リスト。 **[OK]**をクリックします。  
  
    > [!NOTE]
    >  コンピューターにインストール済みの [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] のバージョンによって、バージョン番号が異なる場合があります。  
  
3.  選択**アプリケーション プール**、機能ビューの選択で**BizTalkAppPool**、順にクリック**詳細設定**で、**アクション**ウィンドウです。  
  
4.  **詳細設定**ダイアログ ボックスで、 **Identity**をクリックし、**省略記号 (...)**ボタンをクリックします。  
  
5.  **アプリケーション プール Id**ダイアログ ボックスで、**カスタム アカウント** をクリックし、**設定**です。  
  
6.  入力、**ユーザー名**と**パスワード**administrators グループのメンバーであるユーザー アカウントのパスワードを入力で**パスワードの確認入力**をクリックして**OK** IIS マネージャーに戻りますを 3 回です。  
  
7.  IIS マネージャーで、開く、**サイト**フォルダーです。 右クリックし、 **Default Web Site**ノードをクリックして**アプリケーションの追加**です。  
  
8.  **アプリケーションの追加** ダイアログ ボックスに、入力**Contoso**で、**エイリアス**テキスト ボックス、およびクリック**選択**です。  
  
9. **アプリケーション プールの選択**ダイアログ ボックスで、 **BizTalkAppPool**  をクリック**OK**です。  
  
10. **物理パス**をクリックして、**省略記号 (...)**ボタンをクリックしを参照[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]HttpReceive です。  
  
11. をクリックして**テストの設定**に表示されるエラーがないことを確認し、**接続のテスト** ダイアログ ボックス。 **[閉じる]**をクリックし、 **[OK]**をクリックします。  
  
12. IIS マネージャーでは、Contoso 仮想ディレクトリを選択し、、**機能ビュー**をダブルクリックして**認証**です。  
  
13. **認証**] ページで、[**匿名認証**ことを確認し、**ステータス**は**有効**です。 場合、**ステータス**は**無効になっている**、 をクリックして**を有効にする**で、**アクション**ウィンドウです。  
  
##### <a name="to-configure-the-fabrikam-web-page"></a>Fabrikam Web ページを構成するには  
  
1.  IIS マネージャーで、開く、**サイト**フォルダーです。 右クリックし、 **Default Web Site**ノードをクリックして**アプリケーションの追加**です。  
  
2.  **アプリケーションの追加** ダイアログ ボックスで、入力**Fabrikam**で**エイリアス**、順にクリック**選択**です。  
  
3.  **アプリケーション プールの選択**ダイアログ ボックスで、 **BizTalkAppPool**  をクリック**OK**です。  
  
4.  **物理パス**をクリックして、**省略記号 (...)**ボタンをクリックしを参照[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]sdk \as2 \fabrikam です。  
  
5.  をクリックして**テストの設定**に表示されるエラーがないことを確認し、**接続のテスト** ダイアログ ボックス。 **[閉じる]**をクリックし、 **[OK]**をクリックします。  
  
6.  IIS マネージャーでは、Contoso 仮想ディレクトリを選択し、、**機能ビュー**をダブルクリックして**認証**です。  
  
7.  **認証**] ページで、[**匿名認証**ことを確認し、**ステータス**は**有効**です。 場合、**ステータス**は**無効になっている**、 をクリックして**を有効にする**で、**アクション**ウィンドウです。  
  
##### <a name="to-specify-that-your-virtual-directory-is-not-managed-by-windows-sharepoint-services"></a>仮想ディレクトリが Windows SharePoint Services の管理対象から除外されるように指定するには  
  
1.  Windows SharePoint Services がコンピューターにインストールされている場合にをクリックして**開始**、 をポイント**すべてのプログラム**、指す**管理ツール**をクリックして**SharePoint 3.0 サーバーの全体管理**です。  
  
    > [!NOTE]
    >  この手順は、チュートリアルを設定するコンピューター上に Windows SharePoint Server がインストールされている場合に実行する必要があります。 実行する場合は、IIS 仮想ディレクトリが Windows SharePoint Server の管理対象から除外されるように指定する必要があります。  
  
2.  **サーバーの全体管理**] ページの [**サーバーの全体管理**をクリックして**アプリケーション管理**です。  
  
3.  **アプリケーション管理**] ページで [**管理パスの定義**です。  
  
4.  **管理パスの定義**] ページの [**新しいパスを追加**で、**パス**テキスト ボックスに、入力**Contoso**です。 [**型**、] をクリックして**エクスクルード パス**、順にクリック**OK**です。  
  
5.  Fabrikam 仮想ディレクトリに対して手順 4. を繰り返します。  
  
##### <a name="to-create-a-receive-port-to-receive-the-edi-interchange-over-as2-from-fabrikam"></a>Fabrikam から AS2 経由で EDI インターチェンジを受信する受信ポートを作成するには  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、右クリックし、**受信ポート**ノードの下、 **BizTalk アプリケーション 1**に**新規**をクリックして**一方向受信ポート**です。  
  
2.  受信ポートの名前を指定し、をクリックして**受信場所**コンソール ツリーでします。  
  
3.  **[新規作成]**をクリックします。  
  
4.  名前、受信場所は、select **HTTP**の**型**、順にクリック**構成**です。  
  
5.  **仮想ディレクトリと ISAPI 拡張**、入力`/Contoso/BTSHTTPReceive.dll`です。  
  
6.  選択、**失敗した要求を中断**チェック ボックスをオンし、をクリックして**OK**です。  
  
7.  **受信パイプライン** **AS2EDIReceive**です。  
  
8.  をクリックして**[ok]**、順にクリック**OK**もう一度です。  
  
9. **受信場所**のペイン、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールでは、受信場所を右クリックし、をクリックして**を有効にする**です。  
  
##### <a name="to-create-a-dynamic-send-port-to-send-the-mdn-to-fabrikam"></a>MDN を Fabrikam に送信するための動的な送信ポートを作成するには  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、右クリックし、**送信ポート**ノードの下、 **BizTalk アプリケーション 1**に**新規**をクリックして**動的な一方向送信ポート**です。  
  
2.  **送信ポートのプロパティ**ダイアログ ボックスで、送信ポートの名前。  
  
3.  **送信パイプライン** **AS2Send**です。  
  
4.  コンソール ツリーで、次のように選択します。**フィルター**です。 **プロパティ**、入力**EdiIntAS.IsAS2AsynchronousMDN**; の**演算子**、入力 **==** ; および**値**、入力**True**です。  
  
5.  **[OK]**をクリックします。  
  
##### <a name="to-create-a-send-port-to-send-the-edi-payload-to-a-local-folder"></a>EDI ペイロードをローカル フォルダーに送信する送信ポートを作成するには  
  
1.  Windows エクスプローラで、という名前の Contoso ローカル フォルダーを作成する**EDI_to_Contoso** EDI ペイロードを送信します。  
  
2.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールを右クリックして**送信ポート**、 をポイント**新規**、クリックして**静的な一方向送信ポート**です。  
  
3.  **送信ポートのプロパティ**ダイアログ ボックスで、名前、送信ポートにたとえば、 **Send_Payload**です。 選択**ファイル**の**型**、クリックして**構成**です。  
  
4.  **FILE トランスポートのプロパティ** ダイアログ ボックスの**コピー先フォルダー**を参照して選択、 **EDI_to_Contoso**手順 1. で作成したフォルダーです。 ままにして**ファイル名**として**%MessageID%.xml**です。 **[OK]**をクリックします。  
  
5.  既定の**PassThruTransmit**の**送信パイプライン**です。  
  
6.  をクリックして**フィルター**コンソール ツリーでします。 **プロパティ**、入力**BTS です。MessageType**です。 **演算子**、入力 **==**です。 **値**、メッセージのメッセージの種類を入力`http://schemas.microsoft.com/BizTalk/Edi/X12/2006#X12_00401_864`です。  
  
7.  **[OK]**をクリックします。  
  
8.  **送信ポート**のペイン、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールでは、送信ポートを右クリックし、をクリックして**開始**です。  
  
##### <a name="to-create-a-party-and-a-business-profile-for-fabrikam"></a>Fabrikam のパーティとビジネス プロファイルを作成するには  
  
1.  右クリックし、**パーティ**内のノード、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールをポイント**新規**、クリックして**パーティ**です。  
  
2.  パーティの名前を入力、**名前**テキスト ボックスに入力し**OK**です。  
  
    > [!NOTE]
    >  選択して、**ローカルの BizTalk は、このパーティからメッセージを送信するパーティまたはサポートが受信したメッセージを処理** チェック ボックスを指定できますをホストしている同じ組織のパーティの作成中であること[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]. その指定に基づいて、アグリーメントを作成するときに一部のプロパティが有効または無効になります。 ただし、このチュートリアルでは、このチェック ボックスはオンのままでかまいません。  
  
3.  パーティ名を右クリックし、**新規**、クリックして**ビジネス プロファイル**です。  
  
4.  **プロファイル プロパティ**ダイアログ ボックスの**全般** ページで、入力**fabrikam_profile**で、**名前**テキスト ボックス。  
  
    > [!NOTE]
    >  パーティを作成すると、プロファイルも作成されます。 新しいプロファイルを作成する代わりに、そのプロファイルの名前を変更して使用できます。 プロファイルの名前を変更するプロファイルを右クリックし **プロパティ**です。 **全般** ページで、プロファイルの名前を指定します。  
  
##### <a name="to-create-a-party-and-a-business-profile-for-contoso"></a>Contoso のパーティとビジネス プロファイルを作成するには  
  
1.  右クリックし、**パーティ**内のノード、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールをポイント**新規**、クリックして**パーティ**です。  
  
2.  パーティの名前を入力、**名前**テキスト ボックスに入力し**OK**です。  
  
    > [!NOTE]
    >  選択して、**ローカルの BizTalk は、このパーティからメッセージを送信するパーティまたはサポートが受信したメッセージを処理** チェック ボックスを指定できますをホストしている同じ組織のパーティの作成中であること[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]. その指定に基づいて、アグリーメントを作成するときに一部のプロパティが有効または無効になります。 ただし、このチュートリアルでは、このチェック ボックスはオンのままでかまいません。  
  
3.  パーティ名を右クリックし、**新規**、クリックして**ビジネス プロファイル**です。  
  
4.  **プロファイル プロパティ**ダイアログ ボックスの**全般** ページで、入力**Contoso_Profile**で、**名前**テキスト ボックス。  
  
    > [!NOTE]
    >  パーティを作成すると、プロファイルも作成されます。 新しいプロファイルを作成する代わりに、そのプロファイルの名前を変更して使用できます。 プロファイルの名前を変更するプロファイルを右クリックし **プロパティ**です。 **全般** ページで、プロファイルの名前を指定します。  
  
##### <a name="to-create-an-as2-agreement-between-the-two-business-profiles"></a>2 つのビジネス プロファイル間で AS2 アグリーメントを作成するには  
  
1.  右クリック**fabrikam_profile**、 をポイント**新規**、クリックして**アグリーメント**です。  
  
2.  **全般プロパティ** ページの**名前**テキスト ボックスに、アグリーメントの名前を入力します。  
  
3.  **プロトコル**ドロップダウン リストで、 **AS2**です。  
  
4.  **2 番目のパートナー**  セクションから、**名前**ドロップダウン リストで、 **Contoso**です。  
  
5.  **2 番目のパートナー**  セクションから、**プロファイル**ドロップダウン リストで、 **Contoso_Profile**です。  
  
     2 つの新しいタブの追加を取得 の横に表示されます、**全般**タブです。各タブは、一方向の AS2 アグリーメントの構成用です。  
  
6.  **全般** タブで、**全般プロパティ** ページの 、**共通のホスト設定**セクションで、**レポートをオンに**です。  
  
7.  次のタスクを実行、 **Fabrikam が Contoso ->**タブです。  
  
    1.  **識別子** ページで、値を入力**AS2-から**と**AS2-に**です。 **AS2-から**、入力`Fabrikam`です。 **AS2-To**、入力`Contoso`です。  
  
    2.  **検証** ページで、、**検証および MDN に対してメッセージ ヘッダーの代わりにアグリーメントの設定を使用して** チェック ボックス  
  
    3.  **受信確認 (Mdn)**  ページで、次の操作します。  
  
        1.  選択、 **mdn を要求する**チェック ボックスをオンします。  
  
        2.  確認してください、**署名付き mdn を要求してもする**チェック ボックスはオフです。  
  
        3.  選択、**非同期 MDN を要求する**チェック ボックスをオンします。  
  
        4.  **- Receipt-delivery-option (URL)**テキスト ボックスに、入力`http://localhost/Fabrikam/Default.aspx?Destination=_MDNToFabrikam`です。  
  
8.  次のタスクを実行、 **Contoso が Fabrikam ->**タブです。  
  
    > [!NOTE]
    >  このチュートリアルでは、必要な値をタブに指定し、アグリーメントを正常に作成できるようにします。 アグリーメントを正常に作成する両方の一方向アグリーメント タブの値に対して定義されている必要があります**AS2-から**と**AS2-に**です。  
  
    1.  **識別子** ページで、値を入力**AS2-から**と**AS2-に**です。 **AS2-から**、入力`Contoso`です。 **AS2-To**、入力`Fabrikam`です。  
  
9. **[適用]**をクリックします。  
  
10. **[OK]**をクリックします。 新しく追加したアグリーメントが一覧表示、**契約**のセクションで、**パーティとビジネス プロファイル**ウィンドウです。 新しく追加したアグリーメントは既定で有効になります。  
  
##### <a name="to-create-an-x12-agreement-between-the-two-business-profiles"></a>2 つのビジネス プロファイルの間に X12 アグリーメントを作成するには  
  
1.  右クリック**fabrikam_profile**、 をポイント**新規**、クリックして**アグリーメント**です。  
  
2.  **全般プロパティ** ページの**名前**テキスト ボックスに、アグリーメントの名前を入力します。  
  
3.  **プロトコル**ドロップダウン リストで、 **X12**です。  
  
4.  **2 番目のパートナー**  セクションから、**名前**ドロップダウン リストで、 **Contoso**です。  
  
5.  **2 番目のパートナー**  セクションから、**プロファイル**ドロップダウン リストで、 **Contoso_Profile**です。  
  
     2 つの新しいタブの追加を取得 の横に表示されます、**全般**タブです。各タブは一方向 X12 アグリーメントを構成するためのものです。  
  
6.  **全般** タブで、**全般プロパティ** ページの 、**共通のホスト設定**セクションで、**レポートをオンに**、し、選択**reporting 用メッセージ ペイロードを格納**です。  
  
7.  次のタスクを実行、 **Fabrikam が Contoso ->**タブです。  
  
    1.  **識別子**ページで、**インターチェンジの設定**セクションで、修飾子と識別子のフィールドの値を入力 (**ISA5**、 **ISA6**、 **ISA7**、および**ISA8**) テスト メッセージのヘッダー フィールドの値に対応します。  
  
        > [!NOTE]
        >  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、アグリーメントの解決を実行するために、送信者と受信者の修飾子フィールドおよび ID フィールドを必ず指定する必要があります。 値と照合**ISA5**、 **ISA6**、 **ISA7**、および**ISA8**とアグリーメントのプロパティで、インターチェンジ ヘッダーです。 また、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は、送信者の修飾子および識別子を照合して (受信者の修飾子および識別子は不要)、アグリーメントを解決します。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、アグリーメントを解決できない場合、フォールバック アグリーメントのプロパティが使用されます。  
  
        > [!NOTE]
        >  このチュートリアルでは、次のように設定します**ISA5**に**ZZ**、 **ISA6**に**7654321**、 **ISA7**に**ZZ。**、および**ISA8**に**1234567**です。  
  
    2.  **検証**ページで、、**インターチェンジの設定**セクションで、確認してください**重複している isa13 を確認**オプションがオフになっています。  
  
        > [!NOTE]
        >  オフにすると、**重複している isa13 を確認して**プロパティでは、同じメッセージの複数のインスタンスを受信することができます。  
  
    3.  使用するかどうかに付属する標準スキーマのいずれかの[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]の**ローカル ホストの設定**ページで、**トランザクション セットの設定**セクションで、選択するために使用するスキーマの名前空間受信インターチェンジを処理します。  
  
        |プロパティ|目的|  
        |--------------|----------------|  
        |**[Default]**|列のチェック ボックスをオンにします|  
        |**Target Namespace**|[ `http://schemas.microsoft.com/BizTalk/EDI/X12/2006`] を選択します。|  
  
        > [!NOTE]
        >  プロパティを設定すると、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は、受信 850 インターチェンジの処理に使用するスキーマを決定できるようになります。 グリッド内の行に入力された [GS02] と [ST01] の値がインターチェンジに設定されている場合は、同じ行にあるターゲットの名前空間により、使用するスキーマが決定されます。  
  
    4.  **エンベロープ**ページで、**トランザクション セットの設定**セクションで、次の操作します。  
  
        |プロパティ|目的|  
        |--------------|----------------|  
        |**[Default]**|選択**既定**です。 **注:** 、既定の値は、この行を選択すると**GS1**、 **GS2**、 **GS3**、 **GS7**、および**GS8**が使用される場合でもの値は、**トランザクションの種類**、**バージョン/リリース**、および**ターゲットの名前空間**の一致するものではありません、メッセージ。|  
        |**トランザクションの種類**|たとえば、テスト メッセージのメッセージの種類を選択**864 – テキスト メッセージ**です。|  
        |**バージョン/リリース**|入力**00401**です。|  
        |**ターゲットの名前空間**|選択**http://schemas.microsoft.com/BizTalk/EDI/X12/2006**です。|  
        |**GS1**|テスト メッセージのメッセージの種類が選択されているなどを確認してください。 **TX - テキスト メッセージ (864)**です。|  
        |**[GS2]**|入力**01**です。|  
        |**[GS3]**|入力**7654321**です。|  
        |**GS4**|日付の形式を選択します。 選択**CCYYMMDD**です。 **注:**ドロップダウン リストで、値を選択し、だけでなく、既定値を表示するフィールドをクリックする必要があります。 ドロップダウン リストから値を選択せずにフィールドをクリックしても、値は実際に選択されません。|  
        |**GS5**|時刻の形式を選択します。 選択**HHMMSSdd**です。|  
        |**GS7**|選択**T - 運輸データ調整委員会 (TDCC)**です。|  
        |**GS8**|EDI のバージョンとして入力されたことを確認してください。 **00401**です。|  
  
8.  次のタスクを実行、 **Contoso が Fabrikam ->**タブです。  
  
    > [!NOTE]
    >  このチュートリアルでは、必要な値をタブに指定し、アグリーメントを正常に作成できるようにします。 アグリーメントを正常に作成する両方の一方向アグリーメント タブの値に対して定義されている必要があります**ISA5**、 **ISA6**、 **ISA7**、および**ISA8**です。  
  
    1.  **識別子**ページで、**インターチェンジの設定**セクションで、修飾子と識別子のフィールドの値を入力 (**ISA5**、 **ISA6**、 **ISA7**、および**ISA8**) テスト メッセージのヘッダー フィールドの値に対応します。  
  
        > [!NOTE]
        >  このチュートリアルでは、次のように設定します**ISA5**に**ZZ**、 **ISA6**に**1234567**、 **ISA7**に**ZZ。**、および**ISA8**に**7654321**です。  
  
9. **[適用]**をクリックします。  
  
10. **[OK]**をクリックします。 新しく追加したアグリーメントが一覧表示、**契約**のセクションで、**パーティとビジネス プロファイル**ウィンドウです。 新しく追加したアグリーメントは既定で有効になります。  
  
### <a name="testing-the-walkthrough"></a>チュートリアルのテスト  
 ここでは、チュートリアルをテストする方法について説明します。  
  
##### <a name="to-test-the-solution"></a>ソリューションをテストするには、次の操作を行います。  
  
1.  [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] で、[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\AS2 Tutorial\Sender フォルダーにある Sender.csproj プロジェクトを開きます。  
  
2.  HttpSender.cs で、次の行がコメント アウトされていないことを確認します (//Request Asynchronous MDN コメント行のすぐ下)。  
  
    ```  
    Stream sr = new FileStream(getBizTalkInstallPath() + @"SDK\AS2 Tutorial\X12_00401_864.edi", FileMode.Open, FileAccess.Read);  
    ```  
  
3.  次の行がコメント アウトされていることを確認します (//Request Synchronous MDN コメント行のすぐ下)。  
  
    ```  
    Stream sr = new FileStream(getBizTalkInstallPath() + @"SDK\AS2 Tutorial\X12_00401_864-Sync.edi", FileMode.Open, FileAccess.Read);  
    ```  
  
4.  このプロジェクトをビルドします。  
  
5.  Windows エクスプローラーで、[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\AS2 Tutorial に移動します。 メモ帳で X12_00401_864.edi を開きます。 Disposition-Notification-Options ヘッダーを定義している行を削除し、ファイルを保存します。  
  
6.  Windows エクスプローラで、移動[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]sdk \as2 tutorial \sender\bin\debug 実行と**Sender.exe**です。  
  
    > [!NOTE]
    >  このインスタンスで Sender.exe を実行すると、メッセージ X12_00401_864.edi が Contoso 仮想ディレクトリ (BTS http 受信場所) に送信されます。  
  
7.  作成した Contoso ローカル フォルダーを開き、EDI ペイロードを (\EDI_to_Contoso) に送信します。 フォルダーに .XML ファイルがあることを確認します。 XML ファイルを開き、そのファイルに 864 トランザクション セットが含まれていることを確認します。  
  
8.  Fabrikam ローカル フォルダーを開きます。MDN はここに返されます。 Windows エクスプローラで、移動[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]sdk \as2 Tutorial\\_MDNToFabrikam です。 メモ帳でメッセージ ファイルを開き、MDN を確認します。 MDN AS2-From が Contoso で、AS2-To が Fabrikam であることを確認します。  
  
9. メモ帳でテスト メッセージ X12_00401_864.edi を開き、\EDI_to_Contoso ローカル フォルダー内の出力メッセージのトランザクション セットが、X12_00401_864.edi 入力メッセージのトランザクション セットに対応していることを確認します。  
  
## <a name="see-also"></a>参照  
 [開発と BizTalk Server AS2 ソリューションの構成](../core/developing-and-configuring-biztalk-server-as2-solutions.md)