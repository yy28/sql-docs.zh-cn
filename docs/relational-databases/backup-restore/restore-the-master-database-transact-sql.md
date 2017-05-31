---
title: "还原 master 数据库 (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- master database [SQL Server], restoring
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 36558a8f79b9ad229a90970b5df514a399b68c66
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="restore-the-master-database-transact-sql"></a>还原 master 数据库 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主题介绍如何从完整数据库备份还原 **master** 数据库。  
  
### <a name="to-restore-the-master-database"></a>还原 master 数据库  
  
1.  在单用户模式下启动服务器实例。  
  
     有关如何指定单一用户启动参数 (**-m**) 的信息，请参阅[配置服务器启动选项（SQL Server 配置管理器）](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)。  
  
2.  若要还原 **master**的完整数据库备份，请使用以下 [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
     `RESTORE DATABASE master FROM`  *&lt;backup_device&gt;*  `WITH REPLACE`  
  
     REPLACE 选项指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 即使已经存在同名数据库也要还原指定的数据库。 现有的数据库（如果存在）被删除。 在单用户模式下，建议在 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)中输入 RESTORE DATABASE 语句。 有关详细信息，请参阅 [使用 sqlcmd 实用工具](../../relational-databases/scripting/sqlcmd-use-the-utility.md)。  
  
    > [!IMPORTANT]  
    >  在还原 **master** 后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例会关闭，并终止 **sqlcmd** 进程。 在重新启动服务器实例之前，请删除单用户引导参数。 有关详细信息，请参阅[配置服务器启动选项（SQL Server 配置管理器）](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)。  
  
3.  重新启动服务器实例并继续执行其他恢复步骤，例如还原其他数据库、附加数据库以及更正用户不匹配问题。  
  
## <a name="example"></a>示例  
 下面的示例将在默认服务器实例上还原 `master` 数据库。 该示例假定服务器实例是在单用户模式下运行。 该示例启动 `sqlcmd` 并执行 `RESTORE DATABASE` 语句，以便从磁盘设备 `master` 还原 `Z:\SQLServerBackups\master.bak`的完整数据库备份。  
  
> [!NOTE]  
>  对于命名实例，**sqlcmd** 命令必须指定 **-S***\<ComputerName>*\\*\<InstanceName>* 选项。  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [完整数据库还原（简单恢复模式）](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [完整数据库还原（完整恢复模式）](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [孤立用户故障排除 (SQL Server)](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [重新生成系统数据库](../../relational-databases/databases/rebuild-system-databases.md)   
 [数据库引擎服务启动选项](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)   
 [备份和还原系统数据库 (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)   
 [在单用户模式下启动 SQL Server](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
