---
title: ボトルネックを調査 |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2ab8e485-ffe5-4f71-9ce2-f72c0c939e5d
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e34d01bbfafd1a05f87fff5cda2b21764d43f42b
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22298842"
---
# <a name="investigating-bottlenecks"></a>ボトルネックを調査
このトピックでは、ボトルネックを調査するための推奨プロセスについて説明します。  
  
## <a name="what-is-the-source-of-the-problem"></a>問題の原因は何ですか。  
 ボトルネックの原因がハードウェアまたはソフトウェアに関連する可能性があります。 リソースが使用されていない場合に、通常、ボトルネックを示す値。 ボトルネックは、ハードウェアの制限、非効率的なソフトウェア構成、または両方で発生することができます。  
  
 ボトルネックの特定では、あるボトルネックを緩和すると次のボトルネックが見つかることもまれではなく、作業を積み重ねが必要になります。 こうしたボトルネックの特定と緩和について科学的に説明することがこのトピックの目的です。 システムは、短期間なら最大限の性能を発揮できます。 しかし、スループットを維持するには、そのシステムの最も遅いコンポーネントの速度でしか処理できなくなる場合もあります。  
  
## <a name="using-an-iterative-approach-to-testing"></a>テストを反復的な方法を使用します。  
 エンドポイント (入り口/出口)、システムまたは中間 (オーケストレーション/データベース) でボトルネックが発生することができます。 ボトルネックを特定した後は、ソースを識別するのに構造化されたアプローチを使用します。 ボトルネックが容易になりますが後、もう一度ように新しいボトルネックが生じていないことされて別の場所、システムでパフォーマンスを測定する必要があります。  
  
 識別するボトルネックを修復するプロセスは、反復的な方法で行う必要があります。 一度に 1 つだけのパラメーターを異なる、各テストの実行中に同じ手順を繰り返しますおよび単一の変更の影響を確認するパフォーマンスを測定します。 一度に複数のパラメーターを変更すると、変更の効果がわからなくなってしまう可能性があります。  
  
 たとえば、パラメーター 1 を変更するには、パフォーマンスが向上します。 ただし、パラメーター 1 の変更を組み合わせて 2 番目のパラメーターを変更することが悪影響を与えます、パラメーター 1 の変更の利点を負数化します。 これは、効果はゼロ net につながるとさまざまなパラメーター 1 の効果が偽陰性、偽陽性さまざまなパラメーター 2 の影響にできます。  
  
## <a name="testing-consistency"></a>テストの一貫性  
 設定を変更した後、パフォーマンス特性を測定を行う変更の結果を検証する必要があります。  
  
-   **ハードウェア -** ハードウェアをさまざまな一貫性のない動作が発生し、誤解を招く結果を生成するために、一貫性のあるハードウェアを使用します。 たとえば、BizTalk ソリューションのパフォーマンスをテストするのにラップトップを使用するはされません。  
  
-   **テストの実行期間 -** 結果が維持可能なことを確認する固定最低限の期間のパフォーマンスを測定します。 長期間のテストを実行するようになります、初期ウォーム/増加の場所のすべてのキャッシュが設定されて、データベース テーブルに達しました予期される数は、および調整を 1 回のスループットを制御するための十分な時間を指定した定義済みの期間を通じて、システムになりましたしきい値がヒットします。 このアプローチは、維持可能な最大スループットを特定するのに役立ちます。  
  
-   **テスト パラメーター:** テストの実行するテストの実行からテスト パラメーターは変わりません。 たとえば、マップの複雑さやドキュメントのサイズを変更すると、スループットや待機時間の結果が変わってしまう可能性があります。  
  
