---
title: "第 6 课：使用文件快照备份生成活动和备份日志 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8f3ea59fb612ea692b52ab46bb342d8c4031fb71
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup"></a>第 6 课：使用文件快照备份生成活动和备份日志
在本课中，将生成 AdventureWorks2014 数据库中的活动，并定期使用文件快照备份创建事务日志备份。 有关使用文件快照备份的详细信息，请参阅 [Azure 中数据库文件的文件快照备份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
若要生成 AdventureWorks2014 数据库中的活动，并定期使用文件快照备份创建事务日志备份，请执行以下步骤：  
  
1.  连接到 SQL Server Management Studio。  
  
2.  打开两个新查询窗口，将每个连接到 Azure 虚拟机中的数据库引擎的 SQL Server 2016 实例。  
  
3.  复制以下 Transact-SQL 脚本，将其粘贴到其中一个查询窗口中，并执行。 请注意，在步骤 4 中添加新行之前，Production.Location 表有 14 行。  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
4.  复制以下两个 Transact-SQL 脚本，将它们分别粘贴到这两个不同的查询窗口中。 将 URL 中的存储帐户名称和容器名称更改为第 1 课中指定的名称，然后同时执行这两个查询窗口中的这些脚本。 这些脚本完成时间大约需要 7 分钟。  
  
    ```  
    -- Insert 30,000 new rows into the Production.Location table in the AdventureWorks2014 database in batches of 75  
    DECLARE @count INT=1, @inner INT;  
    WHILE @count < 400  
       BEGIN  
          BEGIN TRAN;  
             SET @inner =1;  
                WHILE @inner <= 75  
                   BEGIN;  
                      INSERT INTO AdventureWorks2014.Production.Location    
                         (Name, CostRate, Availability, ModifiedDate)   
                            VALUES (NEWID(), .5, 5.2, GETDATE());  
                      SET @inner = @inner + 1;  
                   END;  
          COMMIT;  
       WAITFOR DELAY '00:00:01';   
       SET @count = @count + 1;  
       END;  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
    ```  
    --take 7 transaction log backups with FILE_SNAPSHOT, one per minute, and include the row count and the execution time in the backup file name   
    DECLARE @count INT=1, @device NVARCHAR(120), @numrows INT;  
    WHILE @count <= 7  
       BEGIN  
             SET @numrows = (SELECT COUNT (*) FROM AdventureWorks2014.Production.Location);  
             SET @device = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-' + CONVERT (varchar(10),@numrows) + '-' + FORMAT(GETDATE(), 'yyyyMMddHHmmss') + '.bak';  
             BACKUP LOG AdventureWorks2014 TO URL = @device WITH FILE_SNAPSHOT;  
             SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
          WAITFOR DELAY '00:1:00';   
             SET @count = @count + 1;  
       END;  
    ```  
  
5.  查看第一个脚本的输出，并注意最后的行数现在为 29,939。  
  
    ![显示了行数 29,939](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "显示了行数 29,939")  
  
6.  查看第二个脚本的输出，并注意每执行一次 BACKUP LOG 语句，就会创建两个新文件快照，一个是日志文件的文件快照，另一个是数据文件的文件快照 — 每个数据库文件共有两个文件快照。 第二个脚本完成后，请注意现在共有 16 个文件快照，每个数据库文件有 8 个 — 一个来自 BACKUP DATABASE 语句，另一个是 BACKUP LOG 语句每次执行的结果。  
  
    ![结果窗格，其中显示了在创建日志备份时数据和日志文件的文件快照](../relational-databases/media/acd213b8-895e-425c-bd72-2bf10e65a5ba.JPG "结果窗格，其中显示了在创建日志备份时数据和日志文件的文件快照")  
  
    ![显示了四个文件快照](../relational-databases/media/e7eff77d-85b9-4e52-abd8-e49952c8118a.JPG "显示了四个文件快照")  
  
    ![结果窗格，其中共显示了 16 个文件快照](../relational-databases/media/c3ddff17-a83c-4bf0-a670-a38834f9c922.JPG "结果窗格，其中共显示了 16 个文件快照")  
  
7.  在对象资源管理器中，连接到 Azure 存储。  
  
8.  展开容器，展开在第 1 课中创建的容器，并确认容器中显示 7 个新备份文件和之前课程中的 blob（必要时刷新节点）。  
  
    ![Azure 容器，其中显示了 7 个日志备份 blob](../relational-databases/media/cfa5a326-87a2-4202-9a04-38bf577d2d0b.JPG "Azure 容器，其中显示了 7 个日志备份 blob")  
  
**下一课：**  
  
[第 7 课：将数据库还原到时间点](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
  

