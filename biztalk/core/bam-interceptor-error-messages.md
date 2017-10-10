---
title: "BAM インターセプターのエラー メッセージ |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 270dd5b7-33bf-4847-86f1-8798d63421b8
caps.latest.revision: "12"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a4a8678cacaf67d358456da34a495dc34a0e1db2
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="bam-interceptor-error-messages"></a>BAM インターセプターのエラー メッセージ
WF インターセプターまたは WCF BAM インターセプターを使用する場合、無効なインターセプター構成ファイルの問題から、コンテキスト プロパティを抽出する際の実行時の問題、または一方向の WCF 操作の応答からイベント追跡を試行する際の実行時の問題まで、多岐にわたる問題が発生する可能性があります。  
  
 次の表に、bm.exe を使用したソリューションの展開中、または BAM インターセプターが有効になっているアプリケーションの実行中に発生する可能性がある各 BAM インターセプターのエラーの一覧を示します。 各エラーには、原因および 1 つ以上の考えられる解決策が含まれます。  
  
|イベント ログ ID|エラー メッセージ|原因|解決策|  
|------------------|-------------------|-----------|----------------|  
|1001|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'}、インターセプター構成にはテクノロジ '{1}' マニフェスト '{2}' が含まれていますスキーマ検証エラーが ({3}、{4}): \\ 5 \\ です。|インターセプター構成ファイルは、共通のインターセプター構成スキーマまたはテクノロジ固有の (Windows Workflow Foundation または Windows Communication Framework) スキーマに対する検証を行いません。|インターセプター構成ファイルのエラーで示されている場所を見つけ、スキーマと一致するように変更します。|  
|1002|BAM インターセプターは、次のエラーを検出しました: ホストで次のように処理 '{0}'、アプリケーションの構成パラメーター値 '{2}' と ' {1}' を解析できません。|アプリケーションの構成には、適切な型内で解析できない設定が含まれます。|アプリケーションの構成設定を修正します。|  
|1003|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} で、EventSource '{1}' のインターセプター構成に OnEvent '{2}' を '{3}' の無効なデータ操作を含むです。|内部エラーです。|インターセプター構成ファイルで使用している操作の種類を確認します。|  
|1004|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス '{0}'、BAM データ型にデータを解析できません。 '{1}' EventSource '{2}' OnEvent '{3}' のインターセプター構成の実行時。|適切な BAM データ型 DATETIME/INT/FLOAT/NVARCHAR 内の追跡データを解析できません。|この追跡データに対して適切なデータ型が使用されるようインターセプター構成ファイルを修正します。|  
|1010|BAM インターセプターは、次のエラーを検出しました: ホストで次のように処理 '{0}' で EventSource '{2}' OnEvent '{3}' のインターセプター構成の BAM データ型に文字列 '{1}' を解析することができません。|内部エラーです。|インターセプター構成ファイルで使用されているデータ型がサポートされていることを確認します。|  
|1013|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} でブール型の操作中に無効なスタック引数 '{1}' ランタイムの EventSource のインターセプター構成に '{2}' OnEvent '{3}' です。|ブール演算 (例: および) 無効な引数をスタックにします。|インターセプター構成ファイルのエラーを確認して、修正します。|  
|1014|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} で、EventSource '{1}' OnEvent '{2}' のインターセプター構成には操作 '{3}' を含む '{4}' 引数が必要です。|操作中に、インターセプター構成ファイルで間違った # 引数を受け取りました。|インターセプター構成ファイルのエラーを確認して、修正します。 操作のドキュメントを参照してください。|  
|1015|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス '{0}' で EventSource '{1}' のインターセプター構成に不明な名前空間 '{2}' が含まれています。|インターセプター構成ファイル内の操作が、不明な名前空間に属しています。|インターセプター構成ファイルのエラーを確認して、修正します。  common/WF/WCF の名前空間のみを使用します。|  
|1016|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'}、EventSource '{1}' OnEvent '{2}' のインターセプター構成が '{3}' 引数を必要な操作が含まれていますが、'{4}' の引数のみがスタック上に存在します。|スタックから操作に渡される引数の数が正しくありません。|インターセプター構成ファイルのエラーを確認し、問題が発生した操作の引数の数を調整します。 操作の詳細については、「[here:wf]」および「[here:wcf]」を参照してください。|  
|1017|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} で、EventSource '{1}' のインターセプター構成に OnEvent '{2}' を '{3}' 値に評価される式を含むです。|式は単一の結果に評価される必要があります。|インターセプター構成ファイルのエラーを確認して、修正します。|  
|1018|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} で無効なインターセプター設定 '{1}' については、アプリケーションの構成。|アプリケーションの構成に、不明な設定が含まれています。|アプリケーションの構成の設定を修正します。|  
|1019|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'}、EventSource '{1}' のインターセプター構成に OnEvent '{2}' 評価に失敗したデータ式を含むです。|実行時に式を評価できませんでした (内部エラー)。|内部例外を参照してください。|  
|1022|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} で SQL 例外がスローされました。|処理中に SQL エラーが発生しました。|内部 SQL 例外を参照してください。 SQL Server Profiler を使用してエラーを検索することもできます。|  
|1023|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'}、インターセプタ構成ポーリング間隔 '{1}' する必要がありますに最低限の '{2}' 秒です。|ポーリング間隔が無効です。|アプリケーションの構成の設定を修正します。|  
|1024|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} には、アプリケーション構成で BAM プライマリ インポート データベースへの接続文字列を指定します。|BAM PIT への接続文字列を指定する必要があります。|アプリケーションの構成の設定を修正します。|  
|1025|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} を追加作成できません。 BAM インターセプター パフォーマンス カウンター インスタンス EventSource '{1}' のインデックスが最大値 '{2}' を超えているためです。|同一の (イベント ソース、ホスト名の) ペアが多すぎるため、パフォーマンス カウンター インスタンスの一意のインデックスを作成できません。 このシナリオが発生することはほとんどありません。|(イベント ソース、ホスト名の) ペアの数を減らします。|  
|1026|BAM インターセプターは、次のエラーを検出しました: ホストで次のように処理 '{0}'、テクノロジ '{1}' とパフォーマンス カウンターのインスタンスを作成するマニフェスト '{2}' のイベント ソース名が見つかりません。|内部エラーです。|アプリケーション展開および BAM インターセプター構成ファイルを確認します。|  
|1027|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'}、インターセプター構成テクノロジ '{1}' マニフェスト '{2}' が既知のエラーです。 => {3}|(テクノロジ、マニフェストの) 現在のインターセプター構成ファイルに既知の検証エラーが含まれています。  WF インターセプターでは、ポーリングにより有効なインターセプター構成ファイルが検出されるまで、このメッセージが各新規ワークフロー インスタンスに対して継続的に生成されます。  注: プロセス = 追跡。|インターセプター構成ファイルのエラーを確認して、修正します。|  
|1028|BAM インターセプターには、次のエラーが検出されました: eventsource '{1}' OnEvent '{2}' BAM アクティビティ '{3}'、'{0}'、ホスト プロセスでは、アクティビティ ID が null または空の文字列に評価されます。|NULL または空の文字列です。|インターセプター構成ファイルのエラーを確認して、空の文字列に評価されないよう Activity ID を修正します。|  
|1029|BAM インターセプターには、次のエラーが検出されました: eventsource '{1}' OnEvent '{2}' BAM アクティビティ '{3}'、'{0}'、ホスト プロセスで、アクティビティ ID '{4}' からの継続が null または空の文字列に評価します。|NULL または空の文字列です。|インターセプター構成ファイルのエラーを確認して、修正します。  継続が空の文字列に評価されることはできません。|  
|1031|BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} で、EventSource '{1}' のインターセプター構成に OnEvent '{2}' 不明な要素 '{3}' を持つデータ式を含むです。|式に含めることができるのは、'Operation' という名前の付く要素だけです。|インターセプター構成ファイルを確認し、不明な要素をサポートされている要素に置換します。|  
|1032|BAM インターセプターには、次のエラーが検出されました: タイマー スレッドからホスト プロセス ' 0'} で例外がスローされました。|タイマー スレッドにエラーが発生しました。|例外メッセージを参照してください。|  
|1502|BAM インターセプターで次の警告を検出しました: ホストで次のように処理 '{0}'、パフォーマンス カウンターを作成できません: {1} です。|パフォーマンス カウンターの作成に必要な権限がないこと、またはその他の問題によりカウンターの作成がブロックされています。|必要な権限が設定されているアカウントを使用して、パフォーマンス カウンターを再登録します。 詳細については、次を参照してください。 [BAM イベント ソフトウェアをインストールする](../core/installing-the-bam-eventing-software.md)です。|  
|1503|BAM インターセプターには、次のエラーが検出されました: BAM インターセプターのパフォーマンス カテゴリを作成できません: {0}。|パフォーマンス カウンターの作成に必要な権限がないこと、またはその他の問題によりカウンターの作成がブロックされています。|必要な権限が設定されているアカウントを使用して、パフォーマンス カウンターを再登録します。 詳細については、次を参照してください。 [BAM イベント ソフトウェアをインストールする](../core/installing-the-bam-eventing-software.md)です。|  
|1504|BAM インターセプターには、次のエラーが検出されました: BAM インターセプターのパフォーマンス カテゴリを削除できません: {0}。|パフォーマンス カウンターの作成に必要な権限がないこと、またはその他の問題によりカウンターの作成がブロックされています。|必要な権限が設定されているアカウントを使用して、パフォーマンス カウンターを再登録します。 詳細については、次を参照してください。 [BAM イベント ソフトウェアをインストールする](../core/installing-the-bam-eventing-software.md)です。|  
|2001|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス '{0}' で EventSource '{1}' OnEvent '{2}' のインターセプター構成に無効なコンテキスト プロパティ '{3}' が含まれています。|インターセプター構成ファイルのエラーです。|インターセプター構成ファイルを確認し、イベント ソースに対して有効なコンテキスト プロパティが使用されていることを確認します。|  
|2002|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'}、EventSource '{1}' のインターセプター構成に OnEvent '{2}' サポートされていないワークフロー追跡イベント '{3}' にはが含まれています。|インターセプター構成ファイルのエラーです。|インターセプター構成ファイルを確認し、サポートされている WF イベントが使用されていることを確認します。|  
|2006|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス '{0}' で EventSource '{1}' OnEvent '{2}' のインターセプター構成には未解決の指定した文字列 '{3}' からの型。|文字列から .NET 型を解析できません。|インターセプター構成ファイル内の問題が発生した文字列を修正します。 また、対象の型を含むアセンブリが GAC に展開されていることを確認します。|  
|2009|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス '{0}' で EventSource '{1}' OnEvent のインターセプター構成に ' {2} に無効なフィルター式が含まれています: に、ブール型の等号演算子を適用する必要があります、定数および取得操作です。|フィルター パターンは常に (定数、取得操作) または (取得操作、定数) のセットです。|インターセプター構成ファイルのエラーを確認して、修正します。|  
|2010|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセスで '{0}'、EventSource '{1}' のインターセプター構成に OnEvent '{2}' がワークフローからデータを抽出しようとするワークフロー追跡ポイントを作成します。|ワークフロー追跡ポイントは、ワークフローからデータを抽出することはできません。 WF のドキュメントを参照してください。|インターセプター構成ファイルのエラーを確認して、修正します。|  
|2012|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} プロパティの抽出 '{1}' に見つかりませんワークフロー タイプ '{2}' です。|インターセプター構成ファイルのエラーです。|インターセプター構成ファイルのエラーを確認して、修正します。  ワークフロー内のプロパティを抽出します。|  
|2014|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} でワークフロー インスタンス '{1}' がコミット内部例外をスローします。|`Flush` の `EventStream` メソッドが例外をスローしました。|内部例外を参照してください。|  
|2015|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} で、EventSource '{1}' のインターセプター構成に OnEvent '{2}' をサポートされていないアクティビティ実行ステータス イベント '{3}' を含むです。|インターセプター構成ファイルのエラーです。|インターセプター構成ファイルのエラーを確認して、修正します。|  
|2015|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} で、EventSource '{1}' のインターセプター構成に OnEvent '{2}' をサポートされていないアクティビティ実行ステータス イベント '{3}' を含むです。|インターセプター構成ファイルのエラーです。|インターセプター構成ファイルのエラーを確認して、修正します。  追跡ポイントの各種類については、サポートされている操作のドキュメントを参照してください。|  
|2017|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'}、EventSource '{1}' のインターセプター構成に OnEvent '{2}' BAM イベント内の別の追跡ポイントの種類の操作が含まれる。|インターセプター構成ファイルのエラーです。|インターセプター構成ファイルのエラーを確認して、修正します。 Workflow Foundation 追跡ポイントと操作の詳細については、次を参照してください。 [Windows Workflow Foundation での操作](../core/operations-in-windows-workflow-foundation.md)です。|  
|2018|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} で、EventSource '{1}' のインターセプター構成に OnEvent '{2}'、有効な追跡ポイントの種類がないです。|テクノロジ固有の演算 (論理積、等号、定数を除く) は、フィルター式内で一度だけ使用できます。  注: これはのみをサポートしているため、および not またはします。|インターセプター構成ファイルのエラーを確認して、修正します。 Workflow Foundation 追跡ポイントと操作の詳細については、次を参照してください。 [Windows Workflow Foundation での操作](../core/operations-in-windows-workflow-foundation.md)です。|  
|2019|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'}、EventSource '{1}' のインターセプター構成に OnEvent '{2}' を複数回 '{3}' 操作を含むフィルター式を使用します。|内部エラーです。|インターセプター構成ファイルから重複する操作を削除します。|  
|2020|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス '{0}' で EventSource '{1}' のインターセプター構成には未解決の指定した文字列 '{2}' からの型。|文字列で指定された型を解決できませんでした。|インターセプター構成ファイルから問題が発生した型を削除します。|  
|2021|Windows Workflow Foundation の BAM インターセプターは、次のエラーを検出しました: ホスト プロセス ' 0'} で BAM 追跡サービスを一度だけ追加できますワークフロー ランタイムにします。|BAM 追跡サービスのインストールが複数回試行されました。|BAM 追跡サービスの追加は一度だけ行います。|  
|3008|BAM インターセプターの Windows Communication Foundation には、次のエラーが検出されました: EventSource '{0}' OnEvent '{1}' のインターセプター構成にはフィルターで XPath 操作を使用することはできません。|インターセプター構成ファイルは、テクノロジ固有の共通のスキーマに対して検証されません。|インターセプター構成ファイルから問題が発生した XPath ステートメントを削除します。|