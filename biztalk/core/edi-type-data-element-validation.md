---
title: "EDI の種類 (データ要素) の検証 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cd53685f-a49c-41c8-813e-29700fc0b62b
caps.latest.revision: "19"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 88a71a44c305e1eabbcdb9aede32b44439f6b03c
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="edi-type-data-element-validation"></a>EDI の種類 (データ要素) の検証
EDI 受信パイプラインと EDI 送信パイプラインは、トランザクション セット データ要素に対して EDI 検証を実行します。 この検証は上から、またはそのパーティとのアグリーメントのプロパティを通じて、特定のパーティにすべてのメッセージ用に構成された、**検証**ページ (下にある、**トランザクション セットの設定**x12 のいずれかのセクションまたは EDIFACT アグリーメント) で変更します。 場合、 **EDI 型の検証**でプロパティが選択されていない、**検証**ページで、データをこのトピックで説明した検証は実行されません。  
  
 選択する受信と送信メッセージの EDI の種類の検証が有効になっている、 **EDI の種類の検証**プロパティに、**検証**の双方向アグリーメントタブのページ**アグリーメントのプロパティ** ダイアログ ボックス。 受信メッセージと送信メッセージの両方で、このプロパティは既定で選択されているため、EDI の検証は既定で有効になっています。  
  
## <a name="validation-checks"></a>検証の確認  
 EDI 受信パイプラインまたは EDI 送信パイプラインが EDI の検証を実行するとき、以下の点が検証されます。  
  
-   スキーマの EDI プロパティで定義されたデータ型  
  
-   長さ制限  
  
-   空のデータ要素と後続の区切り文字  
  
    > [!NOTE]
    >  この検証では、コード セット (列挙) や、最小または最大の出現は検証されません。  
  
 **文字セット**  
  
 EDI データ要素の検証を行うために、EDI 受信パイプラインと送信パイプラインには、次のように文字セットを設定する必要があります。  
  
-   Edifact の場合、データ要素で、文字セットが確立**UNB1**の**文字セットと区切り記号**の一方向アグリーメント タブのページ、**アグリーメントのプロパティ**ダイアログ ボックスまたは**EDIFACT フォールバックの設定** ダイアログ ボックス (アグリーメントが設定されていない) 場合。  
  
-   データ要素の文字を確立、kedifact **UNB1**の**文字セットと区切り記号**の一方向アグリーメント タブのページ、**アグリーメントのプロパティ**ダイアログEDIFACT の場合と同様のボックスです。 値、 **UNB1.1**に要素を設定する必要があります`KECA`です。  
  
-   X12 では、メッセージの文字セットは、パイプライン プロパティで設定されます。  
  
    > [!NOTE]
    >  BizTalk ランタイムがメッセージの EDI 検証を実行する際には、パイプライン プロパティで選択された X12 文字セットが使用されます。 ただし、プロパティの検証がのページで入力、**アグリーメントのプロパティ** ダイアログ ボックスは、選択された文字セットでを使用して実行、**文字セットと区切り記号**そのダイアログ ボックスのページです。 実行時に、パイプラインは、値を無視 X12 文字セットのプロパティ**文字セットと区切り記号**のページ、**アグリーメントのプロパティ** ダイアログ ボックス。 これら 2 つの設定が同じでない場合 (つまり、X12 文字セット プロパティで、**アグリーメントのプロパティ** ダイアログ ボックスに設定されている**拡張**中に、パイプライン プロパティで設定されているに X12**基本**)、メッセージ検証エラーが発生する可能性があります。  
  
 **データ型の検証**  
  
 X12 では、受信パイプラインまたは送信パイプラインにおける逆アセンブラーまたはアセンブラー コンポーネントによる検証用に、Numeric、Decimal、Identifier、String、Date、Time、Binary、Composite の各 EDI データ型にスキーマ内で注釈が付いています。  
  
 EDIFACT では、受信パイプラインまたは送信パイプラインにおける逆アセンブラーまたはアセンブラー コンポーネントによる検証用に、Alphabetic、Numeric、Identifier、String、Composite の各 EDI データ型にスキーマ内で注釈が付いています。  
  
 **長さの制限**  
  
 X12 と EDIFACT の両方で、要素またはサブ要素の長さ (最小と最大) 要件を検証する必要があります。 長さは、使用されている文字位置の数として定義されます。 長さには、符号および小数点表記は含まれません。  
  
> [!NOTE]
>  X12_AN の文字列データ型では、最小長の要件を満たすために、どのセグメントでも先頭のスペースが保持され、後続のスペースが許可されます。  
  
 KECA では、長さはバイト数として解釈されます。 たとえば、長さが 3 と定義されている場合、要素またはサブ要素含めることができます 3 の 1 バイト文字または 1 つの 2 バイト文字と 1 つの 1 バイト文字の組み合わせのいずれか。  
  
 **空のデータ要素と末尾の区切り文字の検証**  
  
 X12 では、必須とマークされたデータ要素は、セグメントが存在する場合、インスタンス内で空であってはなりません。 データ要素が複合型である場合は、少なくとも 1 つのコンポーネント データ要素に値が格納されていることが必要です。  
  
 EDIFACT では、値のないデータ要素や条件付きのデータ要素 (およびサブコンポーネント) を除外できますが、区切り文字は保持されます。  
  
 X12 または EDIFACT のいずれでも、後続の区切り文字は必須ではありませんが、使用することを推奨します。  
  
