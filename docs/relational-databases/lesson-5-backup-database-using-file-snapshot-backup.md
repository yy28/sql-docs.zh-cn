---
title: "第 5 课：使用文件快照备份来备份数据库 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
caps.latest.revision: "19"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 910053b9953a1352c98b6b8f67dc844204933b2e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-5-backup-database-using-file-snapshot-backup"></a>第 5 课：使用文件快照备份来备份数据库
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]在本课程中，使用文件快照备份来备份 Azure 虚拟机中的 AdventureWorks2014 数据库，以便使用 Azure 快照执行近乎即时的备份。 有关文件快照备份的详细信息，请参阅 [Azure 中数据库文件的文件快照备份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
若要使用文件快照备份来备份 AdventureWorks2014 数据库，请按照下列步骤执行：  
  
1.  连接到 SQL Server Management Studio。  
  
2.  打开一个新查询窗口，连接到 Azure 虚拟机中数据库引擎的 SQL Server 2016 实例。  
  
3.  复制以下 Transact-SQL 脚本，将其粘贴到此查询窗口并执行（请不要关闭此查询窗口 - 在步骤 5 中将再次执行此脚本。） 通过此系统存储过程可查看包含指定数据库的每个文件的现有的文件快照备份。 你会注意到此数据库没有文件快照备份。  
  
    ```  
  
    -- Verify that no file snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
4.  复制以下 Transact-SQL 脚本，然后将其粘贴到查询窗口中。 将 URL 中的存储帐户名称和容器名称更改为第 1 课中指定的名称，然后执行此脚本。 请注意此备份的速度。  
  
    ```  
  
    -- Backup the AdventureWorks2014 database with FILE_SNAPSHOT  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Azure.bak'   
       WITH FILE_SNAPSHOT;  
  
    ```  
  
    ![显示每个数据库文件的文件快照的结果窗格](../relational-databases/media/2a9320e0-067a-485a-8e0e-636660005e5c.JPG "显示每个数据库文件的文件快照的结果窗格")  
  
5.  在确认步骤 4 中的脚本已成功执行之后，再次执行下面的脚本。 请注意，步骤 4 中的文件快照备份操作生成了数据文件和日志文件的文件快照。  
  
    ```  
  
    -- Verify that two file-snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![显示 2 个快照的 sys.fn_db_backup_file_snapshots 函数结果](../relational-databases/media/fca1436e-9607-4432-97ee-f66ac2f2108d.JPG "显示 2 个快照的 sys.fn_db_backup_file_snapshots 函数结果")  
  
6.  在对象资源管理器中，在 Azure 虚拟机的 SQL Server 2016 实例中展开数据库节点，并确认 AdventureWorks2014 数据库已恢复到此实例（必要时请刷新该节点）。  
  
7.  在对象资源管理器中，连接到 Azure 存储。  
  
8.  展开容器。展开在第 1 课中创建的容器，并确认该容器中显示上面步骤 4 中的 AdventureWorks2014_Azure.bak，还显示第 3 课的备份文件和第 4 课的数据库文件（必要时请刷新节点）。  
  
    ![文件快照备份显示在 Azure 容器中](../relational-databases/media/181bc970-4af7-4272-a9ae-4bef674f2e02.JPG "文件快照备份显示在 Azure 容器中")  
  
**下一课：**  
  
[第 6 课：使用文件快照备份生成活动和备份日志](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
## <a name="see-also"></a>另请参阅  
[Azure 中数据库文件的文件快照备份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sys.fn_db_backup_file_snapshots (Transact-SQL)](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
  
  
  
