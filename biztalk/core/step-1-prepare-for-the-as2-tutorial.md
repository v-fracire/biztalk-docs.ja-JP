---
title: '手順 1: AS2 チュートリアルの準備 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3421c33b-0ccd-4e9d-b1c3-b161278e4d98
caps.latest.revision: 39
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6f394df645774752993064676345a371eb3135a0
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37003675"
---
# <a name="step-1-prepare-for-the-as2-tutorial"></a>手順 1: AS2 チュートリアルを準備します。
![手順 11 の 1](../core/media/tut-step1-of-11.gif "Tut_Step1_of_11")  
  
 AS2 チュートリアルは 1 台のコンピューター上で実行されます。 チュートリアルを準備するには、インストールして構成する必要があります[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]」の説明に従って[BizTalk Server 2013 および 2013 R2 のインストールの概要](http://msdn.microsoft.com/library/8041926c-cfc9-4eaf-9c28-a2c6e8015bc5)セクション。 また、このトピックの説明に従って、BizTalk Server EDI アプリケーションへの参照を追加する必要があります。 AS2 チュートリアルに必要なファイルは、[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\AS2 Tutorial フォルダーにあります。  
  
> [!NOTE]
>  このチュートリアルが機能するためには、インプロセス ホスト インスタンスと分離ホスト インスタンスの両方に同じログオン アカウントを使用する必要があります。  
  
> [!NOTE]
>  このチュートリアルが機能するためには、このチュートリアルで使用する BizTalk Server ホストが 32 ビットとマークされている必要があります。  
  
> [!NOTE]
>  このチュートリアルが機能するためには、IIS 7.0 または IIS 7.5 を使用するプラットフォームで実行し、アプリケーション プールの [32 ビット アプリケーションの有効化] を [True] に設定する必要があります。  
  
 AS2 チュートリアル フォルダーには、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] がテスト出力ファイルを書き込む 3 つのフォルダー (EDI payload、997、および MDN) があります。 これらのフォルダーは既に作成されていますが、997 フォルダーと MDN フォルダーのセキュリティ権限を設定する必要があります (次の手順を参照)。  
  
 チュートリアルに必要なフォルダーおよびファイルは次のとおりです。  
  
|そのフォルダー \ ファイル|用途|  
|------------------|-------------|  
|\\_ 997tofabrikam|この空のフォルダーは、EDI 処理後に返される 997 確認メッセージを受信します。 Fabrikam パーティで EDI メッセージを発信するアプリケーションをシミュレートします。|  
|\\_EDIXMLToContoso|この空のフォルダーは、BizTalk Server が EDI メッセージを処理した後 XML ペイロード ファイルを受信します。 EDI ペイロードの最終送信先である基幹業務アプリケーションをシミュレートします。|  
|\\_MDNToFabrikam|この空のフォルダーは、AS2 処理後に BizTalk Server から返される MDN メッセージを受信します。 Fabrikam パーティでアプリケーションをシミュレートします。|  
|\Fabrikam|このフォルダーには、997 を _997ToFabrikam フォルダーに保存し、MDN を _MDNToFabrikam フォルダーに保存する Default.aspx ファイルがあります。|  
|\Schemas|このフォルダーには、X12_00401_864.xsd スキーマ、および BizTalk で EDI メッセージの処理に使用されるその他のスキーマがあります。 スキーマを展開するためにビルドおよび展開する Schemas.btproj プロジェクトもあります。|  
|\Sender|このフォルダーには、Sender.exe を作成するためにビルドおよびコンパイルする Sender.csproj プロジェクトがあります。Sender.exe を使用して、(\AS2 Tutorial フォルダーにある) X12_00401_864.edi テスト メッセージを送信し、MDN を返します。|  
  
## <a name="prerequisites"></a>前提条件  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理者グループのメンバーとしてログオンしている必要があります。  
  
## <a name="procedures"></a>手順  
  
#### <a name="to-set-the-security-permission-for-the-997-and-mdn-folders"></a>997 フォルダーと MDN フォルダーのセキュリティ権限を設定するには  
  
1. Windows エクスプ ローラーで、移動、 [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]sdk \as2 Tutorial\\_ 997tofabrikam フォルダー。 右クリックし、 \\_ 997tofabrikam フォルダー をクリックし、**プロパティ**します。  
  
2. をクリックして、**セキュリティ**タブをクリックし、をクリックし、**編集**します。 **権限**ダイアログ ボックスで、をクリックして**追加**します。  
  
3. **ユーザー、コンピューター、サービス アカウント、またはグループ**ダイアログ ボックスで、オブジェクト名ペインで、入力`Everyone`、順にクリックします**OK**します。  
  
4. 選択**Everyone**で、**グループまたはユーザー名**ボックスに、チェック ボックスをクリックして**書き込み**(下、**許可**列)、で**アクセス許可**ペイン、およびクリック**OK**します。  
  
5. **[OK]** をクリックします。  
  
6. 次の手順を繰り返して、 \\_MDNToFabrikam フォルダー。  
  
#### <a name="to-mark-the-biztalk-server-host-as-32-bit"></a>BizTalk Server ホストを 32 ビットとしてマークするには  
  
1. > [!NOTE]
   >  AS2 パイプラインは、32 ビット プロセスでのみ使用できます。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] が 64 ビット版のオペレーティング システムにインストールされている場合は、以下の手順を実行してホスト プロセスを 32 ビット専用としてマークする必要があります。  
  
    選択**開始**を選択します**すべてのプログラム**を選択します**Microsoft BizTalk Server**、し、 **BizTalk Server 管理**します。  
  
2. コンソール ツリーで、展開**BizTalk Server 管理**を BizTalk グループを展開し、選択**プラットフォームの設定**、し、**ホスト**します。  
  
3. 詳細ペインで、このチュートリアルで使用し、選択するインプロセス ホストを右クリックして**プロパティ**します。  
  
4. **ホストのプロパティ**] ダイアログ ボックス [、**全般**] タブで、[ **32 ビットのみ**、順にクリックします**OK**。  
  
5. 分離ホストについて手順 3. ～ 4. を繰り返します。  
  
   BizTalk Server が 64 ビット版のオペレーティング システムにインストールされている場合は、32 ビットの BizTalk ホスト プロセスを使用するときに IIS も 32 ビット モードで実行されるように設定する必要があります。 IIS を設定するための手順の表示[手順 5: 取引先パートナーの Web ページの構成](../core/step-5-configure-the-trading-partner-web-pages.md)IIS では、32 ビット ワーカー プロセスを設定できるように、アプリケーション プールごと。  
  
#### <a name="to-add-reference-to-the-biztalk-edi-application"></a>BizTalk EDI アプリケーションへの参照を追加するには  
  
1. [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、、**アプリケーション**ノードで、BizTalk アプリケーション 1 などの edi で使用するアプリケーションを右クリックします。 をポイント**追加**、し、[参照] をクリックします。  
  
2. **アプリケーション参照の追加**ダイアログ ボックスで、 **BizTalk EDI アプリケーション**、 をクリックし、 **OK**。  
  
## <a name="next-steps"></a>次の手順  
 」の説明に従って、サンプル X12 スキーマを展開する[手順 2: 作成およびデプロイのサンプル X12 スキーマ](../core/step-2-create-and-deploy-the-sample-x12-schema.md)  
  
## <a name="see-also"></a>参照  
 [チュートリアル 3: AS2 チュートリアル](../core/tutorial-3-as2-tutorial.md)