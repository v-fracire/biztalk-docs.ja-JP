---
title: 動的 MLLP アダプター |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2e22fabb-0edf-4931-b8b2-74a5daccee4a
caps.latest.revision: 2
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 0b1ad131716f5b1bb1b5abdfb7985fa93f2ae41c
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36999811"
---
# <a name="dynamic-mllp-adapter"></a>動的 MLLP アダプター
以降で[!INCLUDE[bts2013r2](../../includes/bts2013r2-md.md)]、一方向または双方向 (要求-応答) の送信ポートを使用して実行時に MLLP アダプターのプロパティを構成することができます。  
  
## <a name="dynamic-properties"></a>動的プロパティ  
 次のプロパティは、 **GlobalPropertySchemas**名前空間。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|メッセージ (MLLP.acceptableACKCodes) =「すべての確認コード」;|値は次のとおりです。<br /><br /> -すべての確認コード<br />-AA と CA<br />-AA、CA、AE、CE<br />-AA、CA、AR、CR<br /><br /> 似ています、**許容される確認コード**MLLP の静的送信ポートのプロパティ。|  
|メッセージ (MLLP します。キャリッジ リターン) ="0 d";|ASCII 文字|  
|メッセージ (MLLP.endBlockDelimiter) ="1 c";|終了ブロックの ASCII 文字|  
|メッセージ (MLLP.startBlockDelimiter) ="0b";|開始ブロック文字の ASCII|  
|メッセージ (MLLP.timeout) =「60000」;|非アクティブな送信ソケット BTAHL7 サーバーはタイムアウトの後にピリオド (0 はタイムアウトなし)|  
|SendPortName(Microsoft.XLANGs.BaseTypes.Address) =「127.0.0.1:11000」;|メッセージのルーティングのアドレスとポート|  
|SendPortName(Microsoft.XLANGs.BaseTypes.TransportType) ="MLLP";|(MLLP) アダプターの種類|  
  
## <a name="additional"></a>追加情報  
  
- For HL7 をオーケストレーションでマルチパート メッセージを作成する場合、メッセージでパーツを作成この次の順序。  
  
  1. MSH セグメント  
  
  2. BodySegments  
  
  3. ZSegments  
  
     別の順序でメッセージ部分を指定する場合は、次のエラーが発生します。  
  
     WrongBodyPartException  
  
- 動的ルーティングをサポートするために、オーケストレーションでは、アダプターのルートのプロパティを指定できます。  
  
## <a name="see-also"></a>参照  
 [構成パラメーターを送信および受信アダプター](../../adapters-and-accelerators/accelerator-hl7/configuration-parameters-for-send-and-receive-adapters.md)   
 [MLLP 受信アダプターの処理](../../adapters-and-accelerators/accelerator-hl7/mllp-receive-adapter-processing.md)   
 [MLLP 送信アダプターの処理](../../adapters-and-accelerators/accelerator-hl7/mllp-send-adapter-processing.md)   
 [MLLP でエンコードされたメッセージの処理](../../adapters-and-accelerators/accelerator-hl7/processing-mllp-encoded-messages.md)