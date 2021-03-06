---
title: EDI セグメントの構造体要素 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1f474a3d-004a-4981-b155-b0a5775918ba
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5b05d7a793fe515b8d0254d63b9b96994ddb35d9
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22242218"
---
# <a name="edi-segment-structural-element"></a>EDI セグメントの構造要素
セグメントは、メッセージの情報の中間単位であり、1 つ以上のデータ要素を含んでいます。 各セグメントは、3 文字のデータ セグメント識別子で始まり、セグメント終端記号 (既定ではアポストロフィ (')) で終わります。 セグメント内のデータ要素は、データ要素区切り記号で区切られます。 既定のデータ要素区切り記号は正符号 (+) です。 セグメントは、必須セグメントまたは省略可能なセグメントに分類されます。 送信インターチェンジの区切り記号は、2 つの取引先間のアグリーメントで設定するか、フォールバック取引先アグリーメントの一部として設定することができます。  
  
## <a name="nesting"></a>入れ子  
 セグメントと呼ばれる階層関係でグループ化する**入れ子**です。 入れ子の 2 つの別個の型がある: 明示的および暗黙的なです。 1 つのインターチェンジでは、1 つの種類の入れ子のみ使用できます。  
  
-   明示的な入れ子では、ループが入れ子にされることが明示的に示されます。 明示的な入れ子が使用される場合、セグメント タグ内の最初のコンポーネント データ要素はセグメント コードになります。 次に、セグメントの繰り返しのレベルと発生頻度を示す条件コンポーネント データ要素が続きます。 この目的で使用されるコンポーネント データ要素の数は、メッセージの構造においてセグメントが表示される階層レベルによって決まります。 セグメントがレベル 1 に表示される場合は、セグメント コードの直後のコンポーネント データ要素が使用されます。 セグメントがレベル 2 に表示される場合は、セグメント コードの直後のコンポーネント データ要素とその次のコンポーネント データ要素が使用されます。 セグメントがレベル 3 に表示される場合は、セグメント コードの直後にある 3 つのコンポーネント データ要素が使用されます。 パイプラインでは、データを階層と比較して構造的な検証を行うことができません。  
  
-   暗黙的な入れ子では、メッセージ構造で指定されたセグメントの順序が厳密に守られます。 セグメント間の入れ子関係は暗黙的に明らかであり、処理の実行のために入れ子関係を明示的に示す必要はありません。  
  
## <a name="loops"></a>ループ  
 1 つまたは複数のセグメントとして繰り返すことができます、**ループ**トランザクション内に設定します。 ループの 2 つの種類があります: 制限および制限します。  
  
### <a name="unbounded-loops"></a>境界のないループ  
 境界のないループには、ループの開始と終了を示す一意の識別セグメントがありません。 境界のないループは、カウントに従って繰り返されます。 カウントの値が設定されていない場合、ループは 2 回繰り返されます。 ループ内の各セグメントは、指定された順序で 1 回だけ出現できます。  
  
 境界のないループの開始は、一意である最初のデータ要素によって設定されます。 最初の要素は、各発生箇所で 1 回だけ出現できます。 境界のないループは、ループ内に入れ子にできます。入れ子にした場合、内側の境界のないループは、外側のループと同じ序数位置で開始できず、外側のループと同じセグメント ID で開始できません。 入れ子になったループは、同じ入れ子構造で外側のループの開始セグメントであるセグメントを含むことができません。  
  
### <a name="bounded-loops"></a>境界のあるループ  
 境界のあるループは、定義済みセグメントの LS (ループ開始) で始まり、定義済みセグメントの LE (ループ終了) で終わります。 LS セグメントが省略可能かどうかの指定は、ループ内の最初のセグメントと一致している必要があります。 境界のあるループは、別の境界のあるループを含むことができます。  
  
> [!NOTE]
>  X12 における境界のあるループと EDIFACT における明示的なループは同じものを指します。  
  
 ループでは、あいまいさを解決するのにバインドが使用されます。 LS/LE セグメントの要件指定子は、ループの最初のセグメントの要件指定子と一致します。 バインドによって、よく繰り返される特定のセグメントの使用に課せられる構造的な制約が緩和されます。 境界のあるループには、開始セグメント ID についての制約がありません。 これにより、次の例のように、同じセグメントを、境界のあるループの開始で使用すると同時に、ループの外側でも使用することができます。  
  
```  
AA  
LS  
BB  
CC  
LE  
BB  
```  
  
 下位のループ (ループ内のループ) を使用できます。 境界のあるループがループ内で入れ子にされている場合、内側のループは外側のループと同じ序数位置で開始できません。 内側の境界のあるループは、そのすぐ外側のループより前に終了する必要があります。  
  
 トランザクション セット内の境界のあるループにそれぞれ 1 ～ 4 文字の大文字または数字から成る一意の <loop_id> 値を割り当てる必要があります。 対応する LS セグメントと LE セグメントの <loop_id> 値に同じ一意の値を割り当てることを推奨します。 < Loop_id > データ要素は、データ型、最小/最大長、フィールドなどの検証し、「標準」のデータ要素として処理されます。(LS および LE) 経由でクロス セグメント検証は行われません。BizTalk Server は、LS および LE セグメントが存在するかどうかのみに基づいてあいまいさの解決を検証します。 データ要素の規則に違反する場合、トランザクション セットはエラーありで受理され、BizTalk Server からの ACK では AK501=E および該当する評価が AK2/AK3 で返されます。  
  
 LS/LE セグメントの組み合わせを強制することも必要です。 一致しない場合、トランザクション セットは内在するあいまいさ解決の問題が理由で拒否され、イベント ビューアーおよび 997 ACK では AK501 = E と AK502 = 5 が返されます。 LS/LE セグメントのどちらか一方または両方がなく、トランザクション セットがあいまいでない場合、トランザクション セットはエラーありで受理され、AK501 = E と AK502 = 5 が返されます。  
  
 LS/LE の組み合わせは、省略可能または必須にできます。 ただし、この組み合わせは、繰り返し可能な上位のループに含まれていない場合は繰り返し可能ではありません。 どちらの場合も、LS/LE の組み合わせの MaxOccurs は両方とも 1 にできますが、1 より大きくすることはできません。これは、スキーマの検証で強制されます。  
  
 LS および LE セグメントは、EDI 逆アセンブラーと EDI アセンブラーで処理されます。 解析中、逆アセンブラーは LS および LE セグメントの XML ノードを作成し、これらのセグメントを検証します。 シリアル化中、アセンブラーは XML ノードから LS および LE セグメントを作成し、これらのセグメントを検証します。 必要な ls または LE セグメントが不足している場合、トランザクション セットは AK501 で中断/拒否 = E と AK502 = 5。 LS/LE セグメントが存在せず、対応するデータ要素と、EDI 検証が有効になっている、トランザクション セットは受け入れられますエラーと、AK501 = E と AK502 = 5 は、イベント ビューアーおよび 997 で報告される確認