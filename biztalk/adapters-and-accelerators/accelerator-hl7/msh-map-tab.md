---
title: "MSH マップ タブ |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: btahl7.configurationexplorer.tab.mshmap
helpviewer_keywords:
- MSH Map tab [Configuration Explorer]
- messages, message headers
ms.assetid: 2c9d81bd-1abc-463d-87d7-0bea77182432
caps.latest.revision: "3"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8d667c26abb66a5e5be007503e759820ad8f1040
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="msh-map-tab"></a>MSH マップ タブ
使用する、 **MSH マップ**受信メッセージのメッセージ ヘッダーの変換を有効にする タブ。  
  
 **BTAHL7 構成エクスプ ローラー**  ダイアログ ボックスで、 **MSH マップ** タブで、次の操作します。  
  
|プロパティ|目的|  
|--------------|----------------|  
|**MSH.3**|メッセージの種類のフィールドは、このメッセージ ヘッダーの上書きします。 **注:**を null には、既存の値を変更するには、入力 **\\**です。|  
|**MSH.4**|メッセージの種類のフィールドは、このメッセージ ヘッダーの上書きします。 **注:**を null には、既存の値を変更するには、入力 **\\**です。|  
|**MSH.5**|メッセージの種類のフィールドは、このメッセージ ヘッダーの上書きします。 **注:**を null には、既存の値を変更するには、入力 **\\**です。|  
|**MSH.6**|メッセージの種類のフィールドは、このメッセージ ヘッダーの上書きします。 **注:**を null には、既存の値を変更するには、入力 **\\**です。|  
|**MSH.8**|メッセージの種類のフィールドは、このメッセージ ヘッダーの上書きします。 **注:**を null には、既存の値を変更するには、入力 **\\**です。|  
|**MSH.9**|メッセージの種類のフィールドは、このメッセージ ヘッダーの上書きします。 **注:**を null に既存の値をオーバーライドするには、次のように入力します。  **\\**です。|  
|**MSH.12**|メッセージの種類のフィールドは、このメッセージ ヘッダーの上書きします。 **注:**を null に既存の値をオーバーライドするには、次のように入力します。  **\\**です。|  
|**MSH.15**|Accept 受信確認の種類の受信確認オーバーライドの次のオプションから選択します。<br /><br /> -   **AL**です。 常に送信する場合、このオプションを選択して受信確認をそのまま使用します。<br />-   **NE**です。 送信しない場合は、このオプションを選択受信確認をそのまま使用します。<br />-   **SU**です。 送信する場合は、このオプションを選択して、メッセージの転送が成功した後に受信確認をそのまま使用します。<br />-   **ER**です。 送信する場合は、このオプションを選択して、エラーが発生した場合のみ肯定応答をそのまま使用します。|  
|**MSH.16**|アプリケーションの受信確認の種類の受信確認オーバーライドの次のオプションから選択します。<br /><br /> -   **AL**です。 常にアプリケーションの受信確認を送信する場合は、このオプションを選択します。<br />-   **NE**です。 アプリケーションの受信確認を送信しない場合は、このオプションを選択します。<br />-   **SU**です。 メッセージの転送が成功した後にアプリケーションの受信確認を送信する場合は、このオプションを選択します。<br />-   **ER**です。 エラーが発生した場合のみアプリケーションの受信確認を送信する場合は、このオプションを選択します。|