## <a name="when-edi-type-validation-is-disabled"></a>EDI の種類の検証が無効になっている場合  
 EDI の種類の検証を無効にすると、EDI 受信パイプラインまたは EDI 送信パイプラインは、処理中のメッセージを中断することなく、EDI の種類の検証によってエラーがチェックされたデータ要素を処理します。  
  
> [!NOTE]
>  EDI の種類の検証が無効であっても、EDI の構造の検証は実行されます。 EDI の種類の検証が無効であっても、基本的な構造の検証でエラーとなったインターチェンジは中断されます。  
  
 メッセージが中断されることなく処理されるエラーには以下のようなものがあります。  
  
-   予期しないまたは未定義のトランザクション セット  
  
-   セグメント/ループおよびデータ要素レベルでの予期せぬデータまたは未定義のデータ  
  
-   セグメント/ループおよびデータ要素レベルでの任意選択 (最小と最大の出現)  
  
-   データ要素レベルでの長さ (最小/最大) 違反 (最大レベルを超える長さのデータまたは最小レベルを下回る長さのデータ)  
  
-   データ要素レベルでのデータ型の不一致 (ID データ型は独自の制御があるため除く)  
  
-   データ要素レベルでの無効な列挙リスト  
  
 EDI の種類の検証が受信側では無効になっており、送信側では有効になっている場合、XML ファイルにエラーが含まれていると、EDI の送信パイプラインは、受信パイプラインで生成された XML を再処理して有効な EDI ファイルを作成することができません。 その結果、送信パイプラインでエラーが発生します。  
  
 EDI の種類の検証が無効になっていると、EDI 受信パイプラインまたは送信パイプラインは以下のようにエラーを処理します。  
  
|||  
|-|-|  
|予期せぬデータ|操作|  
|予期せぬトランザクション セットまたは未定義のトランザクション セット|EDI 受信パイプラインまたは送信パイプラインは、スキーマが展開されていない場合でもトランザクション セットを受け付けます。|  
|予期せぬセグメントまたはレコード|受信パイプラインは、適切なプレフィックスを持つタグを生成: \<unexpectedsegment _ SegmentID % >。<br /><br /> 送信パイプラインは、XML タグ名の最初の 1 ～ 3 文字をセグメント名として使用します。|  
|予期せぬ単純なデータ要素|受信パイプラインは、プレフィックス、セグメント識別子、セグメント中のデータ要素の位置を表すインデックス <UnexpectedDataElement_%FieldName% の付いた XML タグを生成します。|  
|予期せぬ複合データ要素|受信パイプラインは、プレフィックス、セグメント識別子、セグメント中のデータ要素の位置を表すインデックス <UnexpectedCompositeDataElement_%FieldName% の付いた XML タグを生成します。|  
|必須データの不足|パイプラインはデータを省略可能として扱います。|  
|データ要素の長さ違反|パイプラインは無効なデータ要素の長さを有効として扱います (最小がゼロ、最大が無制限)。|  
|インスタンス内の無効な列挙値 (ID データ型に該当)|パイプラインはエラーを無視して処理を続行します。|  
|インスタンス内の最大出現違反|パイプラインはその反復データを有効として扱います (最小出現がゼロ、最大出現が無制限)。|  
  
 **[エラー報告]**  
  
 EDI の種類の検証を無効にすると、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] のイベント ビューアーではエラーは報告されませんが、警告は報告されます。 また、受信確認で Accept がソース パーティに報告されます。その際、X12 997 では AK501 および AK901 が "E" に設定され、EDIFACT CONTRL では UCI.4、UCM.3、UCF.4 が "7" に設定されます。 その結果、将来の送信で訂正される可能性が除去されます。 しかし、メッセージの受信者は、メッセージを拒否または中断するのではなく、手動で介入することによりドキュメントを復旧できる可能性があります。 また、EDI 受信パイプラインでこれらのエラーが発生すると、`Edi.ErrorsInTransactionSet` コンテキスト プロパティが昇格されます。 このプロパティは、EDI 検証エラーまたは拡張検証エラーが発生した場合は True として昇格されます。 エラーが発生しなかった場合は False として昇格されます。  
  
 受信パイプラインまたは送信パイプラインは、予期せぬデータを検出すると、親レベルでエラーを報告し、以下のように子レベルのエラーを無視します。  
  
|||  
|-|-|  
|予期せぬデータ|操作|  
|予期せぬトランザクション セット|受信確認でこのエラーが報告され、セグメント/ループおよびデータ要素レベルでの後続のエラーは無視されます。|  
|予期せぬセグメント/ループ|受信確認でこのエラーが報告され、データ要素レベルでのエラーは無視されます。|  
|予期せぬデータ要素|受信確認でこのエラーが報告され、ID、長さ、出現などのプロパティに関連する複合エラーと、複合データ要素フィールドに関するエラー (該当する場合) は無視されます。|  
  
## <a name="see-also"></a>参照  
 [EDI メッセージの検証](../core/edi-message-validation.md)   
 [拡張 (BTS-XSD) 検証](../core/extended-bts-xsd-validation.md)