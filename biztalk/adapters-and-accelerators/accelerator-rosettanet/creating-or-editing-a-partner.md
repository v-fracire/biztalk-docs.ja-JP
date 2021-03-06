---
title: 作成または編集するパートナー |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- creating, trading partners
- trading partners
- modifying, trading partners
- trading partners, creating
- trading partners, modifying
- trading partners, about trading partners
ms.assetid: 63809035-65a5-472d-b2e5-359c8e9d9d8c
caps.latest.revision: 4
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b6e5f8c666de367860ad4243be444cecac6fa8bf
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37012667"
---
# <a name="creating-or-editing-a-partner"></a>作成または編集するパートナー
ここでは、パートナーの作成方法または編集方法について説明します。 パートナー構成では、パートナーの説明と分類、発信元の否認不可期間の設定、パートナーに対する証明書の構成、および連絡先情報の提供を行います。  

 Microsoft、パートナーを作成する場合[!INCLUDE[BTARN_CurrentVersion_FirstRef](../../includes/btarn-currentversion-firstref-md.md)]そのパートナーには、非同期のいずれかで使用される 2 つの送信ポートを作成および同期します。 これらの送信ポートの名前は\<*パートナー名*\>します。非同期の送信ポートと\<*パートナー名*\>します。同期送信ポートです。 [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] 参加させ、開始を自動的にこれらの送信ポートを取引先アグリーメントに基づいています。 これらのポートは BizTalk 管理コンソールに表示できます。  

 次の表に、パートナーの設定をタブごとに整理して示します。パートナーの作成方法と編集方法については、表の後に示す手順を参照してください。  


