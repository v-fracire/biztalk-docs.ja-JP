---
title: スキーマ |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- schemas, schema types
- deploying, schemas
- schemas
- schemas, about schemas
- property schemas
- envelope schemas
- schemas, deploying
- XML schemas
- flat file schemas
ms.assetid: aea772bd-e7ab-448e-ba82-e7c8f38087db
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 696c79a30bb58cd91536c19c97db54d6159762b6
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
ms.locfileid: "22270090"
---
# <a name="schemas"></a>スキーマ
Microsoft [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 、処理、およびメッセージの構造体としてのこれらの定義を参照するすべてのメッセージの構造を定義する XML スキーマ定義 (XSD) 言語を使用して*スキーマ*です。 ほとんど例外なく、構造化されたメッセージは、アプリケーションの中核を成すものです。 これらの構造化されたメッセージは、大小さまざまな形式になります。また、多種多様なバックエンド システムおよびデータ ストアを対象とします。 構造化されたメッセージを頻繁に作成して使用するシステムは、さまざまな形式を使用します。 構造化されたメッセージの最も一般的な形式は、XML とフラット ファイルです。  
  
 BizTalk Server は、次の 4 種類のスキーマをサポートしています。  
  
-   XML スキーマ :  XML スキーマは XML インスタンス メッセージのクラス構造を定義します。 このタイプのスキーマでは、XSD (XML Schema Definition) 言語を使って、XML インスタンス メッセージの構造が定義されます。XSD 本来の目的に沿っているため、このスキーマでは、単純な方法で XSD が使用されます。 XML スキーマの詳細については、次を参照してください。 [XML スキーマ](../core/xml-schemas.md)です。  
  
-   フラット ファイル スキーマ :  フラット ファイル スキーマは、フラット ファイル形式 (区切り文字/位置指定、あるいは、その組み合わせ) を使用したインスタンス メッセージのクラス構造を定義します。 XSD のネイティブのセマンティック機能に対応していませんフラット ファイル インスタンス メッセージの構造を定義するための要件をすべてため — さまざまな種類の異なるレコードと、フラット ファイル内のフィールドを使用する区切り記号のなど。BizTalk Server では、XSD の注釈機能を使用して、XSD スキーマ内でこの追加情報を格納します。 BizTalk Server には、必要な補足情報をすべて格納することのできる注釈タグが豊富に定義されています。 フラット ファイル スキーマの詳細については、次を参照してください。 [Flat File Schemas](../core/flat-file-schemas.md)です。  
  
-   エンベロープ スキーマ :  エンベロープ スキーマは、XML スキーマの一種です。 XML ビジネス ドキュメントを単一の XML インスタンス メッセージにラップする XML エンベロープの構造を定義するために使用されます。 XML スキーマをエンベロープ スキーマとして定義する場合、エンベロープ スキーマに定義されるルート レコードが複数存在するかどうかなどの条件に応じて、追加のプロパティ設定がいくつか必要となります。 エンベロープ スキーマの詳細については、次を参照してください。[エンベロープ スキーマ](../core/envelope-schemas.md)です。  
  
-   プロパティ スキーマ :  プロパティ スキーマは BizTalk Server 内に 2 つあるプロパティ昇格メカニズムの 1 つで使用されます。 *プロパティの昇格*は、インスタンス メッセージの内部からメッセージ コンテキストに特定の値をコピーするプロセスです。 各種の BizTalk Server コンポーネントは、メッセージ コンテキストを通じて、これらの値に容易にアクセスできるようになります。 これらのコンポーネントが、メッセージ コンテキスト内の値にアクセスすることで、メッセージのルーティングなどの処理が実行されます。 昇格されたプロパティ値は、インスタンス メッセージを宛先に送る直前に、逆の方向にコピーすることもできます。つまり、プロパティ値をアクセスしやすいメッセージ コンテキストから、インスタンス メッセージの内部に戻すことができます。 プロパティ スキーマは BizTalk スキーマの簡易版ですが、昇格されたプロパティをインスタンス メッセージからメッセージ コンテキストへ、あるいはその逆へコピーするプロセスで使用されます。 プロパティ スキーマの詳細については、次を参照してください。[プロパティ スキーマ](../core/property-schemas.md)です。  
  
## <a name="schema-deployment"></a>スキーマの展開  
 スキーマの種類には、メッセージ スキーマ、プロパティ スキーマ、エンベロープ スキーマなどがあります。 スキーマには違いがあるため、展開された後の扱い方が少し異なります。 このセクションでは、すべてのスキーマで共通する事柄と、スキーマの種類によって異なる事柄について説明します。  
  
 スキーマを展開すると、管理データベースにそのスキーマの内容が保存されます。 同じターゲットの名前空間を持つ複数のスキーマを展開できます。 BizTalk Server は、実行時に使用されるパイプライン デザイナーでスキーマを明示的に指定します。 同じスキーマの複数バージョンが展開されていて、既定のパイプラインを使用した場合やパイプライン デザイナーでスキーマを指定しなかった場合は、BizTalk Server が使用するスキーマを決定します。 この場合、最新バージョンに関連付けられているスキーマがあります: 最高のバージョン番号を持つ、そのスキーマを使用して展開するアセンブリのです。  
  
 そのスキーマを展開した最新バージョンのアセンブリを削除すると、同じアセンブリのその次に新しいバージョンのスキーマがアクティブになります。  
  
 重複するターゲットの名前空間を持つスキーマを展開する場合は、カスタム デザインのパイプラインからスキーマを参照する必要があります。 これによって、メッセージング エンジンに正しいスキーマを読み込むための追加情報が提供されます。  
  
 たとえば、複数の Web サービス スキーマを作成する場合などには、重複するターゲットの名前空間を使用します。  
  
## <a name="see-also"></a>参照  
 [BizTalk エディターを使用してスキーマを作成します。](../core/creating-schemas-using-biztalk-editor.md)   
 [スキーマの BizTalk 表記](../core/biztalk-representation-of-schemas.md)   
 [成果物](../core/artifacts.md)