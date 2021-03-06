---
title: メッセージの処理 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- processing
- messages, pipelines
- routing, about routing
- adapters, about adapters
- routing, message types
- processing, messages
- messages, processing
- routing
- messages, routing
- pipelines, about pipelines
- message types
- messages, message types
- messages, adapters
ms.assetid: e6d1f969-20c9-41f6-85cb-46cf92656348
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 49329e23127f051a593596955f808cc879dd76f6
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36987787"
---
# <a name="processing-the-message"></a>メッセージの処理
これまで説明したコンポーネントはすべて、メッセージが BizTalk Server を通過する過程で行われる処理にそれぞれの役割を果たしています。 このセクションでは、これらのコンポーネントが機能的にどのように連携するかについて説明します。最初にメッセージの受信について説明します。 受信ポートの作成と受信プロセスにおけるメッセージ フローを、次の図に示します。  
  
 *受信ポート* は、1 つ以上の受信場所と 0 個以上のマップで構成されます。 マップは、XML メッセージの構造または形式を変換するときに使用する XSLT (Extensible Stylesheet Language Transformations) スタイル シートであり、受信プロセスでメッセージを内部形式に正規化するときによく使用されます。 受信場所は、メッセージを受信するエンドポイントを制御します。 受信場所は、受信アダプターに対して構成したエンドポイントと受信パイプラインで構成されます。  
  
 ![受信ポートの構造と処理](../core/media/arch-message-processing.gif "arch_message_processing")  
  
## <a name="the-role-of-the-adapter"></a>アダプターの役割  
 受信アダプターは、データ ストリームを読み取りメッセージを作成することによって、メッセージの受信プロセスを開始します。 たとえば、ファイル アダプターは、ファイルが構成された場所に配置されたことを検出すると、そのファイルをストリームに読み取ります。 アダプターは、メッセージを作成し (Microsoft.BizTalk.Message.Interop.IBaseMessage インターフェイスの実装)、このメッセージに要素を追加し (Microsoft.BizTalk.Message.Interop.IBasePart インターフェイスの実装)、その要素の内容としてデータ ストリームを提供します。  
  
 また、アダプターは書き込みを行って、場所、アダプターの種類、およびアダプターに関するその他の項目に関連するメッセージ コンテキスト プロパティに昇格させます。 メッセージとコンテキストが作成されると、アダプターはメッセージをエンドポイント マネージャーに渡します。 メッセージは、受信場所に対して構成された受信パイプラインを経由して処理されます。 メッセージがパイプラインによって処理されると、エンドポイント マネージャーがメッセージ エージェントを使用してメッセージを公開する前に、マップを使用してメッセージを目的の形式に変換できます。  
  
## <a name="the-role-of-the-pipeline"></a>パイプラインの役割  
 最初のメッセージがアダプターによって作成されると、受信メッセージで発生する処理の大部分が受信パイプラインで行われます。 パイプラインでは、メッセージの内容だけでなくメッセージのコンテキストも処理します。 メッセージの内容は通常デコード、逆アセンブル、および検証の各ステージで処理されますが、メッセージのコンテキストはすべてのステージで処理することができます。 ただし、パイプラインでは内容もコンテキストも処理されるとは限りません。 たとえば、既定のパススルー パイプラインではコンポーネントが構成されておらず、メッセージの内容またはコンテキストに対する処理を行いません。 説明を簡単にするために、このドキュメントでは、一般にメッセージのルーティングに影響を与える逆アセンブラー コンポーネントについて説明します。  
  
 *逆アセンブラー* では、アダプターから受信したメッセージを処理して、複数のメッセージに逆アセンブルし、メッセージ データを解析します。 受信メッセージに多数のより小さいメッセージが含まれている場合、これは *インターチェンジ*と呼ばれます。 開発者が、前後のコンテンツに関する情報 (つまり、フラット ファイル逆アセンブラーのヘッダーと末尾のスキーマ、および XML 逆アセンブラーのエンベロープ スキーマ) および (繰り返される可能性もある) 本文のコンテンツに関する情報を構成することによって、フラット ファイル逆アセンブラーおよび XML 逆アセンブラーでのインターチェンジ処理が可能になります。 また、これらの逆アセンブラーでは元のメッセージから XML コンテンツへの解析が行われます。 ただし、カスタムの逆アセンブラーでは、BizTalk Server で XML に対するそれ以上の処理を行う必要がない場合、コンテンツの XML への解析を行わないこともあります。 たとえば、単純なルーティングのシナリオで、ある受信場所で受信したメッセージが指定の送信ポートに送信され、マッピングや他の XML ベースの処理を特に要しない場合などがこれにあたります。  
  
