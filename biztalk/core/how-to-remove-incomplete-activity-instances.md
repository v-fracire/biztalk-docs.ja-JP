---
title: 不完全なアクティビティ インスタンスの削除 |Microsoft Docs
description: BizTalk Server で BAM プライマリ インポート データベースから不完全なインスタンスを削除するカスタムの RemoveDanglingInstances SQL スクリプトを実行します。
ms.custom: ''
ms.date: 01/18/2018
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7060578c-6267-487b-8530-efa18f9431ce
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8a4ed81978dd275be8eb0348ff15dc8748258239
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2018
ms.locfileid: "36977171"
---
# <a name="remove-incomplete-activity-instances"></a>不完全なアクティビティ インスタンスを削除します。
BAM 定義ファイルを展開すると、定義ファイルで定義された各アクティビティに対し、5 個のテーブルが BAM プライマリ インポート データベースに作成されます。 作成されるテーブルは次のとおりです。  
  
- bam_`ActivityName`_Active  
  
- bam_`ActivityName`_Completed  
  
- bam_`ActivityName`_ActiveRelationships  
  
- bam_`ActivityName`_CompletedRelationships  
  
- bam_`ActivityName`_Continuations  
  
  `ActivityName` は、ユーザーが定義したアクティビティの名前になります。  
  
  不完全なデータが、bam _ には、通常の実行中に`ActivityName`*アクティブ テーブル。データにリレーションシップおよび参照がある場合はデータには、bam\\*`ActivityName`_ActiveRelationships テーブル。  
  
  Continuation を使用したアクティビティの追跡時には、アクティビティが不完全な状態で BAM データベースに残される場合があります。 このトピックの最後に示すストアド プロシージャ作成スクリプトを使用すると、不完全なレコードを削除するストアド プロシージャを作成できます。  
  
  ストアド プロシージャを作成するには、スクリプトをコピーしてから、SQL Server Management を使用して BAM プライマリ インポート データベースに対しスクリプトを実行します。 スクリプトでは、という名前のストアド プロシージャを生成します。 **RemoveDanglingInstances**データベースにします。  
  
## <a name="create-the-removedanglinginstances-stored-procedure"></a>RemoveDanglingInstances ストアド プロシージャを作成します。  
  
1.  開いている**SQL Server Management Studio**、SQL server に接続します。
  
2.  サーバー名を展開し、**データベース**、BAM プライマリ インポート データベースを選択します。  
  
3.  **[新しいクエリ]** をクリックします。  
  
4.  ストアド プロシージャ作成スクリプトをコピーし、クエリ ペインに貼り付けます。  
  
5.  **実行**スクリプト。 作成されたストアド プロシージャは、dbo としてストアド プロシージャの一覧で表示できます。RemoveDanglingInstances します。  
  
## <a name="remove-incomplete-activity-instances"></a>不完全なアクティビティ インスタンスを削除します。  
  
1.  開いている**SQL Server Management Studio**、SQL server に接続します。
  
2.  サーバー名を展開し、**データベース**、BAM プライマリ インポート データベースを選択します。  
  
3.  **[新しいクエリ]** をクリックします。  
  
4.  クエリ ウィンドウで次のように入力します。`exec RemoveDanglingInstances`と削除の操作を実行するための適切なパラメーター。 たとえば、注文書アクティビティの不完全なインスタンスをすべて削除するには、「`exec RemoveDanglingInstances @ActivityName = 'PurchaseOrder'`」と入力します。  
  
5.  **実行**スクリプト。  
  
## <a name="removedanglinginstances-usage-examples"></a>RemoveDanglingInstances の使用例  
 ストアド プロシージャには、4 つのパラメーターが表示されることができます。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|@ActivityName nvarchar(128)|削除する不完全なアクティビティ インスタンスの名前を指定します。|  
