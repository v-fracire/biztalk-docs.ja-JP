---
title: 'シングル サインオン: イベント 10705 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81456bdd-dfd8-4483-aa76-5ec72350cc70
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c74e4ebe0119698348668eb2ca6f78b5697cc5d0
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36976899"
---
# <a name="single-sign-on-event-10705"></a>シングル サインオン: イベント 10705
## <a name="details"></a>詳細  

|                 |                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------|
|  製品名   |                                         エンタープライズ シングル サインオン                                          |
| 製品バージョン |                         [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                         |
|    イベント ID     |                                                   10705                                                    |
|  イベント ソース   |                                                   ENTSSO                                                   |
|    コンポーネント    |                                                    N\A                                                     |
|  シンボル名  |                                          SSO_WARN_PS_NOT_ADAPTER                                           |
|  メッセージ テキスト   | 指定されたアダプターはアダプター アプリケーションではありません。 アプリケーションの種類を確認してください。%r<br /><br /> アダプタ: %1 |

## <a name="explanation"></a>説明  
 この警告イベントは、指定されたアダプターがアダプター アプリケーションではないことを示します。  

## <a name="user-action"></a>ユーザーの操作  
 この警告を解決するには、次の操作を行います:   

- SSO 管理 MMC スナップインを使用して、指定したアダプターを右クリックし、[プロパティ] をクリックしてアプリケーションの種類を特定するか、コマンド ライン ツール ssops -list および ssops -display を使用してアプリケーションの種類を特定します。  

- SSO 管理 MMC スナップインまたは ssops -addapp を使用して、アダプター アプリケーションを設定します。  

  詳細については、次のリソースを参照してください。  

- [パスワード同期を管理する方法](../core/how-to-administer-password-synchronization.md)
