---
title: X12 997 受信確認 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 62a352fb-635c-4f0e-9844-4b250159333d
caps.latest.revision: 15
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: fde785e5bd287497b851db704dedb5da3632c07c
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36973899"
---
# <a name="x12-997-acknowledgment"></a>X12 997 受信確認
X12 997 機能確認は、受信されたインターチェンジの状態を報告します。 受信したドキュメントの処理中に発生した各エラーが報告されます。 BizTalk EDI 受信パイプラインは、常に 4010 準拠の 997 を生成します。ただし、EDI 受信パイプラインおよび EDI 送信パイプラインは、5010 準拠の 997 も検証できます。  
  
 すべての X12 トランザクション セットと同様に、997 ACK は GS/GE エンベロープ内に送信されます。 ST および SE は、他のトランザクション セットと同様です。  
  
 997 ACK のトランザクション セット内のセグメントを次の表に示します。  
  
|[位置]|Segment<br />ID|名前|求人<br />Des です。|Max 新しく使用する機能|ループ<br />繰り返し|  
|--------------|-----------------|----------|----------------|--------------|------------------|  
|010|ST|トランザクション セット ヘッダー (受信確認の場合)|M|1|-|  
|020|AK1|機能グループ応答ヘッダー|M|1|-|  
|030|AK2|トランザクション セット応答ヘッダー|O|1|999999 <br />(ループ ID = AK2)|  
|040|AK3|データ セグメントの説明|O|1|999999 <br />(ループ ID = AK2/AK3)|  
|050|AK4|データ要素の説明|O|99|-|  
|060|AK5|トランザクション セット応答トレーラ|M|1|-|  
|070|AK9|機能グループ応答トレーラ|M|1|-|  
|080|SE|トランザクション セット トレーラー (受信確認の場合)|M|1|-|  
  
- 求人Des です。 = 指定要件  
  
- M = 必須  
  
- O = 省略可能  
  
  AK セグメントについては以下で説明します。 AK2 から AK5 のループのセグメントは、トランザクション セットでのエラーについての情報を提供します。  
  
## <a name="ak1"></a>AK1  
 AK1 セグメント (必須) は、次のデータ要素を使用して、確認する機能グループを識別します。  
  
-   AK101 は、確認する機能グループの機能グループ ID (GS01) です。  
  
-   AK102 は、確認する機能グループのグループ制御番号 (GS06 および GE02) です。  
  
-   AK103 は省略可能であり、元のトランザクションの GS08 で送信された EDI 実装のバージョンです。 AK103 は受信 5010 準拠の 997 をサポートします。  
  
## <a name="ak2"></a>AK2  
 AK2 セグメント (省略可能) には、受信した機能グループ内のトランザクション セットの受信確認が含まれます。 複数の AK2 セグメントが存在する場合、これらのセグメントは一連のループとして送信されます。 各 AK2 ループは、受信順にトランザクション セットを識別します。 AK2 セグメントは、次の 2 つのデータ要素を使用してトランザクション セットを識別します。  
  
- AK201 は、確認するトランザクション セットのトランザクション セット ID (ST01) です。  
  
- AK202 は、確認するトランザクション セットのトランザクション セット制御番号 (ST02 および SE02) です。  
  
- AK203 は省略可能であり、元のトランザクションの ST03 で送信された EDI 実装のバージョンです。 AK203 は受信 5010 準拠の 997 をサポートします。  
  
  トランザクション セットがエラーの場合、AK2 ループには AK3、AK4、および AK5 セグメントが含まれます。 詳細については、これらのセグメントに関する以下の説明を参照してください。  
  
  承諾または拒否された、またはのみのトランザクション セットを拒否するかどうか、すべてのトランザクション セットの AK2 セグメントが生成されることを指定できます。 BizTalk Server は受理されたトランザクション セットの AK2 セグメントが生成されます (ここ AK501 A を = =) を選択した場合、**受理されたトランザクション セットの AK2 ループを含める** チェック ボックス、**受信確認**のページ、2 つのビジネス プロファイル間のアグリーメントのアグリーメントのプロパティ ダイアログ ボックス (または**受信確認**ページの X12 のビジネス プロファイルの設定 タブ)。 それ以外の場合は、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は拒否されたトランザクション セットについてのみ AK2 ループを生成します。 アグリーメントが応答対象のインターチェンジに解決されない場合、997 の生成の設定は既定でフォールバック アグリーメントの設定になり、受理されたトランザクション セットの AK2 セグメントは生成されません。  
  
## <a name="ak3"></a>AK3  
 AK3 セグメント (省略可能) は、データ セグメント内のエラーおよびそのデータ セグメントの場所を報告します。 AK3 セグメントは、エラーを含むトランザクション セットのセグメントごとに作成されます。 複数の AK3 セグメントが存在する場合、これらのセグメントは一連のループ (1 ループに 1 セグメント) として送信されます。 AK3 セグメントには、エラーを含む各セグメントの場所を示す 4 つのデータ要素があり、その場所で見つかった構文エラーの種類を報告します。  
  
