---
title: 准备批量导入数据 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], about bulk importing
- BULK INSERT statement, guidelines
- BULK INSERT statement, restrictions
- bcp utility [SQL Server], guidelines
- bcp utility [SQL Server], restrictions
- hidden characters
- OPENROWSET function, BCP guidelines
ms.assetid: a82ef43c-d006-4c71-bfca-f001a3ba1ba0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 95deda34b673161bf63c29a912564f39425583a9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011845"
---
# <a name="prepare-to-bulk-import-data-sql-server"></a>准备大容量导入数据 (SQL Server)
  只能使用 **bcp** 命令、BULK INSERT 语句或 OPENROWSET(BULK) 函数从数据文件批量导入数据。  
  
> [!NOTE]  
>  可以编写从对象而非文本文件大容量导入数据的自定义应用程序。 若要从内存缓冲区批量导入数据，请使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (ODBC) 应用程序编程接口 (API) 的 bcp 扩展或 OLE DB **IRowsetFastLoad** 接口。  若要从 C# 数据表批量导入数据，请使用 ADO.NET 批量复制 API，即 **SqlBulkCopy**。  
  
> [!NOTE]  
>  不支持将数据大容量导入到远程表中。  
  
 在将数据文件中的数据大容量导入到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，请使用以下原则：  
  
-   为用户帐户获取所需的权限。  
  
     用户帐户，你在其中使用 **bcp** 实用工具、BULK INSERT 语句或 INSERT ...SELECT * FROM OPENROWSET(BULK...) 语句的用户帐户必须具有表的所需权限，这些权限由表所有者分配。 有关每个方法所需的权限的详细信息，请参阅 [bcp 实用工具、](../../tools/bcp-utility.md)[OPENROWSET (Transact SQL)](/sql/t-sql/functions/openrowset-transact-sql) 和 [BULK INSERT (Transact SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)。  
  
-   使用大容量日志恢复模式。  
  
     此原则适用于使用完整恢复模式的数据库。 对无索引表（“堆”  ）执行批量操作时，大容量日志恢复模式非常有用。 使用大容量日志恢复有助于防止事务日志出现空间不足的情况，因为大容量日志恢复不会插入日志行。 有关大容量日志恢复模式的详细信息，请参阅[恢复模式 (SQL Server)](../backup-restore/recovery-models-sql-server.md)。  
  
     建议您在执行大容量导入操作之前，先将数据库改为使用大容量日志恢复模式。 之后应立即将数据库重设为完整恢复模式。 有关详细信息，请参阅[查看或更改数据库的恢复模式 (SQL Server)](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)。  
  
    > [!NOTE]  
    >  有关如何在批量导入操作期间最小化日志记录的详细信息，请参阅 [批量导入中最小化日志记录的先决条件](prerequisites-for-minimal-logging-in-bulk-import.md)。  
  
-   大容量导入数据后进行备份。  
  
     对于使用简单恢复模式的数据库，建议您在大容量导入操作完成后执行完整备份或差异备份。 有关详细信息，请参阅[创建完整数据库备份 (SQL Server)](../backup-restore/create-a-full-database-backup-sql-server.md) 或[创建差异数据库备份 (SQL Server)](../backup-restore/create-a-differential-database-backup-sql-server.md)。  
  
     对于大容量日志恢复模式或完整恢复模式，只需执行日志备份就足够了。 有关详细信息，请参阅[事务日志备份 (SQL Server)](../backup-restore/transaction-log-backups-sql-server.md)。  
  
-   删除表索引以提高大型大容量导入操作的性能。  
  
     在导入的数据量与表中已有数据量相比很大时，请使用此原则。 在这种情况下，执行大容量导入操作之前删除表中的索引可显著提高性能。  
  
    > [!NOTE]  
    >  如果加载的数据量与表中已有的数据量相比较小时，删除索引会适得其反。 因为重新生成索引所需的时间可能要比大容量导入操作期间所节省的时间更长。  
  
-   查找并删除数据文件中的隐藏字符。  
  
     许多实用工具和文本编辑器都会显示隐藏字符，这些隐藏字符通常位于数据文件末尾。 在大容量导入操作期间，ASCII 数据文件中的隐藏字符会导致问题，这些问题会引发“发现意外空字符”错误。 查找并删除所有隐藏字符有助于避免此问题。  
  
## <a name="see-also"></a>另请参阅  
 [使用 bcp 实用工具导入和导出大容量数据 (SQL Server)](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)   
 [使用 BULK INSERT 或 OPENROWSET (BULK...) 导入批量数据 (SQL Server)](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [bcp 实用工具](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [用于批量导入或导出的数据格式 (SQL Server)](data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
