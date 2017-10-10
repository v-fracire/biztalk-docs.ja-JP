---
title: "アダプターがサイズの大きいメッセージを処理する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c48671fd-b6cf-4507-92b4-35a4cd135714
caps.latest.revision: "15"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: fccfd1e988dc1395f14d6eb92a980ede184d0e0f
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-adapters-handle-large-messages"></a>アダプターがサイズの大きいメッセージを処理する方法
BizTalk メッセージング エンジンでは、サイズが非常に大きいメッセージを処理でき、メッセージの最大サイズに制限はありません。 ただし、最適なパフォーマンスとリソース管理を維持するにはメッセージ サイズの制限を考慮する必要があります。 メッセージ サイズが大きくなると、1 秒あたりの処理メッセージ数は減少します。 シナリオを設計し容量を計画するときには、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] で処理される平均的なメッセージ サイズ、メッセージの種類、およびメッセージの数を検討してください。  
  
## <a name="stream-based-processing"></a>ストリーム ベースの処理  
 アダプターの開発時にサイズの大きなメッセージの処理を考慮することは重要です。 サイズに関係なくデータ ストリーム全体をメモリに読み込むことは、BizTalk Server の処理が停止する可能性があるのでお勧めできません。 BizTalk メッセージング エンジンで処理されるメッセージのサイズと数によっては、仮想メモリが不足し問題が発生します。 メッセージは全体をメモリに読み込むのではなく、次のようにストリーム方式で処理してください。  
  
-   **メッセージを受信します。** 受信メッセージの場合、受信アダプターではネットワーク ストリームを BizTalk メッセージに関連付け、ストリームの "抽出" は BizTalk メッセージング エンジンで行います。  
  
-   **送信メッセージ。** 送信メッセージの場合、ストリームの抽出はアダプターで行います。 この方法により、メッセージ ボックス データベースから送信パイプラインを介して効率的にストリームが抽出されます。 さらに、アダプターから外部にストリーム方式でデータを送信します。  
  
 次の図に、メッセージング エンジンの受信側におけるストリーム ベースの処理を示します。  
  
 ![](../core/media/streambasedprocessing.gif "Streambasedprocessing")  
  
 アダプターでは、メッセージング エンジンにメッセージを送信するときに、データ ストリームを BizTalk メッセージに関連付けます。 一部のアダプターでは、これはネットワーク ストリームの実装となります。 アダプターからメッセージが送信されると、メッセージング エンジンでは受信パイプラインを実行します。 パイプラインの実行中、データの変更を必要とするパイプライン コンポーネントによってメッセージが複製され、新しいメッセージのストリームが前のメッセージのストリームに結合されます。 パイプラインの実行後、メッセージング エンジンでパイプラインからメッセージを取り出し、そのメッセージのストリームを繰り返し読み込みます。 つまり、前のストリームの読み込みを呼び出し、その読み込みによってさらに前のストリームの読み込みを呼び出すという方法で、ネットワーク ストリームまでさかのぼります。 メッセージング エンジンでは読み込んだデータを定期的にメッセージ ボックスにフラッシュし、フラット メモリ モデルを維持します。  
  
 **トラブルシューティングのヒント:**送信側では、アダプターがストリームの読み取りを行う。 送信パイプラインによって昇格または書き込みが行われるメッセージ コンテキスト プロパティを、送信アダプターが読み込む場合、これらのプロパティはストリーム全体が読み込まれるまで書き込まれません。 ストリームが完全に読み込まれて初めて、アダプターではすべてのパイプライン コンポーネントの実行が完了したことを確認できます。  
  
## <a name="locating-a-specific-byte-in-the-stream"></a>ストリーム内の特定バイトの指定  
 シナリオによっては、エラーによって中断されるメッセージを処理するために、アダプターが、ストリームを先頭方向に向かって検索する必要があります。 この例として、チャンク エンコードを使用してデータを受信し、送信請求 - 応答の組み合わせで応答メッセージを送信する HTTP アダプターがあります。  
  
 ただし、多くのシナリオではデータ ストリームを追跡できません。 たとえば、チャンク エンコードを使用してデータを受信する HTTP アダプターの場合、 エラーが発生したメッセージを検出できるようデータ ストリームを設計するには、アダプターでデータを読み込むたびにメモリまたはディスクにキャッシュする必要があります。 これは明らかに最適な処理でなく、余分なリソースを必要とします。 また、追加設定なしで使用できるパイプライン コンポーネントの多くは順方向専用のストリーミング方式で動作します。 このようなシナリオと呼ばれるヘルパー クラスが使用 SDK の BaseAdapter **VirtualStream**です。 この機能を含むファイルは VirtualStream.cs という名前で用意されています。  
  
> [!NOTE]
>  VirtualStream.cs ファイルは、パイプラインの SDK サンプルの 2 つの場所にある — \samples\pipelines\arbitraryxpathpropertyhandler および \samples\pipelines\schemaresolvercomponent\schemaresolverflatfiledasm です。  
  
 仮想ストリームは、ストリーム内のデータをしきい値までメモリ ストリームにキャッシュし、しきい値を超えた分を安全なディスク上の場所にオーバーフローさせるという概念に基づいています。 ストリームが閉じられると、ディスク上のオーバーフロー ファイルは自動的に削除されます。 順方向専用のストリームはこの方法で設計できます。