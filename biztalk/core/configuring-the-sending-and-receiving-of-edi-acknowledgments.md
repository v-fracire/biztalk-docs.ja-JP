---
title: "送信の構成と、EDI 受信確認の受信 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3db1c9f7-bafa-4659-a3c4-0faa56606081
caps.latest.revision: "16"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a88b7596772e951a835ffc13874ade7fefab5137
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="configuring-the-sending-and-receiving-of-edi-acknowledgments"></a>EDI 受信確認の送信と受信の構成
受信したインターチェンジへの応答としての EDI 受信確認の送信を構成するには、次の作業を行う必要があります。  
  
-   受信したインターチェンジを解決した結果となるアグリーメントの中で、受信確認を有効にします。 この設定を行うと、インターチェンジの送信元パーティが受信確認を待ち受けると宣言したことになります。  
  
-   受信確認を返すときに特定のプロパティ セットを指定する (CR LF を有効にする、区切り文字を変えるなど) 必要がある場合は、そのプロパティを他方の一方向アグリーメント タブで設定します。この設定を行うと、パーティからどのように受信確認を返すかを設定したことになります。  
  
    > [!NOTE]
    >  インターチェンジがで定義されているアグリーメントに解決される場合、**パーティ パーティ b->**   タブで、受信確認の生成方法に関連するプロパティで構成されている場合、**パーティ b には、パーティが->**   タブ。これが必要な受信確認コンテキスト プロパティで指定した値の逆に、送信者および受信者の修飾子を設定、**パーティ パーティ b->** タブです。たとえば、インターチェンジ メッセージが解決されたアグリーメントで送信者および受信者の識別子が THEM および US に設定されている場合、受信確認では送信者および受信者のコンテキスト プロパティは US および THEM に設定されます。 通常、他の一方向のアグリーメント タブでも、送信者および受信者の識別子はそれぞれ US および THEM に設定されます。 そのため、受信確認メッセージは、そのアグリーメントに従って解決され、プロパティの設定が取得されます。 別の要素の区切り記号 CR LF を使用する受信確認をするかどうかまたはを使用する受信確認がある場合は、のプロパティを指定するなど、**パーティ b には、パーティが]-> [**タブです。  
  
     概念的には、受信確認のプロパティを同じセンダを持つ任意の一方向アグリーメント タブから取得され、として受信者の修飾子は、受信確認のコンテキスト プロパティで設定します。 ただし、実際に使いやすいように、一般的には、インターチェンジの解決用に作成したアグリーメントのもう 1 つの一方向のアグリーメント タブでこの設定を行います。  
  
-   元のインターチェンジの送信元パーティに EDI 受信確認を返すパーティは、受信確認を取得して送信するための一方向送信ポートを設定するか、受信確認を送信するための双方向受信ポートを設定します。 詳細については、次を参照してください。 [EDI インターチェンジの送信および受信確認を静的な送信ポートを構成する](../core/configuring-a-static-send-port-to-send-edi-interchanges-and-acknowledgments.md)です。  
  
-   EDI 受信確認を待ち受けるパーティは、受信確認を受け取るための双方向送信ポートまたは一方向受信ポートを設定します。 詳細については、次を参照してください。 [EDI メッセージを受信および確認するためのポートを構成する](../core/configuring-a-port-to-receive-edi-messages-and-acknowledgments.md)です。  
  
-   BizTalk EDI アプリケーションには、管理スキーマが含まれています。 このため、EDI ソリューションを含むアプリケーションには、BizTalk EDI アプリケーションへの参照を含める必要があります。 詳細については、次を参照してください。[を BizTalk Server EDI アプリケーションへの参照を追加する方法](http://msdn.microsoft.com/library/7af066fb-372f-4709-b566-c8d6b4a9d782)です。  
  
## <a name="prerequisites"></a>前提条件  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理者グループまたは [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] B2B Operators グループのメンバーとしてログオンしている必要があります。  
  
### <a name="to-request-an-acknowledgment-for-the-party-that-sent-the-original-interchange"></a>元のインターチェンジの送信元パーティへの受信確認を要求するには  
  
1.  > [!NOTE]
    >  ここで説明する手順を実行すると、インターチェンジの送信元パーティが受信確認の返送を待ち受けていることを構成できます。  
  
     [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、をクリックして、**パーティ**ノード。 **パーティとビジネス プロファイル** ページで、アグリーメントの受信確認を有効にする必要のあるパーティをクリックします。 **アグリーメント**セクションで、ページのアグリーメントを右クリックし、をクリックして**プロパティ**です。 **アグリーメントのプロパティ**ダイアログ ボックスで、(受信インターチェンジを解決先) の一方向アグリーメント タブで、次の操作します。  
  
    1.  **識別子**送信者および受信者の値を入力してください ページで、修飾子です。  
  
         X12 でエンコードされた受信確認の場合は、ISA5、ISA6、ISA7、および ISA8 の値を入力します。 ISA5 および ISA6 には、インターチェンジの送信元パーティの値を入力します。 ISA7 および ISA8 には、インターチェンジを受信するパーティの値を入力します。  
  
         EDIFACT でエンコードされた受信確認の場合は、UNB2.1、UNB2.2、UNB3.1、および UNB3.2 の値を入力します。 UNB2.1 および UNB2.2 には、インターチェンジの送信元パーティの値を入力します。 UNB3.1 および UNB3.2 には、インターチェンジを受信するパーティの値を入力します。  
  
    2.  **受信確認** ページの プロパティ が必要ですが、送信側パーティの受信確認の種類を定義します。  
  
         X12 受信確認、選択**TA1 が必要**や**997 が必要**によっては、待ち受ける受信確認が必要です。 各受信確認の種類を選択**をバッチ処理しない\<ACK 型 >**を個別のインターチェンジとして送信する受信確認の各インスタンスの場合。  
  
         EDIFACT 受信確認、選択**メッセージの受信 (CONTRL が必要です)**や**確認 (CONTRL) が必要です**によっては、待ち受ける受信確認が必要です。 各受信確認の種類を選択**をバッチ処理しない\<ACK 型 >**を個別のインターチェンジとして送信する受信確認の各インスタンスの場合。  
  
    3.  **ローカル ホスト設定**ページで、**インターチェンジの設定** セクションで、クリア、**要求-応答で送信パイプラインに確認をルーティングの受信ポート**を返す、一方向の送信ポート経由で非同期的に受信確認します。 このプロパティをオンのままにすると、受信確認は同期的に、双方向受信ポートを介して返されます。  
  
    4.  **送信ポート**] ページの [、**名前**の列、**送信ポート**グリッドで、受信確認の送信を設定している送信ポートを選択します。  
  
        > [!NOTE]
        >  この送信ポート設定は、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] がメッセージを処理するときにどのパーティを使用するかを特定するために使用されます。 詳細については、次を参照してください。[アグリーメントの解決と送信 EDI メッセージのスキーマの決定](../core/agreement-resolution-and-schema-determination-for-outgoing-edi-messages.md)です。  
  
        > [!NOTE]
        >  送信ポートをまだ設定していない場合は、後でこの手順を実行する必要があります。  
  
### <a name="to-configure-how-the-party-sends-the-acknowledgement-back"></a>パーティが受信確認を返す方法を構成するには  
  
1.  > [!NOTE]
    >  ここで説明する手順を実行すると、インターチェンジを受信したパーティが受信確認をどのように返すかを構成することができます。  
  
     同じ**アグリーメントのプロパティ**ダイアログ ボックスで、その他の一方向アグリーメント タブで、次の操作します。  
  
    1.  **識別子**送信者および受信者の値を入力してください ページで、修飾子です。  
  
        > [!NOTE]
        >  受信確認を送信するときは、元のインターチェンジを受信したパーティが送信側になり、元のインターチェンジを送信したパーティが受信側になります。 したがって、ここで [識別子] ページに入力する値は、前の手順で一方向アグリーメント タブに入力した値の逆です。 これは、次の 2 つの目的を果たすためです。  
        >   
        >  -   返された受信確認を解決すると、現在作成している一方向アグリーメントとなります。これは、受信確認のコンテキスト プロパティで指定された送信者と受信者が、この手順で [識別子] ページに入力される送信者と受信者の値に一致するからです。  
        > -   受信確認をカスタマイズしたい場合は、このアグリーメント タブでカスタマイズを構成できます。たとえば、別の区切り文字を使用することや、CR LF を有効にすることが可能です。  
  
         X12 でエンコードされた受信確認の場合は、ISA5、ISA6、ISA7、および ISA8 の値を入力します。 ISA5 および ISA6 には、受信確認の送信元パーティ (元のインターチェンジを受信したパーティと同じです) の値を入力します。 ISA7 および ISA8 には、受信確認を受信するパーティ (元のインターチェンジの送信元パーティと同じです) の値を入力します。  
  
         EDIFACT でエンコードされた受信確認の場合は、UNB2.1、UNB2.2、UNB3.1、および UNB3.2 の値を入力します。 UNB2.1 および UNB2.2 には、受信確認の送信元パーティ (元のインターチェンジを受信したパーティと同じです) の値を入力します。 UNB3.1 および UNB3.2 には、受信確認を受信するパーティ (元のインターチェンジの送信元パーティと同じです) の値を入力します。  
  
    2.  X12 または EDIFACT 受信確認の場合に、必要な場合、**文字セットと区切り記号** ページで、受信確認で使用する区切り記号を指定します。 受信確認の中で CR LF サフィックスの使用を必須にするかどうかを指定することもできます。  
  
    3.  EDIFACT 受信確認の場合に、必要な場合、**エンベロープ**ページで、**インターチェンジの設定**セクションで、含めるを指定するかどうか、受信確認は、UNA または UNG セグメントを選択して、適切なオプションです。  
  
## <a name="see-also"></a>参照  
 [EDI 受信確認を構成します。](../core/configuring-edi-acknowledgments.md)   
 [EDI サービスと管理スキーマ](../core/edi-service-and-control-schemas.md)   
 [EDI 受信確認を送信します。](../core/sending-an-edi-acknowledgment.md)   
 [作成する方法、受信ポート](../core/how-to-create-a-receive-port.md)   
 [送信ポートを作成する方法](../core/how-to-create-a-send-port2.md)