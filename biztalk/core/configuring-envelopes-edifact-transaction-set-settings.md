---
title: エンベロープの構成 (EDIFACT トランザクション セットの設定) |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ec140def-6155-4b8a-8489-6e0a530bd697
caps.latest.revision: 25
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 7a1d910f52d9ea90ae0c486356a7ecb3b01bf07a
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22234634"
---
# <a name="configuring-envelopes-edifact-transaction-set-settings"></a>エンベロープの構成 (EDIFACT トランザクション セットの設定)
**エンベロープ**のページ、**トランザクション セットの設定** セクションで、BizTalk Server が、パーティに送信する EDIFACT エンコード インターチェンジの UNG および UNH セグメントを生成する方法を定義します。  
  
 UNG セグメントは、EDIFACT エンコード インターチェンジの機能グループを識別および指定するヘッダーです。 UNG セグメントには、機能グループに含まれているドキュメントの種類とバージョンのほか、機能グループが準備された日時に関する情報が含まれています。  
  
 UNH セグメントは、EDIFACT エンコード インターチェンジのメッセージ ヘッダー セグメントです。 UNH セグメントは、メッセージの種類と、そのメッセージの種類の公開の保守を担当する機関に関する情報を提供します。 このセグメントは、インターチェンジ内のドキュメントの開始点と、それに続くドキュメントの種類を示します。  
  
 **機能グループ ヘッダー (UNG)**  セクションに関連付ける**UNG**の値を使った**UNH**値と名前空間。 BizTalk Server が、BizTalk XML メッセージに設定される値を持つことを判断するとき、 **UNH**要素および**ターゲットの名前空間**BizTalk Server では、グリッドの行、読み込みます、 **UNG**データ要素にグリッドの同じ行からの値。 値、 **UNH**要素および**ターゲットの名前空間**一意である必要があります。  
  
 メッセージとの一致にいない場合、 **UNH**要素および**ターゲットの名前空間**任意の行では、BizTalk Server はメッセージに設定の値を持つ、 **UNG**既定の行の要素。 メッセージとの一致を持っていない場合でも、これらの値を使用するが、 **UNH**要素および**ターゲットの名前空間**既定の行。  
  
 BizTalk エンジンは、BizTalk XML メッセージは、UNH 要素およびターゲットの名前空間に設定される値であると判断した場合、エンジンはへの追加メッセージに UNG 要素の値が提供される、グリッド内でそれらの設定、**グループの作成セグメント**チェック ボックスをオンします。  
  
> [!NOTE]
>  **機能グループ ヘッダー (UNG)** セクションで、グリッドで、いずれかのフィールドの設定を入力してその設定を削除、行全体を削除する必要が、またはページは検証に失敗します。  
  
> [!IMPORTANT]
>  すべてのプロパティが無効になっている**パーティ A にパーティ B->** をオフにした場合は、一方向アグリーメント タブ、**ローカルの BizTalk パーティまたはこのパーティからのメッセージの送信をサポートして受信メッセージを処理する**チェックパーティ A のボックス同じ ページで、ただし、すべてのプロパティが有効に、**パーティ B には、パーティ A が->**  A の作成中にチェック ボックスをオンの場合 タブ  
  
## <a name="prerequisites"></a>前提条件  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理者グループまたは [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] B2B Operators グループのメンバーとしてログオンしている必要があります。  
  
### <a name="to-define-the-ung-and-unh-segments"></a>UNG セグメントと UNH セグメントを定義するには  
  
1.  EDIFACT」の説明に従ってエンコード アグリーメントを作成する[を構成する一般的な設定 (EDIFACT)](../core/configuring-general-settings-edifact.md)です。 既存のアグリーメントを更新するでアグリーメントを右クリックし、**パーティとビジネス プロファイル** ページで、をクリックして**プロパティ**です。  
  
2.  一方向アグリーメント タブの下にある**トランザクション セットの設定**セクションで、**エンベロープ**です。  
  
