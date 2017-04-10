---
title: "教程：SQL Server 备份和还原到 Windows Azure Blob 存储服务 | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016 Preview"
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# 教程：SQL Server 备份和还原到 Windows Azure Blob 存储服务
欢迎使用“使用 Windows Azure Blob 存储服务进行 SQL Server 备份和还原入门”教程。 本教程将帮助您了解如何将备份写入 Windows Azure Blob 存储服务以及如何从中还原。  
  
## 学习内容  
本教程演示如何创建 Windows 存储帐户和 Blob 容器、创建用于访问存储帐户的凭据、将备份写入 Blob 服务和执行简单还原。 本教程分为四课：  
  
[第 1 课：创建 Windows Azure 存储对象](../Topic/Lesson%201:%20Create%20Windows%20Azure%20Storage%20Objects.md)  
在本课中，您将创建 Windows Azure 存储帐户和 Blob 容器。  
  
[Lesson 2: Create a SQL Server Credential](../Topic/Lesson%202:%20Create%20a%20SQL%20Server%20Credential.md)  
在本课中，您将创建凭据，以存储用于访问 Windows Azure 存储帐户的安全信息。  
  
[第 3 课：将完整数据库备份写入到 Windows Azure Blob 存储服务](../Topic/Lesson%203:%20Write%20a%20Full%20Database%20Backup%20to%20the%20Windows%20Azure%20Blob%20Storage%20Service.md)  
在本课中，您将发出一条 T-SQL 语句，用于将 AdventureWorks2012 数据库的备份写入到 Windows Azure Blob 存储服务。  
  
[第 4 课：从完整数据库备份执行还原](../Topic/Lesson%204:%20Perform%20a%20Restore%20From%20a%20Full%20Database%20Backup.md)  
在本课中，您将发出一条 T-SQL 语句，用于从您在上一课中创建的数据库备份中进行还原。  
  
### 要求  
若要完成本教程中，您必须熟悉 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份和还原概念以及 T-SQL 语法。 若要使用本教程，您的系统必须满足以下要求：  
  
-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]的实例，以及安装了 AdventureWorks2012 数据库。  
  
    SQL Server 实例可以在内部部署中，也可以在 Windows Azure 虚拟机中。  
  
    可以使用用户数据库代替 AdventureWorks2012，并相应地修改 tsql 语法。  
  
-   用于发出 BACKUP 或 RESTORE 命令的用户帐户应属于具有“更改任意凭据”权限的 **db_backup 操作员**数据库角色。  
  
### 其他阅读主题  
以下是一些建议阅读的主题，便于了解概念以及在将 Windows Azure Blob 存储服务用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份时的最佳做法。  
  
1.  [使用 Microsoft Azure Blob 存储服务进行 SQL Server 备份和还原](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [SQL Server 备份到 URL 最佳实践和故障排除](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
## 另请参阅  
[备份数据库和日志](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#databaselog)  
[创建主文件组的完整文件备份](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#filegroups)  
[还原数据库并移动文件](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#restoredbwithmove)  
  
