---
title: オーケストレーション メモリ制限の設定を変更する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Bts10.settings.HostInstanceOrchestration
ms.assetid: f6953c68-7809-4518-87ec-e75c98884af3
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 444f0a53827f99bda3eeb2389c555e614c44fe04
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37022160"
---
# <a name="how-to-modify-orchestration-memory-throttling-settings"></a>オーケストレーション メモリの制限の設定を変更する方法
[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] のホスト インスタンス メモリ制限メカニズムは、制限の条件を継続的に監視し、制限の条件の重大度を評価し、評価された重大度に応じてホスト インスタンス メモリ制限を段階的に適用します。 このトピックでは、設定ダッシュボードを使用して、この操作を変更する手順について説明します。  

## <a name="prerequisites"></a>前提条件  
 ここで示す操作を実行するには、BizTalk Server 管理者グループのメンバーとしてログオンする必要があります。  

### <a name="to-modify-the-orchestration-memory-throttling-settings-of-a-host-instance"></a>ホスト インスタンスのオーケストレーション メモリ制限の設定を変更するには  

1. **BizTalk Server 管理コンソール**、展開[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]を右クリックして**BizTalk グループ**、 をクリックし、**設定**します。  

2. **BizTalk 設定ダッシュ ボード** ダイアログ ボックスで、**ホスト インスタンス** ページで、をクリックして、**オーケストレーション メモリ制限**タブ。  

3. クリックして、次の操作を**適用**を変更を適用し、別のタブに進みます。をクリックしてまたは**OK**変更を適用し、設定ダッシュ ボードを終了します。  


   |     プロパティ      |                                                                                目的                                                                                | 境界値 | 既定値 |
   |-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|---------------|
   | **ホスト インスタンス** | ドロップダウン ボックスから、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ランタイム コンピューター上のホストで実行中のインスタンスを選択します。 |        -        |       -       |

    **物理**  

   |プロパティ|目的|境界値|既定値|  
   |--------------|----------------|---------------------|-------------------|  
   |**最適使用量**|退避制限を有効にする物理メモリの使用量をパーセンテージで指定します。 これはホスト インスタンスに使用する物理メモリの最適なパーセンテージです。|[0 – 100]|70|  
   |**最大使用量**|退避制限が最大になる物理メモリの使用量をパーセンテージで指定します。 これはホスト インスタンスに使用する物理メモリの最大のパーセンテージです。<br /><br /> 最小値**maximalusage**べき**最適使用量**します。|(最適使用量 - 100]<br /><br /> 両方が 0 または 100 の場合は除外します。|85|  

    **仮想**  

   |プロパティ|目的|境界値|既定値|  
   |--------------|----------------|---------------------|-------------------|  
   |**最適使用量**|退避制限を有効にする仮想メモリの使用量をパーセンテージで指定します。<br /><br /> この時点では、 **TestThreshold** 、値を持つ**MaxThreshold**メモリ使用量を超える**OptimalUsage**により**TestThreshold**をより小さい**MaxThreshold**します。|[0 – 100]|65|  
   |**最大使用量**|退避制限が最大になる仮想メモリの使用量をパーセンテージで指定します。<br /><br /> この時点では、 **TestThreshold** 、値を持つ**MinThreshold**メモリ使用量より小さい**MaximalUsage**により**TestThreshold**超える**MinThreshold**します。|(最適使用量 - 100]<br /><br /> 両方が 0 または 100 の場合は除外します。|85|  

   > [!NOTE]
   >  既定の設定を復元するには、次のようにクリックします。**既定値に戻す**します。  

## <a name="see-also"></a>参照  
 [ホスト インスタンスの設定を変更する方法](../core/how-to-modify-host-instance-settings.md)