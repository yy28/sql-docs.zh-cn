---
title: ALTER DATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 1256884f13a576580588e877dd490f0757bfba9e
ms.sourcegitcommit: aac654706b21f70962c7311f3b193000113d00d7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2018
ms.locfileid: "42802566"
---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE (Transact-SQL) 

修改数据库的某些配置选项。 

本文提供所选任何 SQL 产品的语法、参数、注解、权限和示例。

有关语法约定的详细信息，请参阅 [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。 

## <a name="click-a-product"></a>单击一个产品！

在下一行中，单击你感兴趣的产品名称。 单击时此网页上的此位置会显示适合你单击的任何产品的不同内容。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]  
> ||||||  
> |---|---|---|---|---|  
> |**_\* SQL Server \*_** &nbsp;|[SQL 数据库<br />逻辑服务器](alter-database-transact-sql.md?view=azuresqldb-current)|[SQL 数据库<br />托管实例](alter-database-transact-sql.md?view=azuresqldb-mi-current)|[SQL 数据<br />数据仓库](alter-database-transact-sql.md?view=azure-sqldw-latest)|[SQL 并行<br />数据仓库](alter-database-transact-sql.md?view=aps-pdw-2016)|  

&nbsp;

# <a name="sql-server"></a>SQL Server

## <a name="overview"></a>概述