|@ActivityId nvarchar(128)|(省略可能) 指定したインスタンス識別子を持つ未解決のインスタンスだけをストアド プロシージャで削除するように指定します。|  
|@DateThreshold datetime|(省略可能)古いアクティブなテーブルですべてのアクティブなインスタンスのことを指定します (等しくないと古い、古いのみ)、指定された日付よりも削除されます。|  
|@NewTableExtension nvarchar (30)|(省略可能) ストアド プロシージャで、指定された拡張子を既存のアクティビティ テーブルに連結して新しいテーブルを 3 つ作成するように指定します。<br /><br /> 結果のテーブルになります。<br /><br /> bam_ActivityName_Active_\<拡張機能\><br /><br /> bam_ActivityName_ActiveRelationships_\<拡張機能\><br /><br /> bam_ActivityName_Continuations_\<拡張機能\><br /><br /> 不完全なインスタンスは、データベースから削除される代わりに、これらの新しいテーブルに移動されます。<br /><br /> これらのテーブルが既に存在する場合は、再利用されます。存在しない場合は作成されます。 **重要:** ストアド プロシージャ、テーブルが既に存在する場合、これらのスキーマが作成された場合に使用されるものと一致する前提としています。 スキーマが一致しない場合は、ストアド プロシージャはレコードを挿入できず、削除操作が失敗します。|  
  
 `exec RemoveDanglingInstances @ActivityName = 'PurchaseOrder'`  
  
 アクティブ テーブル、アクティブ リレーションシップ テーブル、および Continuation テーブルにある PurchaseOrder アクティビティのアクティブなインスタンスをすべて削除します。  
  
 `exec RemoveDanglingInstances @ActivityName = 'PurchaseOrder', @ActivityId = 'PO220567'`  
  
 PurchaseOrder アクティビティのアクティブ テーブル、アクティブ リレーションシップ テーブル、および Continuation テーブルから、アクティビティ ID が PO220567 であるアクティビティ インスタンスだけを削除します。  
  
 `exec RemoveDanglingInstances @ActivityName = 'PurchaseOrder', @DateThreshold='2005-02-02 19:27:03:533'`  
  
 PurchaseOrder アクティビティのアクティブ テーブル、アクティブ リレーションシップ テーブル、および Continuation テーブルから、LastModified の日時が 2005 年 2 月 2 日午後 7:27:03.533 よりも古いアクティビティ インスタンスをすべて削除します。  
  
 `exec RemoveDanglingInstances @ActivityName = 'PurchaseOrder', @ActivityId = 'PO220567', @DateThreshold='2005-02-02 19:27:03:533'`  
  
 LastModified 列が 2005 年 2 月 2 日午後 7:27:03.533 よりも古い場合にのみ、アクティビティ ID が PO220567 であるアクティビティ インスタンスを削除します。  
  
 `exec RemoveDanglingInstances @ActivityName = 'PurchaseOrder', @DateThreshold='2005-02-02 19:27:03:533', @NewTableExtension=N'Dangling'`  
  
 データベース内に次のテーブルを作成します。  
  
 bam_PurchaseOrder_Active_Dangling  
  
 bam_PurchaseOrder_ActiveRelationships_Dangling  
  
 bam_PurchaseOrder_Continuations_Dangling  
  
 ストアド プロシージャは、PurchaseOrder アクティビティのアクティブ テーブル、アクティブ リレーションシップ テーブル、および Continuation テーブルから、2005 年 2 月 2 日午後 7:27:03.533 よりも古い不完全なアクティビティ インスタンスをすべてコピーし、新しく作成されたテーブルに挿入します。 次に、コピー済みのアクティビティ インスタンスが、アクティブ テーブル、アクティブ リレーションシップ テーブル、および Continuation テーブルから削除されます。  
  
## <a name="stored-procedure-creation-script"></a>ストアド プロシージャ作成スクリプト  
  
