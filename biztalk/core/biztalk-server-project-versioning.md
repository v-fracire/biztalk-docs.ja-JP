---
title: "BizTalk Server プロジェクトのバージョン管理 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcdd5354-6335-4320-adbf-28ac934c9ce6
caps.latest.revision: "13"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1893509d569dc74bf8d6d28680026ebe90ba9149
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="biztalk-server-project-versioning"></a>BizTalk Server プロジェクトのバージョン管理
[!INCLUDE[btsDotNetFramework](../includes/btsdotnetframework-md.md)] を使った開発では、バージョン管理は標準的なルール セットに従って行います。これらのルールに従うと、バージョン番号の変更による影響を最小限に抑えることができます。 状況に応じて、[!INCLUDE[btsDotNetFramework](../includes/btsdotnetframework-md.md)]アプリケーションまたはコンポーネントを展開すると、アプリケーション構成ファイル、XCOPY のインストールを使用して、またはその他の依存関係を処理できる[!INCLUDE[btsDotNetFramework](../includes/btsdotnetframework-md.md)]展開メカニズムです。 以下では、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] を使用することによってバージョン管理と依存関係にどの程度の複雑さが加わるかについて示します。  
  
## <a name="implications-of-changing-version-numbers"></a>バージョン番号の変更による影響  
 [!INCLUDE[btsDotNetFramework](../includes/btsdotnetframework-md.md)] を使った開発では、通常、ビルドが行われる時にアセンブリ バージョン番号を現在のビルド番号に更新します。 ただし、BizTalk ソリューションを開発する場合は、アセンブリ バージョン番号を変更すると、アセンブリと、そのアセンブリ バージョン番号を使って DLL を参照する依存アイテムの間の関係が壊れることがあります。 次の表では、バージョン番号を使って [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] アセンブリを参照するアイテムの一覧と、アセンブリ バージョン番号を変更することによる影響を示します。  
  
|Entity|アセンブリ バージョン番号を変更することによる影響|  
|------------|------------------------------------------------|  
|バインド ファイル|アセンブリ バージョン番号を変更すると、そのアセンブリを参照するすべてのバインド ファイルは失敗します。 この理由は、バインド ファイルはアセンブリの参照に、バージョン番号を含む属性を使用するためです。<br /><br /> メモ帳などのエディターを使用して、バインド ファイルのバージョン情報を更新できます。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理コンソールを使用して、ソリューションを再展開し、バインド ファイルを再生成することもできます。 スクリプトを使用して、展開とバージョン管理を自動化することもできます。 展開の詳細については、次を参照してください。[を管理する BizTalk アプリケーションの展開と](../core/deploying-and-managing-biztalk-applications.md)です。|  
|BAM 追跡プロファイル定義 (.btt) ファイル|アセンブリ バージョン番号を変更すると、既存の BAM 追跡プロファイルの定義ファイルは失敗します。 BAM 追跡ファイルはバイナリ ファイル形式であり編集できないので、再生成する必要があります。 BAM 追跡プロファイルが必須の場合は、次のいずれかの操作を行う必要があります。<br /><br /> -ビルド処理中にバージョン番号を頻繁に更新しないようにします。<br />BAM 追跡プロファイルのバージョン番号が不安定になるまでのビルドが遅くなります。|  
|Web サービス公開ウィザードを使って公開された Web サービス|Web サービス公開ウィザードを使って ASP.NET Web インターフェイスを生成すると、アセンブリ [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] のアセンブリ バージョン番号が ASP.NET ソース コードに含められます。 一部として ASP.NET インターフェイスによって、アセンブリのバージョン番号が実行時に使用される、 **bodyTypeAssemblyQualifiedName** Web サービス操作のプロパティです。 場合のバージョン番号、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]アセンブリの変更を更新せず、 **bodyTypeAssemblyQualifiedName**プロパティ、し、後続の Web サービス操作によって拒否されます[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]です。<br /><br /> 受信場所で XmlDefaultPipeline を使用する場合、サブスクリプションはドキュメントの種類に依存します。 サブスクリプションでは埋め込みアセンブリ情報が使用され、アセンブリが存在しない場合は失敗します。 PassThruPipeline を使用する場合、サブスクリプションではこの埋め込みアセンブリ情報が無視されます。PassThruPipeline は、ポートを公開し、ウィザードで受信場所を作成する場合の既定のパイプラインです。|  
  
 について詳しく調べます[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]アセンブリと展開を参照してください。 [BizTalk アセンブリ](../core/biztalk-assemblies.md)です。  
  
## <a name="approaches-to-versioning"></a>バージョン管理の方法  
 プロジェクトを計画する場合は、次のいずれかの方法を選択できます。  
  
-   任意の成果物に対して固定のアセンブリ バージョンを使用し、ファイルのバージョン番号のみを増やす。  
  
-   開発作業が進行する過程で、アセンブリ バージョン番号とファイルのバージョン番号の両方を増やす。  
  
 これらの比較を次の表に示します。  
  
