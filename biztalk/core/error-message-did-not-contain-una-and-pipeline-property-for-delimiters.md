---
title: メッセージに UNA が含まれていないと、区切り記号のパイプライン プロパティが正しくない形式 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b761d820-e09d-4949-bb41-da9e66054c60
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 717626c6ba38d8e278ad173739c28d502c3d6e0d
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36967779"
---
# <a name="message-did-not-contain-una-and-pipeline-property-for-delimiters-was-incorrect-format"></a>メッセージに UNA が含まれていなかったため、区切り記号のパイプライン プロパティが正しくない形式になっています
## <a name="details"></a>詳細  
  
|                 |                                                                                             |
|-----------------|---------------------------------------------------------------------------------------------|
|  製品名   |     [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]      |
| 製品バージョン |                 [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]                  |
|    イベント ID     |                                              -                                              |
|  イベント ソース   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI    |
|    コンポーネント    |                                         EDI エンジン                                          |
|  シンボル名  |                                EfactDelimiterIncorrectFormat                                |
|  メッセージ テキスト   | メッセージに UNA が含まれていないと、区切り記号のパイプライン プロパティが正しくない形式 '{0}' |
  
## <a name="explanation"></a>説明  
 このエラー/警告/情報イベントは、インターチェンジの処理に必要な区切り記号を特定できなかったため、受信パイプラインで受信 EDIFACT インターチェンジを処理できなかったことを示します。 このイベントは、インターチェンジに UNA セグメントがなく、EfactDelimiters パイプライン プロパティで正しく区切り記号が定義されていない場合に発生する可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、次のいずれかの操作を行います。  
  
1.  インターチェンジの区切り記号を定義する UNA セグメントがインターチェンジにあることを確認し、インターチェンジを再送信します。  
  
2.  送信パイプラインの EfactDelimiters パイプライン プロパティを設定します。そのためには、BizTalk Server 管理コンソールを開き、インターチェンジの受信場所を右クリックして、[プロパティ] をクリックします。次に、パイプラインの省略記号をクリックし、区切り記号の値を含む文字列を入力します。