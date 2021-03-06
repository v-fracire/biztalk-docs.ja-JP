---
title: Message Repair and Submission サービスの新しい処理 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- repairing messages, MrsrRepair orchestration
- orchestrations, MrsrRepair orchestration
- InfoPath forms, valid forms
- messages, BAS
- unparsed messages
- repairing messages, unparsed messages
- messages, unparsed messages
- messages, InfoPath forms
- Business Rule Engine
- MrsrRepair orchestration
- InfoPath forms, messages
- BAS, messages
ms.assetid: fe2ee009-bf63-4bc0-b231-ad8a2633719f
caps.latest.revision: 4
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8edec4b1c852a542068b1b5df6a8b58de390907f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37004435"
---
# <a name="message-repair-and-new-submission-service-processing"></a>Message Repair and Submission サービスの新しい処理
MrsrRepair オーケストレーションで、次の処理を含め、すべて Message Repair and New Submission 操作を処理します。  

-   修復を必要とするメッセージ  

-   未解析メッセージ  

-   MRSR サイトに作成された新しいメッセージ  

## <a name="processing-messages-requiring-repair"></a>修復を必要とするメッセージの処理  
 メッセージを修復する必要がある場合、逆アセンブラーからの受信メッセージが送信されたことのオーケストレーションに通知されました。 作成または修復するロール機能が設定されている場合のみ、逆アセンブラーからのメッセージを処理します。 MrsrRepair オーケストレーションは、次のプロパティを持つメッセージ ボックスからメッセージをサブスクライブします。  

```  
A4SWIFT_Failed==true AND  
BTS_Operation=="A4SWIFT_DasmMarkedAsFailed" AND  
A4SWIFT_SwiftBound==true  
```  

 Message Repair and New Submission を使用するオーケストレーションが、Sts.Outbox.Location にバインドされている MrsrRepair の受信ポートは受信場所です。 [!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]既定のこの受信場所によって、セットアップ プログラムがインストールされます。 ユーザー MRSR サイトにメッセージを送信、この受信場所は、メッセージを取得し、MrsrRepair オーケストレーションにルーティングします。  

 次の表は、有効な一覧[!INCLUDE[btsInpathNoVersion](../../includes/btsinpathnoversion-md.md)]フォーム。  