-   AK301 は、X12 セグメント ID (NM1 など) を使用して、エラーを含むセグメントを識別します。  
  
-   AK302 は、エラーを含むセグメントのセグメント カウントです。 ST セグメントは 1 で、セグメントごとにセグメント カウントが 1 ずつ増えます。  
  
-   AK303 は境界のあるループを識別します。 LS セグメントと LE セグメントで囲まれたループします。 AK303 には、エラーを含むセグメントの範囲を示す LS セグメントと LE セグメントの値が含まれます。  
  
-   AK304 は、データ セグメントのエラーに対応するエラー コードです。 AK304 は省略可能です。ただし、識別されたセグメントにエラーが存在する場合は、必須です。 AK304 のエラー コードの一覧は、次を参照してください。 [X12 997 受信確認エラー コード](../core/x12-997-acknowledgment-error-codes.md)します。  
  
## <a name="ak4"></a>AK4  
 AK4 セグメント (省略可能) は、データ要素または複合データ構造体のエラーを報告し、そのデータ要素の場所を示します。 このセグメントは、AK304 データ要素が 8 (セグメントでデータ要素エラーが発生しています) の場合に送信されます。 1 つの AK3 セグメント内で、最大 99 回まで繰り返すことができます。 AK4 セグメントには、エラーを含むデータ要素または複合データ構造体の場所を示す 4 つのデータ要素があり、その場所で見つかった構文エラーの種類を報告します。  
  
-   AK401 は、フィールド AK41.1、AK41.2、および AK41.3 複合データ要素です。 AK401-1 は、数値カウントを使用して、エラーを含むデータ要素または複合データ構造体を識別します。 たとえば、セグメントの 2 番目のデータ要素にエラーが含まれている場合は、AK401 が 2 になります。 AK401-2 は、エラーを含む複合データ構造体のコンポーネント データ要素の数値カウントを識別します。 AK401 で非複合データ構造体のエラーを報告する場合は、AK401-2 に値が設定されません。  
  
     AK41.3 は省略可能であり、繰り返されるデータ要素の位置です。 AK41.3 は受信 5010 準拠の 997 をサポートします。  
  
-   AK402 は省略可能です。エラーを含む要素の単純な X12 データ要素番号を識別します。 たとえば、NM101 の単純な X12 データ要素番号は 98 です。  
  
-   AK403 は必須です。識別された要素のエラーを報告します。 AK403 のエラー コードの一覧は、次を参照してください。 [X12 997 受信確認エラー コード](../core/x12-997-acknowledgment-error-codes.md)します。  
  
-   AK404 は省略可能です。エラーを含む、識別されたデータ要素のコピーが含まれます。 文字が無効であることを示すエラーの場合、AK404 は使用されません。  
  
## <a name="ak5"></a>AK5  
 AK5 セグメントは、AK2 セグメントで識別されたトランザクション セットが受理されるか、拒否されるか、およびその理由を報告します。 AK2 ループ (省略可能) が受信確認に含まれる場合は、AK5 セグメントが必須です。 AK5 セグメントには、トランザクション セットの状態を示す 1 個の必須データ要素、およびトランザクション セットの構文編集に基づくエラー コードを示す、1 ～ 5 個の省略可能なデータ要素があります。  
  
-   AK501 は、識別されたトランザクション セットが受理されるか、拒否されるかを示します。 AK501 のエラー コードの一覧は、次を参照してください。 [X12 997 受信確認エラー コード](../core/x12-997-acknowledgment-error-codes.md)します。  
  
-   AK502 ～ AK506 は、エラーの性質を示します。 AK501 のエラー コードの一覧は、次を参照してください。 [X12 997 受信確認エラー コード](../core/x12-997-acknowledgment-error-codes.md)します。  
  
## <a name="ak9"></a>AK9  
 AK9 セグメント (必須) は、AK1 セグメントで識別された機能グループが受理されるか、拒否されるか、およびその理由を示します。 AK9 セグメントには、トランザクション セットの状態とエラーの性質を示す 4 個の必須データ要素、および検出されたエラーを示す 1 ～ 5 個の省略可能な要素があります。  
  
-   AK901 は必須です。AK1 で識別された機能グループが受理されるか、拒否されるかを示します。 AK901 のエラー コードの一覧は、次を参照してください。 [X12 997 受信確認エラー コード](../core/x12-997-acknowledgment-error-codes.md)します。  
  
-   AK902 は、識別された機能グループ トレーラ (GE01) に含まれるトランザクション セット数を示します。  
  
-   AK903 は、受信されたトランザクション セットの数を示します。  
  
-   AK904 は、識別された機能グループ内で受理されたトランザクション セット数を示します。  
  
-   AK905 ～ AK909 は、識別された機能グループで検出された 1 ～ 5 個のエラーを示します。 AK905 ~ AK909 のエラー コードの一覧は、次を参照してください。 [X12 997 受信確認エラー コード](../core/x12-997-acknowledgment-error-codes.md)します。  
  
## <a name="see-also"></a>参照  
 [X12 997 受信確認エラー コード](../core/x12-997-acknowledgment-error-codes.md)