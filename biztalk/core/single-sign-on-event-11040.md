---
title: 'シングル サインオン: イベント 11040 |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e6ccdc06-9677-4454-ae2c-8dde78d6f3f8
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: eefc6c65e07b430851606ce7779aad3771776a83
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37019072"
---
# <a name="single-sign-on-event-11040"></a>シングル サインオン: イベント 11040
## <a name="details"></a>詳細  
  
|                 |                                                                                                                                                             |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  製品名   |                                                                  エンタープライズ シングル サインオン                                                                  |
| 製品バージョン |                                                 [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                  |
|    イベント ID     |                                                                            11040                                                                            |
|  イベント ソース   |                                                                           ENTSSO                                                                            |
|    コンポーネント    |                                                                             なし                                                                             |
|  シンボル名  |                                                                  SSO_WARN_NETWORK_SERVICE                                                                   |
|  メッセージ テキスト   | SSO サービスは Network Service アカウントで実行されています。 このアカウントについては、特別な考慮事項があります。 詳細については、マニュアルを参照してください。%r |
  
## <a name="explanation"></a>説明  
 SSO サービスは Network Service アカウントで実行されています。 このアカウントについては、特別な考慮事項があります。 たとえば、ネットワーク サービス アカウントを追加した後は、再起動が必要です。 また、ネットワーク サービス アカウントで実行すると、非常に限定されたシナリオに実行が制限されます。  
  
## <a name="user-action"></a>ユーザーの操作  
 詳細については、次を参照してください。 [SSO のセキュリティに関する推奨事項](../core/sso-security-recommendations.md)します。