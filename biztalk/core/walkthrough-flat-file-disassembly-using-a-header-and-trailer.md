---
title: "チュートリアル: フラット ファイル逆アセンブル ヘッダーとトレーラーを使用して |Microsoft ドキュメント"
description: "フラット ファイル スキーマ ウィザードを使用してヘッダー スキーマ、トレーラー スキーマ、およびボディ スキーマを作成し、BizTalk Server でのフラット ファイル逆アセンブル"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 715af9cc-d718-483d-b593-64462aa5a58b
caps.latest.revision: "16"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5e49014ac4c15f1fd303b2646c74f11b5242aed3
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="walkthrough-flat-file-disassembly-using-a-header-and-trailer"></a>チュートリアル: フラット ファイル逆アセンブル ヘッダーおよびトレーラーを使用します。

## <a name="overview"></a>概要
このチュートリアルでは、フラット ファイル スキーマ ウィザードによって作成されたスキーマを使用して、ヘッダー、トレーラー、および繰り返しのメッセージ ボディを含んでいるファイルのフラット ファイル逆アセンブリを実行する方法を説明します。 このチュートリアルでは、次の要件を満たす架空のエラー追跡システムの一部を開発します。  
  
-   エラー メッセージは社内のさまざまな物理的な場所でログに記録され、集中管理された場所に送信されて、さまざまなバックエンド システムに振り分けられます。  
  
-   エラー メッセージは、場所を示すヘッダー、1 つ以上のエラー メッセージを含むボディ、およびバッチ数を示すトレーラーを含んだフラット ファイル形式で書き込まれます。  
  
-   メッセージは、ヘッダー、ボディ、トレーラーを含んでいない場合、無効と見なされます。  
  
 このチュートリアルを完了すると、フラット ファイルを処理し、バックエンド システムで処理するために XML として出力する BizTalk Server アプリケーションが完成します。  
  
## <a name="prerequisites"></a>前提条件  
 この例では、BizTalk Server プロジェクトの作成、アセンブリへの署名、および BizTalk Server 管理コンソールでのアプリケーションとポートの表示に慣れている必要があります。 おく必要がありますも快適で紹介したアイデアに[チュートリアル: 基本的な BizTalk アプリケーションの展開](../core/walkthrough-deploying-a-basic-biztalk-application.md)です。 フラット ファイル スキーマ ウィザードの基礎知識は役立ちますが、必須ではありません。  
  
## <a name="what-this-example-does"></a>この例の処理  
 この例では、受信フラット ファイルをカスタム パイプラインとフラット ファイル逆アセンブラー コンポーネントを使用して処理します。 ヘッダー スキーマ、トレーラー スキーマ、およびボディ スキーマを使用してメッセージを解析した後、バックエンドで処理するためにそれらのメッセージを送信場所に出力します。  
  
## <a name="example"></a>例  
 この例を作成するには、以下で概要を説明している手順を実行します。  
  
### <a name="create-a-new-biztalk-project"></a>新しい BizTalk プロジェクトの作成  
 BizTalk プロジェクトを作成する必要があるソリューションをビルドする前に、ソリューションに厳密な名前が付いていることを確認し、アプリケーション名をそのソリューションに割り当てます。 アプリケーション名を割り当てると、そのソリューションが BizTalk Server によって既定の BizTalk アプリケーションに配置されるのを防ぐことができます。  
  
1.  [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] を使用して新しい BizTalk プロジェクトを作成します。 このプロジェクト**[ffdisassemblerwalkthrough]**です。  
  
