---
title: SWIFT と受信のバッチを逆アセンブル |Microsoft Docs
description: 受信メッセージを受け取ったし、BizTalk Server で、SWIFT アクセラレータを使用してバッチ処理用のスキーマをカスタマイズします。
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 11cb5672-1155-4648-b1fd-c9a3bc30e351
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: f234ca9c867d978216972f8359c77de88aeebfa8
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36976243"
---
# <a name="disassemble-inbound-batches"></a>受信バッチを逆アセンブルします。

## <a name="debatch-inbound-message"></a>受信メッセージを受け取った
SWIFT 逆アセンブラーは、受信のバッチ解除することを処理するか (ファイルまたは複数の SWIFT メッセージを含むメッセージ) の受信のバッチを逆アセンブルできます。 同じ名前の SWIFT 逆アセンブラーの構成プロパティを使用して受信バッチ解除を有効にするとします。 受信バッチ解除を有効にすると、SWIFT 逆アセンブラーは SWIFT の複数のメッセージを含むバッチを受信したすべてのメッセージが必要です。 バッチがバッチのエンベロープ (バッチ ヘッダーおよびトレーラー バッチ) を含めることはできず、各 SWIFT メッセージのバッチ内でメッセージのエンベロープ (メッセージ ヘッダーとメッセージ トレーラー) を含めることはできません。 SWIFT 逆アセンブラーの次の構成プロパティを使用してこれらのバッチ属性 (形式) を構成できます。  
  
- バッチ ヘッダー スキーマ  
  
- バッチのトレーラー スキーマ  
  
- メッセージ ヘッダーのスキーマ  
  
- メッセージのトレーラー スキーマ  
  
  > [!NOTE]
  >  これらのプロパティを"None"のいずれかを設定すると、受信のバッチにその特定の部分が含まれていないことを示します。  
  
  SWIFT 逆アセンブラーでは、次のような構造にすべての受信バッチが必要です。  
  
  **バッチ ヘッダー**  
  
  **メッセージ ヘッダー**  
  
  **SWIFT のインターチェンジ メッセージ (SWIFT ブロックの 1 ~ 5)**  
  
  **メッセージのトレーラー**  
  
  **バッチのトレーラー**  
  
  この構造内で「メッセージ ブロック」を考慮することができますを **– SWIFT インターチェンジ – メッセージ ヘッダー メッセージのトレーラー**部分。 一連の複数の「メッセージ ブロック」は、複数の SWIFT メッセージのバッチで構成します。 バッチ ヘッダー、メッセージのヘッダー、メッセージのトレーラー、およびトレーラーのバッチは省略可能ですが、繰り返しの間で一貫性のあるである必要があります。  
  
> [!NOTE]
>  SWIFT ヘッダーおよびトレーラのブロックとメッセージのエンベロープ (メッセージ ヘッダーとメッセージ トレーラー) を混同しないでください。 バッチのコンテキストでは、SWIFT ヘッダーおよびトレーラのブロックを含む包括的な (アトミック) の単位として SWIFT メッセージ (インターチェンジ) を表示する必要があります。 このコンテキストでメッセージ ヘッダーとトレーラーのメッセージは、バッチ内で各 SWIFT メッセージをラップするエンベロープを参照してください。  
  
 この構造体、オプション、およびその再現性を正式に express を検討してください。 どの[!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]バッチを定義します。  
  
- **バッチ ヘッダー**で表される**BH**  
  
- **メッセージのヘッダー**で表される**MH**  
  
- **インターチェンジの SWIFT**で表される**SI**  
  
- **メッセージのトレーラー**で表される**MT**  
  
- **トレーラーのバッチ**で表される**BT**します。  
  
  予期されるバッチの構造を表す式は次のとおりです。  
  
  `[BH] ([MH] SI [MT])* [BT]  `
  
  角かっこ ( `[ ] ` ) の一部が省略可能であることを示します。 アスタリスク (**\\* * *)、ブロックが繰り返し可能であることを示します。すべてのユーザーのビルド メッセージのバッチ メッセージ ヘッダーを使用する必要があります (*<em>MH</em>*) とトレーラー (*<em>MT</em>*) の各繰り返しで一貫して (`[MH] SI [MT]`)。  
  
  SWIFT 逆アセンブラーは、構造内の各部分は、フラット ファイル スキーマに準拠しているために、上記の構造に従うすべての受信バッチを処理できます。 ただし、省略可能なバッチ ヘッダー/トレーラーとメッセージのヘッダー/トレーラーを使用しない場合、メッセージはこれらのスキーマに従っていません。 その結果、連続する SWIFT メッセージのみを含むバッチには、バッチ ヘッダー スキーマ、トレーラー スキーマのバッチ、メッセージ ヘッダー スキーマ、およびメッセージ トレーラー スキーマ プロパティが"None"に設定があります。  

