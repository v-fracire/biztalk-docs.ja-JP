---
title: "BizTalk Server がサイズの大きいメッセージを処理する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62c070be-dff5-4349-9e36-dd3a7caf1752
caps.latest.revision: "33"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 26ecae241e1e41fdb67204c7975741a240979c2d
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-biztalk-server-processes-large-messages"></a>BizTalk Server がサイズの大きなメッセージを処理する方法
## <a name="what-is-a-large-message"></a>サイズの大きなメッセージとは何ですか?  
 残念ながら、この質問に対しては、具体的なメッセージ サイズを直接回答することはできません。Microsoft [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] システムの個々のボトルネックによって回答は変わります。 サイズの大きなメッセージに関係する問題は、次のカテゴリに分類できます。  
  
-   **メモリ不足エラー**特定種類のマッピング、検証、およびプロパティの昇格などのメッセージの処理がメモリにメッセージ全体をロードします。 メモリのメッセージのサイズが使用できるリソースを超えると、メモリ不足のエラーが発生します。 このカテゴリに分類されるメッセージのサイズのしきい値は、メモリに読み込まれないメッセージのサイズのしきい値よりも大幅に小さくなります。 たとえば、XML に解析されてマップされる 10 MB のフラット ファイルは、10 倍以上大きくなって 100 MB 以上のメモリを使用する場合があります。一方、解析されないでマップされる 100 MB の XML ドキュメントは、メッセージ ボックス データベースにストリーム送信される際に 1 MB のメモリのみ使用します。  
  
-   **メモリに読み込まれないメッセージのパフォーマンスに関する問題**メッセージをメモリに読み込まれる必要はありませんが、.NET XmlReader インターフェイスを使用して、メッセージ ボックス データベースにストリーム送信されます。 メモリに読み込む必要のあるメッセージのようなサイズ制限はありません。その一方で、メッセージ ボックス データベースにストリーム送信されるメッセージを BizTalk Server が処理する方法に影響する重要な要因がいくつかあります。  
  
## <a name="factors-that-affect-the-processing-of-large-messages"></a>サイズの大きなメッセージの処理に影響を及ぼす要因  
 元のメッセージのサイズ、メッセージ形式、およびメッセージ処理の種類は、すべて BizTalk Server がサイズの大きなメッセージを処理する方法に影響を与えます。  
  
-   **元のメッセージ サイズ**BizTalk Server で受信したメッセージのサイズはの大きさ、メッセージが BizTalk Server によって処理されるときに、最も明確に示します。 メッセージの元のサイズは、メッセージがメッセージ ボックス データベースにストリーム送信される場合よりもメッセージ全体がメモリに読み込まれる場合に、パフォーマンスに大きな影響を及ぼします。  
  
-   **メッセージ形式**で 2 つの主な形式のいずれかの BizTalk Server にメッセージを受信します。 XML ファイルまたはフラット ファイル。  
  
    -   **XML ファイル**BizTalk Server でパススルー ルーティング以外のメッセージに対する処理を実行するためには、メッセージが XML ファイルの形式である必要があります。 処理対象のファイルを XML 形式で受信すると、ほとんどの場合、元のサイズが保存されます。  
  
    -   **フラット ファイル**フラット ファイルは BizTalk Server でパススルー ルーティング以外の処理を行う前に、XML 形式に解析する必要があります。 XML ファイルでフラット ファイルを解析すると、ファイルのサイズが非常に大きくなる可能性があります。 フラット ファイルには、データに関する説明情報を持つ XML タグが含まれません。 一方、XML ファイルは、説明的な XML タグにすべてのデータを格納します。 一部のシナリオでは、解析を行うと、ファイルの XML タグに含まれる説明的なデータの量に応じて、フラット ファイルのサイズが 10 倍以上大きくなる場合があります。  
  
    -   **フラット ファイル ドキュメントの XML ドキュメントに単一の CDATA セクション ノードでラップ**この種類のドキュメントは、XML とフラット ファイルの両方の組み合わせとは問題となるため、BizTalk Server を使用して、ラップされたフラット ファイル ドキュメント全体を前に、メモリに読み込む必要がありますこれを処理します。  
  
