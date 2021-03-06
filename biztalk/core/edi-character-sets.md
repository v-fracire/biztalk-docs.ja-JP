---
title: EDI 文字セット |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 57fae748-d66e-4ecf-be00-70147078ef93
caps.latest.revision: 22
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 38d7b19c751f2bd380dad29ffc31a2be5f79245e
ms.sourcegitcommit: 5abd0ed3f9e4858ffaaec5481bfa8878595e95f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2017
ms.locfileid: "25971392"
---
# <a name="edi-character-sets"></a>EDI 文字セット
[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、文字セットを使用して EDI インターチェンジ全体を検証します。 X12 でエンコードされたメッセージに使用される文字セットと、EDIFACT または KEDIFACT でエンコードされたメッセージに使用される文字セットは、異なる方法で決定されます。  
  
## <a name="edifact-character-set"></a>EDIFACT 文字セット  
 EDIFACT エンコード インターチェンジは、文字セットの観点から見ると、自己記述型です。 UNB1 データ要素が使用されます。 EDIFACT では、タグ名と区切り記号が ASCII 型である必要があります。そのため、UNB1 を探して、関連するコード ページを残りのインターチェンジに適用できます。  
  
 受信した EDIFACT メッセージを処理する場合は、UNB1 データ要素からそのメッセージに使用する文字セットが [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] で決定されます。 取引先アグリーメントでの設定は不要です。  
  
 送信した EDIFACT メッセージを処理する場合は、取引先アグリーメントまたはフォールバック アグリーメントの文字セットが [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] で使用されます。 UNB1 データ要素で設定した、**文字セットと区切り記号**双方向アグリーメント タブのページ (アグリーメントが定義されている) 場合、または**文字セットと区切り記号**のアグリーメントタブのページで**EDIFACT フォールバックの設定** ダイアログ ボックス (アグリーメントが定義されていない) 場合。 UNB1.1 は、構文識別子と呼ばれる必須の複合データ要素です。 UNB1.2 は、EDIFACT 文字セットのバージョンです。 UNB1 データ要素は、取引先管理ユーザー インターフェイスで (Tab キーを押してフィールドから移動する場合や別のページを表示するときではなく) プロパティ セット全体を保存するときに、プロパティに入力した値を検証するためにも使用されます。  
  
 使用できる文字セットは、KECA、UNOA、UNOB、UNOC、UNOD、UNOE、UNOF、UNOG、UNOH、UNOI、UNOJ、UNOK、UNOX、および UNOY です。 既定値は UNOB です。 これらのレベルの完全な文字セットは、ISO 9735 の EDIFACT 構文規則で指定されています。  
  
> [!NOTE]
>  受信インターチェンジまたは送信インターチェンジに UNOC 文字セットが使用されている場合、EDI 逆アセンブラーまたは EDI アセンブラーは、UTF-8 コード ページではなく、ラテン -1 コード ページを使用します。 これが必要なのは、UTF-8 が UNOC のスーパーセットではないためです。 UNOC で許可されている文字の中には、UTF-8 として処理すると、インターチェンジが中断される原因となるものがあります。  
  
 一部の EDIFACT 文字セットで 2 バイト文字である文字が、他の EDIFACT 文字セットでは 1 バイト文字である場合があります。 そのため、インターチェンジ内の文字数に基づいてバッチのリリース条件を設定するときは、使用する文字セットによってインターチェンジ内のバイト数が異なることがあります。  
  
 UNA セグメントとセグメント名 UNB には、ASCII 文字セット内の値のみを使用できます。  
  
## <a name="kedifact-character-set"></a>KEDIFACT 文字セット  
 EDIFACT の場合と同様に、KEDIFACT エンコード インターチェンジの文字セットも UNB1 データ要素で設定されます。 EDIFACT の場合と、文字のセットによって適用すべき[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]KEDIFACT インターチェンジの処理が確立されている場合のデータ要素で**UNB1**の**文字セットと区切り記号**双方向のページアグリーメントのタブ (アグリーメントが定義されている) 場合、または**文字セットと区切り記号**のアグリーメント タブのページで、 **EDIFACT フォールバックの設定** ダイアログ ボックス (アグリーメントが定義されていない) 場合。 値、**識別子 (UNB1.1)** 要素は KECA に設定する必要があります。  
  
## <a name="x12-character-set"></a>X12 文字セット  
 BizTalk 受信パイプラインまたは送信パイプラインが X12 エンコード メッセージの EDI 検証を実行する際には、パイプラインの CharacterSet プロパティで選択された X12 文字セットを使用します。 このプロパティを設定するには、受信場所または送信ポートの [プロパティ] ダイアログ ボックスを開き、受信パイプラインまたは送信パイプラインの横にある省略記号をクリックし、逆アセンブラーまたはアセンブラーの CharacterSet プロパティを設定します。  
  
 パイプラインの CharacterSet プロパティを使用して X12 インターチェンジを検証するのは、EDIFACT や KEDIFACT の場合とは異なり、X12 エンコード インターチェンジは文字セットの観点から見ると自己記述型ではないからです。 ISO エンコードまたは UTF エンコードで ISA ヘッダーを読み込むと、アグリーメントの参照に異なる値が使用されることがあります。 そのため BizTalk では、アグリーメント参照の前 (アグリーメントに適用できる文字セットを取得するとき) に、メッセージの処理に使用される適用可能な文字セットを認識する必要があります。  
  
 X12 を指定する文字セットでのアグリーメントの検証に使用するので、**文字セットと区切り記号**双方向アグリーメント タブのページ (アグリーメントが定義されている) 場合、または**文字セットと区切り記号**、フォールバック アグリーメント タブのページで、 **X12 フォールバック設定** ダイアログ ボックス (アグリーメントが定義されていない) 場合。 ただし、これらの設定は (Tab キーを押してフィールドから移動したり、別のページを表示したりするときではなく) プロパティ セット全体を保存するときに、関連のプロパティに入力した値を検証するためだけに使用されます。 受信パイプラインおよび送信パイプラインでは、これらの文字セットのプロパティは無視されます。  
  
> [!NOTE]
>  アグリーメントまたはフォールバック アグリーメントで指定されている文字セットが、受信パイプラインまたは送信パイプラインに選択されている文字セットと一致しない場合、メッセージ検証エラーが発生することがあります。 たとえば、アグリーメントの X12 文字セットのプロパティが [拡張] に設定され、パイプライン プロパティ内の X12 文字セットのプロパティが [基本] に設定されている場合です。  
  
 使用できる文字セットは、『X12 Specifications/Implementation Guides』に記載されている [基本] と [拡張]、および [UTF8/Unicode] です。 既定値は UTF8 です。  
  
> [!NOTE]
>  双方向アグリーメントまたはフォールバック アグリーメントでデータ要素区切り記号、コンポーネント要素区切り記号、およびセグメント終端記号に入力する値は、ASCII 文字セット内の値に限られます。 これらのプロパティは、X12 文字セットに対しては検証されません。  
  
 基本文字セットには、大文字、数字、スペース、および特殊文字が含まれています A ~ Z、0 ~ 9、!。 “ & ’ ( ) * + , - . / : ; ? (スペース) を = です。  
  
 拡張文字セットには、基本文字セット、および文字の小文字、言語選択文字、およびその他の特殊文字の文字が含まれています。 a ~ z、% @ [] _ {} \ &#124;です。\< \> ~ # $.  
  
## <a name="see-also"></a>参照  
 [EDI メッセージング](../core/edi-messaging.md)   
 [EDI スキーマ](../core/edi-schemas.md)