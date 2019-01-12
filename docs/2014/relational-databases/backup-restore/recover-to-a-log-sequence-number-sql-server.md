---
title: 恢复到日志序列号 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log sequence numbers [SQL Server]
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- LSNs
- database recovery [SQL Server]
- database restores [SQL Server], point in time
ms.assetid: f7b3de5b-198d-448d-8c71-1cdd9239676c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 835057cdef6b7d2a336b64480515a5046cfde070
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124247"
---
# <a name="recover-to-a-log-sequence-number-sql-server"></a>恢复到日志序列号 (SQL Server)
  本主题仅与使用完整恢复模式或大容量日志恢复模式的数据库相关。  
  
 您可以使用日志序列号 (LSN) 定义还原操作的恢复点。 但是，这是为工具供应商提供的专用功能，不太可能广泛使用。  
  
##  <a name="LSNs"></a> 日志序列号的概述  
 RESTORE 顺序期间，在内部使用 LSN 跟踪数据还原到的时间点。 还原备份后，数据被还原到与进行备份的时间点相对应的 LSN。 差异和日志备份将还原的数据库推到稍后的时间，该时间与一个更高的 LSN 相对应。  
  
 事务日志中的每个记录都由一个日志序列号 (LSN) 唯一标识。 LSN 是这样排序的：如果 LSN2 大于 LSN1，则 LSN2 所标识的日志记录描述的更改发生在日志记录 LSN1 描述的更改之后。  
  
 发生重大事件的日志记录的 LSN 对于构造正确的还原顺序可能很有用。 因为 LSN 是有顺序的，所以可以比较它们是否相等（即 **\<**、 **>**、 **=**、 **\<=**、 **>=**）。 构造还原顺序时，这种比较很有用。  
  
> [!NOTE]  
>  LSN 是数据类型为 `numeric` 的值 (25,0)。 算术运算（例如加法或减法）对 LSN 没有任何意义，请不要与 LSN 一起使用。  
  

  
## <a name="viewing-lsns-used-by-backup-and-restore"></a>查看备份和还原使用的 LSN  
 使用下列一种或几种方法可以查看发生给定备份和还原事件的日志记录的 LSN：  
  
-   [backupset](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
-   [backupfile](/sql/relational-databases/system-tables/backupfile-transact-sql)  
  
-   [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)； [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
-   [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)  
  
-   [RESTORE FILELISTONLY](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)  
  
> [!NOTE]  
>  LSN 还显示在某些消息正文中。  
  
## <a name="transact-sql-syntax-for-restoring-to-an-lsn"></a>还原到 LSN 的 Transact-SQL 语法  
 通过使用 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 语句，可以在 LSN 处或刚好在 LSN 之前停止，如下所示：  
  
-   使用 WITH STOPATMARK **='** lsn:_<lsn_number>_**'** 子句，其中 lsn:*\<lsnNumber>* 是一个字符串，它指出包含指定 LSN 的日志记录是恢复点。  
  
     STOPATMARK 前滚到 LSN，并且前滚中包括该日志记录。  
  
-   使用 WITH STOPBEFOREMARK **='** lsn:_<lsn_number>_**'** 子句，其中 lsn:*\<lsnNumber>* 是一个字符串，它指出包含指定 LSN 编号的日志记录之前的日志记录是恢复点。  
  
     STOPBEFOREMARK 前滚到 LSN，并从前滚中排除该日志记录。  
  
 通常会选择要包括或排除的特定事务。 虽然实践中并不总是如此，但指定的日志记录就是事务提交记录。  
  
## <a name="examples"></a>示例  
 以下示例假定 `AdventureWorks` 数据库已更改为使用完整恢复模式。  
  
```  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [还原数据库备份&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)  
  
-   [还原事务日志备份 (SQL Server)](restore-a-transaction-log-backup-sql-server.md)  
  
-   [在完整恢复模式下将数据库还原到故障点 (Transact-SQL)](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [将数据库还原到标记的事务 (SQL Server Management Studio)](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [将 SQL Server 数据库还原到某个时间点（完整恢复模式）](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## <a name="see-also"></a>请参阅  
 [应用事务日志备份 (SQL Server)](transaction-log-backups-sql-server.md)   
 [事务日志 (SQL Server)](../logs/the-transaction-log-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