## <a name="routing-with-the-message-type"></a>メッセージの種類を使用したルーティング  
 ルーティングに使用する最も一般的なメッセージ プロパティの 1 つは、メッセージの種類です。 開発者がメッセージの構造を定義するためのスキーマを作成すると、このスキーマによってメッセージの種類が定義されます。 種類は、スキーマ定義のルート ノードと名前空間によって決められます。 たとえば、次のような XML ドキュメントはメッセージの種類があります。 http://tempuri.org/samples/MessageType#Message  
  
```  
<Message xmlns=http://tempuri.org/samples/MessageType>  
<SomeOtherElement type="sample"/>  
</Message>  
```  
  
 メッセージの種類をルーティングに使用するには、メッセージの種類をコンテキストに昇格させる必要があります。 メッセージ構造に精通している場合は、逆アセンブラーを使用して、この値をメッセージ コンテキストだけでなくパイプライン コンポーネントに昇格させます。 XML 逆アセンブラーとフラット ファイル逆アセンブラーではメッセージを処理するときにメッセージの種類を昇格させます。カスタム逆アセンブラーでも、ルーティングを適切に行うには、このプロパティを昇格させる必要があります。  
  
 メッセージの種類は必ずしも必要ではないことに注意してください。 前述したように、メッセージの各部はバイナリ データにすることができ、その構造を定義するスキーマを含める必要はありません。 このようなメッセージ部分は、通常 BizTalk Server 自体による処理がほとんど行われずに BizTalk Server から渡されます。ただし、オーケストレーションから呼び出されたカスタムのパイプライン コンポーネント、アダプター、コードでは、これらの部分とやりとりする場合もあります。  
  
 また、パイプライン コンポーネントでも、アダプター同様、プロパティの書き込みおよびメッセージ コンテキストへの昇格を行います。 実際、パイプライン コンポーネントは最も一般的なメカニズムであり、ほとんどの開発者がプロパティをメッセージ コンテキストに昇格させるために使用します。 開発者はスキーマを作成し、スキーマのプロパティを昇格させることができます。 この情報を注釈としてスキーマに保存すると、パイプライン コンポーネントで使用できます。 すべての組み込み逆アセンブラーおよびアセンブラー コンポーネント (FlatFile、XML、および BizTalk Framework) はドキュメント スキーマを使用して、昇格させるプロパティに関する情報を取得します。 コメントから XML Path Language (XPath) ステートメントを使用して、逆アセンブラーは、昇格する要素のドキュメントの場所を認識します。 逆アセンブラーは、ドキュメント全体のストリーミング処理時に、いずれかの XPath ステートメントに一致する要素を検出し、必要に応じてその値のコンテキストへの昇格または書き込みを行います。  
  
 カスタム パイプライン コンポーネントでは、送受信メッセージの任意のデータのプロパティをコンテキストに昇格させることができます。 プロパティをコンテキストに昇格させてルーティングに使用するには (おそらくはそのために値を昇格させるわけです)、プロパティを定義したプロパティ スキーマを作成して BizTalk Server に展開する必要があります。 カスタム コンポーネントで使用するプロパティ スキーマを定義する前に、昇格させたさまざまなプロパティの種類を理解する必要があります。 プロパティ スキーマで定義される昇格させたプロパティの基本型は、次のいずれかです。  
  
