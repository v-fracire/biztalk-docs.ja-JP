---
title: エクスポート Bindings6 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bindings, exporting
- exporting, bindings
ms.assetid: 052a429e-3237-44d4-8933-00aa5edfb212
caps.latest.revision: 22
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ee3d7df759dab97dca6a2e7677abb0bad15f8cd7
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37022880"
---
# <a name="exporting-bindings"></a>バインドのエクスポート
このセクションの各トピックでは、BizTalk Server グループ、アセンブリ、またはアプリケーションのバインドを .xml ファイルにエクスポートする方法について説明します  (バインドは、ホスト、送信ポート、送信ポート グループ、受信ポート、受信場所、パーティを、オーケストレーション、パイプライン、マップ、およびスキーマと関連付ける方法を定義します)。その後、.xml ファイルから別のグループまたはアプリケーションにバインドをインポートできます。 バインドをインポートすると、グループまたはアプリケーション内の同じ名前の既存のバインドが上書きされます。 バインドをアプリケーションに追加して、既存のバインドを上書きしないようにすることもできます。 アプリケーションをインポートしない限り、追加したバインドは有効になりません。  
  
 以下のシナリオでバインド ファイルを使用すると、バインドを手動で構成する必要がないので、アプリケーションを迅速に展開できます。  
  
- ある展開環境から別の環境へアプリケーションを移動する場合  
  
- アセンブリを更新する場合  
  
- 複数の BizTalk グループへのバインドと共にアセンブリを展開する場合  
  
  これらの目的のバインド ファイルの使用に関する詳細については、次を参照してください。[バインド ファイルとアプリケーションの展開](../core/binding-files-and-application-deployment.md)します。  
  
  インポートおよびバインドの追加に関する詳細については、次を参照してください[を BizTalk グループにバインドのインポート方法](../core/how-to-import-bindings-into-a-biztalk-group.md)、 [BizTalk アプリケーションにバインドのインポート方法](../core/how-to-import-bindings-into-a-biztalk-application.md)、および[バインディングを追加する方法。ファイルをアプリケーションに](../core/how-to-add-a-binding-file-to-an-application2.md)します。  
  
> [!IMPORTANT]
>  バインド ファイルには機密データが含まれている場合があります。 適切な措置をとり、ファイルが保護されるようにしてください。  
  
> [!NOTE]
>  セキュリティ上の理由により、BizTalk Server では、バインド ファイルのエクスポート時にバインドのパスワードがファイルから削除されます。 バインドをインポートした後で、送信ポートと受信場所のパスワードを再構成する必要があります。 BizTalk Server 管理コンソールの [トランスポートのプロパティ] ダイアログ ボックスで、送信ポートと受信場所のパスワードをそれぞれ構成します。 手順については、次を参照してください。[送信ポートを作成する方法](../core/how-to-create-a-send-port2.md)します。 参照してください[を作成する方法、受信場所](../core/how-to-create-a-receive-location.md)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [BizTalk グループのバインドをエクスポートする方法](../core/how-to-export-bindings-for-a-biztalk-group.md)  
  
-   [BizTalk アプリケーションのバインドをエクスポートする方法](../core/how-to-export-bindings-for-a-biztalk-application.md)  
  
-   [BizTalk アセンブリのバインドをエクスポートする方法](../core/how-to-export-bindings-for-a-biztalk-assembly.md)  
  
-   [EDI AS2 ソリューションのバインドをエクスポートする方法](../core/how-to-export-bindings-for-an-edi-as2-solution.md)