-   **クリーンアップ状態 -** テストが完了したら、テスト環境の状態が次のテストを実行する前にクリーンであることを確認します。 たとえば、履歴データは、実行時のスループットに影響を与えるデータベース内を構築することができます。 サービス インスタンスのリサイクルは、メモリ、データベース接続、およびスレッドのようにキャッシュされたリソースを解放するのに役立ちます。 作成して」の説明に従って、bts_CleanupMsgbox ストアド プロシージャを実行することがあります、テスト環境に[テスト環境でメッセージ ボックス データベースからデータを手動で消去する方法](http://go.microsoft.com/fwlink/?LinkId=158064)(http://go.microsoft.com/fwlink/?LinkId=158064)。 このスクリプトは、実行の間を最新の状態に関して、メッセージ ボックスに、BizTalk Server のテスト環境を返します。 スクリプトは、実行中のすべてのインスタンスとなどの状態、メッセージ、およびサブスクリプションの場合、それらのインスタンスに関するすべての情報を削除がため re-enlist、オーケストレーションまたは送信ポートにする必要はありませんにすべてのアクティベーションのサブスクリプションのままにします。 このツールが実稼働システムでサポートされていないことに注意してください。  
  
-   **パフォーマンス テストとチューニング -** テスト カテゴリの目標は、アプリケーションのパフォーマンスとスループットを最大化し、システムの最大持続可能なスループット (MST) を検索することです。  計画と維持可能な最大のパフォーマンスの測定の詳細については、次を参照してください。[継続的なパフォーマンスの計画](http://go.microsoft.com/fwlink/?LinkId=158065)(http://go.microsoft.com/fwlink/?LinkId=158065) および[維持可能なパフォーマンスは何ですか。](http://go.microsoft.com/fwlink/?LinkId=132304) (http://go.microsoft.com/fwlink/?LinkId=132304)。  
  
     MST は、システムが実稼働環境で無制限に処理できるメッセージ トラフィックの最大負荷です。 実稼働に移行する前に、パフォーマンスとスループットのすべての BizTalk アプリケーションをテストしてください。 少なくとも、最も一般的な使用シナリオを表しているテスト_ケースの代表的なセットを実行する必要があります。 予想される負荷に対してテストして、実稼働環境の特性に一致する別の環境で負荷がピークのことをお勧めします。 この環境は、すべての企業の標準的なサービス インストールされ、監視エージェント、およびウイルス対策ソフトウェアなど、実行が必要です。  
  
-   また、実行されているその他の BizTalk アプリケーションの横には、実稼働環境では、同じハードウェア上での BizTalk アプリケーションをテストすることをお勧めします。 これら他の BizTalk アプリケーションは、BizTalk Server、SQL Server、ネットワーク I/O、およびディスク I/O の負荷を高めます。 さらに、1 つの BizTalk アプリケーション可能性があります (きたら、スプールの深さが大きすぎてなど) を調整します。 すべての BizTalk アプリケーションは、パフォーマンスをする必要があります/ストレス テストから実稼働に移行します。 さらに、ピーク ロードから回復するシステムに要する時間を決定する必要があります。 システム完全復旧しない負荷のピーク時から [次へ] のピーク時の負荷が発生する前に、問題を取得したらです。 システムがさらに表示されます、さらに分離し、決してできるを完全に回復します。  
  
## <a name="expectations-throughput-vs-latency"></a>待機時間とスループットを期待します。  
 ある程度のスループットや待機時間、配置済みのシステムを想定できます。 反対側の要求をシステムに配置する高いスループットと低待機時間を同時に実現しようとしています。 妥当な待機時間では、最適なスループットを期待できます。 スループットが向上しますが、として、システム値の上昇 (など、CPU 消費率が高くより高いディスク I/O の競合、メモリ不足、およびロックの競合が大きい) 強調します。 このような状況では、待機時間にマイナスの影響があります。 システムの最適処理能力を探索するを特定し、ボトルネックを最小限にすることお勧めします。  
  
 完了したインスタンスがデータベース内に存在するには、ボトルネックが発生します。 ボトルネックが発生すると、パフォーマンスが低下することができます。 ドレインするシステムのための十分な時間を与えると、問題を解決するのに役立ちます。 バックログが蓄積された原因を特定と問題を修正することが重要です。  
  
 バックログの原因を検出するには、履歴データを分析し、(を使用パターンを検出し、バックログの原因を診断) パフォーマンス カウンターを監視できます。 一般的には、大量のデータを毎晩バッチ方式で処理されるときにバックログが発生します。 システムとその機能のバックログから回復する容量を検出すると便利です。 この情報は、overdrive シナリオとバッファーの大きさを処理するためにスループットの予想外の急増に対応するシステム内で対応するためのハードウェア要件を予測するのに役立ちます。  
  
 パフォーマンス カウンターを監視するには、実行時に発生する可能性がある潜在的なボトルネックを individuate のに役立つことができます。 ただし、CPU またはメモリのボトルネックの発生源できる場合、ソリューションを構成するカスタム コンポーネントのいずれかの疑いが、ときに強くお勧めで使用する、プロファイリング ツールなどの Visual Studio プロファイラーまたはアリ パフォーマンス プロファイラー パフォーマンス テスト絞り込み、問題を生成するクラスを明確に individuate です。 当然ながら、アプリケーションのプロファイリングでは、パフォーマンスに干渉します。 したがって、メモリ消費量、CPU 使用率や待機時間が発生するこれらのコンポーネントを individuating にこれらのテストの重点を置きますが、これらのテスト中に収集された図形を破棄する必要があります。  
  
 最適なスループット必要詳細なシステムをチューニング、展開されたアプリケーション、長所と、システムの脆弱性および特定のシナリオの使用パターンの詳細についてはします。 ボトルネックを特定し、維持可能な最大スループットを確実に予測するためには、実稼働環境で使用されるものに近いトポロジで徹底的なテストを行うしかありません。 別のホスト インスタンスに (受信場所、送信ポート、オーケストレーション) 1 つの成果物を分離して、パフォーマンス モニター ツール内の正しいカウンターの設定を絞り込むために重要な特定のユース ケースに対してロード テストとストレス テストを実行するときに、ボトルネックの原因。  
  
 このセクションの他のトピックでは、そのトポロジの定義のプロセスを指示し、を軽減し、ボトルネックを回避する方法についてガイダンスを提供します。  
  
## <a name="scaling"></a>スケーリング  
 展開されたトポロジのさまざまな段階でボトルネックが発生することができます。 ボトルネックは、スケール アップまたはスケール アウト環境のいずれかによって対処できます。 スケール アップは、既存のコンピューターをアップグレードするプロセスです。 たとえば、4 プロセッサのコンピューターから BizTalk Server コンピューターをアップグレードするには、8 つのプロセッサのコンピューターだけでなく、既存の Cpu の置換と以上の RAM を追加するのにします。 この方法では、ドキュメントの解析とマッピングなどのリソースを消費するタスクを高速化できます。 スケール アウトは、デプロイにサーバーを追加するプロセスです。 スケール アップまたはアウトするかどうかは、ボトルネックになっていると、構成するアプリケーションの種類によって異なります。 アプリケーションは、スケール アップまたはアウトを活用できる一から構築する必要があります。次のガイダンスでは、発生したボトルネックに基づいてハードウェア展開トポロジを変更する方法について説明します。  
  
 **スケール アップ**、BizTalk ソリューションを実行していることを意味が (CPU の追加など、およびメモリ) のハードウェアをアップグレードします。 1) スケール アウトは、高価すぎますまたは 2) スケール アウトできませんの解決に役立つボトルネックになっているときにスケール アップを確認する必要があります。 たとえば、変換して、高速なマシンでタスクを実行する場合は、サイズの大きいメッセージを処理に費やされた時間を大幅に削減することができます。  
  
 **スケール アウト**アプリケーション プラットフォームは、BizTalk Server グループに BizTalk のノードを追加して、それらを使用して、ソリューションの 1 つまたは複数の部分を実行するので構成されています。 場合 1) に必要な分離送信、受信、処理を追跡ホスト、または 2) のスケール アウトを見てくださいメモリ、I/O またはネットワーク I/O のリソースは単一のサーバーすべてに使用されています。 負荷分散できるように複数のサーバーです。ただし、BizTalk Server グループに新しいノードを追加するには、メッセージ ボックス データベースのロックの競合が増加します。  
  
 したがって必要があるスケール アップまたはスケール アウトしますか。 1 つのタスクを可能になったため、BizTalk ソリューションの待機時間を減らすことができます、プラットフォームのスケール アップ (たとえば、メッセージのマッピング) 高速に実行します。 スケール アウトを向上できます最大持続可能なスループットとスケーラビリティの BizTalk ソリューションのため、複数のマシンに負荷を分散することができます。  
  
## <a name="see-also"></a>参照  
 [検索して、ボトルネックを解消します。](../technical-guides/finding-and-eliminating-bottlenecks.md)