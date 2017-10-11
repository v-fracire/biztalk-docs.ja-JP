---
title: "Inspector パイプライン コンポーネントをメッセージ |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- creating, pipelines
- pipelines, custom pipelines
- pipelines, Message Inspector Pipeline Component
- Message Inspector Pipeline Component
- pipelines, creating
ms.assetid: d9c00718-c8cd-4289-8f58-e4edc61b9a05
caps.latest.revision: "12"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d146dbeaa94d47799794de7fa6f9e6b9082f9fa5
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="message-inspector-pipeline-component"></a>Message Inspector パイプライン コンポーネント
このパイプライン コンポーネントにより、マルチパート メッセージのすべての部分、およびメッセージ コンテキストを確認し、メッセージに問題があるかどうかを判断できます。 このコンポーネントはトラブルシューティングの目的で使用します。  
  
 このパイプライン コンポーネントにより、XML ファイルは指定されたディレクトリにドロップされます。 これらの各ファイルは、RNIFv2.0 メッセージの 4 つの部分 (Preamble Header、Delivery Header、Service Header、Service Content) のいずれか、または RNIFv1.1 メッセージの 3 つの部分 (Preamble Header、Service Header、Service Content) のいずれかを含んでいます。 もう 1 つの XML ファイルは、メッセージ コンテキストを含んでいます。  
  
 このコンポーネントは、カスタム パイプラインに構築し、送信ポートに接続します。 送信ポートにフィルタを作成し、監視するメッセージをサブスクライブします。 このトラブルシューティングは、[!INCLUDE[btsCoName](../../includes/btsconame-md.md)]® [!INCLUDE[BTARN_CurrentVersion_FirstRef](../../includes/btarn-currentversion-firstref-md.md)] が既に実行している標準の処理とは別に実行されます。  
  
## <a name="building-a-custom-pipeline-using-the-message-inspector-pipeline-component"></a>Message Inspector パイプライン コンポーネントを使用したカスタム パイプラインの構築  
 Message Inspector パイプライン コンポーネントを使用するには、このコンポーネントを含むカスタム パイプラインを構築し、展開する必要があります。 詳細については、[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)] ヘルプの「パイプライン デザイナーでのパイプラインの作成」を参照してください。  
  
#### <a name="to-deploy-the-message-inspector-pipeline-component"></a>Message Inspector パイプライン コンポーネントを展開するには  
  
1.  [!INCLUDE[vs2012](../../includes/vs2012-md.md)]を起動します。  
  
2.  **ファイル**メニューのをポイント**開く**、順にクリック**プロジェクト**です。  
  
3.  C:\Program files \microsoft BizTalk 2013 Accelerator for rosettanet \sdk\message Inspector Pipeline Component、選択移動**[messageinspector.csproj]**、クリックして**開く**です。  
  
4.  開く、[!INCLUDE[vs2012](../../includes/vs2012-md.md)]コマンド プロンプトです。  
  
5.  コマンド プロンプトで、C:\Program Files\Microsoft BizTalk 2013 Accelerator for RosettaNet\SDK\Message Inspector Pipeline Component\obj\debug に移動します。  
  
6.  コマンド プロンプトで次のように入力します。 **"sn-k MessageInspector.snk"**キーを作成し、ENTER キーを押します。  
  
7.  [!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]、ソリューション エクスプ ローラーで右クリック**MessageInspector**、クリックして**プロパティ**です。  
  
8.  **MessageInspector プロパティ** ページで **署名** タブをクリックして**アセンブリに署名**チェック ボックスをオンします。  
  
9. **厳密な名前キー ファイルを選択して**ドロップダウン、C:\Program files \microsoft BizTalk 2013 Accelerator for rosettanet \sdk\message Inspector Pipeline component \obj\debug 参照および選択**MessageInspector.snk** をクリックし、**開く**です。  
  
10. ソリューション エクスプ ローラーで右**MessageInspector**をクリックし、**ビルド**です。 出力ペインで、ビルドが成功したことを確認します。  
  
11. をクリックして**開始**、をポイント**すべてのプログラム**、をポイント**アクセサリ**、順にクリック**Windows エクスプ ローラー**です。  
  
12. [!INCLUDE[btsWinNoVersion](../../includes/btswinnoversion-md.md)]エクスプ ローラーで、C:\Program files \microsoft BizTalk 2013 Accelerator for rosettanet \sdk\message Inspector Pipeline component \obj\debug、移動を右クリックして**[microsoft.solutions.btarn.sdk.messageinspector.dll]**、クリックして**コピー**です。  
  
13. C:\Program files \microsoft BizTalk 2013 Accelerator for rosettanet \pipeline Components 移動を右クリックして**パイプライン コンポーネント**、順にクリック**貼り付け**です。  
  
14. [!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]の**ファイル**メニューのをポイント**新規**、クリックして**プロジェクト**です。  
  
