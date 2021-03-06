---
title: マップの検証を構成する方法とパラメーターのテスト |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1768918c-e94f-476f-b288-9e030c691177
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e7aaa62e74f1c49f2e43d96c7d546af023847d91
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36967411"
---
# <a name="how-to-configure-map-validation-and-test-parameters"></a>マップの検証を構成する方法とパラメーターをテストします。
検証して、マップのテスト、前に、マップの検証とテストのパラメーターを設定する必要があります、**プロパティ**マップのウィンドウ。  
  
## <a name="configure-the-map-validation-and-test-parameters"></a>マップの検証とテストのパラメーターを構成します。  
  
1.  ソリューション エクスプ ローラーでマップを構成し、をクリックするのプロパティ ページを右クリックして**プロパティ**します。  
  
2.  プロパティ ウィンドウで、次の操作を行います。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**TestMap 入力を検証します。**|マップのテストの前に、インスタンス メッセージを送信元スキーマと照合して検証するかどうかを設定します。|  
    |**TestMap 出力を検証します。**|マップのテストの後で、インスタンス メッセージを送信先スキーマと照合して検証するかどうかを設定します。|  
    |**TestMap の入力インスタンス**|マップのテストの際に使用するインスタンス メッセージ データの場所を設定します。<br /><br /> 構成する必要があるこのプロパティを設定する場合、 **TestMap の入力**プロパティ。|  
    |**TestMap 出力インスタンス**|マップのテスト操作の出力を格納するファイルの場所を構成します。<br /><br /> 構成する必要があるこのプロパティを設定する場合、 **TestMap 出力**プロパティ。|  
    |**TestMap の入力**|入力インスタンスのデータ形式を設定します。|  
    |**TestMap の出力**|マップのテストの際に使用する出力データ形式を設定します。|  
  
    > [!IMPORTANT]
    >  マップをテストする場合は、マップのプロパティを先に構成する必要があります。  

作成したマップは検証する必要があります。 このトピックでは、マップを検証するための手順について説明します。  
  
## <a name="validate-a-biztalk-map"></a>BizTalk マップを検証します。  
  
1.  ソリューション エクスプローラーで、検証するマップを開きます。  
  
2.  ソリューション エクスプ ローラーで、マップを右クリックし、**マップの検証**です。  
  
3.  **出力**ウィンドウで、結果を確認します。  
  
> [!IMPORTANT]
>  出力でカスタム データまたは定数を使用する場合、送信元のテスト データと送信先の定数値のデータ型が有効であることを確認する必要があります。 マップを検証する場合、BizTalk マッパーでは、スキーマで定義されているデータ型にインスタンス データが違反しているかどうかを確認しません。 データ型の確認は、BizTalk エディターでマップのテストまたはインスタンス データの検証を行うと実行されます。 

## <a name="test-a-biztalk-map"></a>BizTalk マップをテストします。

作成したマップはテストする必要があります。 ここでは、マップ コンパイラによって生成された XSLT を表示する手順も含め、マップをテストするための手順について説明します。  
  
1.  ソリューション エクスプ ローラーで、テスト、および選択するマップを右クリックして**テスト マップ**します。  
  
2.  結果を確認、**出力**ウィンドウ。  
  
    > [!IMPORTANT]
    >  マップをテストする前に、プロパティ ウィンドウで、入力インスタンスと出力インスタンスのプロパティを構成しておくことをお勧めします。  
  
## <a name="review-the-xslt"></a>XSLT を確認してください。  
 マップ コンパイラによって生成された XSLT を理解すると、多くの場合に役立ちます。 XSLT の理解によって得ることができるメリットの一部を次に挙げます。  
  
- ループまたはカスタム Functoid を使用している場合、ループの実行方法やカスタム Functoid の呼び出し方法についての理解が深まります。  
  
- 複雑なマップがある場合は、XSLT の確認を変換マップを変換する方法を確認することが有効にして、あります insight 構造を改良し、置換、またはいずれかの効率化する方法のまたはパーツの詳細はします。  
  
- カスタム スクリプトや他の成果物を使用している場合、XSLT の確認ができます、スクリプト、成果物、およびマップの他の部分がやり取りする方法を参照してください。  
  
  XSLT を確認することで、マップを適切にデバッグすることが可能になります。  
  
#### <a name="view-the-xslt-generated-by-the-map-compiler"></a>マップ コンパイラによって生成された XSLT を表示します。  
  
1.  Visual Studio の BizTalk プロジェクトから選択、**ソリューション エクスプ ローラー** ] タブで、マップを右クリックし、[**マップの検証**です。  
  
2.  [出力] ウィンドウをスクロールして、XSL ファイルの URL を探します。 キーを押して**CTRL**ファイルを表示する URL を選択します。  
  
> [!NOTE]
>  XSL ファイルに加えられた変更は、マップには反映されません、次回のビルドで上書きされます。  
  
## <a name="see-also"></a>参照  

[マップをデバッグする方法](../core/how-to-debug-maps.md)  
[マップのトラブルシューティング](../core/troubleshooting-maps.md)  