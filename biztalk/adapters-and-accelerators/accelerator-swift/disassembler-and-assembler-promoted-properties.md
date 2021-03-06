---
title: 昇格させたプロパティの逆アセンブラーとアセンブラー |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- disassembler, promoted properties
- promoted properties, assembler
- promoted properties, disassembler
- assembler, promoted properties
ms.assetid: 342b0250-bdf7-45ce-8964-3aeda89989b1
caps.latest.revision: 4
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 7bd97789ef793b386cc9ce132db69f89adf8ecdb
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36977219"
---
# <a name="disassembler-and-assembler-promoted-properties"></a>昇格させたプロパティの逆アセンブラーとアセンブラー
逆アセンブラーとアセンブラーのプロパティが 2 つのカテゴリに分類されますルーティングとフィルタ リングのためのルーティング プロパティ。内部の処理のランタイム プロパティ。  
  
このトピックでは、追加、およびメッセージ ボックス データベースに SWIFT 逆アセンブラーによって公開されるすべてのメッセージの昇格されるプロパティの一覧を提供します。  
  
## <a name="routing-properties"></a>ルーティング プロパティ

SWIFT 逆アセンブラーは、ルーティングのプロパティを昇格させます。 これらのプロパティを使用して、コンテンツ ベースのルーティング (送信ポート フィルター) と、オーケストレーションでのフィルター処理を受信できます。  
  
|昇格させた名|説明|データ型|値の範囲|使用例|  
|-------------------|-----------------|---------------|-----------------|-------------------|  
|**A4SWIFT_BatchId**|SWIFT 逆アセンブラーが受信のバッチの処理時に動的に生成されるグローバルに一意の識別子。 逆アセンブラーは、同じバッチの送信元メッセージ ボックス データベースに公開されたすべてのメッセージにこのバッチ識別子を割り当てます。<br /><br /> 設定 **-1**の 1 つのメッセージ (受信のバッチから発信されていない)。|String|「-1」または*グローバル一意識別子 (GUID)*|同じメッセージを関連付ける**A4SWIFT_BatchId**受信した最初を同じバッチにグループ化する値。|  
|**A4SWIFT_BreValidationErrors**|ビジネス ルール エンジン (BRE) の検証中に発生した検証エラーの数を示します。|数値|>= 0|BRE の検証は失敗しなかったメッセージのフィルター (**A4SWIFT_BREValidationErrors**は 0 になります)。|  
|**A4SWIFT_Failed**|メッセージ (解析と検証) を処理中にエラーが発生したかどうかを示します。 設定**True**場合**A4SWIFT_ParseErrors** + **A4SWIFT_XmlValidationErrors** + **A4SWIFT_BreValidationErrors** > 0。|ブール値|True、False|SWIFT メッセージの唯一の有効なフィルター (**A4SWIFT_Failed** equals **False**)。|  
|**A4SWIFT_ParseErrors**|解析中に発生した解析エラーの数を示します。|数値|>= 0|解析は失敗しなかったメッセージのフィルター (**A4SWIFT_ParseErrors**は 0 になります)。|  
|**A4SWIFT_PosInBatch**|受信のバッチから発信されるメッセージの位置を表す序数を示します。 含むバッチの*n*メッセージ、 **A4SWIFT_PosInBatch**を 1 から値を受け取ります*n*メッセージのバッチ内の序数の位置に対応します。<br /><br /> 設定**0**メッセージがバッチ ヘッダーの場合。<br /><br /> 設定**n+1**メッセージがバッチ トレーラーである場合。<br /><br /> 設定**1**メッセージ自体が全体のバッチ (バッチの断片化を無効になっている) 場合。<br /><br /> 設定 **-1**の 1 つのメッセージ (受信のバッチから発信されていない)。|数値|>= -1|同じ受信バッチからのメッセージを受信した元の順序に並べ替えます。|  
|**A4SWIFT_XmlValidationErrors**|XML の検証中に発生した検証エラーの数を示します。|数値|>= 0|XML の検証は失敗しなかったメッセージのフィルター (**A4SWIFT_XmlValidationErrors**は 0 になります)。|  
  
> [!NOTE]
>  通常は、すべてのルーティングやフィルター式を評価する必要があります**A4SWIFT_Failed**その他のルーティング プロパティを評価する前にします。 のみ**A4SWIFT_Failed**昇格させた、使用できるようにすることが保証されます。 有効な単一メッセージ (メッセージのバッチ以外)、メッセージ ボックス データベースに公開の残りのプロパティが利用できません。 その他のプロパティの昇格のみ*できませんでした*1 つのメッセージをバッチのメッセージ (有効または失敗)。  

## <a name="runtime-properties"></a>ランタイム プロパティ

