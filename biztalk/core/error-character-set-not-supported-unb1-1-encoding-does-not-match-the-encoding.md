---
title: "文字セットの UNB1.1 のエンコード情報では、実際のエンコードは一致しないためにサポートされていません |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 085ea8e3-e0d8-45bd-9985-6787b00e4d5a
caps.latest.revision: "8"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 41a6eafbb0e71de5f13e792361cdc0d1fc338088
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="character-set-not-supported-because-the-encoding-information-in-unb11-does-not-match-the-actual-encoding"></a>UNB1.1 のエンコード情報が実際のエンコードと一致しないため、文字セットはサポートされません
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]|  
|製品バージョン|[!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]|  
|イベント ID|-|  
|イベント ソース|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI|  
|コンポーネント|EDI エンジン|  
|シンボル名|-|  
|メッセージ テキスト|文字セットがサポートされていません。 UNB1.1 のエンコード情報が実際のインターチェンジのエンコードと一致しないことが原因の可能性があります。|  
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、インターチェンジで使用されている文字がインターチェンジの UNB1.1 で識別されている文字セットに一致しないため、EDI 受信パイプラインで受信 EDIFACT インターチェンジを処理できなかったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、次のいずれかの操作を行います。  
  
-   インターチェンジで使用されている文字を、インターチェンジの UNB1.1 で指定されている文字セットに一致するように変更します。  
  
-   インターチェンジの UNB1.1 フィールドに指定されている文字セットを変更し、インターチェンジのすべての文字がその文字セットに属する文字になるようにします。