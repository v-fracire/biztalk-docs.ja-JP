---
title: "Update2XMLSchema ツール |Microsoft ドキュメント"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- 2.XML schemas, Update2XMLSchema tool
- schemas, Update2XMLSchema tool
- Update2XMLSchema tool
- Update2XMLSchema tool, syntax
ms.assetid: fd861e2f-ebda-427f-bd52-a2f05b7e22da
caps.latest.revision: "8"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e673e55557af87e5f28005a50c2a01aedf09d2c9
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="update2xmlschema-tool"></a>Update2XMLSchema ツール
Update2XMLSchema ツールでは、HL7 2. XML スキーマを BizTalk エディターでの動作を変更することができます。 これは、特定 HL7 2. XML スキーマが正しく動作しないため[!INCLUDE[btsCoName](../../includes/btsconame-md.md)][!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]変更なし。 スキーマを変更した後、ツールにより、Schemas フォルダーで、[!INCLUDE[btaBTAHL71.3abbrevnonumber](../../includes/btabtahl71-3abbrevnonumber-md.md)]がインストールされている、たとえば、 *\<ドライブ >*: \Program Files\Microsoft BizTalk\<バージョン > Accelerator forHL7\Templates\Schemas です。  
  
 Update2XMLSchema ツールを実行してから作成されるスキーマの一部のフィールドに手動で更新する必要があります。 参照してください[手動更新のために必要な](../../adapters-and-accelerators/accelerator-hl7/required-manual-updates.md)これらのスキーマの一覧についてはします。  
  
## <a name="syntax"></a>構文  
 このツールにあります*\<ドライブ >*: \Program Files\Microsoft BizTalk\<バージョン > Accelerator for HL7\SDK\2XML ユーティリティです。 このツールを実行するには、次のコマンドをコマンド プロンプトで。  
  
```  
Update2XMLSchema /s /v  
```  
  
 次の表には、このコマンドで使用するパラメーターが一覧表示します。  
  
|パラメーター|名前|値|  
|---------------|----------|-----------|  
|*S*|ソース|元の HL7 スキーマの完全なパス|  
|*V*|バージョン|2. XML スキーマのバージョン: 2.3.1、2.4 または 2.5 のいずれか|  
  
## <a name="example"></a>例  
  
-   C:\231XML\v231\xsd ディレクトリにある version 2.3.1 2. XML スキーマを変更する場合は、コマンド プロンプトで次のコマンドを入力しました。  
  
```  
Update2XMLSchema /s c:\231XML\v231\xsd /v 2.3.1  
```  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [必須の手動更新](../../adapters-and-accelerators/accelerator-hl7/required-manual-updates.md)