- [Microsoft.XLANGs.BaseTypes.MessageContextPropertyBase](http://msdn.microsoft.com/library/microsoft.xlangs.basetypes.messagecontextpropertybase.aspx) または  
  
- [Microsoft.XLANGs.BaseTypes.MessageDataPropertyBase](http://msdn.microsoft.com/library/microsoft.xlangs.basetypes.messagedatapropertybase.messagedatapropertybase.aspx)  
  
  MessageDataPropertyBase という基本型を持つプロパティは、このプロパティの値がメッセージの内容に由来することを示します。 これは、プロパティ スキーマで定義されたプロパティの既定値として通常使用されます。 MessageContextPropertyBase で表現されるプロパティは、メッセージ コンテキストに含まれますが、直接メッセージ データに由来するとは限りません。 基本型が MessageContextPropertyBase のプロパティは、しばしばアダプターと逆アセンブラーによって昇格され、メッセージやアダプターの種類など共通のプロパティを含んでいます。  
  
  プロパティを定義する際には、型の相違を理解して、正しく使用することが大切です。 このことは、オーケストレーション内でメッセージのコンテキスト プロパティにアクセスする場合に大きな意味を持ちます。 プロパティが MessageDataPropertyBase として識別された場合、オーケストレーション デザイナーは受信中のメッセージ スキーマを調べて、一致する昇格させたプロパティが定義されていることを確認します。 アクセス中の昇格させたプロパティに関連付けられたスキーマにプロパティがない場合、オーケストレーション デザイナーでプロパティにアクセスすることはできません。 一方、プロパティが MessageContextPropertyBase として定義されていれば、メッセージの種類にかかわらずプロパティにアクセスできます。  
  
  カスタム パイプラインで、コンテキストにプロパティを昇格させるメカニズムと書き込むメカニズムはよく似ています。 プロパティを書き込む場合は、IBaseMessageContext.Write メソッドを呼び出して値をコンテキスト内に配置します。 プロパティを昇格させる場合は、代わりに IBaseMessageContext.Promote メソッドを使用します。 いずれのメソッドでもプロパティ名、名前空間、および値が必要です。 昇格させたプロパティの名前と名前空間は、プロパティ スキーマに定義されており、プロパティ スキーマ アセンブリを参照し、プロパティ用に作成したクラスでプロパティを使用して、簡単にアクセスできます。 識別フィールドが共通の名前空間を使用して http://schemas.microsoft.com/BizTalk/2003/btsDistinguishedFields 、し、値を取得するために使用する XPath 式は通常名として使用します。  
  
  コンテキストにプロパティを昇格させる場合と書き込む場合のコードの例を次に示します。 この例では、識別フィールドがコンテキストに書き込まれます この例は、オーケストレーション デザイナーがフィールドを認識できるようにメッセージ スキーマで識別フィールドを識別しているオーケストレーションにのみ有効です。 コンテキストにプロパティを書き込んで、送信側または受信側の他のパイプライン コンポーネントで使用できるようにすると便利です。  
  
```  
//create an instance of the property to be promoted  
SOAP.MethodName methodName = new SOAP.MethodName();  
  
//call the promote method on the context using the property class for name   
//and namespace  
pInMsg.Context.Promote(methodName.Name.Name, methodName.Name.Namespace,   
"theSOAPMethodName");  
  
//write a distinguished field to the context  
pInMsg.Context.Write("theDistinguishedProperty",   
"http://schemas.microsoft.com/BizTalk/2003/btsDistinguishedFields",   
"theDistinguishedValue");  
```  
  
 値をコンテキストに昇格させる、または書き込む際は、以下の点に注意してください。  
  
- 以前にプロパティを昇格させたときと同じ名前および名前空間を使用してコンテキストに値を書き込むと、プロパティは昇格されなくなります。 書き込みによって、基本的に昇格は上書きされます。  
  
- NULL 値のプロパティは使用できないので、コンテキストに NULL 値を書き込んだ場合は、値が削除されます。  
  
- 昇格させたプロパティの長さは 256 文字までに制限されますが、書き込みプロパティには長さの制限がありません。  
  
  昇格させたプロパティはメッセージ ルーティングに使用されるので、比較と保存を効率よく行うためにサイズが制限されます。 書き込みプロパティにはサイズの制限がありませんが、コンテキストに大きな値を使用すると、値を処理してメッセージと共に渡す必要があるため、パフォーマンスに影響します  
  
  BizTalk Server からメッセージを送信する準備が整うと、送信ポートで予備処理が行われます。 送信パイプラインが実行される前にマップがメッセージに適用されて、パイプラインで処理されアダプター経由で送信される前にメッセージを顧客またはアプリケーション固有の形式に変換できるようになります。 送信パイプラインでは、プロパティをメッセージ コンテキストに昇格させる代わりに、プロパティをコンテキストからメッセージに降格させます。  
  
  ![送信ポートと送信パイプライン処理](../core/media/arch-message-processing-2.gif "arch_message_processing-2")  
  
## <a name="see-also"></a>参照  
 [ランタイム アーキテクチャ](../core/runtime-architecture.md)   
 [BizTalk Server がサイズの大きなメッセージを処理する方法](../core/how-biztalk-server-processes-large-messages.md)