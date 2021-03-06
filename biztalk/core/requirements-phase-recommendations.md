---
title: 要件フェーズの推奨事項 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0b510313-c3a7-42bc-9c9b-336c927a5d4a
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 6bb12022811aceb3c5a5311a6f44914ec60dbae0
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37004579"
---
# <a name="requirements-phase-recommendations"></a>要件フェーズの推奨事項
要件フェーズに関連付けられている主な成果物は、要件仕様、またはパフォーマンスの目標などの要件を含む機能仕様です。 パフォーマンスの正確なプロファイルが派生されるようにするには、これらの目標を決定するときに、システムのエンド ユーザーとビジネス所有者を含めることが非常に重要です。  
  
## <a name="establish-performance-criteria"></a>パフォーマンス条件の設定  
 パフォーマンスの観点からは、このフェーズの間に作成される機能仕様の最も重要な部分は、プロジェクトの詳細なパフォーマンスの目標の定義、およびパフォーマンス リリース条件の設定です。 パフォーマンス条件の定義には、3 つの重要な部分があります。  
  
- パフォーマンスを時間の関数として定義する曲線。  
  
- パフォーマンス関数に関連付けるパフォーマンス要件。  
  
- ファイルのサイズと種類の分布。  
  
  これらの条件は、後ほど[維持可能なパフォーマンスとは何ですか?](../core/what-is-sustainable-performance.md)  
  
  パフォーマンス目標に基づいて、アプリケーションのパフォーマンス リリース条件を決定します。 これらの条件によって、テストをとおして証明できる実現可能で測定可能な動作を具現化します。 アプリケーションは、すべてのリリース条件が満たされるまで、リリースされることはありません。また、リリース条件が実現可能でない場合は、リリース条件に対する例外として識別されます。  
  
  製品サイクルの初期のフェーズ中にリリース条件を設定することが非常に重要です。 そのようにすることによって、目標の内容、および設計と実装が終了する前に目標に到達しなかった場合の結果について、関係するすべてのユーザーが知ることになります。  
  
  また、パフォーマンス テスト ケースは、どのようにリリース条件が測定されるかに基づいて決定されるため、混乱を避けるために条件を詳細に説明する必要があります。 たとえば、特定のスループットを実現する必要があると述べる場合は、次の点を含める必要があります。  
  
- テストを実行する必要があるハードウェア。たとえば、サーバーの数と種類、ディスク速度または種類など。  
  
- テストされるシナリオ。たとえば、アプリケーションをとおしてどのようなパス メッセージが使用されるか。  
  
- どのように測定されるか。たとえば、パフォーマンス カウンター、カスタム コード、共有にメッセージが到着する回数の測定など。  
  
  リリース条件がどのような適切な形式になっているかを判断するために、すべてのユーザーが、説明に従ってリリース条件を調べることができるようになっており、条件を証明するためのテスト ケースを構築する方法を理解している必要があります。  
  
## <a name="identify-performance-risks"></a>パフォーマンスのリスクの特定  
 パフォーマンス リリースの目標と条件が十分に詳細に決定された後で、パフォーマンス リスク領域の最初の評価を実行できます。 この分析の目的は、必要な条件を満たすために設計における特別な注意、代替手段、または削除を必要とする可能性があるアプリケーションの部分を特定することです。  
  
 たとえば、各トランスポート アダプターの種類には、独自のパフォーマンスとスケールの特性があります。 目的のスループットが 1 つ以上のアダプターの種類 (受信または送信) の能力を超える場合、アダプターのスケール設定の代替手段の調査が必要になる可能性があります。  
  
## <a name="estimate-sizing"></a>サイズ調整の推定  
 設定された目標と条件に基づいて、目標を達成するために必要となるハードウェアのサイズ調整を推定するプロセスは、できるだけ早く開始することをお勧めします。 どのようなサイズ調整の推定についても、推定値は実際のテスト結果に基づいている必要があります。 プロジェクトの初期のフェーズの間に、それらの結果を外部ソースから取得する必要があります。 BizTalk Server デベロッパー センターでは、ケース スタディを読むことができます[ http://go.microsoft.com/fwlink/?LinkId=49339](http://go.microsoft.com/fwlink/?LinkId=49339)します。 ケース スタディでは、テストされるシナリオ、テストが実行されたハードウェア、およびテストの構成の詳細について説明しています。 これらのテスト ケースに対して実現されたパフォーマンスから推定して、システムの最初のサイズ調整の推定値を取得できます。  
  
 任意のアプリケーションで実行されているシステムのサイズを正確に予測する予測モデルやシミュレーションがないことに注意してください[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]します。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 独自のパフォーマンスに関する動作と共にをさまざまなアプリケーション ソリューションを展開するプラットフォームです。 このため、既存のケース スタディ結果を使用して派生した推定値は計画のための適切な開始点となりますが、システムの最終的なサイズは最も単純なアプリケーション アーキテクチャに対して調整する必要があります。  
  
## <a name="plan-for-sufficient-testing"></a>十分なテストのための計画  
 前述のように、現在、パフォーマンスの目標を満たすために必要なハードウェアを正確に予測するモデルやシミュレーションはありません。 これは、システムに目標を達成する能力があることを実際に証明する唯一の方法は、実稼働レベルのハードウェアでテストを行うことであることを意味します。 つまり、できるだけ実稼働の設定に近いハードウェアでのテスト ケースを実行することです。  
  
 計画の中でもこの部分は重要であり、維持可能なパフォーマンス、詳細なスループット プロファイルの理解、およびパフォーマンス リリース条件の原則を組み合わせたものになります。 テスト ケースは、既存のデータから推定することによって取得されたスループット プロファイルを使用して、リリース条件を一貫して測定するものである必要があります。 テスト ケースは持続性を念頭に置いて実行する必要があります。 維持可能なテストの例については、次のトピックを参照してください。  
  
-   [維持可能な最大のエンジン スループットの測定](../core/measuring-maximum-sustainable-engine-throughput.md)  
  
-   [維持可能な最大の追跡スループットの測定](../core/measuring-maximum-sustainable-tracking-throughput.md)  
  
## <a name="see-also"></a>参照  
 [プロジェクトの計画フェーズの推奨事項](../core/project-planning-recommendations-by-phase.md)   
 [デザイン フェーズの推奨事項](../core/design-phase-recommendations.md)   
 [実装フェーズの推奨事項](../core/implementation-phase-recommendations.md)   
 [検証フェーズの推奨事項](../core/verification-phase-recommendations.md)   
 [リリース フェーズの推奨事項](../core/release-phase-recommendations.md)