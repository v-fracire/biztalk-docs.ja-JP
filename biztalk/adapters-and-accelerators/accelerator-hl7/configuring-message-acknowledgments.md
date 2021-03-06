---
title: メッセージの受信確認の構成 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- acknowledgements, configuring
- messages, acknowledgements
- configuring, acknowledgements
ms.assetid: 6ebcfc32-0a0b-4388-938f-6569a2014b91
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 339e80776dac32e25f96da5c62675f1a8d6075ee
ms.sourcegitcommit: 5abd0ed3f9e4858ffaaec5481bfa8878595e95f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2017
ms.locfileid: "25962576"
---
# <a name="configuring-message-acknowledgments"></a>メッセージの受信確認を構成します。
使用する、[!INCLUDE[HL7_CurrentVersion_FirstRef](../../includes/hl7-currentversion-firstref-md.md)]構成エクスプ ローラー**受信確認**タブを受信し、生成された受信確認の受信確認プロパティを指定します。  
  
 次の図に示しています、[!INCLUDE[btaBTAHL71.3abbrevnonumber](../../includes/btabtahl71-3abbrevnonumber-md.md)]構成エクスプ ローラー**受信確認**タブです。  
  
 ![](../../adapters-and-accelerators/accelerator-hl7/media/hl7-ops-ack.gif "hl7_ops_ack")  
  
 開くには、次の手順を使用して[!INCLUDE[btaBTAHL71.3abbrevnonumber](../../includes/btabtahl71-3abbrevnonumber-md.md)]エクスプ ローラーの構成とメッセージの受信確認を構成します。  
  
### <a name="to-open-btahl7-configuration-explorer"></a>BTAHL7 構成エクスプ ローラーを開く  
  
-   をクリックして**開始**、 をポイント**プログラム**、 をポイント**Microsoft BizTalk\<バージョン\>Accelerator 用 HL7**、クリックして**BTAHL7 構成エクスプ ローラー**です。  
  
### <a name="to-configure-message-acknowledgments"></a>メッセージの受信確認を構成するには  
  
