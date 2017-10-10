---
title: "BTARN 送信パイプライン |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML Assembler
- send pipelines, message flow
- DOCTYPE headers
- MIME/SMIME Encoder
- send pipelines, BTARN
- BTARN, send pipelines
- XML Preprocessor
- messages, message flow
ms.assetid: 88562132-0ea4-4b5a-9445-b69f6c84e5ea
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8bd102c58f85fd38c2f769f6e4aca2b5fd0d7919
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="btarn-send-pipeline"></a>BTARN 送信パイプライン
[!INCLUDE[btsCoName](../../includes/btsconame-md.md)][!INCLUDE[BTARN_CurrentVersion_FirstRef](../../includes/btarn-currentversion-firstref-md.md)] RNIFSend パイプライン (RNIFSend.btp) で転送するための RosettaNet Implementation Framework (RNIF) メッセージを作成します。 送信パイプラインには、次のものが組み込まれています。  
  
-   XML プリプロセッサ  
  
-   XML アセンブラー  
  
-   MIME/SMIME (Multipurpose Internet Mail Extensions/SecureMultipurpose Internet Mail Extensions) エンコーダー  
  
## <a name="xml-preprocessor"></a>XML プリプロセッサ  
 XML プリプロセッサは、メッセージに DOCTYPE ヘッダーを追加します。 このヘッダーは、メッセージに関連付けるドキュメント型定義 (DTD) スキーマを指定します。 RNIF 仕様には、RNIF 送信のための DOCTYPE ヘッダーが必要です。  
  
## <a name="xml-assembler"></a>XML アセンブラー  
 XML アセンブラは、[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)] XML アセンブラに基づいています。 XML アセンブラーは、メッセージ コンテキストからエンベロープとドキュメントにプロパティを転送します。 そして、XML 部分および添付ファイルからメッセージを構築します。 メッセージの検証は実行しません。  
  
 ネイティブの [!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] XML アセンブラの詳細については、[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)] ヘルプ の「XML 逆アセンブル パイプライン コンポーネント」を参照してください。  
  
## <a name="mimesmime-encoder"></a>MIME/SMIME エンコーダ  
 MIME/SMIME エンコーダは、[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)] MIME/SMIME エンコーダに基づいています。 [!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)] エンコーダは、取引先アグリーメントのプロトコル設定および [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] MIME/SMIME エンコーダの設定に基づいて、次の操作を実行します。  
  
-   RNIF 1.1 メッセージに必要な 8 バイトのバイナリ ヘッダーをメッセージに追加します。  
  
-   メッセージ部分をエンコードし、ダイジェストを計算します。  
  
-   ペイロード (Service Content と添付ファイル) またはペイロード コンテナー (Service Content、Service Header、および添付ファイル) を暗号化します。 設定した場合、**すべてのポートをエンコード**の設定、**プロトコル**を取引先アグリーメントのタブ`False`、エンコーダはペイロードのみを暗号化します。 設定した場合、**すべてのポートをエンコード**設定`True`、エンコーダはペイロード コンテナーを暗号化します。  
  
 ネイティブの [!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] MIME/SMIME エンコーダの詳細については、[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)] ヘルプの「MIME/SMIME エンコーダ パイプライン コンポーネント」を参照してください。  
  
## <a name="message-flow"></a>メッセージ フロー  
 [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] 送信パイプラインを経由するメッセージ フローは次のとおりです。  
  
1.  設定した場合、**すべての部分のエンコード**を取引先アグリーメントの設定`True`、MIME/SMIME エンコーダはすべてのメッセージ部分をエンコードします。 アグリーメントの `Encoding` プロパティに設定されているエンコード方式が使用されます。  
  
2.  RNIF 2.01 では、メッセージがアクション メッセージで添付ファイルがある場合、エンコーダーは各添付ファイルに対して次の処理を実行します。  
  
    1.  添付ファイルがバイナリの場合は、エンコーダーがエンコードします。  
  
    2.  エンコーダーは、添付ファイルのコンテンツ ID を生成します。  
  
    3.  エンコーダーは、添付ファイルの MIME 部分を作成します。  
  
3.  RNIF 2.01 で、パイプラインはメッセージ部分を暗号化し、設定に応じて RNIF メッセージを作成する**永続的な機密性の必要性が**(として、プロセス構成設定で設定)。  
  
    1.  設定した場合**永続的な機密性の必要性が**に**ペイロード**エンコーダーは service content と添付ファイルを暗号化します。 次に、アセンブラーは Service Header、Delivery Header、および Preamble を追加して RNIF メッセージを完成します。  
  
    2.  設定した場合**永続的な機密性の必要性が**に**ペイロード コンテナー**エンコーダーは service header、service content と添付ファイルを暗号化します。 次に、アセンブラーは Delivery Header と Preamble を追加して RNIF メッセージを完成します。  
  
    3.  設定した場合**永続的な機密性の必要性が**に**None**アセンブラーは service content と添付ファイルを (なしに、service header、delivery header、および preamble が追加されます暗号化) をクリックし、最後の RNIF メッセージを構築するためにします。  
  
4.  RNIF 1.1 では、アセンブラーは暗号化せずに RNIF メッセージを完成します。  
  
5.  次の場合、エンコーダーはメッセージに署名します。  
  
    1.  メッセージがシグナル メッセージでは、および**否認不可のために必要な**プロパティ、プロセス構成設定が`True`です。  
  
    2.  メッセージがアクション メッセージでは、および**発信元とコンテンツの否認**プロパティ、プロセス構成設定が`True`です。  
  
6.  RNIF 2.01 では、エンコーダーは MIME メッセージの最初の本文部分のダイジェストを計算して、保持します。 エンコーダーは取引先アグリーメント (SHA-1 または MD5) の `Digest` メソッド プロパティのメソッド セットを使用してダイジェストを計算します。  
  
## <a name="see-also"></a>参照  
 [BTARN でのメッセージ処理](../../adapters-and-accelerators/accelerator-rosettanet/message-processing-in-btarn.md)