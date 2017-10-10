---
title: "Wcf-custom 受信ハンドラーを構成する方法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0208a7aa-6e42-43b7-a934-27ef4409b4ec
caps.latest.revision: "4"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 130e4fbffd9069c8326d0197216791cf2ace3785
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-configure-a-wcf-custom-receive-handler"></a>WCF-Custom 受信ハンドラーを構成する方法
[!INCLUDE[wcfadapter_short](../includes/wcfadapter-short-md.md)] で、machine.config 以外の場所からカスタム動作拡張機能を検索する場合は、受信ハンドラーのプロパティを構成する必要があります。  
  
## <a name="why-should-wcf-custom-adapter-lookup-custom-behavior-extensions-from-locations-other-than-machineconfig"></a>なぜ machine.config 以外の場所から WCF カスタム アダプター ルックアップ カスタム動作拡張機能しますか。  
 によって使用されるカスタム動作拡張機能[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]machine.config に登録されます。[!INCLUDE[wcfadapter_short](../includes/wcfadapter-short-md.md)] は、動作拡張機能を読み込む前に、machine.config で動作拡張機能を検索します。ただし、machine.config は、理想的には、特定のコンピューターで実行されているすべてのアプリケーションに必要な構成情報を格納する使用されます。 一方、WCF カスタム動作拡張機能はコンピューターで実行されているすべてのアプリケーションではなく、[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] でのみ要求されることがあります。 したがって、machine.config にカスタム動作拡張機能を保存すれば目的にかないますが、ここは最適な場所ではありません。  
  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] では、[!INCLUDE[wcfadapter_short](../includes/wcfadapter-short-md.md)] がカスタム動作拡張機能を参照するための追加の場所をアダプター ハンドラーのプロパティで指定します。 machine.config で既に利用可能な動作拡張機能を置き換えるものではないことに注意してください。  
  
### <a name="additional-considerations"></a>その他の注意点  
 WCF-Custom 受信ハンドラーのプロパティを構成する際は、次の点を考慮してください。  
  
-   カスタム動作拡張機能は machine.config かアダプター ハンドラーのプロパティのどちらか一方で利用可能にする必要があります。 カスタム動作拡張機能を両方の場所に重複して設定しないでください。  
  
-   カスタム動作拡張機能が既に machine.config で利用できる場合、同じカスタム動作拡張機能をアダプター ハンドラーのプロパティに設定しようとすると、すぐにエラーが発生します。  
  
-   カスタム動作拡張機能が既にアダプター ハンドラーのプロパティに設定されている場合、machine.config を同じカスタム動作拡張機能で更新すると、実行時エラーが発生し、イベント ログにも記録されます。 受信場所も無効になります。  
  
-   アダプター ハンドラーのプロパティを設定する前に、カスタム動作拡張機能で参照されるアセンブリがグローバル アセンブリ キャッシュ (GAC) に存在する必要があります。  
  
## <a name="configuring-the-adapter-handler-properties"></a>アダプター ハンドラーのプロパティの構成  
 WCF-Custom 受信ハンドラーを構成するには、このトピックの手順を実行します。  
  
#### <a name="to-configure-the-adapter-handler-properties"></a>アダプター ハンドラーのプロパティを構成するには  
  
1.  BizTalk 管理コンソールで  [!INCLUDE[btsBizTalkServer2006r3ui](../includes/btsbiztalkserver2006r3ui-md.md)]**管理**、展開**BizTalk グループ**、展開**プラットフォームの設定**の順に展開および**アダプター**です。  
  
2.  展開したアダプターの一覧でクリックして**Wcf-custom**、右側のペインで、構成する受信ハンドラを右クリックしをクリック**プロパティ**です。  
  
3.  **アダプター ハンドラーのプロパティ** ダイアログ ボックスで、**全般** タブの 、**ホスト名**一覧で、受信ハンドラーが関連付けられているホストを選択し、をクリックして**プロパティ**です。  
  
4.  **Wcf-custom トランスポートのプロパティ** ダイアログ ボックスで、 **WCF 拡張機能** タブで、次の操作します。  
  
    |プロパティ|目的|  
    |--------------|----------------|  
    |**[インポート]**|WCF カスタム動作拡張機能が登録されている WCF 構成ファイルをインポートします。 このボタンをクリックすると開きます、 **WCF 構成のインポート** ダイアログ ボックスを参照して、WCF 構成ファイルを検索します。 有効な WCF 構成ファイルを選択する必要があります。 WCF 構成スキーマの詳細についてを参照してください「Windows Communication Foundation 構成スキーマ」 [http://go.microsoft.com/fwlink/?LinkId=163953](http://go.microsoft.com/fwlink/?LinkId=163953)です。|  
    |**[エクスポート]**|WCF カスタム動作拡張機能を WCF 構成ファイルにエクスポートします。 このボタンをクリックすると開きます、 **WCF 構成のエクスポート** ダイアログ ボックスを参照して、WCF 構成ファイルを保存します。|  
    |**Clear**|既存の WCF カスタム動作拡張機能をアダプター ハンドラーのプロパティから消去します。|  
  
## <a name="see-also"></a>参照  
 [WCF カスタム アダプターを構成します。](../core/configuring-the-wcf-custom-adapter.md)