在 SQL Server 中，此语句修改一个数据库或与该数据库关联的文件和文件组。 在数据库中添加或删除文件和文件组、更改数据库的属性或其文件和文件组、更改数据库排序规则和设置数据库选项。 不能修改数据库快照。 若要修改与复制相关的数据库选项，请使用 [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。  
   
由于 ALTER DATABASE 语法的篇幅较长，因此分为多篇文章。  

ALTER DATABASE  
本文介绍的是用于更改数据库的名称和排序规则的语法和相关信息。  
  
[ALTER DATABASE 文件和文件组选项](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
介绍了用于从数据库中添加和删除文件和文件组以及更改文件和文件组的属性的语法和相关信息。  
  
[ALTER DATABASE SET 选项](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
介绍了使用 ALTER DATABASE 的 SET 选项来更改数据库属性的语法和相关信息。  
  
[ALTER DATABASE 数据库镜像](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)  
介绍了 ALTER DATABASE 与数据库镜像相关的 SET 选项的语法和相关信息。  
  
[ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)  
提供 ALTER DATABASE 的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 选项的语法和相关信息，该语法用来在 AlwaysOn 可用性组的辅助副本上配置辅助数据库。  
  
[ALTER DATABASE 兼容级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
介绍了 ALTER DATABASE 与数据库兼容级别相关的 SET 选项的语法和相关信息。  
  
## <a name="syntax"></a>语法  
  
```  
-- SQL Server Syntax  
ALTER DATABASE { database_name  | CURRENT }  
{  
    MODIFY NAME = new_database_name   
  | COLLATE collation_name  
  | <file_and_filegroup_options>  
  | SET <option_spec> [ ,...n ] [ WITH <termination> ] 
  | SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 | 90 }   
  
}  
[;]  
  
<file_and_filegroup_options>::=  
  <add_or_modify_files>::=  
  <filespec>::=   
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  
  
<option_spec>::=  
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
 
<compatibility_level>
   { 140 | 130 | 120 | 110 | 100 | 90 }   
```  
  
## <a name="arguments"></a>参数  
*database_name*  
要修改的数据库的名称。  
  
> [!NOTE]  
>  此选项在包含的数据库中不可用。  
  
CURRENT  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
指定应更改当前使用的数据库。  
  
MODIFY NAME *=***new_database_name  
使用指定的名称 new_database_name 重命名数据库。  
  
COLLATE collation_name  
指定数据库的排序规则。 collation_name 既可以是 Windows 排序规则名称，也可以是 SQL 排序规则名称。 如果不指定排序规则，则将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的排序规则指定为数据库的排序规则。  
  
在创建使用非默认排序规则的数据库时，数据库中的数据将始终遵循指定的排序规则。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，创建包含的数据库时，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 默认排序规则 Latin1_General_100_CI_AS_WS_KS_SC 来维护内部目录信息。  
  
有关 Windows 和 SQL 排序规则名称的详细信息，请参阅 [COLLATE](~/t-sql/statements/collations.md)。  
  
\<delayed_durability_option> ::=  
**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
有关详细信息，请参阅 [ALTER DATABASE SET 选项](../../t-sql/statements/alter-database-transact-sql-set-options.md)和[控制事务持续性](../../relational-databases/logs/control-transaction-durability.md)。  
  
\<file_and_filegroup_options>::=  
有关详细信息，请参阅 [ALTER DATABASE 文件和文件组选项](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)。  
  
## <a name="remarks"></a>Remarks  
若要删除数据库，请使用 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)。  
  
若要减小数据库的大小，请使用 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
ALTER DATABASE 语句必须在自动提交模式（默认事务管理模式）下运行，且不允许用于显式或隐式事务中。  
  
对数据库文件状态（例如，联机或脱机）的维护是独立于数据库状态的。 有关详细信息，请参阅[文件状态](../../relational-databases/databases/file-states.md)。 文件组中文件的状态决定整个文件组的可用性。 文件组中的所有文件都必须联机，文件组才可用。 如果文件组脱机，则使用 SQL 语句访问文件组的所有尝试都会失败并报告错误。 在为 SELECT 语句生成查询计划时，查询优化器会避免驻留在脱机文件组中的非聚集索引和索引视图。 这样，这些语句就会成功。 但是，如果脱机文件组包含目标表的堆或聚集索引，SELECT 语句将失败。 此外，如果 INSERT、UPDATE 或 DELETE 语句修改的表的索引包含在脱机文件组中，这些语句将失败。  
  
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
  
- 数据库的 AUTO_CLOSE 数据库选项设置为 ON。 在没有用户连接引用或使用该数据库时，后台任务将尝试关闭并自动关闭数据库。  
- 针对具有默认选项的数据库运行多个查询。 然后，删除数据库。  
- 删除源数据库的数据库快照。  
- 您已成功重新生成数据库的事务日志。  
- 还原数据库备份。  
- 分离数据库。  
  
## <a name="changing-the-database-collation"></a>更改数据库排序规则  
在对数据库应用不同排序规则之前，请确保已满足下列条件：  
  
- 您是当前数据库的唯一用户。  
- 没有依赖数据库排序规则的架构绑定对象。  
  
  如果数据库中存在下列依赖于数据库排序规则的对象，则 ALTER DATABASE database_name COLLATE 语句将失败。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将对每个阻塞 ALTER 操作的对象返回一条错误消息：  
  
  - 通过 SCHEMABINDING 创建的用户定义函数和视图。  
  
  - 计算列。  
  
  - CHECK 约束。  
  
  - 表值函数返回包含字符列的表，这些列继承了默认的数据库排序规则。  
  
    数据库排序规则更改时，非绑定到架构的实体的依赖关系信息将自动更新。  
  
改变数据库的排序规则不会在任何数据对象的系统名称中产生重复名称。 如果改变排序规则后出现重复的名称，则下列命名空间可能导致改变数据库排序规则的操作失败：  
  
- 对象名，如过程、表、触发器或视图。  
- 架构名称。  
- 主体，例如组、角色或用户。  
- 标量类型名，如系统和用户定义类型。  
- 全文目录名称。  
- 对象内的列名或参数名。  
- 表范围内的索引名。  
  
由新的排序规则产生的重复名称将导致更改操作失败，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误消息，指出重复名称所在的命名空间。  
  
## <a name="viewing-database-information"></a>查看数据库信息  
可以使用目录视图、系统函数和系统存储过程返回有关数据库、文件和文件组的信息。  
  
## <a name="permissions"></a>Permissions  
需要对数据库拥有 ALTER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-name-of-a-database"></a>A. 更改数据库的名称  
以下示例将 `AdventureWorks2012` 数据库的名称更改为 `Northwind`。  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
### <a name="b-changing-the-collation-of-a-database"></a>B. 更改数据库的排序规则  
以下示例创建了一个名为 `testdb`、排序规则为 `SQL_Latin1_General_CP1_CI_A`S 的数据库，然后将 `testdb` 数据库的排序规则更改为 `COLLATE French_CI_AI`。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```sql  
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
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
- [系统数据库](../../relational-databases/databases/system-databases.md)  

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><a href="alter-database-transact-sql.md?view=sql-server-2016">SQL Server</a></th>
>   <th><strong><em>* SQL 数据库<br />逻辑服务器*</em></strong></th>
>   <th><a href="alter-database-transact-sql.md?view=azuresqldb-mi-current">SQL 数据库<br />托管实例</a></th>
>   <th><a href="alter-database-transact-sql.md?view=azure-sqldw-latest">SQL 数据<br />仓库</a></th>
>   <th><a href="alter-database-transact-sql.md?view=aps-pdw-2016">SQL Parallel<br />数据仓库</a></th>
> </tr>
> </table>

&nbsp;

# <a name="azure-sql-database-logical-server"></a>Azure SQL 数据库逻辑服务器

## <a name="overview"></a>概述

在 Azure SQL 数据库中，使用此语句修改逻辑服务器上的数据库。 使用此语句更改数据库的名称、更改数据库的版本和服务目标、将数据库加入到弹性池或将其从弹性池中删除、设置数据库选项、添加或删除数据库作为异地复制关系中的辅助，以及设置数据库兼容级别。

由于 ALTER DATABASE 语法的篇幅较长，因此分为多篇文章。  

ALTER DATABASE  
本文介绍的是用于更改数据库的名称和排序规则的语法和相关信息。  
  
[ALTER DATABASE SET 选项](../../t-sql/statements/alter-database-transact-sql-set-options.md?&tabs=sqldbls)  
介绍了使用 ALTER DATABASE 的 SET 选项来更改数据库属性的语法和相关信息。  
  
[ALTER DATABASE 兼容级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md?&tabs=sqldbls)  
介绍了 ALTER DATABASE 与数据库兼容级别相关的 SET 选项的语法和相关信息。  

## <a name="syntax"></a>语法 

```  
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name | CURRENT }  
{  
    MODIFY NAME = new_database_name  
  | MODIFY ( <edition_options> [, ... n] ) 
  | SET { <option_spec> [ ,... n ] WITH <termination>} 
  | SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 }   
  | ADD SECONDARY ON SERVER <partner_server_name>  
    [WITH ( <add-secondary-option>::= [, ... n] ) ]  
  | REMOVE SECONDARY ON SERVER <partner_server_name>  
  | FAILOVER  
  | FORCE_FAILOVER_ALLOW_DATA_LOSS  
}  
[;] 

<edition_options> ::= 
{  

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }  
  | EDITION = { 'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical'} 
  | SERVICE_OBJECTIVE = 
       {  <service-objective>
       | { ELASTIC_POOL (name = <elastic_pool_name>) } 
       } 
}  

<add-secondary-option> ::=  
   {  
      ALLOW_CONNECTIONS = { ALL | NO }  
     | SERVICE_OBJECTIVE = 
       {  <service-objective> 
       | { ELASTIC_POOL ( name = <elastic_pool_name>) } 
       } 
   }  

