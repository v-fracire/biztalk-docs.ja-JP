---
title: TestCrypto |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- messages, TestCrypto utility
- troubleshooting, TestCrypto utility
- TestCrypto utility
ms.assetid: 02768794-64ac-4d99-930c-738bed9626c5
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d6948d3883797369c98ad51683cbc59536b9d8fd
ms.sourcegitcommit: 436ebffd959a9c4bdaafd4da9a5843c59a018eb7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2018
ms.locfileid: "34855669"
---
# <a name="testcrypto"></a>TestCrypto
TestCrypto ユーティリティを使用して、メッセージの暗号化解除に関連するトラブルシューティングを行います。 このユーティリティは、暗号化の解除に失敗したかどうかを示します。 暗号化の解除が成功した場合は、証明書が何かが示され、暗号化が解除されたメッセージが表示されます。  
  
 メッセージの暗号化された部分だけを含むファイル (暗号化されていないヘッダーを除く) に対して TestCrypto を実行します。 受信メッセージをスニッフィングするか、`MessageStorageIn` からメッセージを取得して、メッセージの暗号化されたバイナリ ラージ オブジェクト (BLOB) をテキスト ファイルに抽出します。  
  
 メッセージの取得の詳細については`MessageStorageIn`を参照してください[GetMessages サンプル](../../adapters-and-accelerators/accelerator-rosettanet/getmessages-sample.md)です。  
  
## <a name="location-in-sdk"></a>SDK でのパス  
 \<*ドライブ*\>\Program Files (x86) \Microsoft BizTalk\<バージョン\>Accelerator for rosettanet \sdk  
  
## <a name="running-testcrypto"></a>TestCrypto の実行  
  
#### <a name="to-run-testcrypto"></a>TestCrypto を実行するには  
  
1.  をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**アクセサリ**、順にクリック**コマンド プロンプト**です。  
  
2.  移動\<*ドライブ*\>\Program Files (x86) \Microsoft BizTalk\<バージョン\>Accelerator for rosettanet \sdk です。  
  
3.  コマンド プロンプトで次のように入力します。 **TestCrypto.exe \<filename\>**、ENTER キーを押します。  
  
## <a name="remarks"></a>コメント  
 ユーティリティが検出した証明書が適切な証明書ではない場合や無効な証明書である場合、または証明書が検出されない場合、暗号化の解除は失敗します。  
  
## <a name="see-also"></a>参照  
 [ユーティリティ](../../adapters-and-accelerators/accelerator-rosettanet/utilities1.md)