SWIFT 逆アセンブラーは、ランタイム プロパティを昇格し、内部プロセスの実行時にそれらを使用します。 これらはのみ昇格させたと、コンテキストに応じて、いくつかの条件にルーティング可能です。 一般に、ルーティングやフィルター処理はこれらのプロパティを使用しないでください。 昇格させた、使用できるようにすることは保証されません。 一部のシナリオでは、取得またはルーティングのプロパティを使用してフィルター処理の後にこれらのプロパティを検査できます。 次の表は、ランタイム プロパティを一覧表示します。  
  

|           昇格させた名            |                                                                                                                                                                                                                                                                                                                                                                                                            説明                                                                                                                                                                                                                                                                                                                                                                                                             | データ型 |      値の範囲       |                                                                           使用例                                                                           |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **A4SWIFT_IsMessageHeaderValued**  |                                                                                                                                                                                                                                                                                               マルチパート メッセージのヘッダー部にデータが存在するかどうかを示します。 設定**True**ヘッダー部分には、データ (メッセージのバッチから受信したメッセージをエンベロープ ヘッダー) が含まれている場合。 設定**False**ヘッダー部分が空の場合。                                                                                                                                                                                                                                                                                                |  ブール値  |      True、False       |                        (たとえば、メッセージの修復オーケストレーション) で取得したメッセージのヘッダー部分を検査するかどうかを決定します。                         |
| **A4SWIFT_IsMessageTrailerValued** |                                                                                                                                                                                                                                                                                             マルチパート メッセージのトレーラー部にデータが存在するかどうかを示します。 設定**True**トレーラー部には、データ (メッセージをバッチから受信したメッセージのエンベロープ トレーラー) が含まれている場合。 設定**False**トレーラー部が空の場合。                                                                                                                                                                                                                                                                                              |  ブール値  |      True、False       |                        (たとえば、メッセージの修復オーケストレーション) で取得したメッセージのトレーラー部を検査するかどうかを決定します。                        |
|      **A4SWIFT_MessageType**       |                                                                                                                                                                                                                                                                                                                                                                     メッセージの種類を示す、SWIFT、SWIFT ヘッダー 3 桁の数字 (**MT\*xxx**\*)。                                                                                                                                                                                                                                                                                                                                                                      |  String   | *3 桁の数字* |                                                     SWIFT メッセージの種類のメッセージを動的に識別します。                                                     |
|      **A4SWIFT_MessageType2**      |                                                                                                                                                                                                                                                                                                                              メッセージの種類を示す、SWIFT、SWIFT ヘッダー 3 桁の数字 (**MT\*xxx**<em>)。場合にだけ使用\* \*A4SWIFT_MessageType</em> \* SWIFT ヘッダーに含まれていません。                                                                                                                                                                                                                                                                                                                              |  String   | *3 桁の数字* |                                                     SWIFT メッセージの種類のメッセージを動的に識別します。                                                     |
|     **A4SWIFT_NumberOfParts**      | マルチパート メッセージ内の部分の数を示します。<br /><br /> 設定**1**ボディ部では、(バッチ、またはバッチ ヘッダーまたはバッチのエンベロープからバッチ トレーラーから発信されていない、有効な各 SWIFT メッセージを含む) が存在する場合のみです。<br /><br /> 設定**2**かどうか本文とエラーの部分に (ボディ部が失敗したメッセージまたは XML エラーのコレクションを格納しているエラーの部分のバッチを含む) が存在します。<br /><br /> 設定**3**本文、ヘッダー、およびトレーラーの部分が有効な個々 の SWIFT メッセージを使用し、含んでいるメッセージのトレーラー場合のヘッダー部分包含メッセージ エンベロープ ヘッダー、バッチ送信元を格納している (ボディ部を存在するかどうかエンベロープのトレーラーを使用する場合: **A4SWIFT_IsMessageHeaderValued**と**A4SWIFT_IsMessageTrailerValued**ヘッダーとトレーラーの部分にデータが存在するかどうかを示します)。 |  数値  |        1, 2, 3         | メッセージ部分の指定した数のフィルター (たとえばのフィルター **A4SWIFT_NumberOfParts**等しい 2 つのメッセージ修復のオーケストレーションの受信図形)。 |
|  **A4SWIFT_SecondaryMessageType**  |                                                                                                                                                                                                                                                                                                                                                                    SWIFT ヘッダー、SWIFT を示す文字列値をメッセージのサブタイプ (**MT\*xxx_XYZ**\*)。                                                                                                                                                                                                                                                                                                                                                                    |  String   |      *任意の文字列*      |                                                   メッセージの SWIFT メッセージのサブタイプを動的に識別します。                                                    |
 
## <a name="see-also"></a>参照  
[A4SWIFT_* 昇格プロパティ](../../adapters-and-accelerators/accelerator-swift/a4swift-promoted-properties.md)   