---
title: "全般設定 (AS2) の構成 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8592c52e-5156-418c-9c49-7478f73c372e
caps.latest.revision: "5"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 23ff62f90f14238f7834312ab909a137d49bcbab
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="configuring-general-settings-as2"></a>全般的な設定の構成 (AS2)
全般的な設定の一部としてアグリーメント名、アグリーメントで使用するプロトコル (AS2)、およびアグリーメント対象のパーティとプロファイルを指定し、アグリーメントにより処理されるすべてのメッセージに対してレポート機能を有効にするかどうかを指定します。 また、アグリーメントの中でパーティの連絡先情報を指定することもできます。  
  
## <a name="prerequisites"></a>前提条件  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理者グループまたは [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] B2B Operators グループのメンバーとしてログオンしている必要があります。  
  
### <a name="to-configure-general-agreement-settings"></a>アグリーメントの全般設定を構成するには  
  
1.  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールで、をクリックして**パーティ**し、コンソール ツリーで、、**パーティとビジネス プロファイル**] ページで、アグリーメントの一部にする必要があるビジネス プロファイルを右クリックします。作成し、[**新規**、クリックして**アグリーメント**です。  
  
2.  次の表は、さまざまなプロパティと値をプロパティに指定する、**全般プロパティ**ページ。  
  
    1.  **アグリーメントのパラメーター**セクションで、次の操作します。  
  
        |プロパティ|目的|  
        |--------------|----------------|  
        |**名前**|このアグリーメントの名前を指定します。|  
        |**ID**|アグリーメントの一意な ID が表示されます。 このテキスト ボックスは編集できませんしをクリックした後、アグリーメント ID が表示されます**適用**の最初の時刻と設定が受け入れられます。|  
        |**[状態]**|アグリーメントの状態を指定します。 既定では、アグリーメントの作成、 **Active**状態です。 場合は、作成した最初の select があるときに無効にするアグリーメント**無効になっている**ドロップダウン リストからです。|  
        |**[プロトコル]**|アグリーメントのプロトコルを指定します。 AS2 トランスポート プロトコルでは、選択**AS2**ドロップダウン リストからです。|  
  
    2.  **最初のパートナーと**セクションで、次の操作します。  
  
        |プロパティ|目的|  
        |--------------|----------------|  
        |**名前**|このアグリーメントの作成に使用するビジネス プロファイルが属するパートナーの名前が表示されます。 このテキスト ボックスは編集できません。|  
        |**プロファイル**|このアグリーメントの作成に使用するプロファイルの名前を表示します。 このテキスト ボックスは編集できません。|  
        |**プロトコル セット**|ビジネス プロファイルの一部として作成した AS2 プロトコル セットは、ドロップダウン リストから選択できます。 ビジネス プロファイルの一部として作成しなかった AS2 プロトコル セットは、空白のままにすることができます。|  
  
    3.  **2 番目のパートナー**セクションで、次の操作します。  
  
        |プロパティ|目的|  
        |--------------|----------------|  
        |**名前**|ドロップダウン リストから、アグリーメントの作成に使用するビジネス プロファイルが属するパーティを選択します。|  
        |**プロファイル**|ドロップダウン リストから、アグリーメントの作成に使用するプロファイルを選択します。|  
        |**プロトコル セット**|ビジネス プロファイルの一部として作成した AS2 プロトコル セットは、ドロップダウン リストから選択できます。 ビジネス プロファイルの一部として作成しなかった AS2 プロトコル セットは、空白のままにすることができます。|  
  
        > [!TIP]
        >  キーを押して`CTRL`は、アグリーメントの一部にする、いずれかのビジネス プロファイルを右クリックし、 をポイントするビジネス プロファイルを選択して**新規**、順にクリック**アグリーメント**です。 値は、パートナー名と、両方のパートナーのビジネス プロファイルで自動的に設定されますが、**アグリーメントのプロパティ** ダイアログ ボックス。  
  
        > [!NOTE]
        >  2 つのタブが横に追加された別のプロファイルを選択するとすぐに、**全般**タブです。各タブは 2 つのパーティ間の一方向の AS2 アグリーメントを表します。 このタブを使用して、インターチェンジやトランザクション セット関連の設定を指定します。  
  
    4.  選択、**を有効にするアグリーメント**チェック ボックスをアグリーメントを有効にし、次の操作します。  
  
        |プロパティ|目的|  
        |--------------|----------------|  
        |**From**|アグリーメントが有効となる日時を選択します。|  
        |**終了日がないです。**|アグリーメントの有効期限を設定しない場合はこのオプションを選択します。|  
        |**終了日します。**|アグリーメントが有効期限となる日時を指定するにはこのオプションを選択します。|  
  
    5.  **共通のホスト設定**セクションで、次の操作します。  
  
        |プロパティ|目的|  
        |--------------|----------------|  
        |**レポートで有効にします。**|すべての AS2 メッセージ (受信および送信) で状態エントリを表示する、 **AS2 メッセージおよび関連する MDN 状態**のタブ、**グループの概要**ペインで、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理コンソールです。 このオプションがオフの場合、状況を示すエントリは表示されません。|  
  
3.  **全般** タブで、**連絡先情報** ページで、次の操作します。  
  
    1.  **連絡先 1**  タブを使用するアグリーメントを作成するパーティのプロファイルの連絡先情報を入力します。 このデータは参考用であり、BizTalk ランタイムでは使用されません。  
  
    2.  連絡先の別のタブを追加する をクリックして、**新しい連絡先**タブです。  
  
    3.  連絡先 タブを削除しても**削除**タブ ページの右上隅にあるからです。  
  
        > [!NOTE]
        >  削除することはできません、**連絡先 1**タブです。削除できるのは、追加したタブだけです。  
  
4.  **全般** タブで、**追加プロパティ** ページで、次の操作します。  
  
    > [!NOTE]
    >  このページで指定する情報は、BizTalk Server による処理には使用されません。このデータは参考用です。  
  
    1.  **追加プロパティ**グリッドで、パーティまたはアグリーメントに関連する情報を追加する名前と値のペアを入力します。  パーティに関する任意の情報を格納する、名前と値の組み合わせを入力します。 名前と値の組み合わせは、必要な数だけ追加できます。  
  
         名前と値のペアを削除、行を選択し、をクリックする**削除**右上隅からです。  
  
    2.  **テキスト 1**、**テキスト 2**、および**アグリーメント**テキスト ボックスでは、パーティとのアグリーメントに関する情報を入力します。  
  
        > [!IMPORTANT]
        >  クリックすると**[ok]**または**適用**すべての値を提供することは、このページに一覧表示後に、エラーが発生します。 その理由は、アグリーメントの作成に必要な値がまだ入力されていないからです。 これらは、AS2-から AS2 に-の値を**識別子**各一方向アグリーメント タブのページです。  
  
## <a name="next-steps"></a>次の手順  
 アグリーメントの識別子設定を構成する必要があります。 手順を参照してください[識別子の構成 (AS2)](../core/configuring-identifiers-as2.md)です。  
  
## <a name="see-also"></a>参照  
 [AS2 アグリーメント プロパティの構成](../core/configuring-as2-agreement-properties.md)