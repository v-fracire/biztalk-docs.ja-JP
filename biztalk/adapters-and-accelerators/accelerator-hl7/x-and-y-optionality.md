---
title: '&#39;X&#39;と&#39;Y&#39; Optionality |Microsoft Docs'
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- segments, Y optionality
- segments, SegmentDataElements table
- SegmentDataElements table
- segments, X optionality
ms.assetid: 8a59b407-95a2-45ba-a8d6-db4154c91d7b
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: aed5b87216bd2d8e127ff032e3773b3f740835c9
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36981523"
---
# <a name="39x39-and-39y39-optionality"></a>&#39;X&#39;と&#39;Y&#39; Optionality
HL7 Access データベースに SegmentDataElements テーブルにはとして設定されているいくつかのデータ項目 (フィールド) が含まれています**Req/Opt X =**、ように、このトリガー イベントにこのフィールドは、HL7 標準によって関連付けるしないことを意味します次の表にします。  
  
|Segment|バージョン|章|データ項目|必要な/<br /><br /> 省略可|レポート|数値|HTML 標準|  
|-------------|-------------|-------------|---------------|-----------------------------|------------|------------|-------------------|  
|OBX|2.4|7.4.2.9|00577|×|Y|5|ch07.htm#Heading113|  
|OBX|2.4|7.4.2.8|00576|×||0|ch07.htm#Heading112|  
|OBX|2.4|7.4.2.6|00574|×||0|ch07.htm#Heading107|  
|OBX|2.4|7.4.2.17|00936|×|Y|0|ch07.htm#Heading121|  
  
 Microsoft から[!INCLUDE[HL7_CurrentVersion_FirstRef](../../includes/hl7-currentversion-firstref-md.md)]イベントをトリガーで指定されていないことにどのような必須/任意の規則またはオプションかどうかにする必要があります。 ローカル サイトの条件に基づく、optionality ルールを適用する決定可能性があります。 既定では、[!INCLUDE[btaBTAHL71.3abbrevnonumber](../../includes/btabtahl71-3abbrevnonumber-md.md)]として示されている 23 フィールドを提供します。 省略可能なフィールドとして"X"です。  
  
> [!NOTE]
>  値"Y"はエラーです、 [!INCLUDE[btaBTAHL71.3abbrevnonumber](../../includes/btabtahl71-3abbrevnonumber-md.md)] Access データベース。 [!INCLUDE[HL7_CurrentVersion_abbrev](../../includes/hl7-currentversion-abbrev-md.md)] 想定されるすべての値**Y**と**空白**は省略可能です。  
  
## <a name="see-also"></a>参照  
 [HL7 2.X スキーマの使用](../../adapters-and-accelerators/accelerator-hl7/using-hl7-2-x-schemas.md)