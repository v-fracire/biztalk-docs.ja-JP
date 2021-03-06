---
title: 新しい Partner Interface Process の組み込み |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deploying, PIP schemas
- PIP schemas
- PIP schemas, deploying
- PIP schemas, downloading
- creating, PIP schemas
- PIP schemas, creating
ms.assetid: 6a5fcbcb-c6aa-40c0-bcca-dd0c391e7f42
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 558509c85da8de044bad1b320f3beb31c27e006b
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36969795"
---
# <a name="incorporating-a-new-partner-interface-process"></a>新しい Partner Interface Process の組み込み
新しい RosettaNet Partner インターフェイス Process (PIP) スキーマ Microsoft® を組み込むことができます[!INCLUDE[BTARN_CurrentVersion_FirstRef](../../includes/btarn-currentversion-firstref-md.md)]アセンブリ。 次の手順に従ってください。  
  
- RosettaNet の Web サイトから PIP スキーマをダウンロード[ http://go.microsoft.com/fwlink/?linkid=33859](http://go.microsoft.com/fwlink/?linkid=33859)します。  
  
- このスキーマを、[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)] RNPIP アセンブリまたは別の [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] アセンブリの一部として [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] に展開します。 詳細については、次を参照してください。[新しい PIP による BTARN の拡張](../../adapters-and-accelerators/accelerator-rosettanet/extending-btarn-with-a-new-pip.md)します。  
  
- [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] 管理コンソールで新しいプロセス構成設定を作成します。 詳細については、次を参照してください。[を作成またはプロセス構成の編集方法](../../adapters-and-accelerators/accelerator-rosettanet/how-to-create-or-edit-a-process-configuration.md)します。  
  
  ダウンロードしたスキーマは通常は .dtd 形式で、RosettaNet 組織の PIP 仕様が .doc ファイルとして添付されています。 パイプラインが新しいスキーマを使用するように拡張するプロセスで、PIP の .dtd ファイルを .xsd ファイルに変換する必要があります。  
  
  [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] をインストールするときに、[!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] SDK に複数の XSD スキーマもインストールされます。 これらのスキーマを見つけることができます、 \<*ドライブ*\>: \Program Files\Microsoft BizTalk\<バージョン\>Accelerator for rosettanet \sdk\schemas フォルダー。 BTARN がこれらのスキーマを RNPIPs.dll ファイルにビルドします。 スキーマを変更する必要がある場合は、同じフォルダーで RNPIP のプロジェクトを開き、BizTalk エディターで変更してから、アセンブリを再コンパイルして再展開します。 RNPIP の .dll ファイルを再展開したら、そのスキーマを使用するパイプラインを再展開する必要があります。 このプロセスを使用すると、新しいスキーマを BTARN に組み込むことができますが、パイプラインを拡張して新しいスキーマを含める方が簡単です。  
  
### <a name="to-obtain-the-pip-schema"></a>PIP スキーマを取得するには  
  
-   Internet Explorer で RosettaNet の Web サイトに移動します。 [ http://go.microsoft.com/fwlink/?linkid=33859](http://go.microsoft.com/fwlink/?linkid=33859)します。  
  
## <a name="see-also"></a>参照  
 [新しい PIP による BTARN の拡張](../../adapters-and-accelerators/accelerator-rosettanet/extending-btarn-with-a-new-pip.md)