---
title: "X12 の上限にエラー確認の生成に失敗しましたトランザクション パーティ |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c78a7cef-24ae-4d09-9043-2f53c301302d
caps.latest.revision: "9"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c5b82a8251504e1f9ff7b62c4e1cc813d4740a83
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="error-ack-generation-has-failed-as-maximum-limit-of-x12-transaction-party"></a>X12 の上限にエラー確認の生成に失敗しましたトランザクション パーティ
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]|  
|製品バージョン|[!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]|  
|イベント ID|-|  
|イベント ソース|[!INCLUDE[btsBizTalkServer2006r3](../includes/btsbiztalkserver2006r3-md.md)] EDI|  
|コンポーネント|EDI エンジン|  
|シンボル名|-|  
|メッセージ テキスト|パーティ {0} の X12 トランザクション セット制御番号が、許容される上限に到達したため、受信確認の生成に失敗しました。 パートナー アグリーメント マネージャーで、[Party in sender role] の [ST 2] フィールドに移動して、カウンターをリセットしてください。|  
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、受信確認のトランザクション セット参照番号 (ST2) で入力された制御番号が ST2 の最大許容値より大きいために、BizTalk Server が X12 インターチェンジの受信確認を生成できなかったことを示します。 この場合、BizTalk Server は EDI パーティのプロパティを使用して受信確認を作成しました。  
  
 トランザクション セット制御番号の最大値は、制御番号で使用する桁数によって決まります。 3 つのフィールドを合わせた最大長は 9 文字です。プレフィックス フィールドとサフィックス フィールドの最大長は 8 文字です。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、[GS および ST セグメントの定義] ページのトランザクション セット制御番号 (ST2) の制御番号フィールド (ST2.2) を最大値よりも小さい値に設定し直します。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールの [EDI グローバル プロパティ] ダイアログ ボックスでこのプロパティを設定します。