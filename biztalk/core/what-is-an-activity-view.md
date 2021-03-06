---
title: アクティビティ ビューについて | Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- activities [BAM], Activity view [Tracking Profile Editor]
- activities [BAM], definitions
- Tracking Profile Editor, Activity view
- Activity view [Tracking Profile Editor]
ms.assetid: ae6bcdc8-e426-4148-b83d-08a1a5e99ca3
caps.latest.revision: 21
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 48cbf2419f1d3ab0939ed1607df7c17e1ea3f8d1
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36997947"
---
# <a name="what-is-an-activity-view"></a>アクティビティ ビューについて
アクティビティ ビューには、インポートした BAM アクティビティ定義が含まれています。このアクティビティ定義は、Excel 用の BAM アドインで作成します。 BAM アクティビティ定義は、ビジネス プロセスの追跡要件の抽象概念です。 アクティビティは、複数のオーケストレーションおよびポートにまたがることがあります。 アクティビティ定義をインポートすると、その定義の一部を遂行する各オーケストレーション アイテムまたは各メッセージング アイテムにマップされます。  
  
 アクティビティ ビュー リンクは、追跡プロファイル エディター (TPE) のユーザー インターフェイスの左ペインにあります。  
  
## <a name="activity-view-elements"></a>アクティビティ ビューの要素  
 アクティビティ ビューには、追跡プロファイルの全体構造がツリー ビューで表示されます。このビューには、次の要素が含まれます。  
  
- Milestones  
  
- アクティビティのデータ項目  
  
- イベント ソース  
  
- データ ソース  
  
  **マイルス トーン**: マイルス トーンは、特定のプロセスで時点を定義するオブジェクト。 マイルストーンには、次の 3 つのいずれかの方法でアクセスします。  
  
- オーケストレーション スケジュールから図形をドラッグすると、その図形の実行終了時刻がマイルストーンの値として報告されます。  
  
- 右側にあるスキーマ表現からターゲット マイルストーンに、メッセージ プロパティをドラッグできます。  
  
- マイルストーンの値を含んだメッセージ ペイロード スキーマ ノードをドラッグできます。  
  
  > [!NOTE]
  >  DATETIME ONLY 型のスキーマ ノードは実行時に評価されます。 実行時に変換やキャストの問題が発生すると、イベント ログに追跡エラーが記録されます。  
  
  **データ項目**: データ項目は、メッセージ インスタンス、システム、または昇格させたプロパティの XML スキーマから特定の要素を定義するオブジェクト。 データ項目にアクセスするには、スキーマを展開して該当の要素を検索および選択し、適切なデータ項目型のフォルダーにドラッグします。 データ項目に関する情報 (XPath など) がプロファイルに保存されます。  
  
> [!NOTE]
>  TPE では、メッセージ スキーマで特定のデータ フィールド用に定義された 0 対 1 表現のデータ項目のみがサポートされます。 オーケストレーションを追跡するとき、1 対多表現のデータ項目が存在すると、エラーが発生することがあります。 その場合は、BAM プライマリ インポート データベースにデータが保存されません。 エラーが発生しない場合でも、どのデータ項目が追跡されるかについては保証されません。  
  
> [!NOTE]
>  BAM 開発者は、プロパティが BAM ではなく BizTalk Server の処理規則に従って設定されることを認識しておく必要があります。  
>   
>  たとえば、SMTP アダプターでは、SMTPServer、CC、From などのコンテキスト プロパティには、値が明示的に設定されるまで値がありません。 プロパティに値が設定されると、BAM プライマリ インポート データベースに値が反映され、値を追跡できるようになります。  
  
## <a name="activity-view-context-menus"></a>アクティビティ ビューのショートカット メニュー  
 アクティビティ ビューに使用できるアクションのショートカット メニューは、[オーケストレーションの種類] で選択したノードによって動的に変化します。 たとえば、アクティビティ フォルダー ノードを選択した場合のショートカット メニューには、アクティビティ フォルダーで使用するメニュー項目が含まれています。  
  
 ビジネス アクティビティの項目をイベントおよびデータに関連付けるには、右のソース イベント ペインからアクティビティ ビューのイベント ノードまたはデータ ノードに項目をドラッグします。  
  
 アクティビティ ビューのノードのショートカット メニューを表示するには、ツリーのノードを右クリックします。 次の画面に、アクティビティ ビューのルート ノードを示します。 次の表で、アクティビティ ビューのノード別にショートカット メニューの項目を説明します。  
  
 **アクティビティ定義ツリーのルート ノード**  
  
 ![](../core/media/activityviewcontextmenu.gif "activityviewcontextmenu")  
  
|メニュー項目|使用方法|  
|---------------|-----------|  
|[新しい Continuation]|新しい Continuation フォルダーをアクティビティ ツリーに挿入します。 このフォルダーの値は、Continuation の継続元セグメントからマップします。<br /><br /> ContinuationID フォルダーと併用することで、同一のアクティビティを設定する複数のコンポーネント間で処理を渡すことができます。 このように使用できるコンポーネントには、BizTalk オーケストレーション、ポート、BufferedEventStreams、DirectEventStreams などがあります。 **注:** Continuation フォルダーの名前は最大 127 文字を含めることができます。|  
|[新しい ContinuationID]|新しい ContinuationID フォルダーをアクティビティ ツリーに挿入します。 このフォルダーは、Continuation の継続先セグメントにマップします。 たとえば、オーケストレーション A からオーケストレーション B に継続する場合、このフォルダーをオーケストレーション B の項目にマップする必要があります。<br /><br /> Continuation フォルダーと併用することで、同一のアクティビティを設定する複数のコンポーネント間で処理を渡すことができます。 このように使用できるコンポーネントには、BizTalk オーケストレーション、ポート、BufferedEventStreams、DirectEventStreams などがあります。 **注:** ContinuationID フォルダーの名前は最大 127 文字を含めることができます。|  
|[新しいリレーションシップ]|新しい Relationship フォルダーをアクティビティ ツリーに挿入します。 ビューを形成するアクティビティ間のリレーションシップを公開するために使用します。 **注:** Relationship フォルダーの名前は最大 128 文字を含めることができます。 この名前には、サーバー名および BizTalk 管理データベース名を含めます。|  
|[新しい Document Reference URL]|新しい Document Reference URL フォルダーをアクティビティ ツリーに挿入します。 このアクティビティに関連するドキュメントが格納されている場所を参照 URL に設定するために使用します。 **注:** Document Reference URL フォルダー名は最大 128 文字を含めることができます。|  
  
 **プロパティ ノード**  
  
|メニュー項目|使用方法|  
|---------------|-----------|  
|[選択したデータを関連付ける]|メッセージ ペイロードまたはコンテキスト プロパティのデータ項目と、BAM アクティビティ データ項目フォルダーの関連付けを作成するために使用します。|  
  
 **イベント ノード**  
  
|メニュー項目|使用方法|  
|---------------|-----------|  
|[選択したアクションの終了時に関連付ける]|オーケストレーション図形、DateTime メッセージ ペイロード、DateTime コンテキスト プロパティのいずれかのデータ項目と、BAM アクティビティ マイルストーン フォルダーの関連付けを作成するために使用します。|  
  
## <a name="see-also"></a>参照  
 [イベント ストリームを使用した BAM アクティビティを実装します。](../core/implementing-bam-activities-with-event-streams.md)   
 [Excel でビジネス アクティビティとビューの定義](../core/defining-business-activities-and-views-in-excel.md)   
 [TPE のコンポーネント](../core/components-of-the-tpe.md)