2.  キー ファイルを作成してプロジェクトに割り当てます。 このタスクの詳細については、次を参照してください。[署名 ページ、プロジェクト デザイナー](http://go.microsoft.com/fwlink/?LinkId=125876)です。  
  
3.  プロジェクトの配置プロパティで、次のように設定します。**アプリケーション名**を"FlatFileExample"に設定し**ホスト インスタンスを再起動します**に`True`です。 このフラグを設定すると、キャッシュされたアセンブリのインスタンスを消去するようにホストに通知されます。  
  
### <a name="create-the-sample-data-file"></a>サンプル データ ファイルの作成  
スキーマを生成する前に、テスト ファイルを作成する必要があります。   
  
1.  メモ帳または任意のテキスト エディターを起動します。  
  
2.  サンプル テスト ファイルを作成します。 このファイルは、エラーの報告元の場所を示すヘッダー、バッチの ID を含んだトレーラー、および 1 つ以上のエラー レコードで構成されたボディで構成されています。 ファイルの形式を次に示します。  
  
    ```  
    Location  
    ERRORid|type|priority|description|errorDateTime  
    …additional error records   
    BatchID  
    ```  
  
    エラー レコードがテキスト"ERROR"でタグ付けし、区切り、"&#124;"(位置指定) 文字です。 この ERROR レコードのデータ要素を次の表で説明します。  
  
    |要素|データ型|Description|  
    |---|---|---|  
    |ID|整数 (integer)|このエラーの ID。|  
    |型|整数 (integer)|エラーの種類。|  
    |[Priority]|string|優先度インジケーター: Low、Medium、または高です。|  
    |Description|string|エラーの説明です。|  
    |ErrorDateTime|DateTime|エラーが発生した日時です。|  
  
    ファイルには、1 つ以上の ERROR レコードを含めることができます。  
  
     * * - または--* *
  
     新しいファイルに次のサンプル データをコピーします。 最後の行には、ラインフィードが含まれています。
  
    ```  
    East Coast Facility  
    ERROR102|0|High|Sprocket query fails.|1999-05-31T13:20:00.000-05:00  
    ERROR16502|2|Low|Time threshold exceeded.|1999-05-31T13:20:00.000-05:00  
    8675309  
  
    ```  
  
3.  新しいサンプル ファイルをプロジェクト ディレクトリに保存します。 簡単に見つけられるように、"ErrorFile.txt" などのわかりやすい名前を付けてください。  
  
### <a name="create-and-test-the-header-trailer-and-body-schemas"></a>ヘッダー スキーマ、トレーラー スキーマ、およびボディ スキーマの作成  
 サンプル データ ファイルを作成したら、ヘッダー スキーマ、トレーラー スキーマ、およびボディ スキーマを作成します。 これらのスキーマは、受信したメッセージを処理するためにフラット ファイル逆アセンブラー受信パイプライン コンポーネントで使用されます。  
  
##### <a name="use-the-flat-file-schema-wizard-to-create-the-header-schema"></a>フラット ファイル スキーマ ウィザードを使用してヘッダー スキーマを作成するには  
  
1.  新しいスキーマをプロジェクトに追加します。 ソリューション エクスプ ローラーで右クリック**ffdisassemblerwalkthrough**、 をポイント**追加**、クリックして**新しい項目の**します。  
  
2.  **新しい項目の追加**ダイアログ ボックスで、をクリックして**スキーマ ファイル**選択**フラット ファイル スキーマ ウィザード**です。 新しいスキーマ"Header.xsd"という名前をクリックして**追加**です。  
  
3.  **BizTalk フラット ファイル スキーマ ウィザードへようこそ** ページで、をクリックして**次**です。  
  
4.  **フラット ファイル スキーマ情報**] ページで [**参照**先ほど作成したサンプル データ ファイルを見つけます。 変更、**レコード名**"Header"コード ページを確認し、クリックして**次**です。  
  
    > [!NOTE]
    >  サンプル ファイルを Unicode 形式で保存した場合、コード ページはリトル エンディアン UTF16 (1200) になります。 これは、この例に影響しません。  
  
5.  次に、ドキュメント データを選択します。 **[ドキュメント データ**] ページで、改行文字 {CR} を含む、データの最初の行を強調表示と {LF} ように。  
  
     ![ヘッダー スキーマ用に選択されたデータ](../core/media/ffwiz-header-select-document-data.gif "ffwiz_header_select_document_data")  
  
     **[次へ]**をクリックします。  
  
6.  **[レコード書式を**] ページで、をクリックして**次**既定を受け入れます。 データ ファイルでは相対位置を使用していないので、既定の "区切り記号" を使用できます。  
  
7.  **区切られたレコード**] ページで [**次**です。  
  
8.  次に子要素を指定します。 次に示すように、ヘッダーには、"Location" という要素が 1 つ含まれています。  
  
     ![ヘッダーに定義された場所ノード](../core/media/ffwiz-header-child-elements.gif "ffwiz_header_child_elements")  
  
     **[次へ]** をクリックして次に進みます。  
  
9. **スキーマ ビュー**  ページで、スキーマを確認します。  
  
     ![完了を示すスキーマ ビュー ヘッダー スキーマ](../core/media/ffwiz-header-schema-view.gif "ffwiz_header_schema_view")  
  
     問題がなければ、をクリックして**完了**ウィザードを完了します。  
  
10. クリックして、 **\<スキーマ >**ヘッダー スキーマ ペイン内のノードです。 プロパティ ウィンドウで、次のように変更します。 **Element FormDefault**に**Qualified**です。 これは、ローカルに宣言された要素を、ターゲットの名前空間を使用してインスタンス ドキュメント内で修飾する必要があることを示します。  
  
##### <a name="use-the-flat-file-schema-wizard-to-create-the-trailer-schema"></a>フラット ファイル スキーマ ウィザードを使用してトレーラー スキーマを作成するには  
  
1.  新しいスキーマをプロジェクトに追加します。 ソリューション エクスプ ローラーで右クリック**ffdisassemblerwalkthrough**、 をポイント**追加**、クリックして**新しい項目の**します。  
  
2.  **新しい項目の追加**ダイアログ ボックスで、をクリックして**スキーマ ファイル**選択**フラット ファイル スキーマ ウィザード**です。 新しいスキーマ"Trailer.xsd"という名前をクリックして**追加**です。  
  
3.  **BizTalk フラット ファイル スキーマ ウィザードへようこそ** ページで、をクリックして**次**です。  
  
4.  **フラット ファイル スキーマ情報**] ページで [**参照**先ほど作成したサンプル データ ファイルを見つけます。 変更、**レコード名**を"Trailer"コード ページを確認し、をクリックして**次**です。  
  
    > [!NOTE]
    >  サンプル ファイルを Unicode 形式で保存した場合、コード ページはリトル エンディアン UTF16 (1200) になります。 これは、この例に影響しません。  
  
5.  次に、ドキュメント データを選択します。 **[ドキュメント データ**] ページで、改行文字 {CR} を含む、データの最後の行を強調表示と {LF} ように。  
  
     ![トレーラー スキーマ用に選択されたデータ](../core/media/ffwiz-trailer-select-document-data.gif "ffwiz_trailer_select_document_data")  
  
     **[次へ]**をクリックします。  
  
6.  **[レコード書式を**] ページで、をクリックして**次**既定を受け入れます。 データ ファイルでは相対位置を使用していないので、既定の "区切り記号" を使用できます。  
  
7.  **区切られたレコード**] ページで [**次**です。  
  
8.  次に子要素を指定します。 次に示すように、ヘッダーには、"BatchID" という要素が 1 つ含まれています。  
  
     ![トレーラー用に定義された場所ノード](../core/media/ffwiz-trailer-child-elements.gif "ffwiz_trailer_child_elements")  
  
     **[次へ]** をクリックして次に進みます。  
  
9. **スキーマ ビュー**  ページで、スキーマを確認します。  
  
     ![スキーマ ビューを示す完了したトレーラー スキーマ](../core/media/ffwiz-trailer-schema-view.gif "ffwiz_trailer_schema_view")  
  
     問題がなければ、をクリックして**完了**ウィザードを完了します。  
  
10. クリックして、 **\<スキーマ >**トレーラー スキーマ ペイン内のノードです。 プロパティ ウィンドウで、次のように変更します。 **elementFormDefault**に**Qualified**です。 これは、ローカルに宣言された要素を、ターゲットの名前空間を使用してインスタンス ドキュメント内で修飾する必要があることを示します。  
  
##### <a name="use-the-flat-file-schema-wizard-to-create-the-body-schema"></a>フラット ファイル スキーマ ウィザードを使用してボディ スキーマを作成するには  
  
1.  新しいスキーマをプロジェクトに追加します。 ソリューション エクスプ ローラーで右クリック**ffdisassemblerwalkthrough**、 をポイント**追加**、クリックして**新しい項目の**します。  
  
2.  **新しい項目の追加**ダイアログ ボックスで、をクリックして**スキーマ ファイル**選択**フラット ファイル スキーマ ウィザード**です。 新しいスキーマ"Body.xsd"という名前をクリックして**追加**です。  
  
3.  **BizTalk フラット ファイル スキーマ ウィザードへようこそ** ページで、をクリックして**次**です。  
  
4.  **フラット ファイル スキーマ情報**] ページで [**参照**先ほど作成したサンプル データ ファイルを見つけます。 変更、**レコード名**"Body"に、コード ページを確認し、をクリックして**次**です。  
  
    > [!NOTE]
    >  サンプル ファイルを Unicode 形式で保存した場合、コード ページはリトル エンディアン UTF16 (1200) になります。 これは、この例に影響しません。  
  
5.  次に、ドキュメント データを選択します。 **[ドキュメント データ**] ページで、行 2 と 3 つの改行文字 {CR} を含むデータを強調表示と {LF} ように。  
  
     ![ボディ スキーマ用に選択されたデータ](../core/media/ffwiz-body-select-document-data.gif "ffwiz_body_select_document_data")  
  
     **[次へ]**をクリックします。  
  
6.  **[レコード書式を**] ページで、をクリックして**次**既定を受け入れます。 データ ファイルでは相対位置を使用していないので、既定の "区切り記号" を使用できます。  
  
7.  **区切られたレコード**] ページで、[**次**です。  
  
8.  ここでは、子要素を定義します。 変更**Body_Child1**に**エラー**に要素の型を設定および**繰り返しレコード**です。 設定、 **Body_Child2**要素レコードの種類を**無視**です。  
  
9. **スキーマ ビュー**  ページで、をクリックして**次**エラー レコードの子要素を定義します。  
  
10. **ドキュメント データを選択**] ページで [**次**です。 ウィザードによって、レコード定義データが適切に選択されます。  
  
11. **[レコード書式を**] ページで、をクリックして**次**です。 データは、区切り記号で書式設定されます。  
  
12. **区切られたレコード**] ページで、[ **&#124;**の**子区切り記号**です。 次に、選択、**レコードにタグ識別子** チェック ボックス**エラー**タグの値にします。  
  
     ![構成で区切られたレコードのタグ識別子](../core/media/ffwiz-bodyerror-delimited-record.gif "ffwiz_bodyerror_delimited_record")  
  
     **[次へ]**をクリックします。  
  
13. ここでは、Error レコードの子要素を定義します。  
  
     ![5 つの要素で定義されたエラー レコード](../core/media/ffwiz-bodyerror-child-elements.gif "ffwiz_bodyerror_child_elements")  
  
     **[次へ]**をクリックします。  
  
14. **スキーマ ビュー**  ページで、スキーマを確認します。  
  
     ![スキーマ ビューを示す完了したボディ スキーマ](../core/media/ffwiz-bodyerror-schema-view.gif "ffwiz_bodyerror_schema_view")  
  
     入力ミスを行った場合にをクリックして**戻る**し、必要に応じて修正します。 問題がなければ、をクリックして**完了**ウィザードを完了します。  
  
15. クリックして、 **\<スキーマ >** Body スキーマ ペイン内のノードです。 プロパティ ウィンドウで、次のように変更します。 **Element FormDefault**に**Qualified**です。 これは、ローカルに宣言された要素を、ターゲットの名前空間を使用してインスタンス ドキュメント内で修飾する必要があることを示します。  
  
16. クリックして、 **\<エラー >** Body スキーマ ペイン上のノードです。 プロパティ ウィンドウで、次のように変更します。 **Max Occurs**に**1**です。 これにより、フラット ファイル逆アセンブラーによって各エラーがそれぞれのメッセージに分割されます。  
  
##### <a name="test-the-schemas-using-ffdasm"></a>FFDasm を使用してスキーマをテストします。  
  
1.  コマンド プロンプトを開き、ディレクトリをプロジェクト ディレクトリに変更します。  
  
2.  コマンド プロンプトから、次に示すように FFDasm.exe を実行します。  
  
    ```  
    <Samples Path>\SDK\Utilities\PipelineTools\FFDasm ErrorFile.txt  -hs header.xsd -bs body.xsd -ts Trailer.xsd  
    ```  
  
     これとその他のパイプライン ツールの場所については、次を参照してください。[パイプライン ツール](../core/pipeline-tools.md)です。  
  
3.  FFDasm.exe によって、テスト ファイル内の各 ERROR レコードに対応した {GUID}.xml という名前の出力ファイルが 2 つ生成されます。 優先度の高いエラー レコードは、次のようになります。  
  
    ```  
    <Body xmlns="http://FFDisassemblerWalkthrough.Body">  
      <Error>  
        <ID>102</ID>  
        <Type>0</Type>  
        <Priority>High</Priority>  
        <Description>Sprocket query fails.</Description>  
        <DateTime>1999-05-31T13:20:00.000-05:00</DateTime>  
      </Error>  
    </Body>  
    ```  
  
### <a name="create-a-custom-receive-pipeline"></a>カスタム受信パイプラインの作成  
 フラット ファイル スキーマを定義したので、次はフラット ファイル逆アセンブラー コンポーネントを使用するカスタム パイプラインを作成する必要があります。 その後で、フラット ファイル逆アセンブラー コンポーネントを、ヘッダー スキーマ、ボディ スキーマ、およびトレーラー スキーマを使用するように構成して、メッセージを分割できます。    
 
1.  新しい受信パイプラインをプロジェクトに追加します。 ソリューション エクスプ ローラーで右クリックし、 **[ffdisassemblerwalkthrough]**プロジェクトをポイントし、**追加**、順にクリック**新しい項目の**します。  
  
2.  **新しい項目の追加**ダイアログ ボックスをポイント**パイプライン ファイル** をクリックし、**受信パイプライン**です。 新しいパイプライン"FFReceivePipeline"という名前をクリックして**追加**です。  
  
3.  フラット ファイル逆アセンブラー コンポーネントを、[ツールボックス] ペインから逆アセンブル ステップへドラッグして新しいパイプラインを構成します。  
  
4.  プロパティ ペインで、設定、**ドキュメント スキーマ**に**FFDisassemblerWalkthrough.Body**、**ヘッダー スキーマ**に**FFDisassemblerWalkthrough.Header**と**トレーラー スキーマ**に**FFDisassemblerWalkthrough.Trailer**です。  
  
### <a name="deploy-the-application-and-configure-the-send-and-receive-ports"></a>アプリケーションの展開および送信ポートと受信ポートの構成  
 スキーマとカスタム受信パイプラインを作成したら、次はプロジェクトをコンパイルして配置する必要があります。 プロジェクトを配置すると、BizTalk Server 管理コンソールを使用して、送信ポートと受信ポートを構成できます。  

##### <a name="deploy"></a>配置  
1.  内から[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]、プロジェクトを右クリックし、をクリックして、ソリューションを配置**展開**です。  
  
2.  BizTalk Server 管理コンソールを使用して展開し、**アプリケーション**ことを確認するグループ**[flatfileexample]**が、カスタム アプリケーションとして存在します。  
  
##### <a name="configure-the-receive-port"></a>受信ポートを構成します。  
  
1.  "Receive"という名前のディレクトリを作成する Windows エクスプ ローラーを使用して、 **[ffdisassemblerwalkthrough]**プロジェクト ディレクトリ。  
  
2.  BizTalk Server 管理コンソールで、展開、 **flatfileexample**アプリケーションを右クリックして**受信ポート**、 をポイント**新規**をクリックして**一方向受信ポート**です。  
  
3.  **受信ポートのプロパティ** ダイアログ ボックスを"ReceiveError"ポートの名前を設定します。  
  
4.  をクリックして**受信場所**、順にクリック**新規**受信場所を追加します。 新しい受信場所に "ReceiveErrorLocation" という名前を付けます。 設定、**受信パイプライン**に**FFReceivePipeline**です。 **トランスポートの種類****ファイル**をクリックし、**構成**です。 設定し、作成した受信ディレクトリを選択して、**ファイル マスク***.txt にします。  
  
5.  **[OK]**をクリックします。 受信ポートが正しく構成されます。 をクリックして**OK**を閉じます。  
  
##### <a name="configure-the-send-port"></a>送信ポートを構成します。  
  
1.  下の"Send"という名前のディレクトリを作成する Windows エクスプ ローラーを使用して、 **[ffdisassemblerwalkthrough]**プロジェクト ディレクトリ。  
  
2.  BizTalk Server 管理コンソールで、展開、 **flatfileexample**アプリケーションを右クリックして**送信ポート**、 をポイント**新規**をクリックし、 **静的な一方向の送信ポートしています.**.  
  
3.  **送信ポートのプロパティ** ダイアログ ボックスで、「送信」ポートの名前を設定します。  
  
4.  トランスポートの種類を選択**ファイル**、クリックして**構成**です。 送信先のフォルダーを、先ほど作成した送信ディレクトリに設定します。  
  
5.  次は、フィルターを構成します。 をクリックして**フィルター**し、1 つの式を追加します。  
  
    -   BTS です。MessageType = = **http://FFDisassemblerWalkthrough.Body#Body**  
  
6.  をクリックして**OK**送信ポートの構成を完了します。 送信ポートが正しく構成されます。  
  
### <a name="run-the-example"></a>例の実行  
 次に、例を実行します。 BizTalk Server 管理コンソールを使用すると、アプリケーションを起動する、受信場所に、テスト ファイルをコピーし、送信場所に生成される内容を確認します。  
  
1.  BizTalk Server 管理コンソールを右クリックし、 **[flatfileexample]**アプリケーション、およびクリック**開始**です。 送信を開始し、および受信ポートこれを参加させます。  
  
2.  サンプルの Errorfile.txt のコピーを受信ディレクトリに置きます。 2 つの出力ファイルが送信ディレクトリに書き込まれます。  
  