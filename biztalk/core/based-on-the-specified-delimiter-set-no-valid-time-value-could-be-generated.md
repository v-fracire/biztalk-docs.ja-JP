---
title: "指定された区切り記号セットに基づいて有効な時刻値を生成できませんでした |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e7e22958-e1fa-474d-85a2-aa69e05b7228
caps.latest.revision: "9"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 00b8b06922109ae5817c67b26f1a23977d1b607b
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="based-on-the-specified-delimiter-set-no-valid-time-value-could-be-generated"></a>指定された区切り記号セットに基づいて有効な時刻値を生成できませんでした
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]|  
|製品バージョン|[!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]|  
|イベント ID|-|  
|イベント ソース|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI|  
|コンポーネント|EDI エンジン|  
|シンボル名|-|  
|メッセージ テキスト|指定された区切り記号セットに基づいて有効な時刻値を生成できませんでした。 別の区切り記号セットを使用してください。|  
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、送信インターチェンジの時刻フィールドに使用されている文字が、区切り記号の文字と同じだったため、EDI 送信パイプラインで有効な時刻値を生成できなかったことを示します。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、EDI 送信パイプラインでメッセージを作成するために使用される区切り記号の値を変更し、いずれの区切り記号の文字も、時刻フィールドで使用されている文字と同じにならないようにします。 次のいずれかの操作を行います。  
  
-   解決済みのパーティに対して送信される X12 インターチェンジの場合、インターチェンジの受信者となるパーティの [ISA セグメントの定義] ページで区切り記号の設定を変更します。  
  
-   未解決のパーティに対して送信される X12 インターチェンジの場合、[ISA セグメントの定義] グローバル プロパティ ページで区切り記号の設定を変更します。  
  
-   解決済みのパーティに対して送信される EDIFACT インターチェンジの場合、インターチェンジの受信者となるパーティの [UNA セグメントの定義] ページで区切り記号の設定を変更します。  
  
-   未解決のパーティに対して送信される EDIFACT インターチェンジの場合、[UNA セグメントの定義] グローバル プロパティ ページで区切り記号の設定を変更します。