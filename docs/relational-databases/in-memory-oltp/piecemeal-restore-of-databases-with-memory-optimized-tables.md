---
title: "使用内存优化表的数据库的段落还原 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 732c9721-8dd4-481d-8ff9-1feaaa63f84f
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 16
---
# 使用内存优化表的数据库的段落还原
  使用内存优化表的数据库支持段落还原，但有一个限制（参见下文）。 有关段落备份和还原的详细信息，请参阅 [RESTORE (Transact-SQL)](../Topic/RESTORE%20\(Transact-SQL\).md) 和[段落还原 (SQL Server)](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)。  
  
 内存优化文件组必须同主文件组一起备份和还原：  
  
-   备份（或还原）主文件组时，必须指定内存优化文件组。  
  
-   备份（或还原）内存优化文件组时，必须指定主文件组。  
  
 段落备份和还原的关键方案是，  
  
-   段落备份可减小备份尺寸。 以下是一些示例：  
  
    -   配置数据库备份时机，使其在不同时间或不同日期执行，以最大限度地减少对工作负荷的影响。 有时，由于数据库非常大（ 1 TB 以上），完整数据库备份操作无法在所分配的数据库维护时间内完成。 在这种情况下，可使用段落备份将完整的数据库备份到多个段落备份中。  
  
    -   如果文件组标记为只读，则无需在其标记为只读后进行事务日志备份。 将文件组标记为只读后，可选择只备份该文件组一次。  
  
-   段落还原。  
  
    -   段落还原的目的是将数据库的关键部分先行上线（不必待所有数据还原完毕）。 举个例子，如果某数据库包含分区数据，而较旧的分区很少使用。 则可根据需要还原数据。 对于包含历史数据等的文件组，亦可如此操作。  
  
    -   使用页修复可通过指定要还原的页来修复页损坏。 有关详细信息，请参阅[还原页 (SQL Server)](../../relational-databases/backup-restore/restore-pages-sql-server.md)。  
  
## 示例  
 示例使用下面的架构：  
  
```  
CREATE DATABASE imoltp  
ON PRIMARY (name = imoltp_primary1, filename = 'c:\data\imoltp_data1.mdf')  
LOG ON (name = imoltp_log, filename = 'c:\data\imoltp_log.ldf')  
GO  
  
ALTER DATABASE imoltp ADD FILE (name = imoltp_primary2, filename = 'c:\data\imoltp_data2.ndf')  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_secondary  
ALTER DATABASE imoltp ADD FILE (name = imoltp_secondary, filename = 'c:\data\imoltp_secondary.ndf') TO FILEGROUP imoltp_secondary  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod2', filename='c:\data\imoltp_mod2') TO FILEGROUP imoltp_mod   
GO  
```  
  
### 备份  
 该示例演示如何备份主文件组和内存优化文件组。 必须同时指定主文件组和内存优化文件组。  
  
```  
backup database imoltp filegroup='primary', filegroup='imoltp_mod' to disk='c:\data\imoltp.dmp' with init  
```  
  
 下面的示例演示：对于不使用内存优化表的数据库，备份主文件组和内存优化文件组以外的文件组时的操作亦大同小异。 下面的命令用于备份辅助文件组  
  
```  
backup database imoltp filegroup='imoltp_secondary' to disk='c:\data\imoltp_secondary.dmp' with init  
```  
  
### 还原  
 下面的示例演示如何同时还原主文件组和内存优化文件组。  
  
```  
restore database imoltp filegroup = 'primary', filegroup = 'imoltp_mod'   
from disk='c:\data\imoltp.dmp' with partial, norecovery  
  
--restore the transaction log  
 RESTORE LOG [imoltp] FROM DISK = N'c:\data\imoltp_log.dmp' WITH  FILE = 1,  NOUNLOAD,  STATS = 10  
GO  
```  
  
 下一个示例演示：对于不使用内存优化表的数据库，还原主文件组和内存优化文件组以外的文件组时的操作亦大同小异  
  
```  
RESTORE DATABASE [imoltp] FILE = N'imoltp_secondary'   
FROM  DISK = N'c:\data\imoltp_secondary.dmp' WITH  FILE = 1,  RECOVERY,  NOUNLOAD,  STATS = 10  
GO  
```  
  
## 另请参阅  
 [内存优化表的备份、还原和恢复](../Topic/Backup,%20Restore,%20and%20Recovery%20of%20Memory-Optimized%20Tables.md)  
  
  