<service-objective> ::=  { 'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |
       | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' | 'GP_GEN4_24' |
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 'BC_GEN4_24' |
      | 'GP_GEN5_2' | 'GP_GEN5_4' | 'GP_GEN5_8' | 'GP_GEN5_16' | 'GP_GEN5_24' | 'GP_GEN5_32' | 'GP_GEN5_48' | 'GP_GEN5_80' |
      | 'BC_GEN5_2' | 'BC_GEN5_4' | 'BC_GEN5_8' | 'BC_GEN5_16' | 'BC_GEN5_24' | 'BC_GEN5_32' | 'BC_GEN5_48' | 'BC_GEN5_80' |
      }

<option_spec> ::= 
{  
    <auto_option> 
  | <change_tracking_option> 
  | <cursor_option> 
  | <db_encryption_option>  
  | <db_update_option> 
  | <db_user_access_option> 
  | <delayed_durability_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <snapshot_option>  
  | <sql_option> 
  | <target_recovery_time_option> 
  | <termination>  
  | <temporal_history_retention>  
}  
```
  
## <a name="arguments"></a>参数  

*database_name*  

要修改的数据库的名称。  
  
CURRENT  

指定应更改当前使用的数据库。  
  
MODIFY NAME *=***new_database_name  

使用指定的名称 new_database_name 重命名数据库。 以下示例将 `db1` 数据库的名称更改为 `db2`：   

```sql  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

MODIFY (EDITION = ['basic' | 'standard' | 'premium' |'GeneralPurpose' | 'BusinessCritical'])    

更改数据库的服务层。 

以下示例将版本更改为 `premium`：
  
```sql  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

如果数据库的 MAXSIZE 属性设置为该版本支持的有效范围之外的值，则 EDITION 更改会失败。  

MODIFY (MAXSIZE = [100 MB | 500 MB | 1 | 1024…4096] GB)  

指定数据库的最大大小。 该最大大小必须符合针对数据库的 EDITION 属性的有效值集。 更改数据库的最大大小可能导致更改数据库 EDITION。 下表列出 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务层支持的 MAXSIZE 值和默认值 (D)。  
  
**基于 DTU 的模型**

|**MAXSIZE**|**基本**|**S0-S2**|**S3-S12**|**P1-P6**|**P11-P15**|  
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|  
|100 MB|√|√|√|√|√|  
|250 MB|√|√|√|√|√|  
|500 MB|√|√|√|√|√|  
|1 GB|√|√|√|√|√|  
|2 GB|√ (D)|√|√|√|√|  
|5 GB|N/A|√|√|√|√|  
|10 GB|N/A|√|√|√|√|  
|20 GB|N/A|√|√|√|√|  
|30 GB|N/A|√|√|√|√|  
|40 GB|N/A|√|√|√|√|  
|50 GB|N/A|√|√|√|√|  
|100 GB|N/A|√|√|√|√|  
|150 GB|N/A|√|√|√|√|  
|200 GB|N/A|√|√|√|√|  
|250 GB|N/A|√ (D)|√ (D)|√|√|  
|300 GB|N/A|√|√|√|√|  
|400 GB|N/A|√|√|√|√|  
|500 GB|N/A|√|√|√ (D)|√|  
|750 GB|N/A|√|√|√|√|  
|1024 GB|N/A|√|√|√|√ (D)|  
|从 1024 GB 到最大 4096 GB，增量为 256 GB*|N/A|N/A|N/A|N/A|√|√|  
  
\* P11 和 P15 允许 MAXSIZE 达到 4 TB，默认大小为 1024 GB。  P11 和 P15 可以使用最大 4 TB 的内含存储，且无需额外费用。 在高级层中，以下区域当前提供大于 1 TB 的 MAXSIZE：美国东部 2、美国西部、美国弗吉尼亚州政府、西欧、德国中部、东南亚、日本东部、澳大利亚东部、加拿大中部和加拿大东部。 有关基于 DTU 的模型的资源限制的其他详细信息，请参阅[基于 DTU 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)。  

基于 DTU 的模型的 MAXSIZE 值（如果指定）必须为上表中所示的指定服务层的有效值。
 
**基于 vCore 的模型**

**常规用途服务层 - 第 4 代计算平台**
|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_4|GP_Gen4_8|GP_Gen4_16|GP4_24|
|:--- | --: |--: |--: |--: |--: |--:|
|最大数据大小 (GB)|1024|1024|1536|3072|4096|4096|

**常规用途服务层 - 第 5 代计算平台**
|MAXSIZE|GP_Gen5_2|GP_Gen5_4|GP_Gen5_8|GP_Gen5_16|GP_Gen5_24|GP_Gen5_32|GP_Gen5_48|GP_Gen5_80|
|:----- | ------: |-------: |-------: |--------: |--------: |---------:|--------: |---------: |
|最大数据大小 (GB)|1024|1024|1536|3072|4096|4096|4096|4096|


**业务关键服务层 - 第 4 代计算平台**
|性能级别|BC_Gen4_1|BC_Gen4_2|BC_Gen4_4|BC_Gen4_8|BC_Gen4_16|
|:--- | --: |--: |--: |--: |--: |--: |
|最大数据大小 (GB)|1024|1024|1024|1024|1024|1024|

**业务关键服务层 - 第 5 代计算平台**
|MAXSIZE|BC_Gen5_2|BC_Gen5_4|BC_Gen5_8|BC_Gen5_16|BC_Gen5_24|BC_Gen5_32|BC_Gen5_48|BC_Gen5_80|
|:----- | ------: |-------: |-------: |--------: |--------: |---------:|--------: |---------: |
|最大数据大小 (GB)|1024|1024|1024|1024|2048|4096|4096|4096|

如果使用 vCore 模型时未设置 `MAXSIZE` 值，则默认为 32 GB。 针对基于 vCore 的模型，有关其资源限制的其他详细信息，请参阅[基于 vCore 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)。
  
以下规则适用于 MAXSIZE 和 EDITION 参数：  
  
- 如果指定了 EDITION 但未指定 MAXSIZE，则使用版本的默认值。 例如，如果 EDITION 设置为 Standard 并且未指定 MAXSIZE，则 MAXSIZE 将自动设置为 500 MB。  
  
- 如果 MAXSIZE 和 EDITION 均未指定，则 EDITION 设置为 Standard (S0)，MAXSIZE 设置为 250 GB。  

MODIFY (SERVICE_OBJECTIVE = \<service-objective>)  

指定性能级别。 以下示例将高级数据库的服务目标更改为 `P6`：
 
```sql  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  

