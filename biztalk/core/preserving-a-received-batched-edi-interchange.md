---
title: バッチ EDI インターチェンジを受信した保持 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 10d21b9b-9684-422a-8948-8bd71a4d5a10
caps.latest.revision: 20
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4883f6c6df9042d40b82138a4d3a871797a5fa1f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36985779"
---
# <a name="preserving-a-received-batched-edi-interchange"></a>受信したバッチ EDI インターチェンジの保存
> [!NOTE]
>  このトピックで説明されているすべてのユーザー インターフェイスのオプションが表示されます、**ローカル ホスト設定**ページ (**受信者の設定**セクション) で、双方向アグリーメント タブの**アグリーメントのプロパティ** ダイアログ ボックス。  

 EDI 受信パイプラインが受信バッチ EDI インターチェンジを保存する場合、各トランザクション セットまたはメッセージを別々の中間 XML ファイルに解析する通常の処理は実行されません。 EDI 受信パイプラインは、インターチェンジをトランザクション セットまたはメッセージに分割せず、1 つのドキュメントとして処理します。 これが発生したときに、**受信バッチ処理オプション**プロパティに設定されて**インターチェンジの保存 - エラーでインターチェンジを中断**または **- インターチェンジの保存時にトランザクション セットを中断エラー**します。  

 **スキーマの検証**  

 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は、保存されたバッチのエンベロープを、バッチ スキーマとサービス スキーマを使用して検証します。 保存されたメッセージのルート ノードの検証にはバッチ スキーマが使用され、インターチェンジ、グループ、およびトランザクション セットのヘッダーとトレーラーの検証にはサービス スキーマが使用されます。 バッチ スキーマの詳細については、次を参照してください。 [EDI のバッチ スキーマ](../core/edi-batch-schemas.md)します。 サービス スキーマの詳細については、次を参照してください。 [EDI サービスと管理スキーマ](../core/edi-service-and-control-schemas.md)します。  

 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は、バッチ インターチェンジ内のドキュメントを、プロジェクト内のドキュメント スキーマを使用して検証します。  

 **受信側の処理**  

 EDI 逆アセンブラーは、保存されたバッチを次のように処理します。  

- EDI 逆アセンブラーは、保存するバッチを処理するとき、フラット ファイル形式を XML に変換し、X12InterchangeXML または EdifactInterchangeXML を XML ルート ノードとして追加します。 これにより、送信パイプラインに対して、バッチ インターチェンジを保存する必要があること、および、ルート ノードの検証に Edifact_BatchSchema スキーマまたは X12_BatchSchema スキーマを使用する必要があることが通知されます。  

- 逆アセンブラーでは、XML メッセージから、バッチ EDI インターチェンジを生成するときに、送信パイプラインで使用される区切り記号を示すためにバッチ化された XML メッセージのルート ノードに DelimiterSetSerializedData 属性を追加します。 XML メッセージが保存されたバッチである場合、受信パイプラインは、受信メッセージで使用されている区切り記号からこの属性を取得します。 バッチ XML がバッチ処理オーケストレーションによって生成されるとき、この属性はアグリーメントのプロパティで設定された値から取得されます。  

- 逆アセンブラーは、保存された XML エンコード インターチェンジを作成するときに `http://schemas.microsoft.com/BizTalk/EDI/EDIFACT/2006/InterchangeXML` 名前空間または `http://schemas.microsoft.com/BizTalk/EDI/X12/2006/InterchangeXML` 名前空間を使用します。  

- 逆アセンブラーは、インターチェンジを保存されたインターチェンジとして識別するために、コンテキスト プロパティ `EDI.ReuseEnvelope == True` を昇格させます。 これにより、保存されたすべてのバッチ インターチェンジをサブスクライブする送信ポートを作成できます。  

  > [!NOTE]
  >  場合、HIPAA ドキュメントをサブドキュメントに分割されませんが、**受信バッチ処理オプション**に設定されている**インターチェンジの保存**します。 これは、HIPAA スキーマ内のサブドキュメントの作成を中断するための注釈が [はい] に設定されている場合も同じです。  

  **エラー処理**  

  選択した場合に**インターチェンジの保存 - エラーでインターチェンジを中断**の**受信バッチ処理オプション**、インターチェンジ全体は、エラーの結果として中断されます。 保存されたインターチェンジ全体が [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] によって中断されると、インターチェンジの構造と、インターチェンジ内のトランザクション セットの順序が保存されます。 エラーが発生した場合、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は、統合された 1 つのエラー エントリをイベント ログに送信します。 このエントリには、インターチェンジ、機能グループ、およびトランザクション セット レベルのすべてのエラーが含まれます。  

  選択した場合に**インターチェンジの保存 - エラーのトランザクション セットを中断**受信のバッチ処理オプション、EDI 受信パイプラインはインターチェンジから無効なトランザクション セットをすべてをドロップし、作成を続行インターチェンジ XML。 作成されるインターチェンジ XML は、既存の制御セグメントのエンベロープ (X12 エンコード インターチェンジの場合は ISA、GS、GE、および IEA、EDIFACT エンコード インターチェンジの場合は UNA、UNB、UNG、UNE および UNZ) を再利用するために必要です。 このインターチェンジは正常に処理されたドキュメントと見なされますが、イベント ビューアではエラーが報告され、機能確認ドキュメントが生成される場合は機能確認ドキュメントでもエラーが報告されます。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] イベント ログ エラーが発生したトランザクション セットごとに個別のエントリが作成されます。 場合[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]ドロップ誤ったトランザクション セットがインターチェンジのインターチェンジの構造からと順序付けは維持されません。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] インターチェンジ内のトランザクション セットの数が更新されます。  

  以下の特殊なケースが、エラー発生時のトランザクション セットの中断に当てはまります。  

- グループ内のすべてのトランザクション セットが無効である場合、各トランザクション セットが個別に中断されます。しかし、生成されるインターチェンジ XML には、トランザクション セットを持たないグループ制御セグメントが含まれます (これは、トランザクション セットがドロップされたためです)。  

- インターチェンジ内のすべてのトランザクション セットが無効である場合、各トランザクション セットが個別に中断されます。しかし、生成されるインターチェンジ XML には、トランザクション セットを持たないインターチェンジ制御セグメントが含まれます (これは、トランザクション セットがドロップされたためです)。  

- グループ制御セグメントが無効である場合、グループ内のすべてのトランザクション セットが個別に中断されます。  

- インターチェンジ制御セグメントが無効である場合、インターチェンジ内のすべてのトランザクション セットが個別に中断され、インターチェンジ XML は生成されません。 拒否されたインターチェンジのログがイベント ビューアーに作成されます。
