---
title: アプリケーションのバインドの更新 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fe4ee4d8-67bf-4137-94e2-8274107c8ed6
caps.latest.revision: 2
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 0add0638196e992f74ab53ebda7c429c97ca3aab
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36996563"
---
# <a name="updating-the-bindings-in-an-application"></a>アプリケーションのバインドを更新しています
アプリケーションのアセンブリを更新すると、多くの場合、そのバインドが上書きされます。また、アセンブリがまったくバインドされず、バインドの再構成を手動で行う必要が生じることもあります。 これを回避するには、バインド ファイルを使用してアセンブリの同じバージョンを更新または新しいバージョンでアセンブリを更新することができます。  
  
## <a name="updating-the-same-version-of-an-assembly"></a>アセンブリの同じバージョンを更新します。  
 アセンブリに事前バインドされたポートまたは動的ポートがあり、ポート構成を BizTalk Server 管理コンソールで変更した場合、このアセンブリを同じバージョン番号のアセンブリで更新すると、設定は失われます。 更新しようとするアセンブリのバインド ファイルをエクスポートすることができます。 アセンブリを更新した後、アプリケーションにアセンブリをインポートし、以前のバインドを再適用するには、そのバインド ファイルをインポートできます。  
  
## <a name="updating-an-assembly-with-a-newer-version"></a>新しいバージョンでアセンブリを更新しています  
 アセンブリのバージョンを更新するには、バインディングのバインド ファイルに 1 つのアセンブリに関連付けられている、新しいアセンブリのバージョンを反映するように、バインド ファイルを編集し、アプリケーションにアセンブリのバインドをインポートおよびエクスポートします。 バインド ファイルの編集の詳細については、次を参照してください。[バインド ファイルのカスタマイズ](http://go.microsoft.com/fwlink/?LinkID=155000)(HYPERLINK"<http://go.microsoft.com/fwlink/?LinkID=155000>" <http://go.microsoft.com/fwlink/?LinkID=155000>) で[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]ヘルプ。