指定性能级别。 服务目标的可用值包括：`S0`、`S1`、`S2`、`S3`、`S4`、`S6`、`S7`、`S9`、`S12`、`P1`、`P2`、`P4`、`P6`、`P11`、`P15`、`GP_GEN4_1`、`GP_GEN4_2`、`GP_GEN4_4`、`GP_GEN4_8`、`GP_GEN4_16`、`GP_GEN4_24`、`BC_GEN4_1`、`BC_GEN4_2`、`BC_GEN4_4`、`BC_GEN4_8`、`BC_GEN4_16`、`BC_GEN4_24`、`GP_Gen5_2`、`GP_Gen5_4`、`GP_Gen5_8`、`GP_Gen5_16`、`GP_Gen5_24`、`GP_Gen5_32`、`GP_Gen5_48`、`GP_Gen5_80`、`BC_Gen5_2`、`BC_Gen5_4`、`BC_Gen5_8`、`BC_Gen5_16`、`BC_Gen5_24`、`BC_Gen5_32`、`BC_Gen5_48`、`BC_Gen5_80`。  

有关服务目标说明以及大小、版本和服务目标组合的详细信息，请参阅 [Azure SQL 数据库服务层和性能级别](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)、[基于 DTU 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)和[基于 vCore 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)。 删除了对 PRS 服务目标的支持。 如有问题，请使用此电子邮件别名：premium-rs@microsoft.com。 
  
MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>)  

若要向弹性池中添加现有数据库，请将数据库的 SERVICE_OBJECTIVE 设置为 ELASTIC_POOL，并提供弹性池的名称。 还可以使用此选项将数据库更改为相同服务器中的不同弹性池。 有关详细信息，请参阅[弹性池有助于管理和缩放多个 Azure SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)。 若要从弹性池中删除数据库，请使用 ALTER DATABASE 将 SERVICE_OBJECTIVE 设置为单个数据库性能级别。  

ADD SECONDARY ON SERVER \<partner_server_name>  

在伙伴服务器上创建具有相同名称的异地复制辅助数据库（使本地数据库进入异地复制主数据库），并开始将数据从主数据库异步复制到新的辅助数据库。 如果辅助数据库上已存在同名的数据库，则命令会失败。 命令会对承载的本地数据库会成为主数据库的服务器上的 master 数据库执行。  
  
WITH ALLOW_CONNECTIONS { ALL | NO }  

未指定 ALLOW_CONNECTIONS 时，它在默认情况下会设置为 ALL。 如果它设置为 ALL，则是允许拥有适当权限的所有登录名进行连接的只读数据库。  
  
WITH SERVICE_OBJECTIVE {  `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`,    `GP_Gen5_8`,    `GP_Gen5_16`,   `GP_Gen5_24`,   `GP_Gen5_32`,   `GP_Gen5_48`,   `GP_Gen5_80`, `BC_Gen5_2`,  `BC_Gen5_4`,    `BC_Gen5_8`,    `BC_Gen5_16`,   `BC_Gen5_24`,   `BC_Gen5_32`,   `BC_Gen5_48`,   `BC_Gen5_80` }  

未指定 SERVICE_OBJECTIVE 时，会在与主数据库相同的服务级别上创建辅助数据库。 指定了 SERVICE_OBJECTIVE 时，会在指定级别上创建辅助数据库。 此选项支持使用成本较低的服务级别创建异地复制辅助数据库。 指定的 SERVICE_OBJECTIVE 必须处于与源相同的版本中。 例如，如果版本是高级版本，则无法指定 S0。  
  
ELASTIC_POOL (name = \<elastic_pool_name)  

未指定 ELASTIC_POOL 时，不会在弹性池中创建辅助数据库。 指定了 ELASTIC_POOL 时，会在指定池中创建辅助数据库。  
  
> [!IMPORTANT]  
>  执行 ADD SECONDARY 命令的用户必须是主服务器上的 DBManager，在本地数据库中拥有 db_owner 成员身份，以及是辅助服务器上的 DBManager。  
  
REMOVE SECONDARY ON SERVER  \<partner_server_name>  

删除指定服务器上的指定异地复制辅助数据库。 命令会对承载主数据库的服务器上的 master 数据库执行。  
  
> [!IMPORTANT]  
>  执行 REMOVE SECONDARY 命令的用户必须是主服务器上的 DBManager。  
  
FAILOVER  

将异地复制合作关系中对其执行命令的辅助数据库提升为主数据库，并将当前主数据库降级为新的辅助数据库。 作为此过程的一部分，异地复制模式会暂时从异步模式切换为同步模式。 在故障转移过程中：  
  
1.  主数据库停止接收新事务。  
  
2.  所有未完成的事务都刷新到辅助数据库。  
  
