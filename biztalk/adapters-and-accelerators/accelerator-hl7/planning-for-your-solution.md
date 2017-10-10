---
title: "ソリューションの計画 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Greenfield project
- security, BTAHL7
- BTAHL7, security
- installing, planning
- installing, installation types
- HL7, security
- security, HL7
- Embedded installation
- Migration project
- Coexistence installation
ms.assetid: a108c6d0-dd51-4bf9-85a0-103f60fae971
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 73b39dc63621583fc0ecc495d99e9307a2308db6
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="planning-for-your-solution"></a>ソリューションの計画
このセクションの考慮事項を計画するときに関する情報を提供する、 [!INCLUDE[btsCoName](../../includes/btsconame-md.md)] [!INCLUDE[HL7_CurrentVersion_FirstRef](../../includes/hl7-currentversion-firstref-md.md)]ソリューションです。  
  
 次の方法では、BTAHL7 を実装できます。  
  
-   **未開発プロジェクト**です。 このシナリオは、BTAHL7 の新規インストールです。  
  
-   **移行プロジェクト**です。 このシナリオでは、医療保険の組織が既存の integration broker をしだいに減らしときに発生します。 組織は、BTAHL7 に移行します。  
  
-   **共存**です。 このシナリオには、別の統合エンジンと BTAHL7 サイド バイ サイドのインストールが含まれます。  
  
-   **埋め込み**です。 このシナリオには、BTAHL7 の基幹業務アプリケーション内で統合が含まれます。 そのアプリケーションに HL7 メッセージング機能を追加するのにには、BTAHL7 を使用します。  
  
 ユーザーは、最初の場所を作成するまでにかかる作業と比較して時間の経過と共にアプリケーションを管理するまでにかかる労力を過小評価する傾向があります。 これは、一連の複雑なデータの処理と管理タスクを実行する必要がある大規模な分散機関の検索時に特に当てはまります。 病院または統合されたヘルス配信組織がこのような機関の優れた例を示します。 このような機関に直面して多数のアプリケーションから重複して問題のあるデータ エントリ、ユーザーと管理者のトレーニングを提供する必要がないようにアプリケーションに渡される情報を有効にする、関数をサポートするためにソフトウェアを提供する必要があります、ソフトウェア、および、廃止、または期限切れのアプリケーションの置換がによって改善ものを提供します。 この交換プロセスでは、テストおよび教育用の独自の要件があります。  
  
 これは不可能 (負担) を 1 つのすべての機能を管理するには、このような機関の統合されたアプリケーション。 最初の段階で、金融機関は、1 つの仕入先への投資を占有する予定がないと、1 つのベンダーを使用して必要なすべての関数は見つかりません。 2 番目の場所に制度化された処理の単純な運用のニーズに不可能になる 1 つの統合アプリケーションの条件が満たされる機関です。 したがって、機関は複数のアプリケーションのニーズをサポートします。 これらのアプリケーションと相互運用するためには、アプリケーションでは、情報を交換するインターフェイスが必要があります。 アプリケーションと関連するインターフェイスの数が非常に大きいでは多くの場合です。 この分散アプリケーション アーキテクチャを指定するには、インターフェイス エンジンは、時間の経過と共に、機関向けデータ処理を管理するためのキーのインストルメント化です。 重要な問題は、移行、マッピング、および education です。 BTAHL7 のジョブは、簡単かつできるだけ効率的にこれらの問題に対処するのには。  
  
-   **マッピング**です。 インターフェイスの実装では、最大のジョブには、アプリケーションまたはデータベースの構造体、インターフェイスで使用するデータ構造の間のマッピングを作成します。 ツールでは、簡単かつ自然なためには何もお勧めします。 さらに、マッピング ドキュメントが必要になるインターフェイスやアプリケーションの開発者によって使用される仕様ので、そのドキュメントを簡単に生成できる必要があります。 BTAHL7 構成エクスプ ローラーを使用する[!INCLUDE[btsCoName](../../includes/btsconame-md.md)][!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]と[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)]ツールを開発し、これらのマップを実装します。  
  
-   **移行**です。 アプリケーションを変更すると、長期にわたってアプリケーションの相互作用を管理する必要があります。 1 つのアプリケーションを置き換えることに関連する問題を検討する場合、必要では、適用可能なインターフェイスをデータ ソース マッピングを更新します。 インターフェイス エンジンによる必要がありますこれらの 1 つ。 インターフェイスがインストールされているし、インターフェイスの標準時間の経過と共に変更を検討する必要があります。 時間の経過と共にインターフェイスの標準変更を多く使用されている標準に移行する必要がありますが表示されます。 今後のインターフェイスを加えたのアカウントを移行計画が考慮をお勧めします。 標準、間と、標準の異なるバージョン間にマップする必要があります。 1 つの標準の範囲内でさらに、— HL7 V2 など 1 つは特に柔軟性の高い — (多くのアプリケーション) の間で同じ標準の複数の実装に対処する必要があります。 インターフェイス エンジンは、管理が容易であるようにこのような複雑さで処理する必要があります。  
  
     キーへの移行タスクへのインターフェイスの本体の 1 つの標準の移行です。 ここでは、タスク、新しいを古いバージョンを使用するすべてのマッピングを移行する — アカウント インターフェイスの特定のローカリゼーションと拡張機能で使用すると、できる複雑なプロセスです。 ツールには、この移行にサポートを提供する必要があります。  
  
     追加のメッセージの種類のスキーマの名前空間を指定するのにには、BTAHL7 構成エクスプ ローラーの検証 タブを使用します。  
  
-   **教育**です。 管理とアプリケーションをサポートする関係者は、随時変更されます。 さらに、インターフェイスはアプリケーションのコレクションの相互運用機能をサーバーの全体では後のドキュメントがありますはキーの全体的なエンタープライズを管理するツールです。 これら両方の理由は、使いやすく、保守し、やすい) インターフェイスの仕様、b) と、アプリケーションや introversion マッピング、および c) 際の根拠をカスタマイズ、およびアクティビティのドキュメントを提供に大切です。  
  
## <a name="see-also"></a>参照  
[HL7 アクセラレータと使用可能な BizTalk ツールを説明します。](../../adapters-and-accelerators/accelerator-hl7/learn-the-hl7-accelerator-and-the-biztalk-tools-available.md)