|固定のアセンブリ バージョン番号と動的なファイル バージョン番号|動的なアセンブリ バージョン番号と固定または動的なファイル バージョン番号|  
|--------------------------------------------------|-------------------------------------------------------------|  
|アセンブリ バージョン番号を固定の番号にする。<br /><br /> ファイル バージョン番号をビルド番号にする。|アセンブリ バージョン番号をビルド番号にする。<br /><br /> ファイル バージョン番号をビルド番号にする。|  
|複数のアセンブリがインストールされている場合、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] ランタイムで間違ったバージョンのアセンブリが取得される場合があります。|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、複数のアセンブリがインストールされている場合であっても、常に最新バージョンのアセンブリが実行されます。|  
|常にソリューションの 1 バージョンのみが展開されます。|ソリューションの異なるバージョンを、並列で展開可能です (スキーマ定義などソリューションの他の側面がクラッシュすることがあります)。|  
|BizTalk ホストを再起動し、更新したアセンブリを強制的に読み込む必要があります。|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] で新しいアセンブリを強制的に読み込む必要があります。|  
|バインド ファイルや追跡プロファイルなど、アセンブリ バージョン番号を参照するファイルを編集する必要がないので、新しい展開を簡単に作成できます。|アセンブリ バージョン番号を参照するファイルを常に新しいバージョンに更新する必要があり、展開に多くの作業が必要です。|  
  
 システムのプロトタイプを作成したり、他の種類の非配布プロジェクトを開発する場合は、固定のアセンブリ バージョン番号と動的なファイル バージョン番号を使用することもできます。 エンド ユーザーにアプリケーションを配布しない場合は、アセンブリ バージョン番号を固定してファイル バージョン番号を増やすことにより、展開作業を効率化し、依存関係を壊さないようにできます。 バージョンを追跡するには、ビルドごとに必ずファイル バージョン番号を増やします。  
  
 エンド ユーザーに配布するプロジェクトをビルドする場合は、アセンブリ バージョン番号を増やすことを検討してください。意味のあるファイル バージョン番号を保存しておくこともお勧めします。 この方法ではビルド番号とそれに関連する依存関係を修正する作業が生じますが、最新バージョンのアセンブリが確実に使用されるようになります。 自動化された展開スクリプトを使用すれば、バージョン番号の変更に伴う作業を減らすことができます。 展開のサンプルを表示するを参照してください。[アプリケーションの展開 (BizTalk Server Samples フォルダ)](../core/application-deployment-biztalk-server-samples-folder.md)です。  
  
> [!NOTE]
>  適切なファイルを確実に配布でき、管理と機能拡張が簡単なバージョン管理メカニズムを使用してください。  
  
## <a name="map-function-version-numbering"></a>マップ関数のバージョン番号付け機能  
 .NET アセンブリから呼び出せる、マップ内を使用して、**スクリプト**functoid です。 この方法では高い柔軟性が得られ、開発者はカスタム マッピングに関するさまざまな問題を解決することができます。 マップに unique 制約を課します-内部でアセンブリの型名だけでなく、呼び出されている完全なアセンブリ バージョン番号を参照して必要があります。 この結果、マップによって呼び出されるアセンブリのバージョン番号が変わると、そのアセンブリを参照するすべてのリンクが壊れることになります。  
  
 この問題を回避するため、アセンブリをマップから呼び出す必要がある場合は、マップの機能だけを保持する特定のアセンブリを作成し、このアセンブリのアセンブリ バージョン番号を固定することをお勧めします。 こうすると、マップを崩すことなく他のヘルパー関数ではアセンブリ バージョン番号を更新できます。  
  
 マップを開発した後、マップから参照するアセンブリが変更される場合については、マップ エディター外でマップ ファイルを更新し、新しいバージョン番号を反映することを検討してください。  
  
#### <a name="to-use-notepad-to-modify-the-map-file-to-reflect-updated-version-numbers"></a>メモ帳を使用してマップ ファイルを修正し、新しいバージョン番号を反映するには  
  
1.  使用して、**開始**メニューで、メモ帳を起動します。  
  
2.  メモ帳で、上、**ファイル** メニューのをクリックして**開く**です。 **開く** ダイアログ ボックスで、マップ ファイルをクリックして、変更する**開く**です。  
  
3.  **[編集]** メニューの **[検索]**をクリックします。 **検索** ダイアログ ボックスに、入力**アセンブリ =**、クリックして**次を検索**です。  
  
4.  外部アセンブリへのスクリプト参照がある場合、メモ帳では次のような XML 要素が検索されます。  
  
    ```  
    <Script Language="ExternalAssembly" Assembly="Contoso.Scripts, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c5145e4e089" Class="Contoso.Scripts" Function="CalculateValue" AssemblyPath="Contoso.Scripts.dll"/>  
    ```  
  
     バージョン番号を更新します。 複数のインスタンスがある場合は、使用**置換**上、**編集**メニュー。  
  
5.  ファイルを保存します。  
  
     これで、マップ エディターを使用してマップを開くことができます。  
  
## <a name="see-also"></a>参照  
 [BizTalk アプリケーションを配置するためのベスト プラクティス](../core/best-practices-for-deploying-a-biztalk-application.md)   
 [管理者 (BizTalk Server Samples フォルダ)](../core/admin-biztalk-server-samples-folder.md)   
 [展開とプログラムで新しいバージョンのオーケストレーションを開始](../core/deploying-and-starting-a-new-version-of-an-orchestration-programmatically.md)