3.  辅助数据库成为主数据库，并开始与旧的主数据库（即新的辅助数据库）进行异步异地复制。  
  
此顺序可确保不会丢失任何数据。 切换角色期间两个数据库都不可用的时间段大约为 0-25 秒。 总操作所需时间不应超过大约一分钟。 如果在发出此命令时主数据库不可用，则此命令会失败并产生指示主数据库不可用的错误消息。 如果故障转移过程未完成，并且显示为停滞，则可以使用强制故障转移命令并接受数据丢失 — 随后，如果需要恢复丢失的数据，请调用 devops (CSS) 以恢复丢失的数据。  
  
> [!IMPORTANT]  
>  执行 FAILOVER 命令的用户必须是主服务器和辅助服务器上的 DBManager。  
  
FORCE_FAILOVER_ALLOW_DATA_LOSS  

将异地复制合作关系中对其执行命令的辅助数据库提升为主数据库，并将当前主数据库降级为新的辅助数据库。 仅当当前主数据库不再可用时，才使用此命令。 它仅在还原可用性十分关键，并且可接受丢失一些数据时用于进行灾难恢复。  
  
在强制故障转移过程中：  
  
1. 指定的辅助数据库立即成为主数据库，并开始接受新事务。  
  
2. 当原始的主数据库可以与新的主数据库重新连接时，在原始的主数据库上创建增量分布，并且原始的主数据库成为新的辅助数据库。  
  
3. 若要从旧的主数据库上的此增量备份恢复数据，用户可利用 devops/CSS。  
  
4. 如果存在其他辅助数据库，则它们会自动重新配置以成为新的主数据库的辅助数据库。 此过程是异步过程，在此过程完成之前可能会出现延迟。 在重新配置之前，辅助数据库会继续是旧的主数据库的辅助数据库。  
  
> [!IMPORTANT]  
>  执行 FORCE_FAILOVER_ALLOW_DATA_LOSS 命令的用户必须是主服务器和辅助服务器上的 DBManager。  
  
## <a name="remarks"></a>Remarks  

若要删除数据库，请使用 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)。  
若要减小数据库的大小，请使用 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
ALTER DATABASE 语句必须在自动提交模式（默认事务管理模式）下运行，且不允许用于显式或隐式事务中。  
  
清除计划缓存将导致对所有后续执行计划进行重新编译，并可能导致查询性能暂时性地突然降低。 对于计划高速缓存中每个已清除的缓存存储区，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志包含以下信息性消息：“由于某些数据库维护或重新配置操作，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 经历了 '%s' 缓存存储区(计划高速缓存的一部分)的 %d 次刷新”。 每隔五分钟，只要缓存在这段时间间隔内得到刷新，此消息就记录一次。  
  
在以下应用场景中也会刷新过程缓存：对具有默认选项的数据库运行多个查询。 然后，删除数据库。    
  
## <a name="viewing-database-information"></a>查看数据库信息  

可以使用目录视图、系统函数和系统存储过程返回有关数据库、文件和文件组的信息。  
  
## <a name="permissions"></a>Permissions  

只有服务器级主体登录名（由设置过程创建）或 `dbmanager` 数据库角色的成员可以更改数据库。  
  
> [!IMPORTANT]  
>  数据库的所有者不能更改数据库，除非他们是 `dbmanager` 角色的成员。  
  
## <a name="examples"></a>示例  
  
### <a name="a-check-the-edition-options-and-change-them"></a>A. 检查版本选项并更改它们：

```sql
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. 将数据库移动到不同的弹性池  

将现有数据库移动到名为 pool1 的池中：  
  
```sql  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>C. 添加异地复制辅助数据库  

在服务器 `secondaryserver` 上创建本地服务器上的 db1 的可读服务数据库 db1。  
  
```sql  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = ALL )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>D. 删除异地复制辅助数据库  
 
删除服务器 `secondaryserver` 上的辅助数据库 db1。  
  
```sql  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>E. 故障转移到异地复制辅助数据库  

在服务器 `secondaryserver` 上执行时，将服务器 `secondaryserver` 上的辅助数据库 db1 提升为新的主数据库。  
  
```sql  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>另请参阅
  
[CREATE DATABASE - Azure SQL 数据库](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqldbls)   
 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [系统数据库](../../relational-databases/databases/system-databases.md)  

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><a href="alter-database-transact-sql.md?view=sql-server-2016">SQL Server</a></th>
>   <th><a href="alter-database-transact-sql.md?view=azuresqldb-current">SQL 数据库<br />逻辑服务器</a></th>
>   <th><strong><em>* SQL 数据库<br />托管实例 *</em></strong></th>
>   <th><a href="alter-database-transact-sql.md?view=azure-sqldw-latest">SQL 数据<br />仓库</a></th>
>   <th><a href="alter-database-transact-sql.md?view=aps-pdw-2016">SQL Parallel<br />数据仓库</a></th>
> </tr>
> </table>

&nbsp;

# <a name="azure-sql-database-managed-instance"></a>Azure SQL 数据库托管实例

## <a name="overview"></a>概述

在 Azure SQL 数据库托管实例中，使用此语句来设置数据库选项。

由于 ALTER DATABASE 语法的篇幅较长，因此分为多篇文章。  

ALTER DATABASE  
本文提供有关设置文件和文件组选项、设置数据库选项和设置数据库兼容级别的语法和相关信息。  
  
[ALTER DATABASE 文件和文件组选项](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md?&tabs=sqldbmi)：介绍了用于从数据库中添加和删除文件和文件组以及更改文件和文件组的属性的语法和相关信息。  
  
[ALTER DATABASE SET 选项](../../t-sql/statements/alter-database-transact-sql-set-options.md?&tabs=sqldbmi)：介绍了使用 ALTER DATABASE 的 SET 选项来更改数据库属性的语法和相关信息。  
  
[ALTER DATABASE 兼容级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md?&tabs=sqldbmi)：介绍了 ALTER DATABASE 与数据库兼容级别相关的 SET 选项的语法和相关信息。  

## <a name="syntax"></a>语法 

```  
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name | CURRENT }  
{  
    <file_and_filegroup_options>  
  | SET <option_spec> [ ,...n ]  
  | SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 }   
}  
[;] 

