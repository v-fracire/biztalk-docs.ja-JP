---
title: エンベロープの構成 (EDIFACT インターチェンジの設定) |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 501ccc5f-e21c-4c36-9509-217d5b3ba21f
caps.latest.revision: 4
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 80957d82a70b0fca8a11ace428f87496b45dcb31
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36993595"
---
# <a name="configuring-envelopes-edifact-interchange-settings"></a>エンベロープを構成する (EDIFACT インターチェンジの設定)
このセクションでは、送信 EDIFACT メッセージのエンベロープを構成する方法について説明します。  
  
> [!IMPORTANT]
>  オフにした場合、このページで、すべてのプロパティが無効に、**ローカルの BizTalk パーティまたはこのパーティからのメッセージの送信をサポートして受信したメッセージを処理する**チェック ボックスを作成するパーティを作成するときに、契約です。  
>   
>  プロパティが無効になるのは、パーティから受信中のインターチェンジのプロパティに対応する一方向のアグリーメント タブ上のみです。 たとえば、2 つのパーティのパーティ A とパーティ B を作成するチェック ボックスをオフにしたパーティ A の場合は、上記のプロパティが無効になります、**パーティ A にパーティ B]-> [** 一方向アグリーメント タブ。  
  
## <a name="prerequisites"></a>前提条件  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理者グループまたは [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] B2B Operators グループのメンバーとしてログオンしている必要があります。  
  
### <a name="to-configure-the-interchange-envelope"></a>インターチェンジ エンベロープを構成するには  
  
1. EDIFACT エンコード アグリーメントを」の説明に従って作成[を構成する一般的な設定 (EDIFACT)](../core/configuring-general-settings-edifact.md)します。 既存のアグリーメントを更新するでアグリーメントを右クリックし、**パーティとビジネス プロファイル**ページ、およびクリックして**プロパティ**します。  
  
2. 一方向アグリーメント タブで、**インターチェンジの設定**セクションで、**エンベロープ**します。  
  
3. **処理優先度コード (UNB8)**、1 つの文字の最小値、1 つの文字のアルファベット順の値を入力します。 このフィールドの入力は省略可能です。  
  
4. **通信アグリーメント (UNB10)**、1 つの文字の最小値、最大 35 文字の英数字を入力します。 このフィールドは省略可能です。   
  
5. 選択**テスト インジケーター (UNB11)** で、インターチェンジが生成されることを示す[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]がテスト データ。  
  
6. 選択**適用の UNA セグメント (文字列サービス通知)** を送信するインターチェンジの UNA セグメントを生成します。 このオプションがオンの場合、 **UNA6**空にすることはできませんと**UNA6 サフィックス**することはできません**None**します。  
  
   > [!NOTE]
   >  指定した**UNA6**と**UNA6 サフィックス**で、**文字セットと区切り記号**」の説明に従ってページ[を構成する文字セットと区切り記号 (EDIFACT)](../core/configuring-charset-and-separators-edifact.md).  
  
7. 選択**適用の UNG セグメント (機能グループ ヘッダー)** 送信メッセージの機能グループ ヘッダーにグループ化セグメントを作成します。  
  
8. をクリックして**適用**構成では、続行する前に、変更を受け入れるか、をクリックする**OK**変更を検証し、ダイアログ ボックスを閉じます。  
  
## <a name="see-also"></a>参照  
 [インターチェンジの設定の構成 (EDIFACT)](../core/configuring-interchange-settings-edifact.md)