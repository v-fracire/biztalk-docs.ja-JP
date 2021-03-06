---
title: 実装フェーズの推奨事項 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 04877156-cc32-480b-8410-d26eb073c327
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: fce6d7df21f15b40e0312438394859f4b94b7fc2
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22257402"
---
# <a name="implementation-phase-recommendations"></a>実装フェーズの推奨事項
実装フェーズでは、要件フェーズと設計フェーズの成果物を取得し、適切なテクノロジを使用してそれらを実装します。 検証テストについては、このフェーズでテスト ケースを完了し、自動化して検証テストに備えます。 通常、このフェーズでシステムの初期バージョンに関する多数のテストを実施します。テストは、システムの検証だけでなく、テスト ケース自体に問題がないかどうかも検証します。  
  
## <a name="implement-performance-test-cases"></a>パフォーマンス テスト ケースの実装  
 要件フェーズと設計フェーズでは、システムのパフォーマンスがパフォーマンス リリース条件を十分に満たしていることを立証するためのテスト ケースを定義し、設計しました。 実装フェーズでは、これらのテスト ケースを実装して自動化し、実際に実行してみることで、システム各部のコードが完了した時点で、パフォーマンス検証テストをスムーズに実施できるようにします。  
  
 実装フェーズの間に、テストのセットアップ、実行、結果分析を可能な限り自動化することが重要です。 パフォーマンス テストの数が非常に多くなる場合もあれば、それぞれのテストに時間がかかる場合もあります。テストを自動化しておけば、少ない担当者でテストを効率的に実行できます。 また、パフォーマンス ボトルネックの識別と修正を行うことにより、テスト パスの間に検証テストが何度も実行されることが予想されます。 テストを自動化すれば、ビルド間でのパフォーマンス検証の再実行がより簡単でより速くなり、一貫性も増します。  
  
## <a name="build-the-performance-test-bed"></a>パフォーマンス テスト ベッドのビルド  
 すべてのパフォーマンス テストを一貫性のある再現可能な方法で実行することが非常に重要です。 テスト結果を比較可能にするため、まったく同じハードウェアを使用して、ベースラインを確立してテストを実行することが重要です。 ハードウェア変数は、ソリューション アーキテクチャによってさまざまであり、テスト結果に大きな影響を及ぼす可能性があります。  
  
 たとえば、2 つのサーバーが異なるレベルのメモリ キャッシュを持つことはサーバー構成を見てもすぐには判別できない場合もありますが、使用可能なメモリ キャッシュは、それ以外がまったく同一構成のサーバーであっても結果に大きな影響を及ぼすことが知られています。 常に一貫したテスト ベッドでテストを実行することで、比較可能性の問題をすべて取り除くことができます。 新しいシステム サイズの推定値への調整などハードウェア構成を変更する必要がある場合は、ベースラインを再確立することで比較が可能になります。  
  
## <a name="begin-performance-validation-testing"></a>パフォーマンス検証テストの開始  
 パフォーマンス テストは、ほとんどの場合、テストの実装と平行して開始します。  リリース条件の検証は、早く始めるほど問題が発見されたときに早く対処できるので、可能な限り早期に開始することが求められます。  
  
 公式テストの開始時における主な考慮事項は、テスト対象のシステムまたはその一部の稼働準備についてです。 システムの稼働準備は個別の判断によるしかありませんが、以下に示す要素を考慮に入れる必要があります。  
  
 テスト対象となるシステム各部のコードは完成しているか。 追加するコードがまだ大量にある場合は、テストできる状態になるまで、他の作業を優先することをお勧めします。  
  
 システムの機能テストは正常に実行されたか。 パフォーマンス テストの進行を妨げる機能上の問題を見つけるためだけに、システムまたはサブシステムのパフォーマンス テストをセットアップして開始するのは、たいへんな時間の浪費となり非効率となる可能性があります。 パフォーマンス テストを始める前に、経路について十分な機能テストが行われていることを確認してください。  
  
 テストするシステムまたはサブシステムのリスクはどのくらいのレベルか。 システムで最初に検査する経路は、パフォーマンスに関するリリース条件を満たすことについて最も高いレベルのリスクを含んでいる経路にする必要があります。 システムのボトルネックをプロジェクトのライフ サイクルの早期に識別することで、進路を変更するための時間的な余裕を作ることがたいへん重要です。  
  
## <a name="see-also"></a>参照  
 [プロジェクト計画のフェーズの推奨事項](../core/project-planning-recommendations-by-phase.md)   
 [要件フェーズの推奨事項](../core/requirements-phase-recommendations.md)   
 [設計フェーズの推奨事項](../core/design-phase-recommendations.md)   
 [検証フェーズの推奨事項](../core/verification-phase-recommendations.md)   
 [リリース フェーズの推奨事項](../core/release-phase-recommendations.md)