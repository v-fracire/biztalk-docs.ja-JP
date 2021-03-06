---
title: 検証の構成 (EDIFACT トランザクション セットの設定) |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81b30a78-3a4b-4827-9b0a-af9ad3e865a3
caps.latest.revision: 15
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6a9ad8f69accd0f479e05e130cc0c28fe874bb86
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22234002"
---
# <a name="configuring-validation-edifact-transaction-set-settings"></a>検証の構成 (EDIFACT トランザクション セットの設定)
トランザクション セット検証の設定では、BizTalk Server がパーティから受信したトランザクション セットを検証する方法を定義します。 検証設定の一部として、BizTalk Server が受信したインターチェンジに対して実行する検証の種類を指定できます。  
  
> [!IMPORTANT]
>  プロパティは無効では、このページをオフにした場合でも、**ローカルの BizTalk パーティまたはこのパーティからのメッセージの送信をサポートして受信メッセージを処理する**チェック ボックスを作成するパーティを作成するときに、アグリーメント。  
  
## <a name="prerequisites"></a>前提条件  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理者グループまたは [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] B2B Operators グループのメンバーとしてログオンしている必要があります。  
  
### <a name="to-configure-ack-processing-and-validation-settings"></a>ACK 処理と検証の設定の構成  
  
1.  EDIFACT」の説明に従ってエンコード アグリーメントを作成する[を構成する一般的な設定 (EDIFACT)](../core/configuring-general-settings-edifact.md)です。 既存のアグリーメントを更新するでアグリーメントを右クリックし、**パーティとビジネス プロファイル** ページで、をクリックして**プロパティ**です。  
  
2.  一方向アグリーメント タブの下にある**トランザクション セットの設定**セクションで、**検証**です。  
  
3.  グリッドで、異なるトランザクション セットに対して異なる検証設定を定義できます。 **検証** ページで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**[Default]**|既定の検証設定を定義する場合に、チェック ボックスをオンにします。|  
    |**UNH2.1 の場合**|列の空のセルをクリックし、ドロップダウンの一覧からトランザクションの種類を選択します。|  
    |**Edi 型の検証**|選択**EDI の種類**インターチェンジの受信者に対する EDI (データ要素) 検証を有効にします。 この検証は、トランザクション セット データ要素で EDI 検証を実行し、データ型、長さの制限、および空のデータ要素と末尾の区切り記号を検証します。 詳細については、次を参照してください。 [EDI の種類 (データ要素) 検証](../core/edi-type-data-element-validation.md)です。 **注:** スキーマ注釈で有効になって場合クロス フィールド/セグメント検証が実行される場合でも、このプロパティが選択されていません。|  
    |**拡張された検証**|インターチェンジ送信者から受信したインターチェンジの拡張された (BizTalk XSD) 検証を有効にする場合に選択します。 これには、フィールド長、省略可能性、および XSD データ型検証に加えて、繰り返し回数の検証が含まれます。 詳細については、次を参照してください。[拡張された (BTS-XSD) 検証](../core/extended-bts-xsd-validation.md)です。 **注:** 場合にのみ、このチェック ボックスを選択する**Edi 型の検証**が選択されています。|  
    |**先頭および末尾のゼロおよび空白を許可します。**|EDI インターチェンジのデータ要素が、先頭 (または末尾) の 0 または末尾のスペースにより長さの要件に準拠していなくても、それらを削除することで長さの要件に準拠するのであれば、パーティから受信した EDI インターチェンジの検証は失敗しないことを指定する場合にオンにします。 **注:** 場合にのみ、このチェック ボックスを選択する**Edi 型の検証**が選択されています。|  
    |**末尾の区切り記号のポリシー**|-**できません**インターチェンジ送信者から受信したインターチェンジに末尾の区切り記号および区切り文字を許可したくない場合。 インターチェンジに末尾の区切り記号が含まれている場合は、インターチェンジが無効と宣言されます。<br />-**オプション**インターチェンジの有無にかかわらず、末尾の区切り記号および区切り文字を受け入れます。<br />-**必須**場合は、受信したインターチェンジは、末尾の区切り記号および区切り文字を含める必要があります。|  
  
     特定のインターチェンジに対する検証設定を定義するために、必要な数だけ行を追加できます。  
  
     検証の設定を削除する行を選択し、をクリックして**削除**です。  
  
    > [!NOTE]
    >  グリッド内でプロパティを編集する方法は多少複雑です。 編集しているし、で同じプロパティを編集して行を選択する代わりに、**選択した行を編集**セクションです。 ここで指定した設定が、選択した行に反映されます。  
  
4.  をクリックして**適用**構成を続行する前に、変更を受け入れるか、をクリックする**OK**を変更を検証し、ダイアログ ボックスを閉じます。  
  
## <a name="see-also"></a>参照  
 [トランザクション セットの構成設定 (EDIFACT)](../core/configuring-transaction-set-settings-edifact.md)