<file_and_filegroup_options>::=  
  <add_or_modify_files>::=  
  <filespec>::=   
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  

<option_spec> ::= 
{  
    <auto_option> 
  | <change_tracking_option> 
  | <cursor_option> 
  | <db_encryption_option>  
  | <db_update_option> 
  | <db_user_access_option> 
  | <delayed_durability_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <snapshot_option>  
  | <sql_option> 
  | <target_recovery_time_option> 
  | <temporal_history_retention>  
}  

```
  
## <a name="arguments"></a>参数  

*database_name*  

要修改的数据库的名称。  
  
CURRENT  

指定应更改当前使用的数据库。  
  
## <a name="remarks"></a>Remarks  

若要删除数据库，请使用 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)。  
若要减小数据库的大小，请使用 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
ALTER DATABASE 语句必须在自动提交模式（默认事务管理模式）下运行，且不允许用于显式或隐式事务中。  
  
清除计划缓存将导致对所有后续执行计划进行重新编译，并可能导致查询性能暂时性地突然降低。 对于计划高速缓存中每个已清除的缓存存储区，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志包含以下信息性消息：“由于某些数据库维护或重新配置操作，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 经历了 '%s' 缓存存储区(计划高速缓存的一部分)的 %d 次刷新”。 每隔五分钟，只要缓存在这段时间间隔内得到刷新，此消息就记录一次。  
  
在以下应用场景中也会刷新过程缓存：对具有默认选项的数据库运行多个查询。 然后，删除数据库。    
  
## <a name="viewing-database-information"></a>查看数据库信息  

可以使用目录视图、系统函数和系统存储过程返回有关数据库、文件和文件组的信息。  
  
## <a name="permissions"></a>Permissions  

只有服务器级主体登录名（由设置过程创建）或 `dbmanager` 数据库角色的成员可以更改数据库。  
  
> [!IMPORTANT]  
>  数据库的所有者不能更改数据库，除非他们是 `dbmanager` 角色的成员。  
  
## <a name="examples"></a>示例
以下示例显示如何设置自动优化以及如何在托管实例中添加文件。

```sql
ALTER DATABASE WideWorldImporters
    SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON)

ALTER DATABASE WideWorldImporters
    ADD FILE (NAME = 'data_17')
```

## <a name="see-also"></a>另请参阅
  
[CREATE DATABASE - Azure SQL 数据库](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqldbmi)   
[DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
[SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
[EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
[sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
[sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)  [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
[sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
[系统数据库](../../relational-databases/databases/system-databases.md)  

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><a href="alter-database-transact-sql.md?view=sql-server-2016">SQL Server</a></th>
>   <th><a href="alter-database-transact-sql.md?view=azuresqldb-current">SQL 数据库<br />逻辑服务器</a></th>
>   <th><a href="alter-database-transact-sql.md?view=azuresqldb-mi-current">SQL 数据库<br />托管实例</a></th>
>   <th><strong><em>* SQL 数据<br />仓库*</em></strong></th>
>   <th><a href="alter-database-transact-sql.md?view=aps-pdw-2016">SQL Parallel<br />数据仓库</a></th>
> </tr>
> </table>

&nbsp;

# <a name="azure-sql-data-warehouse"></a>Azure SQL 数据仓库

## <a name="overview"></a>概述

为数据库修改名称、最大大小或服务对象。

## <a name="syntax"></a>语法  
  
```  
ALTER DATABASE database_name  

  MODIFY NAME = new_database_name  
| MODIFY ( <edition_option> [, ... n] )  
  
<edition_option> ::=   
      MAXSIZE = { 
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 
          | 92160 | 102400 | 153600 | 204800 | 245760 
      } GB  
      | SERVICE_OBJECTIVE = { 
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' 
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' 
          | 'DW3000' | 'DW6000' | 'DW1000c' | 'DW1500c' | 'DW2000c' 
          | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c' | 'DW7500c' 
          | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }  
```  
  
## <a name="arguments"></a>参数  
*database_name*  
指定要修改的数据库的名称。  

MODIFY NAME = new_database_name  
使用指定的名称 new_database_name 重命名数据库。  
  
MAXSIZE  
默认为 245,760 GB (240 TB)。  

适用于：“已针对弹性进行优化”性能层

允许的最大数据库大小。 数据库大小不能超出 MAXSIZE。 

适用于：“已针对计算进行优化”性能层

数据库中允许的最大行存储数据大小。 存储在行存储表中的数据、列存储索引的增量存储或非聚集索引（聚集在列存储索引上）都不可超过 MAXSIZE。  压缩到列存储格式的数据没有大小限制，不受 MAXSIZE 约束。 
  
SERVICE_OBJECTIVE  
指定性能级别。 有关 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 的服务目标的详细信息，请参阅[性能层](https://azure.microsoft.com/documentation/articles/performance-tiers/)。  
  
## <a name="permissions"></a>Permissions  
需要以下权限：  
  
- 服务器级别主体登录名（由预配进程创建），或者  
- `dbmanager` 数据库角色的成员。  
  
数据库的所有者不能更改数据库，除非该所有者是 `dbmanager` 角色的成员。  
  
## <a name="general-remarks"></a>一般备注  
当前数据库必须不同于你正在更改的数据库，因此连接到 master 数据库之后必须运行 ALTER。  
  
SQL 数据仓库设置为 COMPATIBILITY_LEVEL 130，且不得更改。 有关详细信息，请参阅[在 Azure SQL 数据库中通过兼容性级别 130 优化查询性能](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)。
  
若要减小数据库的大小，请使用 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
要运行 ALTER DATABASE，数据库必须处于联机且非暂停状态。  
  
必须在自动提交模式（默认事务管理模式）下运行 ALTER DATABASE 语句。 此操作在连接设置中进行设置。  
  
ALTER DATABASE 不能是用户定义的事务的一部分。

不可更改数据库排序规则。  
  
## <a name="examples"></a>示例  
在运行这些示例之前，请确保所更改的数据库不是当前数据库。 当前数据库必须不同于你正在更改的数据库，因此连接到 master 数据库之后必须运行 ALTER。  

### <a name="a-change-the-name-of-the-database"></a>A. 更改数据库的名称  

```sql  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>B. 更改数据库的最大大小  
  
