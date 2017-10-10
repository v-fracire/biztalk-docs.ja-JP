---
title: "設計フェーズの推奨事項 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ee3d183e-a6f3-47d0-90ac-99b12c064607
caps.latest.revision: "4"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a0f361734aa7539f12940212a339b582bb4f2641
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="design-phase-recommendations"></a>設計フェーズの推奨事項
設計フェーズの主な成果物は、システムの設計仕様と、システムの機能およびパフォーマンスを検証するためのテスト ケースの設計仕様です。 機能およびテストの実現可能性の調査は、通常、設計プロセスの一部として行われます。以下で説明するように、この調査には初期開発が含まれ、検証設計の場合は POC (Proof of Concept: 概念実証) 実装の早期テストも必要になります。  
  
## <a name="acquire-detailed-throughput-and-latency-profiles"></a>詳細なスループットと待機時間のプロファイルの取得  
 前のプロジェクト フェーズでパフォーマンス リリース条件を確立する際に使用した初期ロード プロファイルを基に、設計フェーズで詳細なスループットと待機時間のプロファイルを設定します。 可能な場合は実稼動システムからパフォーマンス データを取得します。 実稼動データを使用すると、現実的なパフォーマンス プロファイルを基に、設計フェーズでテスト ケースを設計できます。 実稼動データが取得できない場合は、予想される負荷から現実的なプロファイルを推定する必要があります。  
  
 設計フェーズでパフォーマンス テスト ケースを作成する場合は、実稼働環境で求められるシステムを忠実にエミュレートしたパフォーマンス プロファイルをテスト ケースに含めることが重要です。 現実的で維持可能なパフォーマンス プロファイルの作成の詳細については、次を参照してください。[維持可能なパフォーマンスは何ですか。](../core/what-is-sustainable-performance.md)  
  
## <a name="investigate-performance-risk-mitigations"></a>パフォーマンス リスクの緩和策の調査  
 要件フェーズで、必要なパフォーマンス目標の実現に対するリスクと可能な緩和策を特定しました。  リスクおよび緩和策は、設計フェーズのできる限り早い段階で調査する必要があります。これは、必要に応じて設計を変更するための時間を確保するためです。 まず特定した各リスクが問題になることを POC テストで実証し、次に緩和策をテストしてその有効性を評価する必要があります。  
  
 たとえば、FTP を使用して他のシステムと通信するレガシ システムがあるとします。 ここで、レガシ FTP サーバーと BizTalk Server FTP アダプターの組み合わせで実現可能なスループットのレベルを調べてみると、(要件フェーズでリリース条件として確立された) 目標のスループットが実現されないことがわかりました。 プロジェクトのリスクを軽減するために、次の方法は、要件フェーズで識別されます。  
  
-   FTP サーバーをスケール アップまたはスケール アウトし、特定のメッセージ タイプ専用の論理 FTP アドレスを複数作成して負荷を分散する。  
  
-   多数のメッセージをバッチとして単一ファイルで配信するようにレガシ システムを変更し、1 メッセージあたりの転送オーバーヘッドを軽減する。  
  
-   FTP よりも高速な別のプロトコル (MSMQ など) を使用するようにレガシ システムを変更する。  
  
 この例で最初に行う必要がある調査は、現在の FTP システムのパフォーマンスをテストしてリスクの存在を実証することです。 FTP サーバーからメッセージを受信するだけの簡単な概念実証ソリューションを構築および展開し、FTP 経路に必要な実稼動ロード プロファイルをそのソリューションに適用します。 必要な負荷をサーバーが維持できる場合は、リスクが顕在化しないため、詳細な調査を行う必要はありません。 必要な負荷をサーバーが維持できない場合は、コストおよびプロジェクト リスクが最も低く、問題を解決できる可能性が最も高い代替策を、概念実証を通じて調査する必要があります。  
  
## <a name="refine-system-size-estimate"></a>システム サイズの推定値の調整  
 設計フェーズで行った調査により、システムのパフォーマンス機能に関する貴重な経験的情報が得られます。  
  
 たとえば、FTP のパフォーマンスが低すぎると判明した上記の例について引き続き検討してみましょう。 メッセージング トランスポートとして MSMQ を使用するシステムが既に環境に組み込まれているため、MSMQ も使用するようにレガシ システムを変更することを決定しました。 ただし、MSMQ を採用した新しい POC のパフォーマンス テスト中に、メッセージ ボックス データベースがある SQL サーバーの CPU 使用率がほぼ常時 100% に達し、MSMQ 経路で必要なスループットを実現できないことがわかりました。  
  
 SQL Server の構成がアプリケーションに対して最適化されていると想定した場合、目的のスループットに対して SQL Server のハードウェアのサイズが明らかに不足しており、システム サイズを調整する必要があります。 この場合は、SQL Server のハードウェアに CPU を追加するか、より高速な CPU に交換するか、またはその両方を実行する必要があります。  
  
## <a name="see-also"></a>参照  
 [プロジェクト計画のフェーズの推奨事項](../core/project-planning-recommendations-by-phase.md)   
 [要件フェーズの推奨事項](../core/requirements-phase-recommendations.md)   
 [実装フェーズの推奨事項](../core/implementation-phase-recommendations.md)   
 [検証フェーズの推奨事項](../core/verification-phase-recommendations.md)   
 [リリース フェーズの推奨事項](../core/release-phase-recommendations.md)