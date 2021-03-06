---
title: JD Edwards OneWorld スキーマを BizTalk Server プロジェクトにインポート |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- generating schemas
- importing schemas
- schemas, generating
- schemas, importing into BizTalk Server projects
ms.assetid: 5bcaa276-8c76-4212-b373-de86e3008a69
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5954f92e55dac362387d66a8b65375e92fe187fa
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36966147"
---
# <a name="importing-jd-edwards-oneworld-schemas-into-biztalk-server-projects"></a>JD Edwards OneWorld スキーマを BizTalk Server プロジェクトにインポートする
ここでは、JD Edwards OneWorld サーバーを参照し、スキーマを [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] プロジェクトにインポートする方法について説明します。  
  
> [!NOTE]
>  arglist を設定したことを確認する必要があります。 オーケストレーションでスキーマを生成する前に、jdearglist.txt を更新する必要があります。 詳細については、次を参照してください。[文字列値の処理](../core/handling-string-values1.md)します。  
  
> [!NOTE]
>  Jdearglist を変更するたびにそのビジネス オブジェクトのスキーマを再生成する必要があります。  
  
 JD Edwards OneWorld 論理システムを作成した後、BizTalk Server プロジェクトから Microsoft アダプター ウィザードを開くことで、JD Edwards OneWorld を参照できます。  
  
### <a name="to-import-schemas"></a>スキーマをインポートするには  
  
1. [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]を開きます。  
  
2. 右クリックし、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]プロジェクトをポイントして、**追加**、選択および**生成した項目の追加**します。  
  
3. をクリックして**アダプタの追加**を選択し、**オープン**します。  
  
4. アダプターを選択し、クリックして**次**します。  
  
    JD します。 Edwards OneWorld XE システムは、ブラウザーに表示されます。  
  
    ![](../core/media/jdedadapter-04-jdebrowse.gif "JDEdAdapter_04_JDEBrowse")  
  
    アダプター ウィザードには、定義されているすべてのシステムのツリーが表示されます。 JD Edwards OneWorld には、1 つの長いリストに表示するには多すぎるほどのモジュールがあります。 モジュールは名前の最初の 3 文字に従ってグループ化されます。  
  
   - 階層の最初のレベルはモジュール名のすべての 3 文字プレフィックスのリストです。  
  
   - 2 番目のレベルは同じ 3 文字プレフィックスを共有するすべてのモジュールのリストを示します。  
  
   - 最後のレベルはモジュールに属するビジネス関数のリストを示します。 サービス アイコンを展開すると、その操作を表示できます。  
  
     操作を展開すると、入出力引数が表示されます。  
  
     入出力引数を展開すると、引数のデータ型が表示されます。  
  
   > [!NOTE]
   >  サーバー オブジェクト定義が変更されると、スキーマを再生成し、そのデータを更新する必要があります。  
  
   > [!NOTE]
   >  スキーマの生成後に jdearglist.txt を変更した場合、スキーマを再生成してそのデータを更新する必要があります。 Jdearglist.txt についてを参照してください[文字列値の処理](../core/handling-string-values1.md)します。  
  
## <a name="generating-schemas"></a>スキーマを生成します。  
 スキーマを生成するには、次の操作を行います。  
  
#### <a name="to-generate-schemas"></a>スキーマを生成するには  
  
1.  スキーマをインポートする項目を選択します。  
  
2.  項目を追加する をクリックします (またはドラッグ)、**送信**ウィンドウ (J. Edwards OneWorld への受信の呼び出し)。  
  
3.  **[OK]** をクリックします。  
  
     選択した JD Edwards OneWorld 項目に対して生成されたスキーマが BizTalk Server プロジェクトにインポートされます。  
  
> [!NOTE]
>  AddressBook (N0100041) を使用する場合、フィールド名は**cActionCode**します。 アクションは XML ファイル自体の一部です。 コードは次のとおりです。  
>   
>  --A は追加  
>   
>  --C は変更  
>   
>  --D は削除  
>   
>  --I は照会  
  
## <a name="see-also"></a>参照  
 [BizTalk 管理へのアイテムの追加](../core/adding-biztalk-adapter-for-jd-edwards-oneworld.md)