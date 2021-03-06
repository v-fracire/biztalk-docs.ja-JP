---
title: SWIFT ヘッダー |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SWIFT, headers
- headers [SWIFT]
ms.assetid: b599cca2-8ae6-42db-b3a2-712ba12c1017
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e516fc906d2eac0610cb576266a034c54b42cae7
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36984443"
---
# <a name="swift-headers"></a>SWIFT ヘッダー
Microsoft [!INCLUDE[A4SWIFT_CurrentVersion_FirstRef](../../includes/a4swift-currentversion-firstref-md.md)] SWIFT ヘッダーおよびトレーラのスキーマを提供します。 A4SWIFT は、これらのさまざまな財務 (FIN) メッセージのインターチェンジのスキーマに既に組み込みます。 カスタム SWIFT FIN 書式スタイル メッセージの種類 (たとえば、N98 メッセージ) を作成する場合は、独自の形式に、ヘッダーとトレーラーのスキーマを組み込むことができます。  
  
 SWIFT ヘッダー スキーマ (SWIFT Header.xsd) には、次の形式が含まれています。  
  
- 基本的なヘッダー  
  
- アプリケーション用のヘッダー (入力または出力の選択)  
  
- ユーザー ヘッダー  
  
- テキスト ブロックの先頭の区切り文字  
  
  基本的なヘッダーには、メッセージのソースに関する情報が含まれています。 アプリケーションのヘッダーには、メッセージの種類およびメッセージの転送先に関する情報が含まれています。 受信パイプラインで SWIFT 逆アセンブラーがメッセージの種類の解像度は、適切なアプリケーションのヘッダー内のフィールドの内容に基づきます。 ユーザー ヘッダーは、省略可能な特別な処理命令が含まれています。  
  
> [!NOTE]
>  いくつかのメッセージの種類には、フィールド 119 ユーザー ヘッダーの内容に基づいて変数の形式があります。 これらは、A4SWIFT で「二重メッセージ型」です。 A4SWIFT 逆アセンブラーでは、119 フィールドの内容と組み合わせてアプリケーション ヘッダー メッセージの種類を使用して、メッセージ インスタンスの適切なスキーマを選択します。  
  
 ユーザー ヘッダーはオプションですが、および FIN コピーの使用について主に表示します。 ブロック 1 サービス識別子は「01」である必要があります。 ヘッダーが存在する場合、フィールドの少なくとも 1 つが存在する必要があります。 ただし、すべてのフィールドは省略可能です。 ユーザー ヘッダー内のフィールドでは、メッセージのテキスト領域内のものと同じ規則に従います。  
  
 次の表には、すべての SWIFT ヘッダー フィールドの種類が一覧表示します。  
  
|[フィールドの型]|説明|  
|----------------|-----------------|  
|**アプリケーション識別子 (ブロック 1)**|メッセージを伝達するために使用されているアソシエーションを確立したアプリケーションを指定します。 常に使用する**F** FIN メッセージ。|  
|**ブロック (すべて) 識別子**|左中かっこ内の最初の文字。 ブロックの識別子は、コロンで後に常にします。<br /><br /> **1**基本的なヘッダーを =<br /><br /> **2**アプリケーション ヘッダーを =<br /><br /> **3**ユーザー ヘッダーを =<br /><br /> **4**メッセージ テキストを =<br /><br /> (トレーラー用の次の値を参照してください)。|  
|**配信の監視 (ブロック 2) (省略可能)**|場合は、優先順位は**U**配信を監視する必要があります。<br /><br /> **1** = 警告の配信不能<br /><br /> スイッチまたは<br /><br /> **3** = 警告の配信不能と配信通知します。<br /><br /> 場合は、優先順位は**N**配信を監視する必要があります。<br /><br /> **2**配信通知を =<br /><br /> スイッチまたは<br /><br /> 対象外の情報|  
|**送信先アドレス (ブロック 2)**|SWIFT ネットワークに送信されるメッセージの送信先の論理ターミナル (LT) の完全なアドレス。|  
|**末尾の区切り記号 (ブロックのすべて)**|右中かっこを使用する (**}**) の末尾の区切り記号。|  
|**入力/出力の識別子 (ブロック 2)**|**I** SWIFT に送信されるメッセージを = です。<br /><br /> **O** SWIFT から送信されたメッセージを = です。|  
|**入力された時刻と日付 (ブロック 2)**|時間 (HH) と 1 分 (MM) の後に、year (YY)、month (MM) と 1 日 (DD) を送信者が SWIFT にメッセージを送信します。 日付と時刻の入力は、メッセージの送信者にローカルでは常にします。|  
|**ターミナル (LT) の論理アドレス (ブロック 1)**|送信されるメッセージの送信者または SWIFT ネットワークから受信したメッセージの受信者の論理ターミナル アドレス。|  
|**メッセージの入力のリファレンス (MIR) (ブロック 2)**|送信者は、形式、year (YY)、month (MM)、および日 (DD) で記述された SWIFT へメッセージを送信する日付。 MIR は常に、メッセージの送信者にローカルであり、SWIFT するには、送信者のセッション、シーケンスである、メッセージの送信者の完全な LT アドレス。|  
|**メッセージの優先順位 (ブロック 2)**|メッセージの優先順位システム メッセージの"S"(型 000-099)。緊急またはユーザーにメッセージを"N"の"U"(型 100-999)。|  
|**メッセージの種類 (ブロック 2)**|3 桁 FIN メッセージの種類、000-999 です。|  
|**陳腐化期間 (ブロック 2: 省略可能)**|既定では、し、優先順位 N. の 20 単位 (100 分) を 3 ユニット (15 分) の優先順位の値(既定値は常に使用されます。 配信の監視が存在する場合にのみ有効です。|  
|**出力日付 (ブロック 2)**|出力日付では、ローカル、受信者には、次の形式で記述された: YYMMDD します。|  
|**出力時間 (ブロック 2)**|受信側のローカル出力時刻は、次の形式で記述された: HHMM します。|  
|**シーケンス番号 (ブロック 1)**|サービスの識別子を持つすべての FIN メッセージ**01**または**05**転送の方向に適切な次の予期されるシーケンス番号です。<br /><br /> サービスの識別子を含む FIN メッセージ**21**または**25**、確認済みのサービス メッセージのシーケンス番号です。|  
|**サービス Id (ブロック 1)**|FIN アプリケーションに適したサービス メッセージの種類を識別する 2 桁の番号。 FIN 000 ~ 999 の型のすべてのメッセージを使用して、 **01**します。 02 に 43 の種類のすべてのメッセージ、その 2 桁のサービス メッセージの種類を使用します。|  
|**セッション識別子 (ブロック 1)**|必要に応じて、アプリケーションの現在のセッション数が、ログインに基づきます。|  
|**開始区切り記号 (すべてのブロック)**|左中かっこ: **{** します。|  
  
## <a name="see-also"></a>参照  
 [スキーマの操作](../../adapters-and-accelerators/accelerator-swift/working-with-schemas.md)