|                            タブ                             |            設定            |                                                                                                                                                                                                                                                                                                                                                                                    使用方法                                                                                                                                                                                                                                                                                                                                                                                    |
|------------------------------------------------------------|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        **全般**                         |           **名前**            |                                                                                                                                                                                                                                                                                                                                        取引先の名前。<br /><br /> 必須フィールド。<br /><br /> 最大長: 255                                                                                                                                                                                                                                                                                                                                        |
|                        **全般**                         |            **GBI**            |                                                                                                                                                                                                                                                                                                             パートナーのグローバル ビジネス ID (GBI)。 この ID は 9 桁で、DUNS 番号に対応する必要があります。<br /><br /> 必須フィールド。                                                                                                                                                                                                                                                                                                              |
|                        **全般**                         |        **[説明]**        |                                                                                                                                                                                                                                                                                                                                                                 パートナーについての説明。                                                                                                                                                                                                                                                                                                                                                                  |
|                        **全般**                         |        **までの保持します。**         |                                                                                       日付を[!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)]MessagesFromLOB テーブルにメッセージを送信します。 [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] までには、このメッセージは配信しません、**まで保持**日付。 パートナーは、受信パートナーのメッセージ受信可能予定日に基づいて、この日付に同意する必要があります。 この設定は、パートナーがメッセージを処理できない場合 (たとえば休日など) に役立ちます。<br /><br /> 既定値は、現在の日付です。                                                                                       |
|                        **全般**                         |  **パートナーの分類**   |            取引先組織の種類。<br /><br /> **キャリア**(既定)、**ディストリビューター**、**エンドユーザー**、**政府機関**、 **Financier**、**製造元**、**小売業者**、または**買い物客**します。<br /><br /> このフィールドの値は、[!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] の Service Header に含まれます。<br /><br /> アグリーメントの [カスタム プロパティ] タブで PPCC カスタム プロパティを入力すると、メッセージの Service Header に含まれるパートナーの分類に別の値を入力し、このプロパティをオーバーライドすることができます。 詳細については、次を参照してください。[を作成または編集するアグリーメント](../../adapters-and-accelerators/accelerator-rosettanet/creating-or-editing-an-agreement.md)します。            |
|                        **全般**                         | **配信元の否認** | 日数[!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)](受信したことを法的に証明) する否認の MessageStorageIn または MessageStorageOut データベースにメッセージのワイヤ形式を保持します。 [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] 各受信または送信メッセージにこの日付がスタンプされます。<br /><br /> 既定値は、2485 の日です。<br /><br /> ただし、[!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)]この期間が切れると、データベースから、メッセージは削除されません。 これらのメッセージを削除するには、この日時スタンプに基づいて古いメッセージを削除する SQL スクリプトを作成します。 |
| **全般**<br /><br /> (**公開キー証明書**領域) |         **署名**         |                                                                                                                                                     着信メッセージに記されたパートナーの署名を確認するために [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] が使用する公開キー証明書。 この証明書は、[!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] 管理コンソールの証明書 (ローカル コンピュータ) ノードにある [ほかの人] 証明書ストアに格納する必要があります。<br /><br /> 既定値は\<none\>します。                                                                                                                                                     |
| **全般**<br /><br /> (**公開キー証明書**領域) |        **暗号化**         |                                                                                                                                                       パートナーへの送信メッセージの暗号化に [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] が使用する公開キー暗号化証明書。 この証明書は、[!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] 管理コンソールの証明書 (ローカル コンピュータ) ノードにある [ほかの人] 証明書ストアに格納する必要があります。<br /><br /> 既定値は\<none\>します。                                                                                                                                                       |
|                   **連絡先のプロパティ**                   |       **連絡先の名前**        |                                                                                                                                                                                                                                                                                                                                                     パートナーでの連絡先の名前。<br /><br /> 必須フィールド。                                                                                                                                                                                                                                                                                                                                                     |
|                   **連絡先のプロパティ**                   |      **[電子メール アドレス]**       |                                                                                                                                                                                                                                                                                                                                                パートナーでの連絡先の電子メール アドレス。<br /><br /> 必須フィールド。                                                                                                                                                                                                                                                                                                                                                |
|                   **連絡先のプロパティ**                   |     **電話番号**      |                                                                                                                                                                                                                                                                                                                                              パートナーでの連絡先の電話番号。<br /><br /> 必須フィールド。                                                                                                                                                                                                                                                                                                                                               |
|                   **連絡先のプロパティ**                   |        **Fax 番号**         |                                                                                                                                                                                                                                                                                                                                                 パートナーでの連絡先の FAX 番号。<br /><br /> 必須フィールド。                                                                                                                                                                                                                                                                                                                                                  |
|                   **連絡先のプロパティ**                   |     **サプライ チェーン コード**     |                                                                                                                                                                                                                                                                                                                    パートナーのサプライ チェーン コード。 たとえば、"情報技術" または "電子部品" など。<br /><br /> 必須フィールド。                                                                                                                                                                                                                                                                                                                     |

### <a name="to-create-a-partner"></a>パートナーを作成するには  

1. をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**Microsoft**[!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]、順にクリックします[!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]**管理コンソール**.  

2. BTARN 管理コンソールで、[[!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]] を展開します。  

3. 右クリック**パートナー**、 をポイント**新規**、 をクリックし、**パートナー**します。  

4. **新しいパートナーのプロパティ**] ダイアログ ボックスの [、**全般**と**連絡先のプロパティ**タブで、設定値を入力します。 これらの設定の詳細については、上の表を参照してください。  

5. **[OK]** をクリックします。  

### <a name="to-edit-a-partner"></a>パートナーを編集するには  

1. をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**Microsoft**[!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]、順にクリックします[!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]**管理コンソール**.  

2. BTARN 管理コンソールで、[展開[!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]、] をクリックし、**パートナー**します。  

3. 編集するをクリックするパートナーを右クリックして**プロパティ**します。  

4. **\<**<em>パートナー</em> **\>** プロパティ ダイアログ ボックスで、**全般**と**連絡先のプロパティ**タブは必要に応じて設定を変更します。 これらの設定の詳細については、上の表を参照してください。  

5. **[OK]** をクリックします。  

## <a name="see-also"></a>参照  
 [構成、証明書、データベース、およびセキュリティを管理します。](manage-configuration-certificates-databases-security.md)   
 [BTARN 構成の管理](../../adapters-and-accelerators/accelerator-rosettanet/administering-the-btarn-configuration.md)