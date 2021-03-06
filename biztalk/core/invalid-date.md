---
title: 無効な日付 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a41da9c5-9dcf-44cd-be5b-922e6c267ec3
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6a7e5f8003cbb8cc88487f471e10ce0d7ba857e5
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36987755"
---
# <a name="invalid-date"></a>日付が無効です
## <a name="details"></a>詳細  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  製品名   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 製品バージョン |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    イベント ID     |                                           -                                            |
|  イベント ソース   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    コンポーネント    |                                       EDI エンジン                                       |
|  シンボル名  |                              X12DeInvalidDateDescription                               |
|  メッセージ テキスト   |                                      日付が無効です                                      |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、データ要素の日付値が、EDI スキーマで指定されたデータ型に準拠していなかったか、または X12 インターチェンジの GS04 フィールド ヘッダーの日付値が、サービス スキーマ (BaseArtifacts.dll 内の X12ServiceSchema) に準拠していなかったため、受信パイプラインで受信インターチェンジを処理できなかったか、または送信パイプラインで送信インターチェンジを処理できなかったことを示します。 X12 の場合、サービス スキーマは、GS04 フィールドの日付を X12_DT データ型として、6 ～ 8 文字の長さで定義します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、データ要素の時間値が、EDI スキーマで定義されたデータ型に準拠しているか、または X12 インターチェンジの GS04 ヘッダーの日付値がサービス スキーマに準拠していることを確認し、インターチェンジを再送信してもらいます。