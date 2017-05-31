---
title: "第 8 课. 从日志备份还原为新数据库 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 281259fb737bbc41885a61e62a4fcc83b3001119
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-8-restore-as-new-database-from-log-backup"></a>第 8 课. 从日志备份还原为新数据库
在本课程中，需将 AdventureWorks2014 数据库作为新数据库从文件快照事务日志备份进行还原。  
  
在此方案中，是还原到不同虚拟机上的 SQL Server 实例，以便进行业务分析和报告。 还原到不同虚拟机上的不同实例可将工作负荷卸载到针对此用途调整了大小的专用虚拟机，从而从事务系统中消除资源要求。  
  
使用文件快照备份从事务日志备份进行的还原非常快速，比传统流式备份要快得多。 对于传统流式备份，需要使用完整数据库备份，可能要使用差异备份，以及使用部分或所有事务日志备份（或新的完整数据库备份）。 但是，对于文件快照日志备份，只需要最新日志备份（或是任何其他日志备份或任何两个相邻日志备份以实现到两个日志备份时间之间的某个点的时间点还原）。 为清楚起见，只需要一个日志文件快照备份集，因为每个文件快照日志备份会创建每个数据库文件（每个数据文件和日志文件）的文件快照。  
  
若要使用文件快照备份从事务日志备份将数据库还原到新的数据库，请执行以下步骤：  
  
1.  连接到 SQL Server Management Studio。  
  
2.  打开一个新查询窗口，连接到 Azure 虚拟机中数据库引擎的 SQL Server 2016 实例。  
  
    > [!NOTE]  
    > 如果此 Azure 虚拟机与你用于以前课程的虚拟机不同，请确保执行了 [第 2 课：使用共享访问签名创建 SQL Server 凭据](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)中的步骤。 如果要还原到不同容器，请针对新容器执行 [第 1 课：在 Azure 容器上创建存储访问策略和共享访问签名](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md) 和 [第 2 课：使用共享访问签名创建 SQL Server 凭据](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md) 中的步骤。  
  
3.  复制以下 Transact-SQL 脚本，然后将其粘贴到查询窗口中。 选择要使用的日志备份文件。 针对第 1 课中指定的存储帐户名称和容器适当修改 URL，提供日志备份文件名称，然后执行此脚本。  
  
    ```  
  
    -- restore as a new database from a transaction log backup file  
    RESTORE DATABASE AdventureWorks2014_EOM   
        FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<logbackupfile.bak'    
        WITH MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Data.mdf'  
       , MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Log.ldf'  
       , RECOVERY  
    --, REPLACE  
  
    ```  
  
4.  检查输出以验证还原是否成功。  
  
5.  在对象资源管理器中，连接到 Azure 存储。  
  
6.  展开容器，展开在第 1 课中创建的容器（在需要时进行刷新），验证新数据和日志文件是否随以前课程中的 blob 一起出现在容器中。  
  
    ![显示新数据库的数据文件和日志文件的 Azure 容器](../relational-databases/media/e9705083-86bc-4309-a0bf-92c15f174c0a.JPG "显示新数据库的数据文件和日志文件的 Azure 容器")  
  
[第 9 课：管理备份集和文件快照备份](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)  
  
  
  

