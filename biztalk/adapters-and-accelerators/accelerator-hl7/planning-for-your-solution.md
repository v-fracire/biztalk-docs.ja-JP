---
title: ソリューションの計画 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Greenfield project
- security, BTAHL7
- BTAHL7, security
- installing, planning
- installing, installation types
- HL7, security
- security, HL7
- Embedded installation
- Migration project
- Coexistence installation
ms.assetid: a108c6d0-dd51-4bf9-85a0-103f60fae971
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 20e41137d8e300453d3dc4eba7fee6e9dd6ecc0b
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36977275"
---
# <a name="planning-for-your-solution"></a>ソリューションの計画
このセクションでは、Microsoft を計画する際の判断についての情報を提供します。[!INCLUDE[HL7_CurrentVersion_FirstRef](../../includes/hl7-currentversion-firstref-md.md)]ソリューション。  
  
 次の方法では、BTAHL7 を実装できます。  
  
- **未開発プロジェクト**します。 このシナリオは、BTAHL7 の新規インストールです。  
  
- **移行プロジェクト**します。 このシナリオでは、医療保険の組織を既存の統合ブローカーが徐々 にときに発生します。 組織は、BTAHL7 に移行します。  
  
- **共存**します。 このシナリオでは、別の統合エンジン BTAHL7 サイド バイ サイドのインストールでは。  
  
- **埋め込み**します。 このシナリオには、BTAHL7 の基幹業務アプリケーション内で統合が含まれます。 HL7 メッセージング機能をそのアプリケーションに追加するのにには、BTAHL7 を使用します。  
  
  ユーザーは、それらを最初に作成にかかる作業と比較して時間の経過と共にアプリケーションの管理にかかる労力を過小評価する傾向があります。 これは、一連の複雑なデータ処理と管理タスクを実行する必要がある大規模な分散機関を検索するときに特に当てはまります。 病院または統合された正常性の配信の組織がこのような教育機関の優れた例を示します。 このような教育機関に直面無数関数は、アプリケーションからのユーザーと管理者のトレーニングを提供する、重複して問題のあるデータ エントリの必要性を回避するためにアプリケーションに渡される情報を有効にするをサポートするためにソフトウェアを提供する必要がある、ソフトウェア、および古い、または期限切れのアプリケーションの置き換えを向上させるためのものを提供します。 この置換プロセスでは、テストおよび教育機関向けの独自の要件があります。  
  
  これは不可能でしょう (非常にコスト高) を 1 つのすべての機能を管理するこのような教育機関向けの統合アプリケーション。 最初の段階で、金融機関は、1 つのベンダーにその投資を関連付けるにはせず、1 つのベンダーを使用して必要なすべての関数は見つかりません。 教育機関の処理の簡単な運用上のニーズは、2 番目の場所にことを 1 つの統合されたアプリケーションで満足する機関を使用できなくなります。 そのため、教育機関は複数のアプリケーションのニーズをサポートします。 これらのアプリケーションの相互運用するためには、アプリケーションでは、情報を交換するインターフェイスが必要があります。 アプリケーションと関連するインターフェイスの数が非常に大きくでは多くの場合です。 この分散アプリケーション アーキテクチャを指定するには、インターフェイス、エンジンは、時間の経過と共に、教育機関向けデータ処理を管理するためのキーのインストルメント化です。 キーの問題には、移行、マッピング、および教育機関があります。 BTAHL7 のジョブは、簡単で可能な限り効率的なとしてこれらの問題に対処するのには。  
  
- **マッピング**します。 インターフェイスの実装で最も大きなジョブでは、アプリケーションやデータベースの構造体、インターフェイスで使用されるデータ構造とのマッピングを作成します。 ツールでは、簡単かつ自然に何もお勧めします。 さらに、マッピング ドキュメントになるインターフェイスやアプリケーションの開発者によって使用される仕様、ために、そのドキュメントを簡単に生成できる必要があります。 BTAHL7 構成エクスプ ローラー、Microsoft を使用する[!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]および BizTalk Server のツールを開発し、これらのマップを実装します。  
  
- **移行**します。 アプリケーションを変更すると、時間の経過と共にアプリケーションの相互運用性を維持する必要があります。 1 つのアプリケーションを置き換えるには、問題を検討する場合、必要では、適用可能なインターフェイスに、データ ソース マッピングを更新します。 インターフェイス エンジンがあるこれらの 1 つにすぎません。 インターフェイスがインストールされているし、インターフェイスの標準時間の経過と共に変更を検討する必要があります。 時間の経過と共にインターフェイスの標準の変更を流行している標準に移行する必要がありますが表示されます。 インターフェイスが将来変更のアカウントに、移行計画が実行をお勧めします。 標準、間と、標準の異なるバージョン間でマップする必要があります。 1 つの標準の範囲内でさらに、-HL7 V2 など 1 つは特に柔軟性の高い、(多くのアプリケーション) の間で同じ標準の複数の実装を処理します。 インターフェイス エンジンは、管理が容易であるような方法でこのような複雑さを処理する必要があります。  
  
   キーへの移行タスクへのインターフェイスの本体の 1 つの標準の移行です。 ここでは、タスク、新しいに古いバージョンを使用するすべてのマッピングを移行する-アカウント インターフェイスの特定のローカリゼーションと拡張機能で使用すると、される複雑なプロセスです。 ツールは、この移行にアシスタンスを提供する必要があります。  
  
   すべて追加のメッセージの種類のスキーマの名前空間を指定するのにには、BTAHL7 構成エクスプ ローラーの検証 タブを使用します。  
  
- **教育**します。 管理、およびアプリケーションのサポートに関連するユーザーは、随時変更されます。 さらに、インターフェイスは、アプリケーションのコレクションの相互運用機能の中核であるため、ドキュメントになるキーで、全体的なエンタープライズを管理するツール。 これら両方の理由、使いやすく、保守し、やすい) インターフェイスの仕様、b)、アプリケーションや introversion マッピング、および c) のカスタマイズおよびローカライズ アクティビティの論理的根拠のドキュメントを提供する貴重なです。  
  
## <a name="see-also"></a>参照  
[使用可能な HL7 アクセラレータと BizTalk ツールの概要](../../adapters-and-accelerators/accelerator-hl7/learn-the-hl7-accelerator-and-the-biztalk-tools-available.md)