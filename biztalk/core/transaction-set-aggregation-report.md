---
title: "トランザクション セットの集計レポート |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a6e1417e-e0c6-4d30-aab5-d9bfe14cd4b8
caps.latest.revision: "11"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 960fe64eb61504cb07b71be3e1870007b46c5fa9
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="transaction-set-aggregation-report"></a>トランザクション セットの集計レポート
このレポートは、同じトランザクション セット ID、EDI エンコードの種類、送信者パーティ、受信者パーティ、および方向を共有する EDI トランザクション セットの数を示すレコードを 1 つ提供します。 このレポートでは、個々のトランザクション セットの詳細は提供されません。  
  
 この状態レポートを表示するには、BizTalk Server 管理コンソールで [グループ ハブ] ページの最下部にある [トランザクション セットの集計レポート] リンクをクリックします。  
  
## <a name="fields-in-the-status-report"></a>状態レポート内のフィールド  
 トランザクション セットの集計レポートには、受信または送信されたインターチェンジについての次の情報が表示されます。  
  
-   同じトランザクション セット ID、EDI エンコードの種類、送信者パーティ、受信者パーティ、および方向を共有するトランザクション セットの数  
  
-   レコード内の各トランザクション セットの送信者パーティ  
  
-   レコード内の各トランザクション セットの受信者パーティ  
  
-   レコード内の各トランザクション セットの方向 (受信または送信)  
  
-   時間範囲内の最初のトランザクション セットが送信または受信された日付と時刻 (最初の開始日/時刻)  
  
    > [!NOTE]
    >  受け取ったドキュメントで、インターチェンジに指定された日付が YYMMDD 形式であり、YY が 75 以上である場合、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では年を 19YY と表示します。 日付が 75 未満である場合は、20YY として表示されます。  
    >   
    >  たとえば、ISA09 の値が 991113 であるインターチェンジを受信した場合、レポートの初回開始日時は 11/13/1999 と表示されます。  
  
-   時間範囲内の最後のトランザクション セットが送信または受信された日付と時刻 (最後の終了日/時刻)  
  
## <a name="fields-in-the-query-expression-for-the-status-report"></a>状態レポートのクエリ式のフィールド  
 表示されるデータを指定するクエリ式のフィールドを変更することにより、インターチェンジ集計レポートをカスタマイズできます。 使用できるフィールドは以下のとおりです。  
  
|||||  
|-|-|-|-|  
|クエリ式のフィールド|有効な演算子|潜在的な値|既定で含まれますか。|  
|検索|[等しい]|トランザクション セットの集計レポート|指定あり (必須)|  
|インターチェンジの日時|[以下]<br /><br /> [以上]|特定の日時<br /><br /> [今日]<br /><br /> 昨日|はい<br /><br /> 注: は小で 1 回、クエリ式に 2 回含めることが、演算子と、大きい値が 1 回よりも-演算子は、範囲を指定するには|  
|[最大一致数]|[等しい]|整数 (既定値 50)|はい|  
|Direction|[等しい]|すべて (既定)<br /><br /> Receive<br /><br /> Send|不可|  
|受信者パーティ名|[等しい]|すべて (既定)<br /><br /> 特定のパーティ名 (AN 文字列)|不可|  
|送信者パーティ名|[等しい]|すべて (既定)<br /><br /> 特定のパーティ名 (AN 文字列)|不可|  
|[状態]|[等しい]<br /><br /> 等しくないです。|受理<br /><br /> 受理 (ただしエラーが発生)<br /><br /> 送信済み<br /><br /> すべて<br /><br /> 確認が必要<br /><br /> 確認は不要<br /><br /> 拒否しました|不可|  
|トランザクション セット ID|[等しい]|すべて (既定)<br /><br /> 特定のトランザクション セット ID|不可|  
  