15. **新しいプロジェクト**ダイアログ ボックスで、テンプレート ペインで**空の BizTalk Server プロジェクト**で、**名前**ボックスで、プロジェクトの名前を入力します。 **場所**ボックスで、プロジェクトを保存するフォルダーに移動し、をクリックして**OK**です。  
  
16. ソリューション エクスプ ローラーでプロジェクト名を右クリックし、**追加**、クリックして**新しい項目の追加**です。  
  
17. **新しい項目の追加**ダイアログ ボックスで、**送信パイプライン**で、**名前**ボックスで、カスタム パイプライン ファイルの名前を入力し、をクリックして**を開く**.  
  
    > [!NOTE]
    >  Message Inspector パイプライン コンポーネントは、受信ポートではなく、送信ポートのみに追加します。  
  
18. ツールボックス ペインの BizTalk パイプライン コンポーネント ペイン内を右クリックし、をクリックして**アイテムの追加/削除**です。  
  
19. **ツールボックスのカスタマイズ** ダイアログ ボックスで、 **BizTalk パイプライン コンポーネント** タブで  **BTARN Message Inspector Component**、順にクリック**ok**.  
  
20. BizTalk パイプライン コンポーネント ペインで、[ツールボックス] ウィンドウをクリックして押した**BTARN Message Inspector Component**のコンポーネントをドラッグし、**ここにドロップします。** ◆セグ ： 前の TU に含まれる◇  
  
21. [!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]、ソリューション エクスプ ローラーで、パイプライン プロジェクトの名前を右クリックし、をクリックして**プロパティ**です。  
  
22. **プロパティ ページ**ダイアログ ボックスで、をクリックして**共通プロパティ**、クリックして**アセンブリ**です。  
  
23. 関連付けられているテキスト ボックスに、右ペインで**アセンブリ キー ファイル**、省略記号ボタンをクリックして、rosettanet \sdk\message Inspector Pipeline component \obj\debug、選択の C:\Program files \microsoft BizTalk 2013 Accelerator に移動します。**MessageInspector.snk**、クリックして**OK**です。  
  
24. [!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]パイプライン デザイナー、select、 **BTARN Message Inspector Component**図形です。  
  
25. [!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]プロパティ ウィンドウで、**ディレクトリ**ボックスに、XML ファイルをドロップするディレクトリの名前を入力します。  
  
26. ソリューション エクスプ ローラーでプロジェクト名を右クリックし、をクリックして**ビルド**です。 ビルドが成功することを確認します。  
  
27. ソリューション エクスプ ローラーでプロジェクト名を右クリックし、をクリックして**展開**です。 展開が成功することを確認します。  
  
28. [!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]の**ビュー** メニューのをクリックして**BizTalk エクスプ ローラー**です。  
  
29. 右クリック**送信ポート**、クリックして**送信ポートの追加**です。  
  
30. **新しい送信ポートを作成**ダイアログ ボックスで、をクリックして**OK**です。  
  
31. **送信ポートのプロパティ** ダイアログ ボックスで、**名前**と送信ポートの名前を入力ボックスに、**プライマリ**をクリックして選択すると、左側のウィンドウで、**トランスポートの種類**クリックし、右側のペインで**ファイル**です。  
  
32. **送信ポートのプロパティ** ダイアログ ボックスで、**アドレス (URI)**ボックスで、省略記号ボタンをクリックして (**.**).  
  
33. **FILE トランスポートのプロパティ**ダイアログ ボックスで、型、**先**フォルダー名 をクリックして**送信**左側のウィンドウでし、 **送信パイプライン**右側のウィンドウで、先ほど作成したカスタム パイプラインを選択します。  
  
34. をクリックして**フィルターし、マップ**をクリックして、左側のウィンドウ**フィルター**です。  
  
35. 右側のペインにフィルター式を入力し、パイプラインで XML ファイルをドロップするファイルの種類を指定します。 たとえばのすべての RNIF v1.1 メッセージ、ファイルを削除する場合**プロパティ**Microsoft.Solutions.BTARN.Schemas.RNIFv11.GlobalBusinessAction を選択および**演算子**と"Exists"を選択し、クリックして**OK**です。  
  
36. BizTalk エクスプローラで、先ほど作成した送信ポートを右クリックし、をクリックして**Enlist**送信ポートを再度右クリックし、クリックして**開始**です。  
  
## <a name="remarks"></a>解説  
 通常の処理では、一度に確認できるのはメッセージの一部分 (オーケストレーションでメッセージの本文として指定した部分) のみです。 したがって、BizTalk 管理コンソールではメッセージの一部分しか確認できないため、トラブルシューティングの能力も限定されます。 Message Inspector パイプライン コンポーネントでは、この制限を克服するのに役立ちます。  
  
## <a name="see-also"></a>参照  
 [ユーティリティ](../../adapters-and-accelerators/accelerator-rosettanet/utilities1.md)