-   **メッセージ処理の種類**BizTalk Server では、メッセージ処理の 2 つの種類があります。 ルーティングのみとマッピングします。 実行されるメッセージ処理の種類に関連付けられるパフォーマンス変数は、メッセージのサイズとメッセージをメモリに読み込むかどうかです。  
  
    -   **ルーティングのみ**昇格させたメッセージ プロパティに基づいてメッセージをルーティングする場合に BizTalk Server を使用してのみ、.NET XmlReader インターフェイスを使用してメッセージ ボックス データベースに、メッセージをストリーミングし、メッセージ部分が個別にはできませんメモリに読み込まれます。 このシナリオでメモリ不足エラーは問題でありの主な考慮事項は、メッセージ ボックス データベースに書き込むために非常に大きなメッセージ (100 MB を超える) に必要な時間。 BizTalk Server 開発チームでは、ルーティングのみを行う場合に、最大 1 GB までメッセージを処理できることを確認しています。  
  
         このシナリオでパフォーマンスを決定する主な要因は、**サイズの大きいメッセージのフラグメント サイズ**データベースにデータを分割するために使用します。 **サイズの大きいメッセージのフラグメント サイズ**で構成可能なオプションは、 **BizTalk グループのプロパティ**の構成 ページで 102,400 バイト (100 KB) の既定値です。 この値を大きくすると、メッセージをメッセージ ボックス データベースにストリーム送信するために必要なラウンド トリップの回数が少なくなります。  
  
    -   **マッピング**マップでドキュメントを変換すると、メモリを消費する操作が指定できます。 マップでドキュメントを変換すると、BizTalk Server は、メッセージを .Net XSLCompileTransform クラスに渡します。このクラスは XSL スタイル シートを読み込みます。 Load メソッドが正常に完了すると、複数のスレッドから同時に Transform を呼び出すことができます。 [XslCompiledTransform クラス](http://go.microsoft.com/fwlink/p/?LinkID=282683)XSLCompiledTransform クラスについて詳しく説明します。  
  
         [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] は、変換中にドキュメントをメモリに読み込むための構成可能なメッセージ サイズのしきい値を設定して、サイズの大きなドキュメントのメモリ管理を大幅に改善します。 このしきい値よりも小さいサイズのメッセージは、メモリで処理されます。このしきい値よりも大きいサイズのメッセージは、メモリの要件を減らすためにファイル システムにバッファリングされます。 既定のメッセージ サイズのしきい値は 1 MB です。  
  
## <a name="guidelines-for-processing-large-messages"></a>サイズの大きなメッセージを処理するためのガイドライン  
 BizTalk Server でサイズの大きなメッセージを処理する場合は、これらのガイドラインに従って、パフォーマンスを高めます。  
  
1.  マッピング中にファイル システムにバッファリングされるドキュメントのメッセージ サイズのしきい値を大きくします。 サイズのしきい値を変更するには、という名前の DWORD 値を作成**TransformThreshold** BizTalk Server レジストリの次の場所に。  
  
    ```  
    HKLM\Software\Microsoft\BizTalk Server\3.0\Administration\TransformThreshold  
    ```  
  
     この値を作成した後、バイト数を 10 進数で入力して、新しいしきい値を設定します。 たとえば、10 進数値 2097152 を入力して、メッセージ サイズのしきい値を既定値の 1 MB から 2 MB に増やします。 スループットを向上させるため、使用できるメモリ容量が大きいシステムではこの値を大きくしてください。 ドキュメントをディスクにバッファリングすると、全体のスループットに対してメモリが節約されます。  
  
    > [!NOTE]
    >  既定では、マッピング中に、ファイル システムにバッファリングされるドキュメントは書き込むことが、 *%temp%* BizTalk Server コンピューターのディレクトリ。 設定を変更、 *%temp%*環境変数マッピング中に、ファイル システムにサイズの大きいメッセージをバッファリングするときにパフォーマンスを向上させるために非システムのディスクにします。  
  
2.  オーケストレーションでのマップの使用を最小限に抑えます。  
  
    -   マップを使用して、オーケストレーションのビジネス ロジックで使用するプロパティの抽出または設定を行っている場合、識別フィールドまたは昇格させたプロパティを代わりに使用してください。 マップで値を抽出または設定する場合、ドキュメントがメモリに読み込まれます。 識別フィールドまたは昇格させたプロパティを使用すると、オーケストレーション エンジンは、メッセージ コンテキストにアクセスするので、ドキュメントはメモリに読み込まれません。  
  
    -   マップを使用して、複数のフィールドを 1 つのフィールドで集計している場合、識別フィールドまたはオーケストレーションの変数が設定されている昇格したプロパティを使用して、結果セットを累積してください。  
  
    -   オーケストレーションの変換図形は、複数の入力を含めた構成にしないでください。 複数の入力が含まれているオーケストレーションの変換図形では、マッピング中にファイル システムへのストリーム送信が行われません。 この制限により、ドキュメント サイズが指定した TransformThreshold レジストリ値を超えた場合に、ドキュメント全体がメモリに読み込むためにマップされている状態になります。 この問題を回避する手段の 1 つとしては、オーケストレーションの変換図形で複数の入力を受け入れないよう、変換を受信ポート レベル内で適用するという方法があります。  
  
3.  調整、**サイズの大きいメッセージのフラグメント サイズ**で公開されているプロパティ、 **BizTalk グループのプロパティ**の構成 ページ。  
  
     受信したメッセージのメモリ内サイズの指定されたバイト数を超える場合**サイズの大きいメッセージのフラグメント サイズ**メッセージは、指定されたサイズのフラグメントに分割し、フラグメントは、メッセージ ボックス データベースに書き込まれます、。次のように、Microsoft 分散トランザクション コーディネーター (MSDTC) トランザクションのコンテキスト:  
  
    1.  受信メッセージが既存の MSDTC トランザクションのコンテキストで公開されている場合、メッセージのフラグメントをメッセージ ボックス データベースに書き込む際、このトランザクションが使用されます。 たとえば、トランザクション処理のために構成されたトランザクション アダプターによって受信メッセージが公開されている場合、メッセージのフラグメントをメッセージ ボックス データベースに書き込む際、既存のトランザクションが使用されます。  
  
    2.  受信メッセージが既存の MSDTC トランザクションのコンテキストで公開されていない場合、メッセージのフラグメントを書き込むため、新しい MSDTC トランザクションが作成されます。  
  
    -   値を大きく**サイズの大きいメッセージのフラグメント サイズ**をサイズの大きいメッセージが断片化しているし、関連付けられた MSDTC トランザクションの作成の発生頻度を減らす頻度を減らす方法。 MSDTC トランザクションを使いすぎるとパフォーマンスの観点で無駄が多いため、この操作を実行する必要があります。 この値を大きくすると使用できるメモリの量も増える可能性があるので注意してください。  
  
    -   メッセージをメッセージ ボックス データベースに書き込む時間が MSDTC トランザクション タイムアウトの最大許容値の 60 分を超えると、トランザクションがタイムアウトになり、エラーが発生します。また、メッセージの書き込みが失敗し、ロールバックされます。 **サイズの大きいメッセージのフラグメント サイズ**値にする必要がありますを非常に大きなメッセージを処理するときに、この問題を避けるために増加します。 使用できるメモリの量に応じて、この値を最大値 1000000 バイトに設定する必要があります。  
  
    -   メッセージの各フラグメントは、メッセージ ボックス データベースに対して 1 つ以上の SQL Server データベース ロックを作成します。 ロックの数が数十万を超えると、SQL Server が "ロックの範囲外" エラーを生成する可能性があります。 この問題が発生した場合を増やす、**サイズの大きいメッセージのフラグメント サイズ**メッセージ ボックス データベースに対して行われた SQL Server データベース ロックの数を減らします。  
  
4.  "ロックの範囲外" エラーが発生した場合、64 ビット バージョンの SQL Server でメッセージ ボックス データベースを使用することを検討してください。 64 ビット バージョンの SQL Server では、使用できるロックの数が大幅に増えます。  
  
5.  調整、**サイズの大きいメッセージのしきい値**で公開されているプロパティ、 **BizTalk グループのプロパティ**の構成 ページ。  
  
     メッセージとしてバッチが処理される、メッセージ バッチのメモリ内サイズが指定されたバイト数に達すると**サイズの大きいメッセージのしきい値**が処理されたメッセージ バッチの一部が前に、メッセージ ボックス データベースに書き込まれますメッセージ バッチの残りの部分が処理されます。 次のように、MSDTC トランザクションのコンテキストでこの処理が実行されます。  
  
    1.  メッセージ バッチが既存の MSDTC トランザクションのコンテキストで公開されている場合、メッセージ バッチの処理部分をメッセージ ボックス データベースに書き込む際、このトランザクションが使用されます。 たとえば、トランザクション処理のために構成されたトランザクション アダプターによって受信メッセージ バッチが公開されている場合、メッセージ バッチの処理部分をメッセージ ボックス データベースに書き込む際、既存のトランザクションが使用されます。  
  
    2.  メッセージ バッチが既存の MSDTC トランザクションのコンテキストで公開されていない場合、メッセージ バッチの部分をメッセージ ボックス データベースに書き込むため、新しい MSDTC トランザクションを作成する必要があります。 MSDTC トランザクションを使用すると、特定のメッセージ バッチのすべての部分がメッセージ ボックス データベースに正常に書き込まれます。  
  
     **サイズの大きいメッセージのしきい値**設定は、メッセージのバッチに直接適用が、メッセージ バッチは、1 つの値に設定することができます、**サイズの大きいメッセージのしきい値**設定解除することも直接個々 のメッセージに適用されます。 たとえば、メッセージ バッチの 1 つのメッセージを超えた場合に、指定した**サイズの大きいメッセージのしきい値**パラメーター、**サイズの大きいメッセージのしきい値**有効で、バッチ内の 1 つのメッセージにのみ適用されます。  
  
    -   **サイズの大きいメッセージのしきい値**メッセージ ボックスにメッセージのバッチを分配するために使用 MSDTC トランザクションの作成を軽減するためにパラメーターを調整する必要があります。 これは、MSDTC トランザクションの過剰な使用がパフォーマンスの観点から高価なのために実行する必要があります。 どのような最小値を判断するには次の計算を使用して、**サイズの大きいメッセージのしきい値**設定が不必要に MSDTC トランザクションを作成しないように注意する必要があります。  
  
        ```  
        Batch Size * Average size (in bytes) of each message in the batch after being processed by the receive pipeline < Large message threshold  
        ```  
  
         メッセージ バッチのバイト単位の合計サイズが指定された値を超えない限り、**サイズの大きいメッセージのしきい値**メッセージ ボックスに、メッセージ バッチを分配する biztalk で、MSDTC トランザクションを開始する必要はありませんし、データベースです。