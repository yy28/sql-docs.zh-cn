---
title: "备份镜像媒体集 (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# 备份镜像媒体集 (Transact-SQL)
  本主题介绍在备份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库时如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) 语句指定镜像介质集。 在 BACKUP 语句中的 TO 子句中指定第一个镜像。 然后，在它自己的 MIRROR TO 子句中指定每个镜像。 TO 和 MIRROR TO 子句必须指定相同数量和类型的备份设备。  
  
## 示例  
 下例创建上一图中所述的镜像介质集并将 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库同时备份到两个镜像。  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
    FORMAT,  
    MEDIANAME = 'AdventureWorks2012Set1';  
GO  
```  
  
## 相关任务  
 **从镜像备份还原**  
  
-   [RESTORE (Transact-SQL)](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
## 另请参阅  
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [镜像备份媒体集 (SQL Server)](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  