| [!INCLUDE[btsInpathNoVersion](../../includes/btsinpathnoversion-md.md)] フォーム |       |       |              |              |       |
|-------------------------------------------------------------------------------|-------|-------|--------------|--------------|-------|
|                                     MT010                                     | MT011 | MT012 |    MT015     |    MT019     | MT020 |
|                                     MT021                                     | MT022 | MT023 |    MT028     |    MT029     | MT030 |
|                                     MT031                                     | MT032 | MT035 |    MT036     |    MT037     | MT039 |
|                                     MT041                                     | MT042 | MT043 |    MT044     |    MT045     | MT046 |
|                                     MT047                                     | MT048 | MT049 |    MT050     |    MT051     | MT052 |
|                                     MT055                                     | MT056 | MT057 |    MT059     |    MT061     | MT062 |
|                                     MT063                                     | MT064 | MT065 |    MT066     |    MT067     | MT068 |
|                                     MT069                                     | MT072 | MT073 |    MT074     |    MT075     | MT076 |
|                                     MT077                                     | MT081 | MT082 |    MT083     |    MT085     | MT087 |
|                                     MT090                                     | MT092 | MT094 |    MT102     |  MT102PLUS   | MT103 |
|                                   MT103Plus                                   | MT104 | MT105 |    MT106     |    MT107     | MT110 |
|                                     MT111                                     | MT112 | MT121 |    MT190     |    MT191     | MT192 |
|                                     MT195                                     | MT196 | MT198 |    MT199     |    MT200     | MT201 |
|                                     MT202                                     | MT203 | MT204 |    MT205     |    MT206     | MT207 |
|                                     MT210                                     | MT256 | MT290 |    MT291     |    MT292     | MT295 |
|                                     MT296                                     | MT298 | MT299 |    MT300     |    MT303     | MT304 |
|                                     MT305                                     | MT306 | MT307 |    MT308     |    MT320     | MT321 |
|                                     MT330                                     | MT340 | MT341 |    MT350     |    MT360     | MT361 |
|                                     MT362                                     | MT364 | MT365 |    MT380     |    MT381     | MT390 |
|                                     MT391                                     | MT392 | MT395 |    MT396     |    MT398     | MT399 |
|                                     MT400                                     | MT405 | MT410 |    MT412     |    MT416     | MT420 |
|                                     MT422                                     | MT430 | MT450 |    MT4555    |    MT456     | MT490 |
|                                     MT491                                     | MT492 | MT495 |    MT496     |    MT498     | MT499 |
|                                     MT500                                     | MT501 | MT502 |    MT503     |    MT504     | MT505 |
|                                     MT506                                     | MT507 | MT508 |    MT509     |    MT510     | MT513 |
|                                     MT514                                     | MT515 | MT516 |    MT517     |    MT518     | MT519 |
|                                     MT524                                     | MT526 | MT527 |    MT528     |    MT529     | MT535 |
|                                     MT536                                     | MT537 | MT538 |    MT540     |    MT541     | MT542 |
|                                     MT543                                     | MT544 | MT545 |    MT546     |    MT547     | MT548 |
|                                     MT549                                     | MT558 | MT559 |    MT564     |    MT565     | MT566 |
|                                     MT567                                     | MT568 | MT569 | MT574_IRSLST | MT574_W8BENO | MT575 |
|                                     MT576                                     | MT577 | MT578 |    MT579     |    MT581     | MT582 |
|                                     MT584                                     | MT586 | MT587 |    MT588     |    MT589     | MT590 |
|                                     MT591                                     | MT592 | MT595 |    MT596     |    MT598     | MT599 |
|                                     MT600                                     | MT601 | MT604 |    MT605     |    MT606     | MT607 |
|                                     MT643                                     | MT644 | MT645 |    MT646     |    MT649     | MT690 |
|                                     MT691                                     | MT692 | MT695 |    MT696     |    MT698     | MT699 |
|                                     MT700                                     | MT701 | MT705 |    MT707     |    MT710     | MT711 |
|                                     MT720                                     | MT721 | MT730 |    MT732     |    MT734     | MT740 |
|                                     MT742                                     | MT747 | MT750 |    MT752     |    MT754     | MT756 |
|                                     MT760                                     | MT767 | MT768 |    MT769     |    MT790     | MT791 |
|                                     MT792                                     | MT795 | MT796 |    MT798     |    MT799     |       |
|                                     MT800                                     | MT801 | MT802 |    MT810     |    MT812     | MT813 |
|                                     MT820                                     | MT821 | MT822 |    MT823     |    MT824     | MT890 |
|                                     MT891                                     | MT892 | MT895 |    MT896     |    MT898     | MT899 |
|                                     MT900                                     | MT910 | MT920 |    MT935     |    MT940     | MT941 |
|                                     MT942                                     | MT950 | MT960 |    MT961     |    MT962     | MT963 |
|                                     MT964                                     | MT965 | MT966 |    MT967     |    MT970     | MT971 |
|                                     MT972                                     | MT973 | MT985 |    Mt986     |    MT990     | MT991 |
|                                     MT992                                     | MT995 | MT996 |    MT998     |    MT999     |       |

## <a name="processing-unparsed-messages"></a>未解析メッセージの処理  
 MrsrRepair オーケストレーション メッセージを解析できませんでした、MRSR に、メッセージを送信し、適切なフラグを設定すると判断した場合は、受信トレイをサイトで修復のため、[!INCLUDE[btsInpathNoVersion](../../includes/btsinpathnoversion-md.md)]未解析メッセージの形式。 オーケストレーションは、修復が完了したら、メッセージを受信したときに、BTS を設定します。操作のプロパティを"[!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]_MRSRCompleted"および[!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]_Failed プロパティを False にし、メッセージ ボックスに、メッセージをルーティングします。 これらのプロパティは、未解析メッセージはメッセージの修復処理をもう一度入力していないことを確認します。  

 未解析の修復のフォームと呼ばれる**未解析メッセージ**します。  