## <a name="customize-schemas-for-batching"></a>バッチ処理用のスキーマをカスタマイズします。  
 バッチ ヘッダー/トレーラーとメッセージのヘッダーとトレーラーのスキーマをカスタマイズすることができます。 例では、次のバッチを示します。  
  
```  
4  
SWIFT Message # 1  
$  
SWIFT Message # 2  
$  
SWIFT Message # 3  
$  
SWIFT Message # 4  
$  
```  
  
 この種類のバッチを処理するには、ように、バッチ スキーマのプロパティを設定は。  
  
- 復帰で区切られた 1 つの数値 (メッセージ数) を解析するフラット ファイル スキーマを取得するには、バッチ ヘッダー スキーマ プロパティを設定します。  
  
- メッセージのトレーラー スキーマを 1 つの $ 記号と復帰を解析するフラット ファイル スキーマに設定します。  
  
- 残りのエンベロープ スキーマ (バッチ トレーラー スキーマおよびメッセージ ヘッダーのスキーマ) は、None に設定します。  
  
  SWIFT 逆アセンブラーを作成し、適切なエンベロープをフラット ファイル スキーマの組み合わせを指定する任意の SWIFT メッセージ バッチを処理するよう構成できます。 この機能は、非常に柔軟性があります。  
  
  SWIFT 逆アセンブラーは、常に、途中でエラーが発生した場合でも、バッチ全体の処理を完了しようとします。 これにより、収集し、すべて一度にできるだけ多くのエラーを報告することができます。 この「ベスト エフォート」を実行するには、ヒューリスティック、SWIFT 逆アセンブラーください特定の決定と仮定新しいパーツを検出したときに使用するスキーマを選択するときに、または解析エラーが発生した場合。 適切なスキーマを選択することはできません常に、解析エラーとエンベロープ スキーマと SWIFT インターチェンジ スキーマ間のあいまいさ/類似性の場所と性質によって異なります。 場合によっては、適切に設計されたエンベロープ スキーマを使用して、間違ったスキーマを選択した場合の可能性を最小限に抑えることができます。 逆アセンブラーに致命的な解析エラーが発生した場合は、逆アセンブラーは、正しいスキーマを決定できません、逆アセンブラーでは、残りのデータを処理することがなく、バッチは失敗します。  
  
  ときに**受信バッチ解除処理**は**有効になっている**(に設定**True**)、SWIFT 逆アセンブラーは、バッチのエンベロープ (バッチ ヘッダー スキーマの指定されたスキーマを使用してバッチを解析します。およびバッチ トレーラー スキーマ) とメッセージのエンベロープ (メッセージ ヘッダーのスキーマおよびメッセージのトレーラー スキーマ) だけでなく、バッチ内の SWIFT メッセージ (インターチェンジ) を解析するために指定されたスキーマです。 SWIFT メッセージ バッチのでは、メッセージの種類とスキーマに動的に検出でき (SWIFT ヘッダー スキーマを指定する) を 1 つのバッチ以外のメッセージと同じ方法で読み込まれます。 SWIFT 逆アセンブラーがスキーマの解決を実行する方法の詳細については、次を参照してください。[動的メッセージ型の探索とスキーマの解決](../../adapters-and-accelerators/accelerator-swift/dynamic-message-type-discovery-and-schema-resolution.md)します。  
  
  SWIFT 逆アセンブラーは、解析し、各 SWIFT メッセージの受信のバッチを個別に検証します。 シーケンス処理する次のバッチを実行します。  
  
1. バッチ ヘッダーのスキーマを指定した場合は、バッチ ヘッダーを解析します。  
  
2. メッセージ ヘッダーのスキーマを指定した場合は、メッセージのエンベロープのヘッダーを解析します。  
  
3. SWIFT のインターチェンジ (メッセージ) を解析します。  
  
4. XML 検証を有効にした場合は、XML の制約に照らして SWIFT メッセージを検証します。  
  
5. BRE の検証を有効にした場合は、BRE ポリシー (SWIFT ネットワークと使用状況規則) に対して SWIFT メッセージを検証します。  
  
6. メッセージのトレーラー スキーマが指定されている場合は、メッセージのエンベロープのトレーラーを解析します。  
  
7. 逆アセンブラーでは、バッチには、メッセージをそれ以上が見つからないまでは、手順 2. を 6 に繰り返されます。  
  
8. バッチのトレーラー スキーマを指定した場合は、バッチのトレーラーを解析します。  
  
   バッチ データを解析し、次の SWIFT 逆アセンブラーの構成プロパティを使用して検証を別の作業を行う SWIFT 逆アセンブラーを構成することができます。  
  
