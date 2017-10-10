---
title: "SWIFT ヘッダーおよびトレーラ スキーマ |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- trailer schemas
- schemas, headers
- schemas, trailers
- header schemas
ms.assetid: 82cd33d4-6bbb-4124-9506-fd35b5dca8a4
caps.latest.revision: "4"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c8f3cb45e14a7c7e900fc26a4cbc8fcfb5d7b66e
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="swift-header-and-trailer-schemas"></a>SWIFT ヘッダーおよびトレーラ スキーマ
[!INCLUDE[btsCoName](../../includes/btsconame-md.md)][!INCLUDE[A4SWIFT_CurrentVersion_FirstRef](../../includes/a4swift-currentversion-firstref-md.md)] SWIFT のヘッダーおよびトレーラのスキーマを提供します。 A4SWIFT が既に組み込まれているこれらのさまざまな FIN メッセージのインターチェンジのスキーマにします。 カスタム SWIFT FIN 書式スタイル メッセージの種類 (たとえば、N98 メッセージ) を作成する場合は、独自の形式にヘッダーとトレーラーのスキーマを組み込むことができます。  
  
 SWIFT ヘッダー スキーマ (SWIFT Header.xsd) には、次の形式が含まれています。  
  
-   基本的なヘッダー  
  
-   アプリケーション用のヘッダー (入力または出力の選択肢)  
  
-   ユーザー ヘッダー  
  
-   テキスト ブロックの先頭の区切り文字  
  
 基本的なヘッダーには、メッセージのソースに関する情報が含まれています。 アプリケーション ヘッダーには、メッセージの種類およびメッセージの転送先に関する情報が含まれています。 受信パイプラインに SWIFT 逆アセンブラーでメッセージの種類の解像度は、適切なアプリケーション ヘッダー内のフィールドの内容に基づいています。 ユーザー ヘッダーはオプションであり、特別な処理命令が含まれています。  
  
> [!NOTE]
>  いくつかのメッセージの種類には、フィールド 119 ユーザー ヘッダーの内容に基づいて変数の形式があります。 これらは、A4SWIFT で「デュアル メッセージの種類」です。 A4SWIFT 逆アセンブラーは、メッセージ インスタンスの適切なスキーマを選択するのに 119 フィールドの内容と共に、アプリケーション用のヘッダー内のメッセージの種類を使用します。  
  
 *SWIFT ユーザー マニュアル*、すべてこれらのヘッダーの SWIFT サービス用のドキュメント、FIN の一部について説明します。  
  
 テキスト ブロックの先頭が"{4:"、キャリッジ リターンとライン フィード続きます。 テキスト ブロックの先頭が必要です。  
  
 SWIFT のみを含むインターチェンジの処理 (解析と検証) を格納するためにブロック 4 では、インターチェンジのスキーマ内のすべてのヘッダーおよびトレーラ ブロックは省略可能としてマークされます。 これは、基本的なヘッダー ブロック 1、およびアプリケーション用のヘッダー ブロック 2 は必須、SWIFT FIN 仕様から逸脱です。 これにより、ヘッダーを必要としないメッセージを処理するインターチェンジのスキーマを使用することができます。 たとえば、FileAct を通じて受信するメッセージを受け取る場合バッチ ヘッダーは共通のメッセージ型と同様に、メッセージのソースを含めることができます。  
  
 ランタイム スキーマ DLL には、ヘッダー スキーマも含まれています。 A4SWIFT インストール環境では、ランタイム スキーマ DLL と A4SWIFT プロパティ スキーマを展開します。 処理のため、独自のヘッダーを使用する必要がある場合を定義および展開カスタム ヘッダー スキーマ、でき、メッセージの解決に適したプロパティを昇格します。 これを行う場合は、SWIFT の逆アセンブラー (DASM) に新しいヘッダーを指定する必要があります。 カスタム ヘッダー スキーマ必要はありません、SWIFT ヘッダー スキーマとしてドキュメントの種類が同じその A4SWIFT のインストールが実行時のスキーマ DLL にデプロイします。 スキーマの名前空間またはルート ノード名、またはその両方を変更することを確認します。  
  
 SWIFT トレーラー スキーマ (**SWIFT Trailer.xsd**)、次の形式が含まれています。  
  
-   テキスト ブロックの末尾の区切り記号  
  
-   ユーザーのトレーラー (ユーザーおよびシステム情報)  
  
-   システムのトレーラー  
  
 テキスト ブロックの終了区切り記号は、「-」} です。 トレーラー ブロックが始まる"{5:"です。 トレーラーのブロックの内容には、ユーザー情報 (チェックサム、メッセージの認証、独自の認証およびなど) とシステム情報 (遅延メッセージ、メッセージの参照を使用可能な重複するメッセージ、およびなど) の両方が含まれます。 SWIFT によって追加されたトレーラーで区切られた 3 番目のブロックを提供も"{s:"です。 *SWIFT ユーザー マニュアル*、「FIN サービスの説明」の下でについて詳しく説明 5 のブロックの内容。 A4SWIFT が %s のブロックの内容を検証できません。  
  
 実際、FIN インターフェイスまたは SWIFT ネットワークは、トレーラーを追加します。 メッセージにトレーラーが含まれるは、A4SWIFT メッセージを受信するとき、A4SWIFT はメッセージにトレーラーを実行します。 A4SWIFT では、A4SWIFT はメッセージを受信メッセージにトレーラーがない場合、エラーは発生しません。 として、ヘッダー付き自体のブロックを含む、トレーラーのエントリはすべて A4SWIFT では省略可能です。  
  
## <a name="see-also"></a>参照  
 [スキーマの操作](../../adapters-and-accelerators/accelerator-swift/working-with-schemas.md)