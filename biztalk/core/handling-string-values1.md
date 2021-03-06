---
title: 文字列 Values1 の処理 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jdearglist.txt, configuring strings
- strings, left-justified
- strings, configuring
- strings, right-justified
ms.assetid: a180b818-1009-45f5-a503-d10ed7dd27fc
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 51397965a416169c8f71ffef8d9466f99f30c093
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36988915"
---
# <a name="handling-string-values"></a>文字列値の処理
このトピックでは、一部の文字列引数を右揃え (および左側に埋め込み) で構成する方法について説明します。  
  
## <a name="types-of-string-values"></a>文字列値の種類  
 JD Edwards OneWorld は、その相互運用性レイヤーを通じて、次の 2 種類の文字列値を公開します。  
  
- char: 単一の文字  
  
- 最大文字列長  
  
  JD Edwards OneWorld のビジネス関数では、ハンガリアン記法を使用してこれらの型の引数を指定します。 たとえば、これらの種類の引数は以下から始まります。  
  
- c  
  
- sz  
  
### <a name="left-justified-values"></a>左揃えの値  
 sz 型の引数 (最大長の文字列または文字配列) の大半について、JD Edwards OneWorld では左揃えの値にする必要があります。 たとえば最大長が 40 の住所行の場合、JD Edwards OneWorld では次のように指定する必要があります。  
  
 "4567 Main St"  
  
 長さ 40 の空白を埋めます。 空白の埋め込みは Microsoft BizTalk Adapter for JD Edwards OneWorld により行われます。 このため、クライアント コードに入力する必要があるのは「4567 Main St.」だけです。  
  
### <a name="right-justified-values"></a>右揃えの値  
 この種類の値のサブセットについて、JD Edwards OneWorld では左側に空白が埋め込まれた右揃えの値にする必要があります。 たとえば、B4200310 ソース モジュールでビジネス関数の場合、引数 szbusinessunit の長さは 12 です。 この引数は、生産施設などのプラントを表します。 プラント番号が 30、j. d. Edwards OneWorld XE では、値が必要です。  
  
 "          30"  
  
 右揃えになる値を入力するには、jdearglist.txt という名前のファイルにパラメーターを入力する必要があります。 スキーマを生成するときに、jdearglist.txt が読み取られます。 このテキスト ファイルに記述される値は右揃えの値に自動変換され、左に空白が埋め込まれます。  
  
 エントリをこれらのパラメーターを記述して jdearglist.txt はテキスト エディターを作成し、次のフォルダーに保存する必要があります: %BizTalk_Install_Adapter%\config\JDE\  
  
 場所 **%biztalk_install_adapter** JD Edwards OneWorld を BizTalk Adapter をインストールしたディレクトリです。  
  
 このファイルが存在しないか空の場合、Microsoft BizTalk Adapter for JD Edwards OneWorld が最初に開くときに情報メッセージがログに記録されます。  
  
> [!NOTE]
>  スキーマの生成後にこのファイルを変更した場合は、スキーマを再生成してスキーマに含まれるデータを更新する必要があります。  
  
 このファイルに含まれる最新の情報を使用していることを確認するため、スキーマを再生成する前に、タスク マネージャーを使用して browsingagent.exe プロセスを停止することができます。ただし、この確認は必須ではありません。  
  
 以下は、jdearglist.txt に記述するエントリの形式の例です。  
  
```  
<SourceModule>.<BusinessFunction>.<Argument>  
```  
  
 以下に例を示します。  
  
```  
B4200310.F4211FSBeginDoc.szBusinessUnit  
```  
  
 同じビジネス モジュールに属するビジネス関数の場合、(同じ種類の引数で) 似た名前の付いた引数は、ビジネス関数の一部またはすべてにおいて共有されます。 ビジネス関数名の代わりにワイルドカード文字 (*) を使用できます。 以下に例を示します。  
  
```  
B4200310.*.szBusinessUnit  
```  
  
> [!NOTE]
>  JD Edwards OneWorld ビジネス プロセスを別のコンピューターにインポートする場合は、手動で jdearglist.txt をコピーする必要があります。  
  
## <a name="see-also"></a>参照  
 [Jdearglist での文字列の位置](../core/setting-string-justification-in-jdearglist.md)   
 [付録 A: データ型](../core/appendix-a-data-types.md)