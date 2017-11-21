---
title: "ALTER DATABASE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_TSQL
- ALTER DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- databases [SQL Server], modifying
- ALTER DATABASE statement
- databases [SQL Server], renaming
- renaming databases
- database modifications [SQL Server]
- ALTER DATABASE statement, syntax described
- database names [SQL Server], ALTER DATABASE
- modifying databases
- collations [SQL Server], modifying
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 15f8affd-8f39-4021-b092-0379fc6983da
caps.latest.revision: 282
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 6c498acedd2821127137ec6be1bd2e04e6b3da09
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改一个数据库或与该数据库关联的文件和文件组。 在数据库中添加或删除文件和文件组、更改数据库的属性或其文件和文件组、更改数据库排序规则和设置数据库选项。 不能修改数据库快照。 若要修改与复制相关联的数据库选项，使用[sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。  
   
 由于 ALTER DATABASE 语法的篇幅较长，因此分为以下主题：  
  
 ALTER DATABASE  
 当前主题介绍的是用于更改数据库的名称和排序规则的语法。  
  
 [ALTER DATABASE 文件和文件组选项](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
 介绍了用于从数据库中添加和删除文件和文件组以及更改文件和文件组的属性的语法。  
  
 [ALTER DATABASE SET 选项](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
 介绍了使用 ALTER DATABASE 的 SET 选项来更改数据库属性的语法。  
  
 [ALTER DATABASE 数据库镜像](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)  
 介绍了 ALTER DATABASE 与数据库镜像相关的 SET 选项的语法。  
  
 [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)  
 提供的语法[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]在 Always On 可用性组的辅助副本上配置辅助数据库的 ALTER DATABASE 选项。  
  
 [ALTER DATABASE 兼容级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
 介绍了 ALTER DATABASE 与数据库兼容级别相关的 SET 选项的语法。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
有关 Azure SQL 数据库，请参阅[ALTER DATABASE &#40;Azure SQL Database &#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
有关 Azure SQL 数据仓库，请参阅[ALTER DATABASE &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
有关并行数据仓库，请参阅[ALTER DATABASE &#40;并行数据仓库 &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).
  
## <a name="syntax"></a>语法  
  
```  
-- SQL Server Syntax  
ALTER DATABASE { database_name  | CURRENT }  
{  
    MODIFY NAME = new_database_name   
  | COLLATE collation_name  
  | <file_and_filegroup_options>  
  | <set_database_options>  
}  
[;]  
  
<file_and_filegroup_options >::=  
  <add_or_modify_files>::=  
  <filespec>::=   
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  
  
<set_database_options>::=  
  <optionspec>::=   
  <auto_option> ::=   
  <change_tracking_option> ::=  
  <cursor_option> ::=   
  <database_mirroring_option> ::=   
  <date_correlation_optimization_option> ::=  
  <db_encryption_option> ::=  
  <db_state_option> ::=  
  <db_update_option> ::=  
  <db_user_access_option> ::=  <delayed_durability_option> ::=  <external_access_option> ::=  
  <FILESTREAM_options> ::=  
  <HADR_options> ::=    
  <parameterization_option> ::=  
  <query_store_options> ::=  
  <recovery_option> ::=   
  <service_broker_option> ::=  
  <snapshot_option> ::=  
  <sql_option> ::=   
  <termination> ::=  
  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 要修改的数据库的名称。  
  
> [!NOTE]  
>  此选项在包含的数据库中不可用。  
  
 CURRENT  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定应更改当前使用的数据库。  
  
 修改名称 **=**  *new_database_name*  
 重命名数据库名称指定为*new_database_name*。  
  
 COLLATE *collation_name*  
 指定数据库的排序规则。 *collation_name*可以是 Windows 排序规则名称或 SQL 排序规则名称。 如果不指定排序规则，则将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的排序规则指定为数据库的排序规则。  
  
 在创建使用非默认排序规则的数据库时，数据库中的数据将始终遵循指定的排序规则。 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，当创建包含的数据库，使用保留的内部目录信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]默认排序规则， **Latin1_General_100_CI_AS_WS_KS_SC**。  
  
 有关 Windows 和 SQL 排序规则名称的详细信息，请参阅[COLLATE &#40;Transact SQL &#41;](~/t-sql/statements/collations.md).  
  
 **\<delayed_durability_option >:: =**  
 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 有关详细信息请参阅[ALTER DATABASE SET 选项 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)和[控制事务持续性](../../relational-databases/logs/control-transaction-durability.md)。  
  
 **\<file_and_filegroup_options >:: =**  
 有关详细信息，请参阅[ALTER DATABASE 文件和文件组选项 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
## <a name="remarks"></a>注释  
 若要删除数据库，使用[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)。  
  
 若要减小数据库大小，使用[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
 ALTER DATABASE 语句必须在自动提交模式（默认事务管理模式）下运行，且不允许用于显式或隐式事务中。  
  
 对数据库文件状态（例如，联机或脱机）的维护是独立于数据库状态的。 有关详细信息，请参阅[文件状态](../../relational-databases/databases/file-states.md)。 文件组中的文件的状态决定整个文件组的可用性。 文件组中的所有文件都必须联机，文件组才可用。 如果文件组脱机，则使用 SQL 语句访问文件组的所有尝试都会失败并报告错误。 在为 SELECT 语句生成查询计划时，查询优化器会避免驻留在脱机文件组中的非聚集索引和索引视图。 这样，这些语句就会成功。 但是，如果脱机文件组包含目标表的堆或聚集索引，SELECT 语句将失败。 此外，如果 INSERT、UPDATE 或 DELETE 语句修改的表的索引包含在脱机文件组中，这些语句将失败。  
  
 当数据库处于 RESTORING 状态时，多数 ALTER DATABASE 语句都将失败。 设置数据库镜像选项除外。 在活动还原操作期间，或者当数据库还原操作或日志文件还原操作由于备份文件损坏而失败时，数据库可以处于 RESTORING 状态。  
  
 通过设置以下选项之一来清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计划缓存。  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY|PAGE_VERIFY|  
  
 清除计划缓存将导致对所有后续执行计划进行重新编译，并可能导致查询性能暂时性地突然降低。 对于计划高速缓存中每个已清除的缓存存储区，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志包含以下信息性消息：“由于某些数据库维护或重新配置操作，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 经历了 '%s' 缓存存储区(计划高速缓存的一部分)的 %d 次刷新”。 每隔五分钟，只要缓存在这段时间间隔内得到刷新，此消息就记录一次。  
  
 在下列情况下，也会刷新过程缓存：  
  
-   数据库的 AUTO_CLOSE 数据库选项设置为 ON。 在没有用户连接引用或使用该数据库时，后台任务将尝试关闭并自动关闭数据库。  
  
-   针对具有默认选项的数据库运行多个查询。 然后，删除数据库。  
  
-   删除源数据库的数据库快照。  
  
-   您已成功重新生成数据库的事务日志。  
  
-   还原数据库备份。  
  
-   分离数据库。  
  
## <a name="changing-the-database-collation"></a>更改数据库排序规则  
 在对数据库应用不同排序规则之前，请确保已满足下列条件：  
  
-   您是当前数据库的唯一用户。  
  
-   没有依赖数据库排序规则的架构绑定对象。  
  
     以下对象，依赖于数据库排序规则，如果存在在数据库中，ALTER DATABASE*database_name*COLLATE 语句将失败。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将对每个阻塞 ALTER 操作的对象返回一条错误消息：  
  
    -   通过 SCHEMABINDING 创建的用户定义函数和视图。  
  
    -   计算列。  
  
    -   检查约束。  
  
    -   表值函数返回包含字符列的表，这些列继承了默认的数据库排序规则。  
  
     数据库排序规则更改时，非绑定到架构的实体的依赖关系信息将自动更新。  
  
 改变数据库的排序规则不会在任何数据对象的系统名称中产生重复名称。 如果更改排序规则产生重复的名称，则以下命名空间可能会导致数据库排序规则更改的故障：  
  
-   对象名，如过程、表、触发器或视图。  
  
-   架构名称。  
  
-   主体，例如组、角色或用户。  
  
-   标量类型名，如系统和用户定义类型。  
  
-   全文目录名称。  
  
-   对象内的列名或参数名。  
  
-   表范围内的索引名。  
  
由新的排序规则产生的重复名称将导致更改操作失败，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误消息，指出重复名称所在的命名空间。  
  
## <a name="viewing-database-information"></a>查看数据库信息  
 可以使用目录视图、系统函数和系统存储过程返回有关数据库、文件和文件组的信息。  
  
## <a name="permissions"></a>Permissions  
 需要对数据库拥有 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-name-of-a-database"></a>A. 更改数据库的名称  
 以下示例将 `AdventureWorks2012` 数据库的名称更改为 `Northwind`。  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
### <a name="b-changing-the-collation-of-a-database"></a>B. 更改数据库的排序规则  
 以下示例创建了一个名为 `testdb`、排序规则为 `SQL_Latin1_General_CP1_CI_A`S 的数据库，然后将 `testdb` 数据库的排序规则更改为 `COLLATE French_CI_AI`。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE master;  
GO  
  
CREATE DATABASE testdb  
COLLATE SQL_Latin1_General_CP1_CI_AS ;  
GO  
  
ALTER DATABASE testDB  
COLLATE French_CI_AI ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
- [ALTER DATABASE &#40;Azure SQL Database &#41;](alter-database-azure-sql-database.md)  
- [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
- [DATABASEPROPERTYEX (Transact-SQL)](../../t-sql/functions/databasepropertyex-transact-sql.md)   
- [DROP DATABASE (Transact SQL)](../../t-sql/statements/drop-database-transact-sql.md)   
- [SET TRANSACTION ISOLATION LEVEL (Transact-SQL)](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
- [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
- [sp_spaceused &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
- [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
- [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
- [sys.database_mirroring_witnesses &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
- [sys.data_spaces &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
- [sys.filegroups &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
- [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
- [系统数据库](../../relational-databases/databases/system-databases.md)  
  

