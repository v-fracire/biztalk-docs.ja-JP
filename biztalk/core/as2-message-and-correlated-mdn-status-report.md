---
title: AS2 メッセージおよび関連する MDN 状態レポート |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 48ed0ee3-c844-4cb9-a84d-32b719ab8fab
caps.latest.revision: 17
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e1ce4aed138f4e32e87cb1d428050999cc2b764a
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22232978"
---
# <a name="as2-message-and-correlated-mdn-status-report"></a>AS2 メッセージおよび関連する MDN の状態レポート
このレポートでは、AS2 送信パイプラインおよび受信パイプラインで処理されるすべての AS2 メッセージ、およびそれらのインターチェンジに関連する MDN が示されます。  
  
## <a name="fields-in-the-status-report"></a>状態レポート内のフィールド  
 AS2 メッセージおよび関連する ACK の状態レポートには、以下の受信インターチェンジまたは送信インターチェンジに関する情報と、それらに関連する受信確認が表示されます。  
  
-   送信者パーティ名  
  
-   受信者パーティ名  
  
-   AS2 の差出人  
  
-   AS2 の宛先  
  
-   AS2 メッセージ ID  
  
-   AS2 メッセージの日時  
  
-   受信日時  
  
-   パーティ ロール  
  
-   MDN の状態  
  
-   暗号化の状態  
  
-   署名の状態  
  
-   EDI インターチェンジの状態  
  
-   AS2 メッセージを重複するには  
  
-   重複を確認する日数  
  
-   Filename  
  
-   信頼できるメッセージ処理を有効化  
  
## <a name="fields-in-the-query-expression-for-the-status-report"></a>状態レポートのクエリ式のフィールド  
 表示されるデータを指定するクエリ式のフィールドを変更することにより、AS2 メッセージと関連する ACK の状態レポートをカスタマイズできます。 使用できるフィールドは以下のとおりです。  
  
|||||  
|-|-|-|-|  
|クエリ式のフィールド|有効な演算子|潜在的な値|既定で含まれますか。|  
|検索|[等しい]|AS2/MDN の状態|指定あり (必須)|  
|[メッセージの状態]|[等しい]<br /><br /> 等しくないです。|すべて<br /><br /> 確認済み - 処理済み<br /><br /> 確認済み - 失敗<br /><br /> 処理済み - MDN 保留中<br /><br /> 処理済み - MDN は不要<br /><br /> 未確認 - 再送信の試行回数を超過<br /><br /> 未確認 – 再送信期間を超過|はい|  
|AS2 メッセージの日時|[以下]<br /><br /> [以上]|特定の日時<br /><br /> [今日]<br /><br /> 昨日|はい<br /><br /> メモ: クエリ式に 1 回以上含めることができます。|  
|[最大一致数]|[等しい]|整数 (既定値 50)|はい|  
|AS2 メッセージ ID|[等しい]|すべて<br /><br /> 固有の AS2 メッセージ ID|不可|  
|Direction|[等しい]|すべて (既定)<br /><br /> Receive<br /><br /> Send|不可|  
|受信者パーティ名|[等しい]|すべて (既定)<br /><br /> 特定のパーティ名|不可|  
|送信者パーティ名|[等しい]|すべて (既定)<br /><br /> 特定のパーティ名|不可|  
  
## <a name="additional-as2-message-and-correlated-mdn-status-reports"></a>AS2 メッセージおよび関連する MDN の状態の追加レポート  
 AS2 メッセージおよび関連する MDN 状態レポートに一覧表示されている AS2 メッセージを右クリックすると、次のより詳細な状態レポートのいずれかを表示できます。  
  
|状態レポート|表示される状態|  
|-------------------|----------------------|  
|インターチェンジ/確認の状態|AS2 メッセージの EDI ペイロードの状態|  
|再送信の状態の詳細|メッセージの再送信の状態|  
|メッセージのワイヤ形式|AS2 メッセージのワイヤ形式|  
|デコードされたメッセージ|AS2 メッセージのデコード形式|  
|MDN メッセージ|AS2 メッセージに関連する MDN メッセージ|  
  
 最後の 3 つのメッセージの形式はそれぞれ同じです。 詳細については、次を参照してください。 [AS2 メッセージ コンテンツ状態レポート](../core/as2-message-content-status-reports.md)です。  
  
## <a name="correlate-an-as2-message-with-its-edi-payload"></a>その EDI ペイロードを持つ AS2 メッセージを関連付ける  
 AS2 状態レポートと EDI 状態レポートでは、AS2 メッセージの状態エントリとその EDI ペイロードを関連付けることができます。 AS2 状態レポートと EDI 状態レポートの両方を有効にしている場合、AS2 メッセージの AS2 状態レポートで状態エントリが作成され、さらにその AS2 メッセージの EDI ペイロードの EDI 状態レポートで状態エントリが作成されます。 AS2 メッセージの状態エントリを右クリックし、をクリックして、AS2 メッセージの EDI ペイロードの状態を表示するには、AS2 状態レポートの表示があれば、**インターチェンジ/確認の状態**です。 AS2 メッセージに EDI インターチェンジが 1 つしかない場合、この操作では、そのインターチェンジの状態エントリが表示されます。  
  
 AS2 メッセージには、複数の EDI インターチェンジが含まれているし、AS2 メッセージに複数の EDI インターチェンジの状態を表示しようとすると、最後の EDI インターチェンジだけが、インターチェンジ/確認の状態レポートに表示されます。 さらに、 **EDI のインターチェンジ制御番号**AS2/MDN の状態レポート内のフィールドは、最後のインターチェンジ制御番号のみを表示します。 インターチェンジ制御番号によって、AS2 メッセージとその EDI インターチェンジ ペイロードが関連付けられます。  
  
 AS2 メッセージ内のすべての EDI インターチェンジのデータは、状態レポート データベースに保存されます。 場合、インターチェンジ/確認の状態レポートで AS2 メッセージ内のすべてのインターチェンジを表示することができます、 **Control ID Equals All**状態レポート クエリでは、句。 これによって、AS2 メッセージに含まれていない他のインターチェンジも表示される可能性がありますが、"送信者パーティ"、"受信者パーティ"、"インターチェンジの日時" などのフィールドを調べることで、単一の AS2 メッセージに含まれる EDI インターチェンジを特定できます。  
  
 **パーティ ロール**AS2 状態レポートにフィールドと**方向**EDI 状態レポートにフィールドの意味は正反対です。 EDI ペイロードを持つ受信 AS2 メッセージの**パーティ ロール**フィールドは AS2 メッセージが表示されます**送信者**中、**方向**フィールドは、EDI インターチェンジになります**受信**です。 この理由は、パーティから受信する受信メッセージでは、そのパーティのロールは送信者であるためです。 パーティが送信する AS2 メッセージに関連するそのパーティのプロパティは、AS2 メッセージ送信者としてのパーティのプロパティであり、パートナー アグリーメント マネージャーの [AS2 のプロパティ] ダイアログ ボックスで定義されるパーティのプロパティです。 したがって、AS2 パーティのロールは EDI の方向とは反対になります。  
  
## <a name="next-steps"></a>次の手順
  
-   [AS2 メッセージ コンテンツ状態レポート](../core/as2-message-content-status-reports.md)  
  
-   [再送信状態詳細レポート](../core/resend-status-details-report.md)  
  
## <a name="see-also"></a>参照  
 [AS2 メッセージおよび関連する MDN 状態レポート](../core/as2-message-and-correlated-mdn-status-report.md)   
