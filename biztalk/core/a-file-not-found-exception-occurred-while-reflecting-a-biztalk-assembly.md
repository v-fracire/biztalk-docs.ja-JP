---
title: ファイルが BizTalk アセンブリの反映中に例外が発生しましたが見つかりません |。Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 223147eb-785f-4dfc-b2a6-7d50dfaf8092
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ee0cffc331765924b4fe7d29d95f7094b14aecb3
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37000843"
---
# <a name="a-file-not-found-exception-occurred-while-reflecting-a-biztalk-assembly"></a>BizTalk アセンブリの反映中に、ファイルが見つからないことを示す例外が発生しました
## <a name="details"></a>詳細  

|                 |                                                                                                                                                                                                                                                                                                                                        |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                                                                           [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]                                                                                                                           |
| 製品バージョン |                                                                                                                                       [!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]                                                                                                                                       |
|    イベント ID     |                                                                                                                                                                   0                                                                                                                                                                    |
|  イベント ソース   |                                                                                                                                                                   0                                                                                                                                                                    |
|    コンポーネント    |                                                                                                                                                                   0                                                                                                                                                                    |
|  シンボル名  |                                                                                                                                                                   0                                                                                                                                                                    |
|  メッセージ テキスト   | ファイルが BizTalk アセンブリの反映中に例外が発生しましたが見つかりません。"{0}"。 この問題は、1 つまたは複数の依存関係が使用できない場合に発生することがあります。 この問題を修正する、次のいずれかの操作を試してください: 1。 アセンブリの依存関係を同じフォルダーにコピーします。 2. 足りない依存関係をグローバル アセンブリ キャッシュにインストールします。 |

## <a name="explanation"></a>説明  
 このエラーは、公開されている BizTalk アセンブリが、グローバル アセンブリ キャッシュ (GAC) または同じディレクトリにないアセンブリを参照していることを示します。  

## <a name="user-action"></a>ユーザーの操作  
 エラー メッセージに指定された操作に加え、参照アセンブリをグローバル アセンブリ キャッシュに移動するか、BizTalk アセンブリと同じ場所にコピーします。  

1. クリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**Visual Studio**、順にクリックします**Visual Studio**します。  

2. コマンド プロンプトを開きます。  

3. アセンブリの場所を参照し、入力**gacutil/I/\<**<em>アセンブリ名</em>**\>.dll**
