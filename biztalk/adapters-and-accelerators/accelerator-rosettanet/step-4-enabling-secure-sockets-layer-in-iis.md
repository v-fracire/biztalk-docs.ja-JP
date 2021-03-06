---
title: '手順 4: セキュリティで保護を有効にする IIS のレイヤーをソケット |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Secure Socket Layers
- IIS
- double action tutorial, enabling SSL in IIS
- SSL
ms.assetid: 96109294-595a-46ac-974e-33123df79ed5
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: be53660b5632450d8fa8cb38480c9b728d460bad
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37009163"
---
# <a name="step-4-enabling-secure-sockets-layer-in-iis"></a>手順 4: IIS でレイヤーをソケット セキュリティで保護を有効にします。
SSL (Secure Sockets Layer) は、クライアントとサーバーとの間の通信チャネルをセキュリティで保護するためのプロトコルです。 Contoso 組織と Fabrikam 組織は、Microsoft® インターネット インフォメーション サービス (IIS) 7.5 または 7.0 で SSL を有効にすることにより、すべてのデータ転送に認証と暗号化を使用して通信を行います。 ここでは、IIS 7.5 または 7.0 で SSL を有効にする手順について学びます。  
  
> [!NOTE]
>  Contoso のコンピューターと Fabrikam のコンピューターの両方でこの手順を実行する必要があります。  
  
### <a name="to-prepare-a-new-server-certificate"></a>新しいサーバー証明書を準備するには  
  
1. クリックして**開始**、 をポイント**管理ツール**、順にクリックします**インターネット インフォメーション サービス (IIS) マネージャー**します。  
  
2. インターネット インフォメーション サービスの左側のウィンドウで  **\<** <em>computer_name</em> **\>** (*ローカル コンピューター*)、展開**Websites**を右クリックして**既定の Web サイト**、順にクリックします**プロパティ**します。  
  
3. 既定の Web サイト ダイアログ ボックスで、上、**ディレクトリ セキュリティ** タブで **サーバー証明書**を開始する、 **IIS 証明書ウィザード**。  
  