## <a name="processing-new-messages-created-in-mrsr"></a>MRSR に作成された新しいメッセージの処理  
 MrsrRepair オーケストレーションで受信メッセージは、MRSR サイトで作成されている場合、オーケストレーションにから受信メッセージが送信されたことに警告[!INCLUDE[btsInpathNoVersion](../../includes/btsinpathnoversion-md.md)](逆アセンブラーではありません)、およびメッセージが署名されています。  

## <a name="common-operations"></a>一般的な操作  
 修復が必要を解析できませんでした、または新しいメッセージかどうか、MrsrRepair オーケストレーションは、一連のすべてのメッセージの一般的な操作を実行します。 オーケストレーションは、キーを再入力検証など、ワークフローの各ステップの一般的な操作を実行するループを実行、作成、修復、および承認します。 このオーケストレーションは、部門とロールとは関係なく使用されます。  

 一般的な手順を以下に示します。  

1. エンベロープ形式でメッセージを配置します。  

2. MRSR サイトにメッセージを送信します。  

3. (ユーザーの操作) の後、Sts.Outbox.Location を通じて MRSR サイトからメッセージを受信場所を受信します。 タイムアウトが発生する場合、オーケストレーションは、タイムアウトを処理します。ユーザーの修復、検証、または、メッセージの承認中にタイムアウトが発生した場合[!INCLUDE[btaA4SWIFT2.3abbrevnonumber](../../includes/btaa4swift2-3abbrevnonumber-md.md)]修復段階にワークフローをリセットする修復の受信トレイにメッセージを返します。  

   > [!NOTE]
   >  Message Repair and New Submission を使用するオーケストレーションが、Sts.Outbox.Location にバインドされている MrsrRepair の受信ポートは受信場所です。 これは、受信場所にインストールされている MRSR サイトを持つサーバーにバインドされている BizTalk ホストで実行する必要があります。 そのホストは通常、BizTalkServerApplication ですが、別のホストであることができます。 別のホストである場合は、ホストのバインド先となるサーバーは、MRSR のサイトにインストールされているでいることを確認する必要があります。  

4. ユーザーが入力署名が、ロールの適切なことを確認し、ロールの制限を確認するには、その署名を格納します。  

5. 場合は、メッセージの内容が格納された、前の手順では、格納されたメッセージを使用した MRSR サイトから受信したコンテンツを比較します。 オーケストレーションでは、一致するものがない場合、メッセージが失敗します。  

6. メッセージは、ユーザーには、変更が拒否された場合に失敗します。  

7. ユーザーには、変更が受け入れられた場合は、メッセージの XSD および BRE の検証を実行します。  

8. 該当する場合は、次の手順に移動します。  

## <a name="customizing-the-repair-orchestration"></a>修復オーケストレーションをカスタマイズします。  
 MrsrRepair オーケストレーションをカスタマイズするには、前処理または後処理機能を追加します。 たとえば、前処理の手順にオーケストレーションを追加したり、プロパティを昇格させる既存の送信図形の前にオーケストレーション図形を追加します。 ただし、作成または MrsrRepair オーケストレーションはそれらを認識できないために、契約または Message Repair and New Submission に関連付けられているプロファイルを変更できません。 修理会社、作成者、検証、または承認者を超える新しいロールの定義を追加することはできません。 構造体を変更またはオーケストレーションの基本機能を追加できません。  

## <a name="business-rules-policies"></a>ビジネス ルール ポリシー  
 修復プロセスは、修復オーケストレーションが BizTalk ビジネス ルール エンジン (BRE) マスター MT103_Master_Policy.xml など、メッセージの種類のポリシーを読み込むを呼び出します。 オーケストレーションでは、メッセージの種類と本文に、BRE が渡されます。 メッセージのマスター ポリシーには、そのメッセージの種類に関連するその他のすべてのポリシーの一覧が含まれています。 BRE では、メッセージの種類のすべてのポリシーを読み込みます。 これらのポリシーには、SWIFT_Reference_Policy、SWIFT_PartyIdentifier_Policy、ネットワーク ルール ポリシー、およびメッセージの種類に固有の検証ポリシーが含まれます。 BRE では、すべてのエラーに関係なく、マスター ポリシーの一覧にポリシーを実行し、すべてのエラーを返します。