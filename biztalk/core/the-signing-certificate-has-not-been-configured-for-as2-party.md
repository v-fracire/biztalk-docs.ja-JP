---
title: AS2 パーティの署名証明書が構成されていません |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 82928a39-3acf-447b-a0e8-f7c25b6f38dc
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4d26323670f0229377b304e5f51671de8ef10021
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36967547"
---
# <a name="the-signing-certificate-has-not-been-configured-for-as2-party"></a>AS2 パーティに署名証明書が構成されていません
## <a name="details"></a>詳細  
  
|                 |                                                                                           |
|-----------------|-------------------------------------------------------------------------------------------|
|  製品名   |    [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]     |
| 製品バージョン |                [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]                 |
|    イベント ID     |                                             -                                             |
|  イベント ソース   |  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI   |
|    コンポーネント    |                                        AS2 エンジン                                         |
|  シンボル名  |                               SigningCertNotConfiguredError                               |
|  メッセージ テキスト   | AS2 パーティに署名証明書が構成されていません。  AS2-から: {0} AS2-に。 {1} |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、グループに署名証明書が構成されていなかったため、送信パイプラインで送信メッセージを処理できなかったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、次の操作を行って署名証明書を構成します。  
  
1.  BizTalk Server 管理コンソールを開きます。  
  
2.  [グループ] ノードに移動し、[証明書] ノードをクリックします。  
  
3.  証明書の共通名と拇印を入力します。