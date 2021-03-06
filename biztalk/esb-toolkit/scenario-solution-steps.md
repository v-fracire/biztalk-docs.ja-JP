---
title: ソリューションのシナリオの手順 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 77751c15-9b67-4587-8bc8-2be65f13d339
caps.latest.revision: 2
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: dff3b2feda86ad0b8edbbded26a290c7276a63af
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22294842"
---
# <a name="scenario-solution-steps"></a>ソリューションのシナリオの手順
ESB 例外管理フレームワークでは、このトピックで前述したよう、請求書メッセージの処理中に、エラーの原因となる無効なデータが含まれる場合、例外を処理するため、簡単なソリューションを提供します。 以下は、1 つの方法がかかる場合があります。  
  
1.  チームの開発者に、Microsoft BizTalk に基づいて最後に配置された、財務報告アプリケーションに対する責任を割り当てます。  
  
2.  ESB の管理ポータルで新しい ESB フォールト メッセージが到着します。メッセージでは、財務報告の BizTalk アプリケーション内のオーケストレーションでデータ整合性の問題を示します。  
  
3.  管理者やオペレーターに通知が新しい例外の開発者または例外が発生したときに、開発者が自動で通知を登録します。 次の理由のいずれかのこの通知が発生する可能性があります。  
  
    -   これは、例外でイベントに基づくビジネス アクティビティ監視 (BAM) の定義済みのしきい値を超えたために発生します。  
  
    -   これは、特定のアプリケーション、サービス、スコープ、および開発者には、例外を転送するエラー コードの BizTalk サブスクリプションが存在するために発生します。  
  
4.  開発者は、エラー メッセージ、個別のオーケストレーションのメッセージと、永続化されたコンテキスト プロパティの値を調べます。 開発者は、ESB の管理ポータルや BizTalk サブスクリプションを通じて Microsoft Outlook を使用して、この情報を表示できます。  
  
5.  開発者は、これは、一般的なエラーであることを決定します。 手動による介入と修正は、システムに再送信を続けて、財務チームが、必要があります。  
  
6.  開発者は、作成し、特定のアプリケーションと例外の種類をサブスクライブする独立した BizTalk オーケストレーション プロジェクトを展開します。  
  
7.  オーケストレーション プロジェクトで、ESB フォールト メッセージから無効なメッセージを取得、財務チーム修正のためにメッセージを送信、修正されたメッセージをオーケストレーションに関連している、およびを再送信します。  
  
8.  1 週間後、開発者は、このソリューションの配置以降に無効なメッセージのアプリケーションの例外の傾向の減少が大幅に設定したを検出する ESB の管理ポータルに移動します。