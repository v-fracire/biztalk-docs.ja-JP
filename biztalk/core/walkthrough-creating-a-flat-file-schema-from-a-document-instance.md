---
title: "チュートリアル: ドキュメント インスタンスからフラット ファイル スキーマの作成 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a5e1453f-0380-4505-97a9-9d3526db0923
caps.latest.revision: "47"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9077e8c8b878b3e24319ef112eb391a3eaf4e0ef
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="walkthrough-creating-a-flat-file-schema-from-a-document-instance"></a>チュートリアル: ドキュメント インスタンスからフラット ファイル スキーマの作成
このチュートリアルでは、BizTalk フラット ファイル スキーマ ウィザードを使用してドキュメント インスタンスからフラット ファイル スキーマを作成する方法について説明します。ここでは注文書のサンプルを使用します。 BizTalk フラット ファイル スキーマ ウィザードの概要については、次を参照してください。 [BizTalk フラット ファイル スキーマ ウィザードを使用する方法](../core/how-to-use-biztalk-flat-file-schema-wizard.md)です。  
  
 ![サンプルの発注書](../core/media/flatfileschema-samplepurchaseorder.gif "FlatFileSchema_SamplePurchaseOrder")  
  
 注文書の各行は、復帰と改行 (CRLF) で終わります。この部分は緑色で表されます。 注文書は PO タグで始まります。このタグは赤色で表され、後に日付が続きます。 2 回繰り返される固定の位置指定フィールドには顧客情報が含まれます。このフィールドは紫色で表されます。 コメント フィールドの後に、複数のコンマ (,) で区切られたレコードとパイプ (&#124;) で区切られたデータ値を含む ITEMS タグで始まる反復的フィールドは青色で示されるをします。  
  
## <a name="prerequisites"></a>前提条件  
 このチュートリアルを実行する前には、サーバー上に次のソフトウェアがインストールされ構成されていることを確認してください。  
  
-   Microsoft [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]  
  
-   Microsoft[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]で、 **Developer tools**インストール
  
 チュートリアルでは、ドキュメント インスタンスを準備するには、以下の内容をテキスト エディターにコピーおよびテキスト ファイルとして保存します。 すべての行をコピーするフィードおよび改行を必ずください。  
  
```
PO1999-10-20
US        Alice Smith         123 Maple Street    Mill Valley    CA 90952
US        Robert Smith        8 Oak Avenue        Old Town       PA 95819
ITEMS,ITEM872-AA|Lawnmower|1|148.95|Confirm this is electric,ITEM926-AA|Baby Monitor|1|39.98|Confirm this is electric

```

  
## <a name="start-the-wizard"></a>ウィザードを開始する  
  
1.  [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]を開き、**ソリューション エクスプ ローラー**です。  
  
2.  新しいフラット ファイル スキーマを追加するには、プロジェクトを右クリックして**追加**です。 をクリックして**新しい項目の**します。  
  
3.  **新しい項目の追加** ウィンドウで、次の操作します。  
  
    1.  **カテゴリ**セクションで、**スキーマ ファイル**です。  
  
    2.  **テンプレート**セクションで、**フラット ファイル スキーマ ウィザード**です。  
  
    3.  **名前**フィールドに「 **PurchaseOrder.xsd**新しいスキーマ。  
  
    4.  **[追加]**をクリックします。  
  
4.  BizTalk フラット ファイル スキーマ ウィザードが開くと、[ようこそ] ページが表示されます。   
    今後ウィザードを実行している場合は、この画面をスキップするには、選択、**今後このページを表示しない**ボックス。 **[次へ]** をクリックして次に進みます。  
  
## <a name="selecting-purchase-order-instance"></a>注文書インスタンスを選択します。  
  
-   **フラット ファイル スキーマ情報**画面で、インスタンスを選択し、次の情報を入力します。 完了したら、をクリックして**次**を続行します。  
  
    -   **インスタンス ファイル:**をクリックして、**参照**スキーマの生成元となる、フラット ファイルを検索するボタンをクリックします。 チュートリアルの前提条件セクションで作成した、テキスト ファイルを含むフォルダーを参照: フラット ファイル スキーマから、ドキュメント インスタンスを作成します。  
  
    -   **レコード名:**型**PO**スキーマのルート名になります。  
  
    -   **ターゲットの名前空間:**型**http://Flat_File_Project.PurchaseOrder**スキーマのターゲット名前空間。  
  
    -   **コード ページ:**選択**utf-8 (65001)**ドロップダウン リストからです。  
  
    -   **バイト単位で位置のカウント:**バイトで位置指定データ フィールドをカウントする場合、チェック ボックスをオンします。 既定では、位置指定データ フィールドは文字数でカウントされます。 このチュートリアルでのままにして、 **(バイト単位) の位置のカウント**チェック ボックスをオンになっていません。  
  
## <a name="select-purchase-order-data"></a>注文書データを選択します。  
  
-   **[ドキュメント データ**] 画面で、フラット ファイルの内容が表示されます。 スキーマを作成するために必要なデータを選択し、クリックして**次**です。  
  
    > [!NOTE]
    >  ドキュメント インスタンス全体を使用するには、キーを押します**CTRL + A**すべてを選択します。  
  
    > [!NOTE]
    >  確認**長い行を折り返す**エディット ボックス、ウィザードにラップされたドキュメント全体のインスタンスの内容を表示する場合します。  
  
    > [!NOTE]
    >  インターチェンジ インスタンスからスキーマを作成する場合は、個別のドキュメント構造を表す部分のみを選択します。  
  
## <a name="delimit-purchase-order-record"></a>注文書レコードを区切り  
  
-   キャリッジ リターンで注文書の各行が終わると改行 (CRLF) で、選択**区切り記号**、クリックして**次へ**で**レコード書式を**画面。  
  
## <a name="specify-purchase-order-record-property"></a>注文書レコードのプロパティを指定します。  
  
-   **区切られたレコード**画面で、次のスキーマの最初のレベルを定義したら、をクリックして入力**次**です。  
  
    -   **子区切り記号:**選択**{CR} {LF}**です。  
  
        > [!NOTE]
        >  **子区切り記号**プロパティは、編集可能なドロップダウン リスト ボックスには、既定値のセットが含まれています。 **子区切り記号**文字、または 16 進数の値として指定することができます。 たとえば、  **\\{**または**{0x0d0a}**です。  
  
    -   **エスケープ文字:**エスケープ文字とそれに続く文字の特殊な意味を抑制する単一の文字はします。 参照してください[エスケープ文字](../core/escape-characters.md)詳細についてはします。 このチュートリアルでは空白のままにします。  
  
        > [!NOTE]
        >  使用する場合 **\\** 、 **{、**と**}**の**子区切り記号**または**エスケープ文字**、バック スラッシュを使用する必要があります。 たとえば、  **\\ \\、**と **\\{**です。  
  
    -   確認**レコードにタグ識別子**ボックス**PO**で**タグ**です。 複数のレコード ファイルで**PO**個々 のレコードの識別に使用されます。 **[次へ]** をクリックして次に進みます。  
  
     ![区切られたレコード 画面](../core/media/flatfileschemawizard-delimitedrecord1.gif "FlatFileSchemaWizard_DelimitedRecord1")  
  
## <a name="define-the-element-in-the-purchase-order-record"></a>注文書レコード内の要素を定義します。  
  
1.  ウィザードのここまでの作業で、注文書レコードの 4 つの要素を指定しました。次は、要素のプロパティを定義する必要があります。 最初の行で、次の操作を行います。  
  
    1.  型**日付**の**要素名**です。  
  
    2.  選択**フィールド要素**の**要素型**です。  
  
    3.  選択**日付**ドロップダウン選択の一覧から**データ型**です。  
  
2.  次の要素について手順 a ～ c を繰り返します。 完了したら、をクリックして**次**です。  
  
    |要素名|[要素の種類]|データ型|  
    |------------------|------------------|---------------|  
    |**顧客**|**繰り返しレコード**||  
    ||**無視します。**||  
    |**項目**|**レコード**||  
  
     ![子要素 画面](../core/media/flatfileschemawizard-childelements.gif "FlatFileSchemaWizard_ChildElements")  
  
    > [!NOTE]
    >  複数の行を選択し、変更することができます、**要素型**マウスと shift キーまたは CTRL キーを使用して単一の型にします。  
  
    > [!NOTE]
    >  クリックした後**次へ**上、**子要素** 画面で、をクリックしてできません**戻る**再定義するか、子要素を変更します。 子要素を再定義または変更するには、ウィザードを終了し、もう一度ウィザードを起動してフラット ファイルを定義する必要があります。  
  
3.  以上の手順を完了すると、次に示すようにスキーマの最初のレベルが生成されます。 ここでは 3 つの一意な要素が定義されています。この後で、注文書レコード内の要素の子レコードを定義します。 **[次へ]**をクリックします。  
  
     ![サンプル スキーマ 画面](../core/media/flatfileschemawizard-schema1.gif "FlatFileSchemaWizard_Schema1")  
  
## <a name="define-the-customer-record"></a>顧客レコードを定義します。  
  
1.  定義したので、**顧客**要素として、**繰り返しレコード**型および**項目**要素として、**レコード**BizTalk を入力します。フラット ファイル スキーマ ウィザードは、さらにこれら 2 つの要素を定義するようになりました続行します。 **スキーマ ビュー**画面で、**顧客**、順にクリック**次へ**を続行します。  
  
2.  顧客レコードを操作するには、要素を表すデータを選択する必要があります。 このレコードは繰り返しレコードなので、任意の行を使用してレコードを定義できます。 顧客データの最初の行を選択し、クリックして**次**を続行します。  
  
3.  **レコード書式を**ページで、選択**相対位置**をクリックし、 **次へ**です。  
  
4.  このウィザードでは、フィールドの間隔を表示および計算するためのビジュアル ツールを利用できます。 **位置指定レコード** ページで、マウスの左ボタンを使用して、名前 フィールドの開始位置を表す位置マーカー 10 をクリックします。 次の位置マーカーを残りのデータ フィールドをクリックします。  
  
    |フィールド名|位置マーカー|  
    |----------------|---------------------|  
    |street|30|  
    |city|50|  
    |state|65|  
    |postalcode|68|  
  
     **[次へ]** をクリックして次に進みます。  
  
     ![位置指定レコード 画面](../core/media/flatfileschemawizard-positionalrecord.gif "FlatFileSchemaWizard_PositionalRecord")  
  
5.  **子要素** ページで、子要素のプロパティを指定します。 最初の行と種類を選択**国**として、**要素名**です。 他の列では既定値をそのまま使用します。 他のプロパティに次の値を入力、**要素名**:  
  
    |要素名|値|  
    |------------------|-----------|  
    |**customer_Child2**|**fullName**|  
    |**customer_Child3**|**番地**|  
    |**customer_Child4**|**市区町村**|  
    |**customer_Child5**|**状態**|  
    |**customer_Child6**|**[郵便番号]**|  
  
     **[次へ]** をクリックして次に進みます。  
  
     ![子要素 画面](../core/media/flatfileschemawizard-childelements2.gif "FlatFileSchemaWizard_ChildElements2")  
  
6.  次に示すように、顧客レコードの子要素が作成されます。 をクリックして**次**品目レコードの子要素を定義します。  
  
     ![サンプル スキーマ 画面](../core/media/flatfileschemawizard-schema2.gif "FlatFileSchemaWizard_Schema2")  
  
#### <a name="define-the-items-record"></a>品目レコードを定義します。  
  
1.  **スキーマ ビュー** ] ページで、[**項目**、順にクリック**次**です。  
  
2.  **ドキュメント データを選択**ページで、行全体が項目では、開始、クリックして選択**[次へ]**をその子要素を定義します。  
  
3.  **レコード書式を**ページで、選択**区切り記号**、クリックして**次へ**です。  
  
4.  品目レコードでは、個々の品目の区切りにコンマを使用します。 したがって、上、**区切られたレコード** ページで、items レコードを定義するには、次を入力します。 完了したら、をクリックして**次**です。  
  
    -   選択**、**から**子区切り記号**ドロップダウン選択リストです。  
  
    -   ままにして、**エスケープ文字**ボックスは空白です。  
  
    -   選択**レコードにタグ識別子**および種類**項目**で**タグ**です。  
  
         複数の items レコードで**項目**個々 のレコードの識別に使用します。  
  
5.  値を使用して、**区切られたレコード** ページで、ウィザードは、2 つの子要素を識別します。 うち 1 つは繰り返しレコードであるため、最初の要素を選択し、入力**項目**要素名、および選択**繰り返しレコード**ドロップダウンの選択リストから**要素の型**. 残りの列の値は既定値のまま使用します。 2 番目の行を選択し、選択、**無視**から**要素型** ボックスの一覧です。 クリックすると**次**スキーマに items レコードの次のレベルを作成します。 続けて、注文書スキーマの最後の部分を定義します。  
  
6.  選択**項目** をクリックし、 **次へ**を続行する、**スキーマ ビュー**ページ。  
  
7.  **[ドキュメント データ**] ページで選択**ITEM872 AA & #124 です。芝刈り機 (&) #124; 1 &#124; 148.95 & #124 です。これが電気ことを確認**です。 **[次へ]** をクリックして次に進みます。  
  
8.  **レコード書式を**ページで、選択、**区切り記号**個々 のアイテムは、パイプ (&#124;) で区切られたオプションを指定します。  
  
9. **区切られたレコード** ページで、品目レコードを定義するには、次を入力します。 完了したら、をクリックして**次**です。  
  
    -   選択**&#124;**から、**子区切り記号**ドロップダウン リストで選択します。  
  
    -   ままにして、**エスケープ文字**ボックスは空白です。  
  
10. **子要素** ページで、ウィザードが 5 つの子要素を識別します。 最初の行を選択し、入力**productCode**の**要素名**です。 残りの列では既定値をそのまま使用します。 残りの部分、**要素名のプロパティ**次を入力します。  
  
    |要素名|値|  
    |------------------|-----------|  
    |**item_Child2**|**説明**|  
    |**item_Child3**|**数量**|  
    |**item_Child4**|**unitPrice**|  
    |**item_Child5**|**注意事項**|  
  
     **[次へ]** をクリックして次に進みます。  
  
11. これで、注文書スキーマのすべてのノードを定義しました。 **スキーマ ビュー** ] ページで [**完了**です。  
  
12. これで、最終的な注文書スキーマを表示できます。 BizTalk スキーマ エディターでスキーマの定義を更新することもできます。 フラット ファイル プロパティの名前のテーブルと、プロパティ テーブルで参照してください**スキーマ ノードのプロパティ**です。 このプロパティの詳細について[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]です。
  
## <a name="summary"></a>概要  
 このチュートリアルでは、BizTalk フラット ファイル スキーマ ウィザードを使用して、ドキュメント インスタンスからフラット ファイル スキーマを作成する方法について学習しました。  
  
## <a name="next-steps"></a>次の手順  
  
### <a name="validate-po-instance"></a>PO インスタンスを検証します。  
 PurchaseOrder.xsd スキーマで適切に PO インスタンスが解析されることを確認するには、次の操作を行います。  
  
1.  ソリューション エクスプ ローラーで右クリックし、 **PurchaseOrder.xsd**し、**プロパティ**です。  
  
2.  **プロパティ ページ**、ことを確認して、**入力インスタンス ファイル名**フィールドが、チュートリアルの前提条件セクションで作成した PO インスタンスの場所を指している: フラット ファイルを作成します。ドキュメント インスタンスからスキーマです。 をクリックして**OK**ダイアログ ボックスを閉じます。  
  
3.  ソリューション エクスプ ローラーで右クリック**PurchaseOrder.xsd**、し、**インスタンスの検証**です。 検証コンポーネントが開きます。  
  
4.  検証が完了すると、PurchaseOrder.xsd スキーマによる PO インスタンスの解析結果に基づいた XML 出力を確認するためのリンクが表示されます。 この XML 出力を表示するには、Ctrl キーを押しながらリンクをクリックします。  
  
### <a name="create-pipelines-for-the-schema"></a>スキーマのパイプラインを作成します。  
 ここで、BizTalk アプリケーションで使用するための、PurchaseOrder.xsd スキーマに基づく受信パイプラインまたは送信パイプラインを作成できます。  
  
 新しいパイプラインを作成するを参照してください。[新しいパイプラインを作成する方法](../core/how-to-create-a-new-pipeline.md)です。 フラット ファイル パイプライン コンポーネントを構成するのを参照してください。 [、フラット ファイル アセンブラー パイプライン コンポーネントを構成する方法](../core/how-to-configure-the-flat-file-assembler-pipeline-component.md)と[、フラット ファイル逆アセンブラー パイプライン コンポーネントを構成する方法](../core/how-to-configure-the-flat-file-disassembler-pipeline-component.md)です。  
  
## <a name="see-also"></a>参照  
 [BizTalk フラット ファイル スキーマ ウィザードを使用する方法](../core/how-to-use-biztalk-flat-file-schema-wizard.md)   
 [BizTalk フラット ファイル スキーマ ウィザードを使用してスキーマを作成します。](../core/creating-schemas-using-biztalk-flat-file-schema-wizard.md)