1.  BTAHL7 構成エクスプ ローラーで、上、**パーティ** タブで、構成するパーティを選択し、**受信確認** タブで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**受信確認の種類**|次のオプションから選択します。<br /><br /> -   **None**。 受信確認を構成したくない場合は、このオプションを選択します。<br />-   **OriginalMode**です。 構成するのには、このオプションを選択**MSH1 – フィールド区切り文字**、 **MSH2 – 文字のエンコード**、および**MSH8 – セキュリティ**オプションのみです。<br />-   **EnhancedMode**です。 すべての受信確認の使用可能なオプションを構成するには、このオプションを選択します。<br />-   **DeferredMode**です。 構成するのには、このオプションを選択**MSH1 – フィールド区切り文字**、 **MSH2 – 文字のエンコード**、および**MSH8 – セキュリティ**オプションのみです。<br />-   **StaticMode**です。 構成するのには、このオプションを選択、**成功**と**エラー発生時に**受信確認のオプションです。|  
    |**MSH 15 は、受信確認の種類をそのまま使用します。**|次のオプションから選択します。<br /><br /> -   **AL**です。 常に送信する場合、このオプションを選択して受信確認をそのまま使用します。<br />-   **NE**です。 送信しない場合は、このオプションを選択受信確認をそのまま使用します。<br />-   **SU**です。 送信する場合は、このオプションを選択して、メッセージの転送が成功した後に受信確認をそのまま使用します。<br />-   **ER**です。 送信する場合は、このオプションを選択して、エラーが発生した場合のみ肯定応答をそのまま使用します。|  
    |**MSH 16 アプリケーションの受信確認の種類**|次のオプションから選択します。<br /><br /> -   **AL**です。 常にアプリケーションの受信確認を送信する場合は、このオプションを選択します。<br />-   **NE**です。 アプリケーションの受信確認を送信しない場合は、このオプションを選択します。<br />-   **SU**です。 メッセージの転送が成功した後にアプリケーションの受信確認を送信する場合は、このオプションを選択します。<br /><br /> **ER**。 エラーが発生した場合のみアプリケーションの受信確認を送信する場合は、このオプションを選択します。|  
    |**MSH1 – フィールド区切り文字**|フィールドの区切り記号としては、一意の文字を入力します。 既定値は、パイプ文字 (**& #124;**)、最大文字数は 1 つの文字とします。 MSH1 を変更する必要がある場合、使用することする必要があります、HL7 メッセージ コンテキストに MSH1 の適切な値の書き込みを行うオーケストレーションに注意してください。 BTAHL7 シリアライザーでは、コンテキストから値を読み取るし、シリアル化されたメッセージで使用します。|  
    |**MSH2-エンコードの文字**|HL7 標準に従ってエンコードの文字として一意の文字を入力します。 既定のエンコードの文字は、^、~、 \\、および (& a)。 必要な最小文字は、2 つの文字、最大 4 文字です。 場合 MSH2_3 または MSH2_4 (エスケープおよびサブコンポーネント動的区切り記号) が指定されていない、元のメッセージの ACK メッセージが自動的にそれらのフィールドを入力します。 たとえば、元のメッセージ MSH セグメントは`MSH&#124;^~&#124;`のみ、コンポーネントおよび繰り返し区切り記号が指定されたは、ACK メッセージと 3 番目と 4 番目のコンポーネントを含めるには、そのフィールドを自動的に設定し、場所、`MSH&#124;^~\&`これら値は、BTAHL7 構成エクスプ ローラーで受信確認のセクションで構成されていません。|  
    |**MSH 3**|送信元アプリケーションに対し、生成された確認のフィールドの値を入力します。 最大長は 180 文字総称です。<br /><br /> 構成されていないときに生成された受信確認を含む受信**MSH5**メッセージの値。 **注:** 2.X メッセージには、このオプションがのみ適用されます。 **注:** を null には、既存の値を変更するには、入力 **\\**です。|  
    |**MSH 5**|コピー先のアプリケーションに対し、生成された確認のフィールドの値を入力します。 最大長は 180 文字総称です。<br /><br /> 構成されていないときに生成された受信確認を含む受信**MSH3**メッセージの値。 **注:** 2.X メッセージには、このオプションがのみ適用されます。 **注:** を null には、既存の値を変更するには、入力 **\\**です。|  
    |**MSH8 – セキュリティ**|省略可能なセキュリティ文字を入力します。|  
    |**MSH 9**|生成された受信確認メッセージの種類のフィールド値を入力します。<br /><br /> 構成されていないときに生成された受信確認を含む受信**MSH9**メッセージの値。 **注:** 2.X メッセージには、このオプションがのみ適用されます。 **注:** を null には、既存の値を変更するには、入力 **\\**です。|  
    |**MSH15 – 受信確認の種類を受け入れる**|Accept 受信確認の種類の次のオプションから選択します。<br /><br /> -   **AL**です。 常に送信する場合、このオプションを選択して受信確認をそのまま使用します。<br />-   **NE**です。 送信しない場合は、このオプションを選択受信確認をそのまま使用します。<br />-   **SU**です。 送信する場合は、このオプションを選択して、メッセージの転送が成功した後に受信確認をそのまま使用します。<br />-   **ER**です。 送信する場合は、このオプションを選択して、エラーが発生した場合のみ肯定応答をそのまま使用します。|  
    |**成功した場合**|成功のメッセージ配信の受信確認の静的テキストを入力します。|  
    |**エラー発生時に**|失敗したメッセージ配信の受信確認の静的テキストを入力します。|  
    |**要求-応答で送信パイプラインに確認をルーティングする送信ポート**|ソース LOB アプリケーションに、同期の確認メッセージを送信するには、このオプションを選択します。 このオプションは、送信請求-応答送信ポートでのみ使用できます。<br /><br /> このオプションが選択されていない場合、受信パイプラインは、受信確認の設定に基づき、ACK メッセージを生成します。|  
  
2.  **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [確認の構成の設定](../../adapters-and-accelerators/accelerator-hl7/ack-configuration-settings.md)   
 [確認の設定](../../adapters-and-accelerators/accelerator-hl7/acknowledgment-settings.md)   
 [受信確認の作成と処理](../../adapters-and-accelerators/accelerator-hl7/creating-and-processing-acknowledgments.md)