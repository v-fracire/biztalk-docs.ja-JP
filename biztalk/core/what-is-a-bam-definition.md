---
title: BAM 定義について | Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- definitions [BAM], observation models
- definitions [BAM], about BAM definitions
- definitions [BAM]
ms.assetid: 1ba1f45e-85fe-492f-8a2e-98bf3570c633
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9d3285d2dfaf40d302fb6009eb63219ed89edd6a
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "37006131"
---
# <a name="what-is-a-bam-definition"></a>BAM 定義について
BAM 定義は、BAM 監視モデルの XML 表現で、監視するビジネス プロセスの概要を定義したものです。 監視モデル (つまり BAM 定義) の主要部分は、マイルストーン、収集するデータ イベント (BAM アクティビティ)、データ収集の説明、および情報をユーザー (BAM ビュー) に表示する方法で構成されています。  
  
> [!NOTE]
>  BAM スキーマに準拠した XML ファイルを手作業で作成することはできますが、定義が検証されないので BAM 定義を作成する方法としてはお勧めしません。  
  
 BAM 定義には、次の項目を含めることができます。  
  
- ビジネス アクティビティ : 有効な BAM 定義には、ビジネス アクティビティ (BAM アクティビティ) が含まれている必要があります。 その他の項目はすべて省略できます。 定義に、ビジネス アクティビティを追加する方法の詳細については、次を参照してください。[ビジネス アクティビティを定義する方法](../core/how-to-define-a-business-activity.md)します。  
  
- ビュー : ビジネス アクティビティで定義されたデータにアクセスできるユーザーを定義します。 ビューは、フィルター処理されたデータ、フィルター処理されたデータの集計、およびフィルター処理されたデータの表示方法 (ピボットグラフ レポートなど) で構成されます。 BAM では、1 つのアクティビティに対して複数のビューを定義できます。  
  
   ビューでは、次のビジネス プロセスを定義できます。  
  
  -   エイリアスに基づいたビジネス データ : エイリアスを使用することで、データ項目にフレンドリ名を適用することができます。 たとえば、開発者が項目"LName"と呼ばれるデータを定義できます。 別名を作成することができます"LName"が「姓」、BAM を表示するときにライブ データが表示されるようにします。  エイリアスの詳細については、次を参照してください。[ビュー項目の名前を変更する方法](../core/how-to-rename-view-items.md)します。  
  
  -   期間 : アクティビティを監視する期間です。  
  
  -   マイルストーン グループ : 一連のビジネス マイルストーンです。 グループを使用して、ある期間のビジネス マイルストーンの開始または終了のいずれかを表すことができます。  
  
  -   集計 : これらは、リアルタイム集計 (RTA) またはスケジュール済みの集計 (オンライン分析処理 (OLAP)) のいずれかで、次の項目で構成されます。  
  
- メジャー : Analysis Services (OLAP) キューブのファクト テーブルの列に基づいた OLAP キューブに格納されている数値のセットです。  
  
- 進捗ディメンション : 処理中のアクティビティの進捗状況に関する集計を作成する場合に使用します。  
  
- データ ディメンション : 集計を分類する場合に使用します。 データ ディメンションは、BAM アクティビティに含まれている文字列型のデータ項目に基づいています。  
  
- 時間ディメンション : 定義済みの時間単位の集計を作成する場合に使用します。  
  
- 数値範囲ディメンション : 特定の数値範囲のフレンドリ名に基づいた集計を分類する場合に使用します。  
  
  BAM 定義には、ビューで定義した警告の定義を含めることができます。 また、ピボットテーブル レイアウトも含めることができます。 BAM 定義を展開すると、ライブ ビジネス データを含むピボットテーブル レポートは、Excel のライブ データ ブックまたは BAM ポータルを使用して表示することができます。  
  
> [!NOTE]
>  Excel 用 BAM アドインを使用して作成された BAM 定義には、アラートを含めることはできません。  
  
## <a name="see-also"></a>参照  
 [Excel でビジネス アクティビティとビューの定義](../core/defining-business-activities-and-views-in-excel.md)   
 [BAM ポータル](../core/bam-portal.md)   
 [BAM 動的インフラストラクチャ](../core/bam-dynamic-infrastructure.md)