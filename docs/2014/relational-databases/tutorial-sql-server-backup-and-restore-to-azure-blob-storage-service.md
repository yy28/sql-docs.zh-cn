---
title: 教程：将 SQL Server 备份和还原到 Azure Blob 存储服务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
ms.openlocfilehash: e3eee1449ec42285d5a95ac33d91f439dcd131ac
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002485"
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>教程：将 SQL Server 备份和还原到 Azure Blob 存储服务
  欢迎使用使用 Azure Blob 存储服务进行备份和还原 SQL Server 教程的入门。 本教程将帮助您了解如何将备份写入 Azure Blob 存储服务以及如何从中还原。  
  
## <a name="what-you-will-learn"></a>学习内容  
 本教程演示如何创建 Windows 存储帐户和 Blob 容器、创建用于访问存储帐户的凭据、将备份写入 Blob 服务和执行简单还原。 本教程分为四课：  
  
 [第1课：创建 Azure 存储对象](../tutorials/lesson-1-create-windows-azure-storage-objects.md)  
 在本课中，你将创建 Azure 存储帐户和 Blob 容器。  
  
 [第 2 课：创建 SQL Server 凭据](../tutorials/lesson-2-create-a-sql-server-credential.md)  
 在本课中，你将创建凭据，以存储用于访问 Azure 存储帐户的安全信息。  
  
 [第 3 课：将完整数据库备份写入到 Azure Blob 存储服务](../tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)  
 在本课中，你将发出一条 T-SQL 语句，用于将 AdventureWorks2012 数据库的备份写入到 Azure Blob 存储服务。  
  
 [第 4 课：从完整数据库备份执行还原](../tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)  
 在本课中，您将发出一条 T-SQL 语句，用于从您在上一课中创建的数据库备份中进行还原。  
  
### <a name="requirements"></a>要求  
 若要完成本教程，你必须熟悉 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份和还原概念以及 T-SQL 语法。 若要使用本教程，您的系统必须满足以下要求：  
  
-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的实例，以及安装了 AdventureWorks2012 数据库。  
  
     SQL Server 实例可以在本地，也可以在 Azure 虚拟机中。  
  
     可以使用用户数据库代替 AdventureWorks2012，并相应地修改 tsql 语法。  
  
-   用于发出 BACKUP 或 RESTORE 命令的用户帐户应属于具有“更改任意凭据”  权限的 **db_backup 操作员**数据库角色。  
  
### <a name="additional-reading"></a>其他阅读材料  
 以下是一些建议阅读的主题，便于了解概念以及在将 Azure Blob 存储服务用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 备份时的最佳做法。  
  
1.  [使用 Azure Blob 存储服务进行 SQL Server 备份和还原](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [从 SQL Server 备份到 URL 的最佳做法和故障排除](backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