- **断片化**かどうか SWIFT 逆アセンブラー発行各メッセージ バッチをメッセージ ボックス データベースで個別にプロパティを決定します (つまり、メッセージごとに、上記の手順 6 のそれぞれの発生後の)、またはその必要がありますすべての手順 1 ~ 8 とのネイティブ形式 (入力の正確なコピー)、メッセージ ボックス データベースに 1 つのメッセージ、バッチ全体を公開します。 設定する**断片化**に**True**を断片化を有効にし、バッチからのメッセージを個別に発行します。 設定する**断片化**に**False**断片化を無効にし、バッチ全体を処理した後にのみ、1 つのメッセージとしてネイティブ形式で、バッチ全体を公開します。 通常、設定**断片化**に**無効**な場合は、必要なだけ BizTalk Accelerator for SWIFT の ([!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]) を解析し、受信バッチと失敗、または転送するには、いずれかを検証するには同じフォームを[!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]それらを受信します。 通常、設定した**断片化**に**有効**ようにするシナリオ[!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]を変換または解析と検証した後、またはしたい場合は、バッチ内のメッセージを変更[!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]を内容と異なる順序にバッチ内のメッセージを再度並べ替える[!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]最初に受信します。 設定することも**断片化**に**有効**のシナリオが異なるの最終的な送信先のメッセージが受信のバッチに含まれています。  
  
- **バッチ ヘッダーの保存]、[バッチのトレーラーを保持する**SWIFT 逆アセンブラーを破棄する必要がありますか、またはそれを解析した後、バッチのエンベロープ (ヘッダーとトレーラー) データを保持するかどうか、プロパティが決定します。 設定した場合**バッチ ヘッダーを保持またはバッチのトレーラーを保持する**に**True**、逆アセンブラーは、個々 のメッセージとしてメッセージ ボックス データベースに対応するバッチの一部 (解析された XML) を公開します。 逆アセンブラーは、マルチパート メッセージのボディ部で、データを発行します。 逆アセンブラーは、特別なコンテキスト プロパティを昇格させます。 ように[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]がバッチ内の序数の位置と、元のバッチにこれらのメッセージを関連付けることができます (バッチ ヘッダーの最初の位置、トレーラーのバッチの最後の位置)。 設定した場合**バッチ ヘッダーを保持またはバッチのトレーラーを保持する**に**False**、逆アセンブラーは、解析後に対応するバッチの一部 (解析されたデータ) を破棄します。  
  
  > [!NOTE]
  >  これらの構成プロパティは、断片化が有効になっている場合にのみ有効です (**断片化**に設定**True**)。 情報保持の設定は関連しませんので、逆アセンブラーが、メッセージ ボックス データベースへのネイティブ形式で、バッチ全体の正確なコピーを発行断片化を無効にすると、(*すべて*は保持されます)。  
  
- **メッセージ ヘッダーを保持する** / **メッセージ トレーラーの保持**プロパティは、SWIFT 逆アセンブラーを破棄する必要がありますか、またはメッセージのエンベロープ (メッセージ ヘッダーとトレーラー) を保持するかどうかを決定します。後に、それらを解析します。 設定した場合**メッセージ ヘッダーの保存または保持するメッセージのトレーラー**に**True**、逆アセンブラーは、メッセージ ボックス データベースに対応するバッチの一部 (解析された XML) を発行*と共に、ラップして個々 の SWIFT メッセージ*します。 逆アセンブラーでメッセージのエンベロープのヘッダーを公開する、**ヘッダー**マルチパート メッセージの一部です。 逆アセンブラーでメッセージのエンベロープのトレーラーの発行、**トレーラー**マルチパート メッセージの一部です。 逆アセンブラーでメッセージのエンベロープに含まれている SWIFT のメッセージを発行する、**本文**同じマルチパート メッセージの一部です。 逆アセンブラーは、特別なコンテキスト プロパティを昇格させます。 ように[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]、元のバッチとバッチ内の序数位置にこれらのメッセージを関連付けることができます。 設定した場合**メッセージ ヘッダーの保存または保持するメッセージのトレーラー**に**False**、逆アセンブラーは、解析後に対応するバッチの一部 (解析されたデータ) を破棄します。  
  
  > [!NOTE]
  >  これらの構成プロパティは、断片化が有効になっている場合にのみ有効です (**断片化**に設定**True**)。 情報保持の設定は関連しませんので、逆アセンブラーが、メッセージ ボックス データベースへのネイティブ形式で、バッチ全体の正確なコピーを発行断片化を無効にすると、(*すべて*は保持されます)。  
  
  各構成プロパティの詳細についてと、その他の使用法と構成情報を参照してください。 [SWIFT 逆アセンブラーの構成プロパティ](../../adapters-and-accelerators/accelerator-swift/swift-disassembler-configuration-properties.md)します。 メッセージ ボックス データベースの発行とマルチパート メッセージの詳細については、BizTalk Server のヘルプを参照してください。  
  
## <a name="next-step"></a>次の手順
  
[バッチに関連する昇格プロパティ](batch-related-promoted-properties.md)
