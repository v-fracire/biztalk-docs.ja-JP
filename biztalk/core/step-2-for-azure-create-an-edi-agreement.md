---
title: '(Azure) の手順 2: EDI アグリーメントを作成 |Microsoft ドキュメント'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a8003697-4955-45c0-ba0b-e7c293a050a2
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: bc2db7361aef663c70c7227febfea5fc08dc699a
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22280074"
---
# <a name="step-2-for-azure-create-an-edi-agreement"></a>EDI アグリーメントを作成する (Azure) の手順 2。
このトピックでは、[!INCLUDE[appfabricintegration](../includes/appfabricintegration-md.md)] の一部として利用できる Azure BizTalk ポータルを使用してパートナーを作成します。 また、2 つのパートナー (Northwind と Contoso) 間のアグリーメントも作成し、Contoso により Northwind に送信される X12 販売注文メッセージを処理します。  
  
### <a name="to-create-partners"></a>パートナーを作成するには  
  
1.  Microsoft アカウントを使用して、ポータルにログインに[http://go.microsoft.com/fwlink/p/?LinkId=235056](http://go.microsoft.com/fwlink/p/?LinkId=235056)です。  
  
2.  Northwind のパートナーを作成します。 手順に従う[パートナーとプロファイル](http://msdn.microsoft.com/library/windowsazure/hh689791)にパートナーを作成します。  
  
    > [!IMPORTANT]
    >  このパートナーを管理対象のパートナーとしてマークします。  
  
3.  手順を繰り返して Contoso のパートナーを作成します。 ***そうしない***このパートナー管理対象のパートナーとしてマークします。  
  
### <a name="to-create-an-agreement"></a>アグリーメントを作成するには  
  
1.  ポータルのホーム ページで、をクリックして**契約**です。  
  
2.  **契約** ページで、をクリックして、 **X12**いない場合は既にそのタブをタブです。をクリックして**アグリーメントの作成**です。  
  
3.  **新しいアグリーメント** ページで、次の詳細を入力します。  
  
    |||  
    |-|-|  
    |**フィールド**|**Description**|  
    |名前|アグリーメントの名前を入力します。 このチュートリアルでは、名前を指定、として`DemoAgreement`です。<br /><br /> **注:** これは必須フィールドです。 アグリーメントの名前は一意にする必要があります。|  
    |Description|アグリーメントのメモまたは説明を入力します。|  
    |パートナー 1 プロファイル (管理対象)|アグリーメントの管理対象のパートナーを選択します。 管理対象のパートナーはサービス プロバイダーにより管理されるパートナーで、アグリーメントの展開時にはそのパートナーにパイプラインが展開されます。 通常、サービス プロバイダーにより管理されるパートナーは管理対象のパートナーとして構成されますが、エンタープライズ パートナーは管理対象のパートナーとしてはマークされません。<br /><br /> **注:** このチュートリアルでは、管理対象のパートナーは**Northwind**です。<br /><br /> **注:** プロファイル フィールドで、既定のプロファイルが表示されます。 パートナー用に構成された、該当するプロファイルを選択します。|  
    |パートナー 2 プロファイル|アグリーメントの (管理対象のパートナーではない) パートナーを選択します。<br /><br /> **注:** プロファイル フィールドで、既定のプロファイルが表示されます。 パートナー用に構成された、該当するプロファイルを選択します。|  
  
     **Id**  
  
    |**フィールド**|**Description**|  
    |---------------|---------------------|  
    |パートナー 1 ID 修飾子|取引先に一意のビジネス ID を提供する認証修飾子を選択します。 このチュートリアルでは、次のように選択します。 **ZZ-相互定義**です。|  
    |値|入力`Northwind`です。|  
    |パートナー 2 の ID 修飾子|取引先に一意のビジネス ID を提供する認証修飾子を選択します。 このチュートリアルでは、次のように選択します。 **ZZ-相互定義**です。|  
    |値|入力`Contoso`です。|  
  
     **追跡**  
  
    |**フィールド**|**Description**|  
    |---------------|---------------------|  
    |送信側メッセージのプロパティを追跡する|EDI メッセージがパートナーに送信される場合にメッセージのプロパティを格納するには、これをオンにします。 クリックしてこのデータを照会して保存されると、**追跡**左側のウィンドウで、Azure BizTalk Portal からです。<br /><br /> チェックして、メッセージ本文を格納できますも有効にすると、**トラックの送信側メッセージ本文**です。|  
    |受信側メッセージのプロパティを追跡する|パートナーから EDI メッセージを受信する場合にメッセージのプロパティを格納するには、これをオンにします。 クリックしてこのデータを照会して保存されると、**追跡**左側のウィンドウで、Azure BizTalk Portal からです。<br /><br /> チェックして、メッセージ本文を格納できますも有効にすると、**トラックの受信側メッセージ本文**です。|  
  
4.  **[続行]** をクリックします。  
  
     クリックすると**続行**2 つの新しいタブが追加の 1 つの受信設定および他の送信設定用です。 各タブは、2 つのパートナー間の一方向のアグリーメント用で、メッセージの受信用と送信用があります。  
  
5.  受信の設定を指定します。  
  
    1.  **トランスポート** ページで、設定、**トランスポートの種類**を HTTP にします。  
  
         **エンドポイント**フィールドは、X12 に送信する必要がある Contoso URL が表示販売注文メッセージです。  
  
    2.  **プロトコル** ページで、次の値を指定します。  
  
        1.  必要である場合、ISA1、ISA2、ISA3、および ISA4 の値を指定します。  
  
        2.  **受信確認** **TA1 が必要**と**997 が必要です**を受信するための応答で技術確認と機能確認を生成する場合、メッセージ。  
  
        3.  **スキーマ**をクリックして、**アップロード**ボタンをクリックし、アップロード、 **X12 840 スキーマ**(からダウンロードした[http://go.microsoft.com/fwlink/p/?LinkId = 235057](http://go.microsoft.com/fwlink/p/?LinkId=235057)) および**SalesOrder**スキーマ (で作成した[EDI プロジェクト内のスキーマを作成する](../core/step-1-for-azure-create-the-edi-project.md#BKMK_CreateSchema))。  
  
             次のプロパティを設定、**スキーマ**セクションです。  
  
            |||  
            |-|-|  
            |バージョン|00401|  
            |トランザクションの種類 (ST1)|840|  
            |スキーマ|/X12_00401_840.xsd|  
  
    3.  **変換**で作成した変換のアップロード ページで、 [EDI プロジェクト内の変換を作成する](../core/step-1-for-azure-create-the-edi-project.md#BKMK_CreateTrfm)です。  
  
         **このアグリーメントの一部として実行するマップを選択**、選択 **/X12_00401_840.xsd**の**スキーマ**と **/EDI840TOSALESORDER です。TRFM**の**変換ファイル名**です。  
  
    4.  **ルート**] ページで、[ **Service Bus キューへのルート**し、メッセージは送信キューの相対アドレスを指定します。 このチュートリアルでは、指定の相対アドレスとして`queueordersedi`完全な URL が実行されるよう`https://<namespace>.servicebus.appfabriclabs.com/queueordersedi`です。  
  
        > [!NOTE]
        >  このチュートリアルでは、エラー メッセージが、[メッセージ保留の設定] で指定したエンドポイントに送信されるシナリオについては説明しません。 ただし、アグリーメントの展開を成功させるには、この設定に値を指定する必要があります。 空ではない値を入力できます。  
  
6.  送信の設定を指定します。  
  
    > [!NOTE]
    >  このチュートリアルで説明するシナリオの場合、アグリーメントに送信側の構成は必要ありません。 ただし、送信の設定を指定しないと、設定がダミーの値であっても、アグリーメントを展開できません。 また、[、**送信の設定**] タブで、ダミーの値を指定する必要がない**受信 URI**、**変換**と**バッチ処理**です。  
  
    1.  **プロトコル**] ページの [**スキーマ**をクリックして、**アップロード**ボタンをクリックし、X12 のスキーマをアップロード 840 メッセージ。  
  
         設定、**バージョン**に**00401**、**トランザクション タイプ**に**840**、および**スキーマ**に**X12_00401_840**です。  
  
    2.  **トランスポート** ページで、パートナーへの応答メッセージまたは受信確認を送信する先のエンドポイントを指定します。 正常に処理されたメッセージだけでなく、処理中のエラーにより保留になったメッセージにも、エンドポイントを指定する必要があります。  
  
7.  をクリックして**アグリーメントの展開**アグリーメントをデプロイします。 表示された URL で、アグリーメントがデプロイされるようになりました、**トランスポート**のページ、**受信の設定**タブです。  
  
## <a name="see-also"></a>参照  
 [チュートリアル 4: BizTalk Server 2013 を使用するハイブリッド アプリケーションを作成します。](../core/tutorial-4-creating-a-hybrid-application-using-biztalk-server-2013.md)