```sql  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>C. 更改性能级别  
  
```sql  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>D. 更改最大大小和性能级别  
  
```sql  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>另请参阅  
[CREATE DATABASE（Azure SQL 数据仓库）](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqldw.md)
[参考文章的 SQL 数据仓库列表](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-reference/) 
 
::: moniker-end
::: moniker range="=aps-pdw-2016||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><a href="alter-database-transact-sql.md?view=sql-server-2016">SQL Server</a></th>
>   <th><a href="alter-database-transact-sql.md?view=azuresqldb-current">SQL 数据库<br />逻辑服务器</a></th>
>   <th><a href="alter-database-transact-sql.md?view=azuresqldb-mi-current">SQL 数据库<br />托管实例</a></th>
>   <th><a href="alter-database-transact-sql.md?view=azure-sqldw-latest">SQL 数据<br />仓库</a></th>
>   <th><strong><em>* SQL Parallel<br />数据仓库*</em></strong></th>
> </tr>
> </table>

&nbsp;

# <a name="sql-parallel-data-warehouse"></a>SQL 并行数据仓库

## <a name="overview"></a>概述

修改并行数据仓库中复制表、分布式表和事务日志的最大数据库大小选项。 使用此语句可在数据库大小增长或收缩时管理数据库的磁盘空间分配。 本文还介绍与并行数据仓库中设置数据库选项相关的语法。

## <a name="syntax"></a>语法  
  
```  
-- Parallel Data Warehouse  
ALTER DATABASE database_name    
    SET ( <set_database_options>   | <db_encryption_option> )  
[;]  
  