3.  グリッドの行に、次の値を入力します。  
  
    -   **メッセージの種類 UNH2.1**列で、トランザクション セットの種類を入力します。 最大文字数は 6 文字です。  
  
    -   **UNH2.2**列で、メッセージのバージョン番号を入力します。 (1 ～ 3 文字です)。  
  
    -   **UNH2.3**列で、メッセージ リリース番号を入力します。 (1 ～ 3 文字です)。  
  
    -   **UNH2.5**列で、割り当てコードを入力します。 (最大文字数は 6 文字です。 英数字である必要があります)。  
  
    -   **ターゲットの名前空間**列で、スキーマのターゲットの名前空間を選択します。 このフィールドは必須です。  
  
        > [!NOTE]
        >  これらの値は、BizTalk Server で作成中のインターチェンジに関連付けられている値と比較されます。  
  
4.  グリッドの同じ行に、次の値を入力します。  
  
    -   **UNG1** (機能グループ id) に、1 つの文字の最小値、最大 6 文字の英数字を入力します。 このフィールドは必須です。  
  
    -   **UNG2.1** (アプリケーション送信者 id)、1 つの文字の最小値、最大 35 文字の英数字を入力します。 このフィールドは必須です。  
  
    -   **UNG2.2** (アプリケーション送信者コード修飾子)、最大 4 文字の英数字の値を入力します。 このフィールドの入力は省略可能です。  
  
    -   **UNG3.1** (アプリケーション受信者 id)、1 つの文字の最小値、最大 35 文字の英数字を入力します。 このフィールドは必須です。  
  
    -   **UNG3.2** (アプリケーション受信者コードの修飾子)、最大 4 文字の英数字の値を入力します。 このフィールドの入力は省略可能です。  
  
    -   **UNG6** (制御機関)、1、2 つの最大値以下で英数字値を入力します。 このフィールドは必須です。  
  
    -   **UNG7.1** (メッセージの種類のバージョン番号)、1 つの文字の最小値、最大 3 つの文字の英数字を入力します。 このフィールドは必須です。  
  
    -   **UNG7.2** (メッセージの種類のリリース番号)、1 つの文字の最小値、最大 3 つの文字の英数字を入力します。 このフィールドは必須です。  
  
    -   **UNG7.3** (関連付けの割り当てコード)、1 文字の最小値、最大 6 文字の英数字を入力します。 このフィールドは必須です。  
  
    -   **UNG8** (アプリケーションのパスワード)、1 つの文字の最小値、最大 14 文字の英数字を入力します。 このフィールドは必須です。  
  
        > [!NOTE]
        >  これらは、BizTalk Server で入力する場合の構築には、インターチェンジの UNG フィールドの値となる、**メッセージの種類 UNH2.1**、 **UNH2.2**、 **UNH2.3**、 **UNH2.5**、および**ターゲットの名前空間**の同じ行の要素がインターチェンジに関連付けられているものと一致します。  
  
5.  手順 4. および手順 5. を繰り返して、追加行をグリッドに入力します。  
  
6.  グリッドで 1 つの行をクリックして**既定**既定の行として指定します。  
  
    > [!NOTE]
    >  メッセージとの一致にいない場合、 **UNH2.1**、 **UNH2.2**、 **UNH2.3**、 **UNH2.5**、および**のターゲット名前空間**任意の行では、BizTalk Server 内の要素の値を持つメッセージの設定は、 **UNG1**、 **UNG2.1**、 **UNG2.2**、 **[Ung3.1]**、 **UNG3.2**、 **UNG6**、 **UNG7.1**、 **UNG7.2**、 **UNG7.3**、および**UNG8**既定行の要素。 これらの値は、メッセージとの一致を持っていない場合でも、使用は、**メッセージの種類 UNH2.1**、 **UNH2.2**、 **UNH2.3**、 **UNH2.5**、および**ターゲットの名前空間**既定の行の要素。  
  
    > [!NOTE]
    >  既定の行が選択されていないと、メッセージには、一致するものはありません、 **UNH2.1**、 **UNH2.2**、 **UNH2.3**、 **UNH2.5**、および**ターゲットの名前空間**BizTalk のいずれかの行要素は、メッセージを中断します。  
  
7.  をクリックして**適用**構成を続行する前に、変更を受け入れるか、をクリックする**OK**を変更を検証し、ダイアログ ボックスを閉じます。  
  
## <a name="see-also"></a>参照  
 [トランザクション セットの構成設定 (EDIFACT)](../core/configuring-transaction-set-settings-edifact.md)