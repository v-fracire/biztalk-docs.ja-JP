---
title: フォールバック識別子 (EDIFACT) の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2ce56c1-44f1-42dc-94e8-36e5ba664f53
caps.latest.revision: 3
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: f7db7e20f8ccb4db8da53483e7c33285f4b75afb
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36991987"
---
# <a name="configuring-fallback-identifiers-edifact"></a>フォールバック識別子の構成 (EDIFACT)
未承認の受信者がインターチェンジを受信していないことを確認するには、フォールバック アグリーメントで、受信者の参照パスワードを設定する必要があります。  
  
## <a name="prerequisites"></a>前提条件  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理者グループまたは [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] B2B Operators グループのメンバーとしてログオンしている必要があります。  
  
### <a name="to-set-the-sender-recipient-recipient-password"></a>送信者、受信者、受信者のパスワードを設定するには  
  
1. [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールを右クリックし、**パーティ**ノード、およびクリック**EDIFACT フォールバックの設定**します。  
  
2. **EDIFACT フォールバックの設定**] ダイアログ ボックスで、 **EDIFACT アグリーメント ページ**] タブの [、**インターチェンジの設定**セクションで、[**識別子**.  
  
3. **送信者 (UNB2)** セクションで、次の操作を行います。  
  
   1.  **Id (UNB2.1)**、1 つの最小値、35 文字の英数字を入力します。 このフィールドは必須です。  
  
   2.  **コードの修飾子 (UNB2.2)**、ドロップダウン リストから値を選択します。 このフィールドの入力は省略可能です。  
  
   3.  **逆ルーティングのアドレス (UNB2.3)**、1 つの文字の最小値、最大 14 文字の英数字を入力します。 このフィールドの入力は省略可能です。  
  
   4.  **アプリケーション参照識別子 (UNB7)**、1 つの文字の最小値、最大 6 文字の英数字を入力します。 このフィールドは必須です。  
  
4. **受信者 (UNB3)** セクションで、次の操作を行います。  
  
   1.  **Id (UNB3.1)**、1 つの最小値、35 文字の英数字を入力します。 このフィールドは必須です。  
  
   2.  **コードの修飾子 (UNB3.2)**、ドロップダウン リストから値を選択します。 このフィールドの入力は省略可能です。  
  
   3.  **逆ルーティングのアドレス (UNB3.3)**、1 つの文字の最小値、最大 14 文字の英数字を入力します。 このフィールドの入力は省略可能です。  
  
   4.  必要な場合、**受信者の参照パスワード (UNB6)** セクションで、受信者の参照パスワードの値を入力します。 **値 (UNB6.1)**、1 つの最小値、14 文字の英数字を入力します。 **修飾子 (UNB6.2)**、1 つの文字の最小値、最大 2 つの文字の英数字を入力します。 これらは省略可能なフィールドです。 これらの値が、受信したインターチェンジの "UNB6.1" フィールドおよび "UNB6.2" フィールドと一致しない場合、インターチェンジは中断されます。  
  
       > [!NOTE]
       >  組み合わせた**UNB6.1**と**UNB6.2**で一意である必要があります。  
  
       > [!NOTE]
       >  [UNB6.1] と [UNB6.2] の両方に値を入力し、変更を適用してから、[UNB6.1] の値を削除すると、[UNB6.2] の値も削除されて、このフィールドが無効になります。  
  
5. をクリックして**適用**構成では、続行する前に、変更を受け入れるか、をクリックする**OK**変更を検証し、ダイアログ ボックスを閉じます。  
  
## <a name="see-also"></a>参照  
 [インターチェンジ処理に対する EDIFACT フォールバック アグリーメント プロパティの構成](../core/configuring-edifact-fallback-agreement-properties-for-interchange-processing.md)