<set_database_options> ::=   
{  
    AUTOGROW = { ON | OFF }  
    | REPLICATED_SIZE = size [GB]  
    | DISTRIBUTED_SIZE = size [GB]  
    | LOG_SIZE = size [GB]
    | SET AUTO_CREATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS { ON | OFF } 
    | SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
```  
  
## <a name="arguments"></a>参数  
*database_name*  
要修改的数据库的名称。 要在设备上显示数据库列表，请使用 [sys.databases (Transact SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。  
  
AUTOGROW = { ON | OFF }  
更新 AUTOGROW 选项。 当 AUTOGROW 为 ON 时，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 根据需要自动为复制表、分布式表和事务日志增大分配空间，以适应存储需求的增长。 当 AUTOGROW 为 OFF 时，如果复制表、分布式表或事务日志超出最大大小设置，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 会返回一个错误。  
  
REPLICATED_SIZE = size [GB]  
指定每个计算节点的新最大 GB 数，以便存储要更改的数据库中的所有复制表。 如果正在计划设备存储空间，需要用 REPLICATED_SIZE 乘以设备中的计算节点数。  
  
DISTRIBUTED_SIZE = size [GB]  
指定每个数据库的新的最大 GB 数，以便存储要更改的数据库中的所有分布式表。 该大小分布到设备的所有计算节点中。  
  
LOG_SIZE = size [GB]  
指定每个数据库的新的最大 GB 数，以便存储要更改的数据库中的所有事务日志。 该大小分布到设备的所有计算节点中。  
  
ENCRYPTION { ON | OFF }  
将数据库设置为加密的 (ON) 或未加密的 (OFF)。 只能在 [sp_pdw_database_encryption](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md) 已设置为 **1** 时为 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 配置加密。 必须先创建数据库加密密钥，然后才能配置透明数据加密。 有关数据库加密的详细信息，请参阅[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)。  

SET AUTO_CREATE_STATISTICS { ON | OFF } 在自动创建统计信息选项 AUTO_CREATE_STATISTICS 为 ON 时，查询优化器将根据需要在查询谓词中的单独列上创建统计信息，以便改进查询计划的基数估计。 这些单列统计信息在现有统计信息对象中尚未具有直方图的列上创建。

升级到 AU7 后创建的新数据库的默认值为 ON。 升级前创建的数据库的默认值为 OFF。 

有关统计信息的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)

SET AUTO_UPDATE_STATISTICS { ON | OFF } 在自动更新统计信息选项 AUTO_UPDATE_STATISTICS 为 ON 时，查询优化器将确定统计信息何时可能过期，然后在查询使用这些统计信息时更新它们。 统计信息将在插入、更新、删除或合并操作更改表或索引视图中的数据分布后过期。 查询优化器通过计算自最后统计信息更新后数据修改的次数并且将这一修改次数与某一阈值进行比较，确定统计信息何时可能过期。 该阈值基于表中或索引视图中的行数。

升级到 AU7 后创建的新数据库的默认值为 ON。 升级前创建的数据库的默认值为 OFF。 

有关统计信息的详细信息，请参阅[统计信息](../../relational-databases/statistics/statistics.md)。


SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF } 异步统计信息更新选项 AUTO_UPDATE_STATISTICS_ASYNC 将确定查询优化器是使用同步统计信息更新还是异步统计信息更新。 AUTO_UPDATE_STATISTICS_ASYNC 选项适用于为索引创建的统计信息对象、查询谓词中的单列以及使用 CREATE STATISTICS 语句创建的统计信息。

升级到 AU7 后创建的新数据库的默认值为 ON。 升级前创建的数据库的默认值为 OFF。 

有关统计信息的详细信息，请参阅[统计信息](/sql/relational-databases/statistics/statistics)。

## <a name="permissions"></a>Permissions  
需要具有针对数据库的 ALTER 权限。  
  
## <a name="error-messages"></a>错误消息
如果“自动统计信息”功能被禁用，而你尝试更改统计信息设置，则 PDW 会给出错误“PDW 中不支持此选项”。 系统管理员可通过启用功能开关 [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md) 来启用“自动统计信息”功能。

## <a name="general-remarks"></a>一般备注  
REPLICATED_SIZE、DISTRIBUTED_SIZE 和 LOG_SIZE 的值可以大于、等于或小于数据库的当前值。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
增长和收缩操作是近似的。 所得到的实际大小可能因大小参数而异。  
  
[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 不会将 ALTER DATABASE 语句作为原子操作执行。 如果在执行期间中止该语句，将保持已发生的更改。  

统计信息设置只有在管理员已启用“自动统计信息”功能时才可工作。管理员可使用功能开关 [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md) 启用或禁用“自动统计信息”功能。 
  
## <a name="locking-behavior"></a>锁定行为  
在 DATABASE 对象上采用共享锁。 无法更改另个用户正在读取或写入的数据库。 这包括已在数据库上发出 [USE](../language-elements/use-transact-sql.md) 语句的会话。  
  
## <a name="performance"></a>“性能”  
收缩数据库可能需要大量时间和系统资源，具体取决于数据库中的实际数据大小和磁盘上的碎片量。 例如，收缩数据库可能需要几个小时或更长时间。  
  
## <a name="determining-encryption-progress"></a>确定加密进度  
可使用以下查询来确定数据库透明数据加密进度的百分比：  
  
```sql  
WITH  
database_dek AS (  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,  
        dek.encryption_state, dek.percent_complete,  
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,  
        type  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
        ON dek.database_id = node_db_map.database_id   
        AND dek.pdw_node_id = node_db_map.pdw_node_id  
    LEFT JOIN sys.pdw_database_mappings AS db_map  
        ON node_db_map .physical_name = db_map.physical_name  
    INNER JOIN sys.dm_pdw_nodes nodes  
        ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
),  
dek_percent_complete AS (  
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete  
    FROM database_dek  
    WHERE type = 'COMPUTE'  
    GROUP BY database_dek.database_id  
)  
SELECT DB_NAME( database_dek.database_id ) AS name,  
    database_dek.database_id,  
    ISNULL(  
       (SELECT TOP 1 dek_encryption_state.encryption_state  
        FROM database_dek AS dek_encryption_state  
        WHERE dek_encryption_state.database_id = database_dek.database_id  
        ORDER BY (CASE encryption_state  
            WHEN 3 THEN -1  
            ELSE encryption_state  
            END) DESC), 0)  
        AS encryption_state,  
dek_percent_complete.percent_complete,  
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint  
FROM database_dek  
INNER JOIN dek_percent_complete   
    ON dek_percent_complete.database_id = database_dek.database_id  
WHERE type = 'CONTROL';  
```  
  
有关演示实现 TDE 的所有步骤的完整示例，请参阅[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)。  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. 更改 AUTOGROW 设置  
将数据库 `CustomerSales` 的 AUTOGROW 设置为 ON。  
  
```sql  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. 更改复制表的最大存储  
下面的示例将数据库 `CustomerSales` 的复制表存储限制设置为 1 GB。 这是每个计算节点的存储限制。  
  
```sql  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. 更改分布式表的最大存储  
 下面的示例将数据库 `CustomerSales` 的分布式表存储限制设置为 1000 GB (1 TB)。 这是设备上所有计算节点的组合存储限制，而不是每个计算节点的存储限制。  
  
```sql  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. 更改事务日志的最大存储  
 下面的示例更新数据库 `CustomerSales`使设备的最大 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事务日志大小为 10 GB。  
  
```sql  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  

### <a name="e-check-for-current-statistics-values"></a>E. 检查当前的统计信息值

以下查询返回所有数据库的当前统计信息值。 值 1 表示功能处于开启状态，而 0 表示功能处于关闭状态。

```sql
SELECT NAME,
    is_auto_create_stats_on,
    is_auto_update_stats_on,
    is_auto_update_stats_async_on
FROM sys.databases;
```
### <a name="f-enable-auto-create-and-auto-update-stats-for-a-database"></a>F. 为数据库实现自动创建和自动更新统计信息
使用以下语句可为数据库 CustomerSales 自动且异步地创建和更新统计信息。  这将根据需要创建和更新单列统计信息，从而创建高质量的查询计划。

```sql
ALTER DATABASE CustomerSales
    SET AUTO_CREATE_STATISTICS ON;
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS ON; 
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS_ASYNC ON;
```
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE（并行数据仓库）](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlpdw)   
 [DROP DATABASE (Transact SQL)](../../t-sql/statements/drop-database-transact-sql.md)  

::: moniker-end
