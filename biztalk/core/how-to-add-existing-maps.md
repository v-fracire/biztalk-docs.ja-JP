---
title: 既存のマップを追加する方法 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fbeaea05-016e-488c-90f3-af8c6b9a3d84
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 415a5112c5cca457f7cbbe229ce073219de95631
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36970145"
---
# <a name="how-to-add-existing-maps"></a>既存のマップを追加する方法
既存のマップを BizTalk プロジェクトに追加できます。 この操作を行う前に、マップの送信元スキーマおよび送信先スキーマがマップを追加する BizTalk プロジェクトに含まれている (または対応する .NET アセンブリによって参照されている) ことを確認してください。  
  
### <a name="to-add-an-existing-map-to-a-biztalk-project"></a>既存のマップを BizTalk プロジェクトに追加するには  
  
1. ソリューション エクスプ ローラーで BizTalk プロジェクトを右クリックし、[**追加**、] をクリックし、**既存項目の**します。  
  
2. **既存項目の追加** ダイアログ ボックスで、追加で選択しをクリックするマップを含むフォルダーを参照し**追加**します。  
  
    マップは、BizTalk マッパーで開きます。 また、新しく追加したマップは、現在の BizTalk プロジェクトの子としてソリューション エクスプローラーに表示されます。  
  
   > [!NOTE]
   >  BizTalk プロジェクト フォルダー以外のフォルダーを参照すると、追加したマップのコピーがプロジェクト フォルダーに作成されます。マップのこのコピーがプロジェクトに追加されます。 マップに対するその後の変更は、このコピーに対して行われます。他のフォルダーの元のマップには行われません。  
   > 
   > [!IMPORTANT]
   >  BizTalk マップは、BizTalk マッパー (Microsoft [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] シェルにホストされている) によってのみ開くことができます。 Windows エクスプローラーのマップをダブルクリックして、対応するスキーマが正常に読み込まれた場合は、[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] の新しいインスタンスが開き、マップが BizTalk マッパーで開かれます。  
   > 
   > [!NOTE]
   >  既存のマップにカスタム Functoid が含まれる場合は、対応する DLL を "%BTSINSTALLPATH%\Developer Tools\Mapper Extensions" フォルダーにコピーする必要があります。 コピーしない場合、カスタム Functoid の読み込みに失敗するため、マップは読み込まれず、エラーがスローされます。  
  
## <a name="see-also"></a>参照  
 [プロジェクト内のマップを管理します。](../core/managing-maps-within-projects.md)   
 [カスタム Functoid の開発](../core/developing-custom-functoids.md)