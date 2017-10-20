---
title: "暂停和恢复数据迁移 (Stretch Database) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, pausing and resuming
- pausing Stretch Database
- resuming Stretch Database
ms.assetid: 65d6a990-b295-41b2-97f9-7b6bf3000e4d
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 0fef9c7f912cb824b3f1fcf8653a82fa99a35561
ms.openlocfilehash: a291fd543d572fc621e7b59e968e7ca69d79552e
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="pause-and-resume-data-migration-stretch-database"></a>暂停和恢复数据迁移 (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  若要暂停或恢复将数据迁移到 Azure，请为 SQL Server Management Studio 中的表选择“延伸”  ，然后选择“暂停”  可以暂停数据迁移，或选择“恢复”  可以恢复数据迁移。 你也可以使用 TRANSACT-SQL 来暂停或恢复数据迁移。  
  
 若要排查本地服务器上的问题，或最大限度地扩大可用网络带宽，请暂停各个表上的数据迁移。  

## <a name="pause-data-migration"></a>暂停数据迁移  
  
### <a name="use-sql-server-management-studio-to-pause-data-migration"></a>使用 SQL Server Management Studio 暂停数据迁移  
  
1.  在 SQL Server Management Studio 的对象资源管理器中，选择要对其暂停数据迁移的已启用延伸的表。  
  
2.  右键单击并选择“延伸”，然后选择“暂停”。  
  
### <a name="use-transact-sql-to-pause-data-migration"></a>使用 TRANSACT-SQL 暂停数据迁移  
 运行以下命令。  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>  
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = PAUSED ) ) ;  
GO 
```  
  
## <a name="resume-data-migration"></a>恢复数据迁移  
  
### <a name="use-sql-server-management-studio-to-resume-data-migration"></a>使用 SQL Server Management Studio 恢复数据迁移  
  
1.  在 SQL Server Management Studio 的对象资源管理器中，选择要对其恢复数据迁移的已启用延伸的表。  
  
2.  右键单击并选择“延伸”，然后选择“继续”。  
  
### <a name="use-transact-sql-to-resume-data-migration"></a>使用 TRANSACT-SQL 恢复数据迁移  
 运行以下命令。  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>   
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = OUTBOUND ) ) ;  
 GO
```  

## <a name="check-whether-migration-is-active-or-paused"></a>检查迁移处于活动状态还是暂停状态

### <a name="use-sql-server-management-studio-to-check-whether-migration-is-active-or-paused"></a>使用 SQL Server Management Studio 检查迁移处于活动状态还是暂停状态
在 SQL Server Management Studio 中，打开“Stretch Database 监视器”并检查“迁移状态”列的值。 有关详细信息，请参阅[数据迁移的监视与故障排除](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)。

### <a name="use-transact-sql-to-check-whether-migration-is-active-or-paused"></a>使用 Transact-SQL 检查迁移处于活动状态还是暂停状态
查询目录视图 **sys.remote_data_archive_tables** 并检查 **is_migration_paused** 列的值。 有关详细信息，请参阅 [sys.remote_data_archive_tables](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md)。

## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
[数据迁移的监视与故障排除](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 
  