```  
EXEC sp_stored_procedures @sp_name = 'RemoveDanglingInstances'  
IF @@ROWCOUNT > 0 DROP PROCEDURE RemoveDanglingInstances  
GO  
  
CREATE PROCEDURE RemoveDanglingInstances  
    @ActivityName nvarchar(128),  
    @ActivityId nvarchar(128) = NULL,  
    @DateThreshold datetime = NULL,  
    @NewTableExtension nvarchar(30) = NULL  
AS  
    DECLARE @QueryString nvarchar(4000)  
    DECLARE @ActiveTableName sysname  
    DECLARE @ActiveRelationshipsTableName sysname  
    DECLARE @ContinuationsTableName sysname  
    DECLARE @DanglingActiveTableName sysname  
    DECLARE @DanglingActiveRelationshipsTableName sysname  
    DECLARE @DanglingContinuationsTableName sysname  
  
    SET @ActiveTableName = 'bam_' + @ActivityName + '_Active'  
    SET @ActiveRelationshipsTableName = 'bam_' + @ActivityName + '_ActiveRelationships'  
    SET @ContinuationsTableName = 'bam_' + @ActivityName + '_Continuations'  
  
    SET TRANSACTION ISOLATION LEVEL READ COMMITTED  
    BEGIN TRAN  
  
    DECLARE @LockActivity nvarchar(128)  
    SELECT @LockActivity = ActivityName  
    FROM bam_Metadata_Activities WITH (XLOCK)  
    WHERE ActivityName = @ActivityName  
  
    EXEC sp_tables @table_name = #DanglingActivities  
    IF @@ROWCOUNT > 0 DROP TABLE #DanglingActivities  
  
    CREATE TABLE #DanglingActivities(ActivityID nvarchar(128) PRIMARY KEY)  
  
    SET @QueryString = N'INSERT INTO #DanglingActivities (ActivityID) SELECT ActivityID FROM [bam_' + @ActivityName + '_Active]'  
  
    IF (@DateThreshold is not NULL) OR (@ActivityId is not NULL)  
    BEGIN  
        SET @QueryString = @QueryString + ' WHERE'  
    END  
  
    IF (@DateThreshold is not NULL)  
    BEGIN  
        SET @QueryString = @QueryString + ' LastModified < N''' + CONVERT(nvarchar(50), @DateThreshold, 109) + ''''  
        IF (@ActivityId is not NULL)  
        BEGIN  
            SET @QueryString = @QueryString + ' AND'  
        END  
    END  
  
    IF (@ActivityId is not NULL)  
    BEGIN  
        SET @QueryString = @QueryString + ' ActivityID = N''' + @ActivityId + ''''  
    END  
  
    EXEC sp_executesql @QueryString  
    SELECT * FROM #DanglingActivities  
  
    SET @QueryString = N''  
  
    -- If the user gave a table extension, the dangling instances will be inserted  
    -- into that table.   
    IF (isnull(@NewTableExtension, '') <> '')  
    BEGIN  
        SET @DanglingActiveTableName = @ActiveTableName + '_' + @NewTableExtension  
        SET @DanglingActiveRelationshipsTableName = @ActiveRelationshipsTableName + '_' + @NewTableExtension  
        SET @DanglingContinuationsTableName = @ContinuationsTableName + '_' + @NewTableExtension  
  
        -- If the table for the dangling instances exists then insert into it  
        -- If the table does not exist, then create the dangling instances table  
        -- and then insert into it. SELECT INTO will do that.  
        EXEC sp_tables @table_name = @DanglingActiveTableName  
        IF @@ROWCOUNT > 0  
        BEGIN  
            SET @QueryString = N'INSERT INTO ' + '[' + @DanglingActiveTableName + '] SELECT active.* FROM [' + @ActiveTableName + '] active INNER JOIN #DanglingActivities dangling ON active.ActivityID = dangling.ActivityID'  
            EXEC sp_executesql @QueryString  
        END  
        ELSE  
        BEGIN  
            SET @QueryString = N'SELECT active.* INTO [' + @DanglingActiveTableName + '] FROM [' + @ActiveTableName + '] active INNER JOIN #DanglingActivities dangling ON active.ActivityID = dangling.ActivityID'  
            EXEC sp_executesql @QueryString  
        END  
  
        -- Now do what you did for the Active Instances table for the   
        -- ActiveRelationships table  
        EXEC sp_tables @table_name = @DanglingActiveRelationshipsTableName  
        IF @@ROWCOUNT > 0  
        BEGIN  
            SET @QueryString = N'INSERT INTO ' + '[' + @DanglingActiveRelationshipsTableName + '] SELECT active.* FROM [' + @ActiveRelationshipsTableName + '] active INNER JOIN #DanglingActivities dangling ON active.ActivityID = dangling.ActivityID'  
            EXEC sp_executesql @QueryString  
        END  
        ELSE  
        BEGIN  
            SET @QueryString = N'SELECT active.* INTO [' + @DanglingActiveRelationshipsTableName + '] FROM [' + @ActiveRelationshipsTableName + '] active INNER JOIN #DanglingActivities dangling ON active.ActivityID = dangling.ActivityID'  
            EXEC sp_executesql @QueryString  
        END  
  
        -- And finally for the continuations table  
        EXEC sp_tables @table_name = @DanglingContinuationsTableName  
        IF @@ROWCOUNT > 0  
        BEGIN  
            SET @QueryString = N'INSERT INTO ' + '[' + @DanglingContinuationsTableName + '] SELECT active.* FROM [' + @ContinuationsTableName + '] active INNER JOIN #DanglingActivities dangling ON active.ParentActivityID = dangling.ActivityID'  
            EXEC sp_executesql @QueryString  
        END  
        ELSE  
        BEGIN  
            SET @QueryString = N'SELECT active.* INTO [' + @DanglingContinuationsTableName + '] FROM [' + @ContinuationsTableName + '] active INNER JOIN #DanglingActivities dangling ON active.ParentActivityID = dangling.ActivityID'  
            EXEC sp_executesql @QueryString  
        END  
    END  
  
    -- Remove the dangling instances from the Active Instances Table  
    SET @QueryString = 'DELETE FROM [' + @ActiveTableName + '] FROM [' + @ActiveTableName + '] active INNER JOIN #DanglingActivities dangling ON active.ActivityID = dangling.ActivityID '  
    EXEC sp_executesql @QueryString  
  
    SET @QueryString = 'DELETE FROM [' + @ActiveRelationshipsTableName + '] FROM [' + @ActiveRelationshipsTableName + '] active INNER JOIN #DanglingActivities dangling ON active.ActivityID = dangling.ActivityID '  
    EXEC sp_executesql @QueryString  
  
    SET @QueryString = 'DELETE FROM [' + @ContinuationsTableName + '] FROM [' + @ContinuationsTableName + '] active INNER JOIN #DanglingActivities dangling ON active.ParentActivityID = dangling.ActivityID '  
    EXEC sp_executesql @QueryString  
  
    DROP TABLE #DanglingActivities  
  
    COMMIT TRAN      
GO  
```  

## <a name="another-method-of-resolving-incomplete-instances"></a>不完全なインスタンスを解決する別の方法
BAMPrimaryImport データベースからの不完全なアクティビティ インスタンスは、SQL クエリを使用しても解決できます。 参照してください[不完全なアクティビティ インスタンスを解決する](how-to-resolve-incomplete-activity-instances.md)します。

## <a name="see-also"></a>参照  
 [BAM データベースの管理](../core/managing-bam-databases.md)