4. **Web サーバー証明書ウィザードへようこそ**] ページで [**次**します。  
  
5. **サーバー証明書**] ページで、[**新しい証明書を作成**、順にクリックします**次**します。  
  
6. **証明書の要求**] ページで [**次**します。  
  
7. **名およびセキュリティの設定**] ページで [ **[次へ]**、既定値を保持します。  
  
8. **組織情報**ページで、**組織**ボックスに「 **Contoso** Contoso のコンピューター上にある場合または**Fabrikam**上にある場合、Fabrikam のコンピューターで、**組織単位**ボックスに「**テスト**、順にクリックします**次**します。  
  
9. **サイトの一般名**] ページの [、**共通名**ボックスで、コンピューターの名前を入力し、クリックして **[次へ]** します。  
  
10. **地理情報**] ページの [、**都道府県**ボックスで、都道府県を入力、**市区町村**ボックスで、/地域、市区町村を入力し、順にクリックします**次**します。  
  
11. **証明書要求ファイル名**] ページの [、**ファイル名**ボックスで、既定値のままに**C:\certreq.txt**、順にクリックします**次**します。  
  
12. **要求ファイルの概要**] ページで [**次**します。  
  
13. **Web サーバー証明書ウィザードの完了**] ページで [**完了**を閉じる、 **IIS 証明書ウィザード**します。  
  
### <a name="to-generate-a-new-server-certificate"></a>新しいサーバー証明書を生成するには  
  
1.  Internet Explorer で、検索し、開きます http://\<*contoso_machine*\>/CertSrv します。  
  
    > [!NOTE]
    >  手順 1 で、開く http://\<*contoso_machine*\>/CertSrv Contoso または Fabrikam のコンピューターにします。  
  
2.  **Microsoft 証明書サービス ウィザードへようこそ**] ページで [**証明書を要求します。**  
  
3.  **証明書を要求**] ページで [**高度な証明書の要求**します。  
  
4.  **証明書要求の高度な**] ページで [ **base 64 エンコード CMC または PKCS #10 ファイルを使用して証明書の要求を送信するか、または base 64 エンコード PKCS #7 ファイルを使用して、更新要求を送信する**します。  
  
5.  **証明書の要求または更新要求を送信**] ページで [**ファイルを挿入する参照**します。  
  
    > [!NOTE]
    >  メモ帳または別のテキスト エディターでファイル C:\certreq.txt を開き、リンクをクリックすると、セキュリティ エラーが発生した場合、ファイルの内容をコピーおよびでその情報を貼り付けて、**保存された要求**ボックスをクリックして**送信**します。 これで、手順 10. に進めます。  
  
6.  をクリックして**参照**を開く、 **Choose File**  ダイアログ ボックス。  
  
7.  **ファイルの選択** ダイアログ ボックスで、検索、 *\<ドライブ\>*: \ フォルダー、certreq.txt ファイルを選択し、順にクリックします**オープン**します。  
  
8.  **証明書の要求または更新要求を送信**] ページで [**読み取り**します。  
  
9. **証明書の要求または更新要求を送信**] ページで [**送信**新しい証明書を生成します。  
  
10. **証明書は発行**] ページで [**証明書のダウンロード**します。  
  
11. **ファイルのダウンロード**ダイアログ ボックスで、をクリックして**保存**します。  
  
12. **付けて** ダイアログ ボックスで、証明書を保存\<ドライブ\>: \Certs\SSLCert.cer をクリック**保存**します。  
  
13. クリックして**閉じます**を閉じる、**ダウンロードの完了** ダイアログ ボックス。  
  
### <a name="to-prepare-a-new-server-certificate-for-iis"></a>IIS で新しいサーバー証明書を準備するには  
  
1.  クリックして**開始**、 をポイント**管理ツール**、順にクリックします**インターネット インフォメーション サービス (IIS) マネージャー**します。  
  
2.  インターネット インフォメーション サービスの左側のウィンドウで < computer_name > (ローカル コンピューター) をクリックして、ダブルクリック**サーバー証明書**右側のペインでします。 選択**証明書の要求の作成**操作 ウィンドウ。  
  
3.  識別名のプロパティ ダイアログ ボックスで、一般的な名前でコンピューターの名前を入力します組織内のテキスト ボックス: ボックスに「 **Contoso** Contoso のコンピューター上にある場合または**Fabrikam** Fabrikam 上にある場合。組織単位内のコンピューター: ボックスに「市区町村 ボックスで、テスト、都道府県ボックスに市区町村、、国/地域ドロップダウンを選択、国/地域都道府県を入力およびクリック**次へ**.  
  
4.  暗号化サービス プロバイダーのプロパティ] ダイアログ ボックスで、[**次**します。  
  
5.  ファイル名 ダイアログ ボックスで、テキスト ボックスで C:\certreq.txt を指定する をクリックして**完了**します。  
  
### <a name="to-generate-a-new-server-certificate-for-iis"></a>IIS で新しいサーバー証明書を生成するには  
  
1.  Internet Explorer を http://<contoso_machine>/CertSrv を開きます。  
  
    > [!NOTE]
    >  手順 1 で、Contoso または Fabrikam のコンピューター上の http://<contoso_machine>/CertSrv を開きます。  
  
2.  Microsoft 証明書サービス ウィザードへようこそ ページで、**証明書を要求**します。  
  
3.  要求の証明書 ページで、をクリックして**証明書の要求の高度な**します。  
  
4.  証明書要求の詳細設定 ページで、次のようにクリックします。**証明書の要求を送信**で base 64 エンコード CMC または PKCS #10 ファイルを使用して、または base 64 エンコード PKCS #7 ファイルを使用して、更新要求を送信します。  
  
5.  メモ帳または別のテキスト エディターでファイル C:\certreq.txt を開き、ファイルの内容をコピーおよび貼り付け、**保存された要求**ボックス証明書の要求または更新要求のページでは、送信、をクリックして**送信**します。  
  
6.  証明書の発行 ページで、**証明書のダウンロード**します。  
  
7.  ファイルのダウンロード] ダイアログ ボックスで、[**保存**します。  
  
8.  名前を付けて保存 ダイアログ ボックスで、保存する証明書を\<ドライブ\>: \Certs\SSLCert.cer をクリック**保存**します。  
  
### <a name="to-import-the-server-certificate-into-iis"></a>サーバー証明書を IIS にインポートするには  
  
1.  クリックして**開始**、 をポイント**管理ツール**、順にクリックします**インターネット インフォメーション サービス (IIS) マネージャー**します。  
  
2.  インターネット インフォメーション サービスの左側のウィンドウで次のようにクリックします。 **(ローカル コンピューター)**、ダブルクリック**サーバー証明書**右側のウィンドウでします。 選択**証明書要求の完全な**[操作] ウィンドウから。  
  
3.  証明機関の応答の指定 ダイアログ ボックスに「 **\<ドライブ\>: \Certs\SSLCert.cer**で**証明機関から応答を格納するファイル名**テキスト ボックス。 フレンドリ名テキスト ボックスに「 **ContosoSSLCert**します。  
  
### <a name="to-enable-ssl-bindings-for-iis"></a>IIS で SSL バインドを有効にするには  
  
1.  クリックして**開始**、 をポイント**管理ツール**、順にクリックします**インターネット インフォメーション サービス (IIS) マネージャー**します。  
  
2.  インターネット インフォメーション サービスの左側のウィンドウで  **(ローカル コンピューター)**、展開**サイト**、右クリックして**既定の Web サイト**、順にクリックします**編集バインド**します。  
  
3.  [サイト バインド] ダイアログ ボックス**追加**します。 サイト バインドの追加 ダイアログ ボックスで、次のように選択します**https**型ドロップダウンから、次のように選択します。 **ContosoSSLCert** SSL 証明書ドロップダウンから、次のようにクリックします。 **OK**、 をクリック**閉じる。**.  
  
### <a name="to-import-the-server-certificate-into-iis"></a>サーバー証明書を IIS にインポートするには  
  
1. クリックして**開始**、 をポイント**管理ツール**、順にクリックします**インターネット インフォメーション サービス (IIS) マネージャー**します。  
  
2. インターネット インフォメーション サービスの左側のウィンドウで [ **\<** <em>computer_name</em> \> (*ローカル コンピューター*)、展開**Webサイト**、右クリック**既定の Web サイト**、] をクリックし、**プロパティ**します。  
  
3. 既定の Web サイトのプロパティ ダイアログ ボックスで、**ディレクトリ セキュリティ** タブで **サーバー証明書**を開始する、 **IIS 証明書ウィザード**。  
  
4. **Web サーバー証明書ウィザードへようこそ**] ページで [**次**します。  
  
5. **保留中の証明書要求**] ページで、[**保留中の要求を処理し、証明書をインストール**、順にクリックします**次**します。  
  
6. **保留中の要求を処理**ページで、**パスとファイル名**ボックスに「 **\<ドライブ\>: \Certs\SSLCert.cer** (またはそのファイルを参照)クリックして**次**します。  
  
7. **SSL ポート ページ**、 をクリックして**次**します。  
  
8. **証明書の概要**] ページで [**次**します。  
  
9. **Web サーバー証明書ウィザードの完了**] ページで [**完了**します。  
  
## <a name="see-also"></a>参照  
 [Contoso ソリューションの作成と構成](../../adapters-and-accelerators/accelerator-rosettanet/creating-and-configuring-the-contoso-solution.md)