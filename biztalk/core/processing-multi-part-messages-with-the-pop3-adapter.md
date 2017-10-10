---
title: "POP3 アダプターでメッセージの処理のマルチパート |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 56ad041f-f155-4c1c-ab87-1405c80d9b68
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 26aff4569414103ad8c4f37a9e4699a85874e481
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="processing-multi-part-messages-with-the-pop3-adapter"></a>POP3 アダプタでのマルチパート メッセージの処理
POP3 アダプターに記載された IETF 標準に準拠する MIME でエンコードされたメッセージを処理できる[RFC 2045](http://go.microsoft.com/fwlink/?LinkId=58810)、 [RFC 2046](http://go.microsoft.com/fwlink/?LinkId=58811)、および[RFC 2047](http://go.microsoft.com/fwlink/?LinkId=58812)です。 MIME エンコード メッセージは、コンテンツの種類が異なる 1 つ以上の部分を含めることができます。 このトピックでは、POP3 アダプタがマルチパートの MIME エンコード メッセージを処理する方法について説明します。  
  
## <a name="receiving-multi-part-messages-with-the-pop3-adapter"></a>POP3 アダプタでのマルチパート メッセージの受信  
 POP3 アダプターを使用する受信場所がいるかどうか、 **MIME デコードの適用**オプションに設定**True** MIME エンコード メッセージを受信するときに、POP3 アダプターが、次の操作を実行します。  
  
1.  受信した MIME エンコード メッセージの部分から、マルチパート BizTalk メッセージを作成します。 このマルチパート メッセージには、1 つ以上の部分を含めることができます。含まれる部分の数は、受信した MIME エンコード メッセージの部分の数と同じになります。  
  
2.  MIME エンコード メッセージのヘッダーをスキャンします。 かどうか、任意のヘッダーは、トピックに記載されているプロパティの一覧を一致[POP3 アダプタ プロパティ スキーマおよびプロパティ](../core/pop3-adapter-property-schema-and-properties.md)し、これらのヘッダーは、コンテキスト プロパティとしてマルチパート BizTalk メッセージに昇格されます。  
  
3.  構成可能なアルゴリズムを使用して、MIME エンコード メッセージの部分の 1 つを BizTalk メッセージのボディ部として指定します。 BizTalk メッセージのボディ部にどのメッセージ部分を決定するためのアルゴリズムは、以下のセクションで説明されて**本文部分選択アルゴリズム使用 POP3 アダプターによって**です。  
  
4.  マルチパート BizTalk メッセージをメッセージ ボックスに公開します。  
  
## <a name="body-part-selection-algorithm-used-by-the-pop3-adapter"></a>POP3 アダプタで使用されるボディ部の選択アルゴリズム  
 POP3 アダプタは、受信した MIME エンコード メッセージの部分からマルチパート BizTalk メッセージを作成するときに、メッセージ部分の 1 つを、BizTalk メッセージのボディ部として選択します。 BizTalk メッセージのボディ部は、BizTalk Server でのメッセージ検証、マッピング、プロパティの昇格、フラット ファイル アセンブリなどの操作に使用されます。 マルチパート BizTalk メッセージのサブスクライバはすべてのメッセージ部分を受信しますが、マルチパート メッセージを理解できるオーケストレーション、カスタム パイプライン、またはアダプタを使用する場合を除いて、BizTalk メッセージの指定されたボディ部だけを処理します。 たとえば、マルチパート メッセージのすべての部分を読み取るようにオーケストレーションを構成できます。また、SMTP アダプタは、マルチパート メッセージのすべての部分を読み取ることができます。MIME/SMIME エンコーダ パイプライン コンポーネントを使用するようにカスタム パイプラインを構成することもできます。 オーケストレーションを使用して、マルチパート メッセージを使用する方法の詳細については、以下のセクションを参照してください**マルチパート メッセージの処理オーケストレーションで**です。  
  
 POP3 アダプターの指定された値に基づいて使用可能なボディ部から BizTalk メッセージのボディ部の選択、**ボディ部のインデックス**と**ボディ パーツのコンテンツ タイプ**です。  
  
> [!NOTE]
>  POP3 アダプターは、ボディ パーツ コンテンツの種類で定義されているを認識するように設計されています[RFC 2046](http://go.microsoft.com/fwlink/?LinkId=119569)です。  
  
 電子メールの BizTalk メッセージのボディ部を選択するために使用されるアルゴリズムを次に示します。  
  
1.  場合、**ボディ部のインデックス**0 に設定されていると、**ボディ パーツのコンテンツの種類**次のアルゴリズムの使用を BizTalk メッセージのボディ部を選択し、空白であります。  
  
    -   Content-Description ヘッダーが "body" に設定されている、最初の MIME 部分を使用します。  
  
    -   それ以外の場合は、Content-Type ヘッダーが "text/xml" に設定されている、最初の MIME 部分を使用します。  
  
    -   それ以外の場合は、Content-Type ヘッダーが "text/plain" に設定されている、最初の MIME 部分を使用します。  
  
    -   それ以外の場合は、Content-Type ヘッダーが "text/" に設定されている、最初の MIME 部分を使用します。  
  
    -   それ以外の場合は、最初の MIME 部分を使用します。  
  
2.  それ以外では、**ボディ部のインデックス**0 に設定されていると、**ボディ パーツのコンテンツの種類**セットを指定された一致する受信メッセージの最初のボディ部**ボディ パーツのコンテンツの種類**が BizTalk メッセージのボディ部として選択します。 コンテンツの種類が一致する部分がない場合、メッセージは中断されます。  
  
3.  それ以外では、**ボディ部のインデックス**0 より大きい値に設定されて、**ボディ パーツのコンテンツの種類**が空白に指定したインデックスのボディ部が BizTalk メッセージのボディ部として選択されています。 指定されたインデックスがボディ部の数より大きい場合、メッセージは中断されます。  
  
4.  それ以外では、**ボディ部のインデックス**0 より大きい値に設定されて、**ボディ パーツのコンテンツ タイプ**が設定されている、**ボディ部のインデックス**のみに適用に本文はパーツを指定された一致**ボディ パーツのコンテンツの種類**対応するボディ部が BizTalk メッセージのボディ部として選択されているとします。 指定されたインデックスが、コンテンツの種類が一致する部分の数より大きい場合、メッセージは中断されます。 コンテンツの種類が一致する部分がない場合、メッセージは中断されます。  
  
5.  BizTalk メッセージのボディ部として選択された部分が、メッセージ ボックスに公開されるマルチパート BizTalk メッセージの最初の部分になり、メッセージの残りの部分は、元の MIME エンコード メッセージ内での順序のまま維持されます。  
  
## <a name="processing-multi-part-messages-in-orchestrations"></a>オーケストレーションでのマルチパート メッセージの処理  
 POP3 アダプタが受信した MIME エンコード メッセージからマルチパート BizTalk メッセージを作成するときは、1 つの部分だけが BizTalk メッセージのボディ部として指定されていても、すべての部分がメッセージ ボックス データベースに公開されます。 その後、マルチパート メッセージをサブスクライブするオーケストレーションで、これらの部分を処理できます。 ここでは、オーケストレーションでマルチパート メッセージを処理する際の考慮事項について説明します。  
  
### <a name="processing-multi-part-messages-with-a-known-number-of-parts-and-known-part-types"></a>部分の数と部分の種類が設定されているマルチパート メッセージの処理  
 オーケストレーションで部分の数と部分の種類が設定されているマルチパート メッセージを受信する場合は、オーケストレーション内でマルチパート メッセージを宣言し、部分の数と部分の種類をデザイン時に設定できます。  
  
### <a name="processing-multi-part-messages-with-unknown-part-types"></a>部分の種類が不明なマルチパート メッセージの処理  
 かどうかは、オーケストレーションが不明な部分の種類とマルチパート メッセージを受信し、使用してオーケストレーションでマルチパート メッセージを宣言することができます、 **XmlDocument**対象の型が不明な要素別の型。  
  
### <a name="processing-multi-part-messages-with-an-unknown-number-of-parts-and-all-of-the-part-types-are-unknown"></a>部分の数とすべての部分の種類が不明なマルチパート メッセージの処理  
 かどうか、オーケストレーションがパーツ数が不明なマルチパート メッセージを受信し、1 つの部分でマルチパート メッセージを宣言することができます、 **XmlDocument**メッセージを受信するオーケストレーションの種類。 宣言された部分の数よりも大きい値を含むマルチパート メッセージを受信する場合、オーケストレーション エンジン読み取りの数の部分がありますが、メッセージに作成で宣言されたメッセージ部分の数に一致する部分の適切な部分の種類型と、コンストラクト**XmlDocument**残りの部分の部分です。