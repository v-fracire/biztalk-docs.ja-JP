---
title: "送信 EDI メッセージのデータを格納する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a6e576fc-37fd-417d-ae68-607a0a8bcc0a
caps.latest.revision: "10"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 278ab244ab48d2e11a84e99f0af2e02948ff961a
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-data-is-stored-for-outbound-edi-messages"></a>送信 EDI メッセージのデータ格納方法
[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は次の操作を実行して、送信インターチェンジの状態レポート エントリを生成します。  
  
1.  送信メッセージ XML が EDI 送信パイプラインに送信されると、送信パイプラインは状態レポートのデータ ストアに次の値のエントリを作成します。  
  
    -   インターチェンジ状態エントリは [処理済み] に設定されています。  
  
    -   インターチェンジ確認状態エントリ (インターチェンジごとに 1 つ) は、[必要] に設定されています。  
  
    -   機能確認状態エントリ (X12 ではグループごとに 1 つ、EDIFACT ではすべてのグループに 1 つ) は、[必要] に設定されています。  
  
2.  EDI メッセージが取引先に送信され、取引先から受信確認が返された後に、受信確認を受信する EDI 受信パイプラインは、インターチェンジ状態、インターチェンジ確認状態、および機能確認状態エントリを、必要に応じて [受理] / [一部受理] / [拒否] に更新します。  
  
## <a name="data-stored-by-the-send-pipeline-for-outbound-interchanges"></a>送信インターチェンジの送信パイプラインによって格納されるデータ  
 送信パイプラインは、送信する各インターチェンジの状態レポート データ ストアにレコードを作成します。 エントリに必要なほとんどのデータは、インターチェンジのヘッダー/トレーラー セグメント (ISA/IEA または UNB/UNZ) から使用可能です。 他のデータは、送信ポートのプロパティから使用できます。 格納されるデータは次のとおりです。  
  
-   レコードの種類 = インターチェンジの状態  
  
-   インターチェンジの方向 = 更新データ = 送信  
  
-   インターチェンジの受信者 = 更新データ  
  
-   インターチェンジの送信者 = 更新データ  
  
-   インターチェンジの日付 = 更新データ  
  
-   インターチェンジの時刻 = 更新データ  
  
-   インターチェンジ制御 ID = 更新データ  
  
-   インターチェンジ状態: 処理済み/送信済み。 [処理済み] 状態は、送信パイプラインが正常にインターチェンジを処理し、配信用に送信アダプターに渡したことを示します。  
  
-   インターチェンジ制御カウント (X12 でのグループ/メッセージ) = データ  
  
-   インターチェンジ送信ポート ID = データ  
  
## <a name="data-stored-by-the-receive-pipeline-for-each-technical-acknowledgment-received-in-response-to-an-outbound-interchange"></a>送信インターチェンジへの応答として受信した各技術確認用の受信パイプラインによって格納されるデータ  
 受信パイプラインは、受信した各技術確認用の状態レポート データ ストアにレコードを作成します。 受信パイプラインでは、状態レポート データ ストアで受信した各インターチェンジのレコードを作成します。 取引先に送信されたインターチェンジへの応答として受信した各技術確認用のデータ ストアに 1 つの技術確認の状態レポート エントリを作成します。 技術確認は、X12 では TA1 で、EDIFACT では UCI セグメントのみを持つ CONTRL メッセージです。 格納されるデータは次のとおりです。  
  
-   レコードの種類 = インターチェンジ確認状態  
  
-   インターチェンジ確認方向 = 送信 – 更新データ  
  
-   インターチェンジの受信者 = 更新データ (関連付けに必要)  
  
-   インターチェンジの送信者 = 更新データ (関連付けに必要)  
  
-   インターチェンジの日付 = 更新データ (X12 関連付けに必要)  
  
-   インターチェンジ制御 ID = 更新データ (関連付けに必要)  
  
-   インターチェンジ確認状態 = 生成または該当なし\<注 0 を参照してください >-データを更新します。  
  
-   インターチェンジ確認制御 ID= 値なし – 送信側によって適用  
  
-   インターチェンジ確認日付 = 値なし – 送信側によって適用  
  
-   インターチェンジ確認時刻 = 値なし – 送信側によって適用  
  
-   確認/アクション コード = 更新データ\<注 1 を参照 > (TA104 X12 または EDIFACT UCI4) から *  
  
-   確認通知コード = 更新データ\<注 2 を参照 > (から X12-TA105、EDIFACT には適用不可) *  
  
 次の確認/アクション コードが使用されます。  
  
|確認/アクション コードのデータ|レポートのエラーの説明|コメント (適用範囲)|  
|------------------------------|-------------------------------------|-------------------------------|  
|A|受理|X12|  
|E|受理、エラー検出|X12|  
|P|一部受理|X12|  
|R|拒否しました|X12|  
|4|拒否しました|EDIFACT|  
|8|受理/一部受理|EDIFACT|  
  
 次の確認通知コードが使用されます。  
  
|確認通知コードのデータ (X12)|Description|  
|--------------------------------------|-----------------|  
|000|Success|  
|001|インターチェンジ制御番号が一致しません。|  
|002|標準がサポートされていません。|  
|003|バージョンのコントロールはサポートされていません|  
|004|セグメント終端記号が無効です。|  
|005|送信者のインターチェンジ ID 修飾子が無効です。|  
|006|インターチェンジ送信者 ID が無効です。|  
|007|受信者のインターチェンジ ID 修飾子が無効です。|  
|008|インターチェンジ受信者 ID が無効です。|  
|009|インターチェンジ受信者 ID が不明です。|  
|010|認証情報修飾子の値が無効です。|  
|011|認証情報の値が無効です。|  
|012|無効なセキュリティ情報修飾子の値|  
|013|セキュリティ情報の値が無効です。|  
|014|無効なインターチェンジ日付の値|  
|015|無効なインターチェンジ時刻の値|  
|016|無効なインターチェンジ標準識別子の値|  
|017|インターチェンジ バージョン ID の値が無効です。|  
|018|無効なインターチェンジ制御番号の値|  
|019|確認要求の値が無効です。|  
|020|テスト インジケーターの値が無効です|  
|021|含まれているグループの数の値が無効です。|  
|022|制御構造が無効です。|  
|023|ファイルの終わりが正しくありません。|  
|024|インターチェンジの内容が無効です。|  
|025|インターチェンジ制御番号が重複しています。|  
|026|データ要素区切り記号が無効です。|  
|027|コンポーネント要素区切り記号が無効です。|  
|028|遅延配信要求の配信日が無効です。|  
|029|遅延配信要求の配信時刻が無効です。|  
|030|遅延配信要求に無効な配信時のコード|  
|031|サービスの評価が無効です。|  
  
## <a name="data-updated-by-the-receive-pipeline-for-each-technical-acknowledgment-received-in-response-to-an-outbound-interchange"></a>送信インターチェンジへの応答として受信した各技術確認用の受信パイプラインによって更新されるデータ  
 受信パイプラインが受信した各技術確認用に、関連する送信インターチェンジの状態レポート エントリが更新されます。  
  
 EDI 逆アセンブラーは、次のように受信確認の UCI および TA1 セグメントのデータを使用して、データ ストア内でレコードを検索します。  
  
|確認のフィールド|データ ストアのフィールド|解説|  
|-------------------|--------------------------|-------------|  
|インターチェンジの送信者 ID|インターチェンジの受信者|-|  
|インターチェンジの受信者 ID|インターチェンジの送信者|-|  
|-|インターチェンジ日付|-|  
|インターチェンジ制御番号|インターチェンジ制御 ID|-|  
|-|インターチェンジ方向 = 送信|保存されたバッチ シナリオの一意性に必要|  
|レコードの種類|インターチェンジ状態とインターチェンジ確認状態|-|  
  
 格納されるデータは次のとおりです。  
  
-   インターチェンジ確認方向 = 受信 – 既存データ  
  
-   インターチェンジ確認状態 = 受信  
  
-   インターチェンジ受信者 = 既存データ  
  
-   インターチェンジ送信者 = 既存データ  
  
-   インターチェンジ日付 = 既存データ  
  
-   インターチェンジ制御 ID = 既存データ  
  
-   インターチェンジ確認制御 ID = 更新データ  
  
-   インターチェンジ確認日付 = 更新データ  
  
-   インターチェンジ確認時刻 = 更新データ  
  
-   確認/アクション コード = 更新データ (TA104 X12 または EDIFACT UCI4) から *\<注 1 を参照してください >  
  
-   確認通知コード 2 = 更新データ (X12 TA105 から edifact と) *\<注 2 を参照してください >  
  
 ACK X12:TA1-104 または EDIFACT UCI4 からのデータは、次のようにマップされます。  
  
|確認/アクション コードのデータ|状態レポートでのマップ|解説|  
|------------------------------|---------------------------------|-------------|  
|A|受理|X12|  
|P|一部受理|X12|  
|R、M、W、X|拒否しました|X12|  
|E|エラーを伴って承諾済み|X12|  
|4|拒否しました|EDIFACT|  
|7、8|受理/一部受理|EDIFACT|  
  
 次の確認通知コードが使用されます。  
  
|確認通知コードのデータ (X12)|状態レポートでのマップ|  
|--------------------------------------|---------------------------------|  
|000|Success|  
|001|インターチェンジ制御番号が一致しません。|  
|002|標準がサポートされていません。|  
|003|バージョンのコントロールはサポートされていません|  
|004|セグメント終端記号が無効です。|  
|005|送信者のインターチェンジ ID 修飾子が無効です。|  
|006|インターチェンジ送信者 ID が無効です。|  
|007|受信者のインターチェンジ ID 修飾子が無効です。|  
|008|インターチェンジ受信者 ID が無効です。|  
|009|インターチェンジ受信者 ID が不明です。|  
|010|認証情報修飾子の値が無効です。|  
|011|認証情報の値が無効です。|  
|012|無効なセキュリティ情報修飾子の値|  
|013|セキュリティ情報の値が無効です。|  
|014|無効なインターチェンジ日付の値|  
|015|無効なインターチェンジ時刻の値|  
|016|無効なインターチェンジ標準識別子の値|  
|017|インターチェンジ バージョン ID の値が無効です。|  
|018|無効なインターチェンジ制御番号の値|  
|019|確認要求の値が無効です。|  
|020|テスト インジケーターの値が無効です|  
|021|含まれているグループの数の値が無効です。|  
|022|制御構造が無効です。|  
|023|ファイルの終わりが正しくありません。|  
|024|インターチェンジの内容が無効です。|  
|025|インターチェンジ制御番号が重複しています。|  
|026|データ要素区切り記号が無効です。|  
|027|コンポーネント要素区切り記号が無効です。|  
|028|遅延配信要求の配信日が無効です。|  
|029|遅延配信要求の配信時刻が無効です。|  
|030|遅延配信要求に無効な配信時のコード|  
|031|サービスの評価が無効です。|  
  
## <a name="data-stored-by-the-receive-pipeline-for-each-functional-acknowledgment-received-in-response-to-outbound-interchanges"></a>送信インターチェンジへの応答として受信した各機能確認用の受信パイプラインによって格納されるデータ  
 受信パイプラインは、受信した各機能確認用の状態レポート データ ストアにレコードを作成します。  技術確認は、X12 では 997 で、EDIFACT では CONTRL メッセージの全文です。 グループごとに 1 つのエントリが作成されます。 インターチェンジおよびグループ ヘッダーからのデータは、このエントリの作成中に使用されます。 格納されるデータは次のとおりです。  
  
-   レコードの種類 = 機能確認状態  
  
-   機能確認方向 = 送信  
  
-   機能確認状態 =\<生成された、または該当なし、注 1 を参照してください >  
  
-   インターチェンジの受信者 = 更新データ (関連付けに必要)  
  
-   インターチェンジの送信者 = 更新データ (関連付けに必要)  
  
-   インターチェンジの日付 = 更新データ (X12 関連付けに必要)  
  
-   インターチェンジ制御 ID = 更新データ (関連付けに必要)  
  
-   グループ制御番号 = 更新データ (EDIFACT ではオプション、X12 関連付けに必要)  
  
-   機能 ID コード = 更新データ (GS01/UNG01)  
  
-   トランザクション セットの数 = 更新データ (UNE1/UNZ1)  
  
-   機能確認インターチェンジ制御 ID = 値なし – 送信側によって適用  
  
-   機能確認インターチェンジ日付 = 値なし – 送信側によって適用  
  
-   機能確認インターチェンジ時刻 = 値なし – 送信側によって適用  
  
-   受信したトランザクション セットの数 = 更新データ (X12-AK903 および EDIFACT エンコード用にエンジンで計算)  
  
-   受理したトランザクション セットの数 = 更新データ (X12-AK904 および EDIFACT エンコード用にエンジンで計算)  
  
-   確認/アクション コード = 更新データ\<注 2 を参照 > (X12 AK901 edifact-uci4 から) *  
  
-   エラー/構文エラー コード  = 更新データ (X12-AK905、EDIFACT UCI5) 注 3  
  
-   追加の X12 確認エラー コード 2 = 更新データ (X12-AK906)  
  
-   追加の X12 確認エラー コード 3 = 更新データ (X12-AK907)  
  
-   追加の X12 確認エラー コード 4 = 更新データ (X12-AK908)  
  
-   追加の X12 確認エラー コード 5 = 更新データ (X12-AK909)  
  
 次の確認/アクション コードが使用されます。  
  
|確認/アクション コードのデータ|レポートのエラーの説明|コメント (適用範囲)|  
|------------------------------|-------------------------------------|-------------------------------|  
|A|受理|X12|  
|E|エラーを伴って承諾済み|X12|  
|P|一部受理|X12|  
|R|拒否しました|X12|  
|4|拒否しました|EDIFACT|  
|7|受理/一部受理|EDIFACT|  
  
 次のエラー/構文エラー コードが EDIFACT に使用されます。  
  
|エラー/構文エラー コード内のデータ<br /><br /> (EDIFACT に適用可能)|レポートのエラーの説明|  
|--------------------------------------------------------------------|-------------------------------------|  
|2|構文のバージョンまたはレベルがサポートされていません。|  
|7|インターチェンジの受信者が実際の受信者ではありません。|  
|12|値が無効です。|  
|13|Missing|  
|14|この位置ではサポートされていない値です。|  
|15|サポートされていない位置です。|  
|16|含まれている要素が多すぎます。|  
|17|アグリーメントがありません。|  
|18|不特定のエラー|  
|19|無効な小数点表記です。|  
|20|サービス文字として無効な文字です。|  
|21|無効な文字です。|  
|22|サービス文字が無効です。|  
|23|インターチェンジの送信者が不明です。|  
|24|古すぎます。|  
|25|テスト インジケーターがサポートされていません。|  
|26|重複が検出されました。|  
|27|セキュリティ機能がサポートされていません。|  
|28|参照が一致しません。|  
|29|制御数が受信したインターチェンジの数と一致しません。|  
|30|グループとメッセージ/パッケージが混在しています。|  
|31|グループ内に複数のメッセージの種類があります。|  
|32|下位レベルが空です。|  
|33|メッセージ、パッケージ、またはグループの外側に無効な項目があります。|  
|34|インジケーターの入れ子は認められていません。|  
|35|データ要素またはセグメントの繰り返しが多すぎます。|  
|36|セグメント グループの繰り返しが多すぎます。|  
|37|文字の種類が無効です。|  
|38|小数点の記号の前に数値がありません。|  
|39|データ要素が長すぎます。|  
|40|データ要素が短すぎます。|  
|41|永続的な通信ネットワーク エラー|  
|42|一時的な通信ネットワーク エラー|  
|43|インターチェンジの受信者が不明です。|  
|45|末尾の区切り記号が見つかりました。|  
|46|文字セットがサポートされていません|  
|47|エンベロープ機能はサポートされません。|  
|48|依存状態が違反しています。|  
|70|トランザクション セットがないか、トランザクション セットの識別子が無効です。|  
|71|トランザクション セット制御番号またはグループ制御番号が一致していません。|  
|72|セグメント ID が認識されません|  
|73|XML の位置が正しくありません。|  
|74|セグメント グループの繰り返しが少なすぎます。|  
|75|セグメントの繰り返しが少なすぎます。|  
|76|見つかったデータ要素が少なすぎます|  
  
 次のエラー/構文エラー コードが X12 で使用されます。  
  
|エラー/構文エラー コード内のデータ<br /><br /> (X12 に適用可能)|レポートのエラーの説明|  
|----------------------------------------------------------------|-------------------------------------|  
|1|機能グループがサポートされていません。|  
|2|機能グループのバージョンがサポートされていません。|  
|3|機能グループ トレーラーがありません。|  
|4|機能グループ ヘッダーとトレーラーのグループ制御番号が一致しません。|  
|5|含まれているトランザクション セットの数が実際の数と一致しません。|  
|6-26|その他のサポートされていない検証エラー|  
  
## <a name="data-updated-by-the-receive-pipeline-for-each-functional-acknowledgment-received-in-response-to-outgoing-interchanges"></a>送信インターチェンジへの応答として受信した各機能確認用の受信パイプラインによって更新されるデータ  
 受信パイプラインが受信した各機能を確認するたびに、関連する送信インターチェンジの状態レポート エントリが更新されます。  
  
 EDI 逆アセンブラーは、次のように受信確認のインターチェンジおよびグループ ヘッダー セグメントのデータを使用して、データ ストア内でレコードを検索します。  
  
|確認のフィールド|データ ストアのフィールド|解説|  
|-------------------|--------------------------|-------------|  
|インターチェンジの送信者 ID|インターチェンジの受信者|X12 および EDIFACT に適用可能|  
|インターチェンジの受信者 ID|インターチェンジの送信者|X12 および EDIFACT に適用可能|  
|-|インターチェンジ日付|-|  
|インターチェンジ制御番号|インターチェンジ制御 ID|EDIFACT のみに適用可能|  
|グループ制御番号|グループ制御番号|X12 のみに適用可能|  
|-|インターチェンジ方向 = 送信|BIBO シナリオ以降の一意性に必要|  
|レコードの種類|機能確認状態|X12 および EDIFACT に適用可能|  
  
 格納されるデータは次のとおりです。  
  
-   レコードの種類 = 機能確認状態  
  
-   機能確認方向 = 受信  
  
-   機能確認状態 = 受信したとおりの更新データ  
  
-   インターチェンジ受信者 = 既存データ  
  
-   インターチェンジ送信者 = 既存データ  
  
-   インターチェンジ日付 = 既存データ  
  
-   インターチェンジ制御 ID = 既存データ  
  
-   グループ制御番号 = 既存データ  
  
-   機能 ID コード = 既存データ  
  
-   トランザクション セットの数 = 既存データ  
  
-   機能確認インターチェンジ制御 ID = 更新データ  
  
-   機能確認インターチェンジ日付 = 更新データ  
  
-   機能確認インターチェンジ時刻 = 更新データ  
  
-   配信されたトランザクション セットの数 = 更新データ (X12-AK903、EDIFACT には適用不可)  
  
-   受理されたトランザクション セットの数 = 更新データ (X12-AK904、EDIFACT には適用不可)  
  
-   確認/アクション コード = 更新データ (X12 AK901 および UCI4) 注 1 を参照  
  
-   エラー/構文エラー コード  = (X12 AK905 および UCI5) 注 2 を参照  
  
-   追加の X12 確認エラー コード 2 = 更新データ (X12-AK906)  
  
-   追加の X12 確認エラー コード 3 = 更新データ (X12-AK907)  
  
-   追加の X12 確認エラー コード 4 = 更新データ (X12-AK908)  
  
-   追加の X12 確認エラー コード 5 = 更新データ (X12-AK909)  
  
 次の確認/アクション コードが使用されます。  
  
|確認/アクション コードのデータ|状態レポートでのマップ|解説|  
|------------------------------|---------------------------------|-------------|  
|A|受理|X12|  
|P|一部受理|X12|  
|R、M、W、X|拒否しました|X12|  
|E|エラーを伴って承諾済み|X12|  
|4|拒否しました|EDIFACT|  
|7、8|受理/一部受理|EDIFACT|  
  
 次のエラー/構文エラー コードが EDIFACT に使用されます。  
  
|エラー/構文エラー コードのデータ<br /><br /> (EDIFACT に適用可能)|レポートのエラーの説明|  
|-------------------------------------------------------------------|-------------------------------------|  
|2|構文のバージョンまたはレベルがサポートされていません。|  
|7|インターチェンジの受信者が実際の受信者ではありません。|  
|12|値が無効です。|  
|13|Missing|  
|14|この位置ではサポートされていない値です。|  
|15|サポートされていない位置です。|  
|16|含まれている要素が多すぎます。|  
|17|アグリーメントがありません。|  
|18|不特定のエラー|  
|19|無効な小数点表記です。|  
|20|サービス文字として無効な文字です。|  
|21|無効な文字です。|  
|22|サービス文字が無効です。|  
|23|インターチェンジの送信者が不明です。|  
|24|古すぎます。|  
|25|テスト インジケーターがサポートされていません。|  
|26|重複が検出されました。|  
|27|セキュリティ機能がサポートされていません。|  
|28|参照が一致しません。|  
|29|制御数が受信したインターチェンジの数と一致しません。|  
|30|グループとメッセージ/パッケージが混在しています。|  
|31|グループ内に複数のメッセージの種類があります。|  
|32|下位レベルが空です。|  
|33|メッセージ、パッケージ、またはグループの外側に無効な項目があります。|  
|34|インジケーターの入れ子は認められていません。|  
|35|データ要素またはセグメントの繰り返しが多すぎます。|  
|36|セグメント グループの繰り返しが多すぎます。|  
|37|文字の種類が無効です。|  
|38|小数点の記号の前に数値がありません。|  
|39|データ要素が長すぎます。|  
|40|データ要素が短すぎます。|  
|41|永続的な通信ネットワーク エラー|  
|42|一時的な通信ネットワーク エラー|  
|43|インターチェンジの受信者が不明です。|  
|45|末尾の区切り記号が見つかりました。|  
|46|文字セットがサポートされていません|  
|47|エンベロープ機能はサポートされません。|  
|48|依存状態が違反しています。|  
|70|トランザクション セットがないか、トランザクション セットの識別子が無効です。|  
|71|トランザクション セット制御番号またはグループ制御番号が一致していません。|  
|72|セグメント ID が認識されません|  
|73|XML の位置が正しくありません。|  
|74|セグメント グループの繰り返しが少なすぎます。|  
|75|セグメントの繰り返しが少なすぎます。|  
|76|見つかったデータ要素が少なすぎます|  
  
 次のエラー/構文エラー コードが X12 で使用されます。  
  
|エラー/構文エラー コード内のデータ<br /><br /> (X12 に適用可能)|レポートのエラーの説明|  
|----------------------------------------------------------------|-------------------------------------|  
|1|機能グループがサポートされていません。|  
|2|機能グループのバージョンがサポートされていません。|  
|3|機能グループ トレーラーがありません。|  
|4|機能グループ ヘッダーとトレーラーのグループ制御番号が一致しません。|  
|5|含まれているトランザクション セットの数が実際の数と一致しません。|  
|6-26|その他のサポートされていない検証エラー|  
  
## <a name="see-also"></a>参照  
 [EDI および AS2 状態レポートのデータを格納する方法](../core/how-data-is-stored-for-edi-and-as2-status-reports.md)   
 [受信 EDI メッセージのデータを格納する方法](../core/how-data-is-stored-for-inbound-edi-messages.md)