---
title: コンポーネントのマップ |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- file types, maps
- BizTalk Mapper, output
- maps, file type
- maps, file contents
- BizTalk Mapper, file type
- maps, components
ms.assetid: be438d21-80a8-49d8-bd08-d85618ab23de
caps.latest.revision: 10
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b1590ad1450453602b4dd5f25b2d52a4364787af
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36996771"
---
# <a name="map-components"></a>マップの構成要素
マップの構成要素のほとんどは、.btm 拡張子を持つマップ ファイルに保存されます。 このファイルに格納される項目を次に示します。  
  
- 送信元スキーマおよび送信先スキーマへの参照  
  
- リンク (リンクのプロパティを含む)  
  
- Functoid とそのプロパティ (入力パラメーターなど)  
  
- その他さまざまなプロパティ (グリッドやマップそのものに関連付けられたプロパティなど)  
  
  BizTalk マッパーは、.btm ファイル内のマップを XSLT (Extensible Stylesheet Language Transformations) ファイルとしてコンパイルしますが、XSLT がこのファイルの一部になることはありません。 BizTalk マッパーがマップの XSLT を生成するのは、プロジェクトのコンパイル時とマップの検証時だけです。 BizTalk マッパーは、XSLT をプロジェクト アセンブリの一部としてパッケージします。  
  
## <a name="see-also"></a>参照  
 [マップ](../core/maps.md)   
 [BizTalk マッパーを使用してマップを作成します。](../core/creating-maps-using-biztalk-mapper.md)