---
title: "変換図形を構成する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- configuring [Orchestration Designer], Transform shape
- Transform shape [Orchestration Designer]
ms.assetid: ca81d153-77a6-4bcc-b14f-8f48469fffe0
caps.latest.revision: "8"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 48cdca50620262581469e924fbb2975dde7e91fe
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-configure-the-transform-shape"></a>変換図形を構成する方法
![](../core/media/ebiz-orch-transform.gif "ebiz_orch_transform")  
変換図形  
  
 変換は、そのため、メッセージを構築するときにのみ使用、**変換**内の図形が常に表示される、**メッセージの構築**図形です。 削除することができます、**メッセージの構築**デザイン画面で図形のしてから、削除、**変換**するか、内部の図形を削除するだけ、**変換**設計上の図形画面、および作成、囲んでいるオーケストレーション デザイナーは**メッセージの構築**図形です。  
  
> [!NOTE]
>  内の送信元または送信先のメッセージ、**変換**スキーマに基づいている必要があります。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-configure-a-transform-shape"></a>変換図形を構成するには  
  
1.  [プロパティ] ウィンドウ、**省略記号**(**.**) ボタンをクリックして、**入力メッセージ**、**出力メッセージ**、または**マップ名**プロパティです。  
  
2.  使用して、**変換の構成**を構成するダイアログ ボックス、**変換**図形です。  
  
> [!NOTE]
>  A**変換**図形を配置できる内でのみ、**メッセージの構築**図形です。 ドラッグした場合、**メッセージの割り当て**図形のデザイン サーフェイスでは、他の場所から新しい**メッセージの構築**図形が作成されます。  
  
### <a name="important-performance-considerations"></a>パフォーマンスに関する重要な考慮事項  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、サイズの大きいメッセージに対して変換を実行する機能が最適化されます。つまり、サイズの大きいドキュメント全体を一度にメモリに読み込むのではなく、ストリーム方式で読み込みながら変換を適用します。 この最適化により、以前のバージョンの BizTalk Server で制限されていたサイズよりも大きなサイズのドキュメントを、マップまたは変換できるようになりました。 ただしこの最適化を行う場合、オーケストレーションの変換図形で複数の入力または出力、あるいはその両方を受け入れるときに制限が発生します。  
  
 オーケストレーションの変換図形で複数の入力または出力、あるいはその両方を受け入れる場合、ドキュメントのストリーム処理は実行されず、メモリ使用量は著しく増大します。 この問題を回避する手段の 1 つとしては、オーケストレーションの変換図形で複数の入力または出力を受け入れないよう、1 つまたは複数の変換を受信パイプライン内で適用するという方法があります。  
  
### <a name="newexisting-map-file"></a>新しいマップ ファイルまたは既存のマップ ファイル  
 このセクションでをクリックするか、**新しいマップ**または**既存のマップ**に割り当てるマップを選択するオプション ボタン、**変換**図形です。  
  
 使用して、**名前**フィールド マップを指定する選択したオプション ボタンの下。 選択した場合は**新しいマップ**、割り当てるマップの名前を入力することができます。 使用すると、**新しいマップ**オプション、テキスト ボックスに、マップの完全修飾名を指定する必要があります。 プロジェクトの名前空間に基づく一意の識別子の名前を持つことはあらかじめ設定されているため、テキスト ボックスが既定では、このような名前の例を表示および**変換**図形の名前:\<プロジェクトの名前空間 >.\<変換図形の名前 > _Map (例、MyProject.Transform3_Map)。  
  
 選択した場合**既存のマップ**の下向き矢印をクリックして、**名前**フィールドを使用するマップ ファイルを選択します。 このリスト ボックスには、プロジェクトで使用できるすべての既存のマップがアルファベット順に表示されます。 テキストをクリックした場合、この一覧に\<参照されたアセンブリから選択 > では、**成果物の種類の選択** ダイアログ ボックスが表示されます。 使用できるように、選択の詳細については、次を参照してください。[成果物の種類の選択 ダイアログ ボックスを使用する方法](../core/how-to-use-the-select-artifact-type-dialog-box.md)です。  
  
### <a name="select-source-and-destination-messages"></a>変換元のメッセージと変換先のメッセージの選択  
 この部分を使用して、**変換の構成**で選択したマップを構成するダイアログ ボックス、**新規または既存マップ ファイルですか?**セクションです。 選択した場合は**新しいマップ**セクションでは、このセクションで構成することによってそのマップを作成します。  
  
 選択した場合**既存のマップ**、次の 2 つのいずれかの操作をこのセクションの内容を使用することができます。  
  
-   既存のマップを選択し、現在の変換でそのまま再使用する。  
  
-   既存のマップを選択して変更 (再構成) し、現在の変換の新しい構成で使用する。  
  
 使用して送信元と送信先のメッセージの指定、**ソース メッセージ**と**送信先メッセージ**グリッド コントロール。 これらのグリッド コントロールを使用すると、マップ ファイルをいくつかの方法で変更できます。 各グリッド コントロールの行で示されるメッセージを削除、追加したり、別の種類のメッセージを選択する場合は、マップの構造を変更します。 マップの構造を変更する場合は、そのマップを使用する他のすべての変換を、マップの新しい構造に合わせて変更する必要があります。 メッセージを削除して同じ種類のメッセージを代わりに挿入するなど、その他の変更の場合は、マップの構造を変更しないでください。  
  
 **ソース メッセージ**と**送信先メッセージ**グリッド コントロールは、外観や動作と同じです。 各グリッド コントロールが 2 つの列: メッセージと型。 [メッセージ] 列でメッセージを選択すると、グリッド コントロールに行を追加できます (データは [メッセージ] 列にのみ追加でき、[種類] 列は読み取り専用です)。[メッセージ] 列のセルはドロップダウン リストになっており、現在のオーケストレーションのスコープ内にあるメッセージ インスタンスが表示されます。  
  
 クリックして、グリッド コントロールで行を選択することができます、*右矢印*グリッド コントロールの左側にある (>) ボタンをクリックします。 行を選択した後で <localizedText>Delete</localizedText> キーを押すと、その行を削除できます。 行 (メッセージ) を削除すると、その行が含まれるマップ ファイルの構造が変更されます。 編集できるマップ ファイルは、プロジェクトにローカルのマップ ファイルだけです。  
  
### <a name="when-i-click-ok-launch-the-biztalk-mapper"></a>[[OK] をクリックしたら Biztalk マッパーを起動する]  
 クリックすると**ok をクリックしたら BizTalk マッパーを起動** をクリックすると、BizTalk マッパーを自動的に開きます**OK**を閉じる、**変換の構成** ダイアログ ボックスし、保存変更します。 ただし、必要な情報が不足している場合は変更を保存できません。 ここでは、ダイアログ ボックスのフィールドの入力を完了し、をクリックして**OK**です。  
  
## <a name="see-also"></a>参照  
 [マップの概要](../core/about-maps.md)   
 [メッセージの構築](../core/constructing-messages.md)   
 [メッセージを動的に変換する式を使用する方法](../core/how-to-use-expressions-to-dynamic-transform-messages.md)