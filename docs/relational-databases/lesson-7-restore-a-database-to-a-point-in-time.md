---
title: "第 7 课：将数据库还原到某个时点 | Microsoft Docs"
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
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a25788a3b7eda518aeff01329eb5e207d9092bd6
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-7-restore-a-database-to-a-point-in-time"></a>第 7 课：将数据库还原到时间点
在本课程中，需将 AdventureWorks2014 数据库还原到两个事务日志备份之间的时间点。  
  
借助传统备份来完成时间点还原，需要使用完整数据库备份（可能是差异备份）以及所有达到以及刚刚超过想要还原到的时间点的事务日志文件。 借助文件快照备份，则只需要两个相邻日志备份文件，文件提供想要还原的时间前后的目标帖子。 由于每个日志备份会创建每个数据库文件（每个数据文件和日志文件）的文件快照，因此只需要两个日志文件快照备份集。  
  
要将数据库从文件快照备份集还原到指定的时间点，请执行下列步骤：  
  
1.  连接到 SQL Server Management Studio。  
  
2.  打开一个新查询窗口，连接到 Azure 虚拟机中数据库引擎的 SQL Server 2016 实例。  
  
3.  复制以下 Transact-SQL 脚本，将其粘贴到查询窗口中，并执行。 在将 Production.Location 表还原到步骤 5 中它所有的行更少时的某个时间点之前，验证该表是否有 29,939 行。  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location  
  
    ```  
  
    ![显示 29,939 行计数](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "显示 29,939 行计数")  
  
4.  复制以下 Transact-SQL 脚本，然后将其粘贴到查询窗口中。 选择两个相邻的日志备份文件并将文件名转换为此脚本所需的日期和时间。 针对第 1 课中指定的存储帐户名称和容器适当修改 URL，提供第一个和第二个备份文件名称，提供“June 26, 2015 01:48 PM”格式的 STOPAT 时间，然后执行此脚本。 此脚本将需要几分钟完成  
  
    ```  
  
    -- restore and recover to a point in time between the times of two transaction log backups, and then verify the row count  
    ALTER DATABASE AdventureWorks2014 SET SINGLE_USER WITH ROLLBACK IMMEDIATE;  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<firstbackupfile>.bak'   
       WITH NORECOVERY,REPLACE;  
    RESTORE LOG AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<secondbackupfile>.bak'    
       WITH RECOVERY, STOPAT = 'June 26, 2015 01:48 PM';  
    ALTER DATABASE AdventureWorks2014 set multi_user;  
    -- get new count  
    SELECT COUNT (*) FROM AdventureWorks2014.Production.Location ;  
  
    ```  
  
5.  检查输出。 请注意，还原后，行计数为 18,389，介于日志备份 5 和 6 的行计数之间（你的行计数会有所变化）。  
  
    ![显示时间点还原后的行计数的结果窗格](../relational-databases/media/4a0c6d8b-e2ed-4e93-bd7a-ade22a4aecc6.JPG "显示时间点还原后的行计数的结果窗格")  
  
**下一课：**  
  
[第 8 课：从日志备份还原为新数据库](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
  

