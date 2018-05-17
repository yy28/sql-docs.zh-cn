---
title: ALTER DATABASE（Azure SQL 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: 37
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: c275770e6bbf7579d3d9f02a21937d22a2a66dfa
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  修改 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 更改数据库的名称、数据库的版本和服务目标、联接弹性池以及设置数据库选项。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name }  
{  
    MODIFY NAME = new_database_name  
  | MODIFY ( <edition_options> [, ... n] ) 
  | SET { <option_spec> [ ,... n ] } 
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
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' 
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 
      }

```  
  
```
-- SET OPTIONS AVAILABLE FOR SQL Database  
-- Full descriptions of the set options are available in the topic 
-- ALTER DATABASE SET Options. The supported syntax is listed here.  

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
  
<auto_option> ::= 
{  
    AUTO_CREATE_STATISTICS { OFF | ON [ ( INCREMENTAL = { ON | OFF } ) ] } 
  | AUTO_SHRINK { ON | OFF } 
  | AUTO_UPDATE_STATISTICS { ON | OFF } 
  | AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }  
}  

<change_tracking_option> ::=  
{  
  CHANGE_TRACKING 
   { 
       = OFF  
     | = ON [ ( <change_tracking_option_list > [,...n] ) ] 
     | ( <change_tracking_option_list> [,...n] )  
   }  
}  

   <change_tracking_option_list> ::=  
   {  
       AUTO_CLEANUP = { ON | OFF } 
     | CHANGE_RETENTION = retention_period { DAYS | HOURS | MINUTES }  
   }  

<cursor_option> ::= 
{  
    CURSOR_CLOSE_ON_COMMIT { ON | OFF } 
}  
  
<db_encryption_option> ::=  
  ENCRYPTION { ON | OFF }  
  
<db_update_option> ::=  
  { READ_ONLY | READ_WRITE }  
  
<db_user_access_option> ::=  
  { RESTRICTED_USER | MULTI_USER }  
  
<delayed_durability_option> ::=  DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
<parameterization_option> ::=  
  PARAMETERIZATION { SIMPLE | FORCED }  
  
<query_store_options> ::=  
{  
  QUERY_STORE 
  {  
    = OFF 
    | = ON [ ( <query_store_option_list> [,... n] ) ]  
    | ( < query_store_option_list> [,... n] )  
    | CLEAR [ ALL ]  
  }  
} 
  
<query_store_option_list> ::=  
{  
  OPERATION_MODE = { READ_WRITE | READ_ONLY } 
  | CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = number )  
  | DATA_FLUSH_INTERVAL_SECONDS = number 
  | MAX_STORAGE_SIZE_MB = number 
  | INTERVAL_LENGTH_MINUTES = number 
  | SIZE_BASED_CLEANUP_MODE = [ AUTO | OFF ]  
  | QUERY_CAPTURE_MODE = [ ALL | AUTO | NONE ]  
  | MAX_PLANS_PER_QUERY = number  
}  
  
<snapshot_option> ::=  
{  
    ALLOW_SNAPSHOT_ISOLATION { ON | OFF }  
  | READ_COMMITTED_SNAPSHOT {ON | OFF }  
  | MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT {ON | OFF }  
}  
<sql_option> ::= 
{  
    ANSI_NULL_DEFAULT { ON | OFF }   
  | ANSI_NULLS { ON | OFF }   
  | ANSI_PADDING { ON | OFF }   
  | ANSI_WARNINGS { ON | OFF }   
  | ARITHABORT { ON | OFF }   
  | COMPATIBILITY_LEVEL = { 100 | 110 | 120 | 130 | 140 }  
  | CONCAT_NULL_YIELDS_NULL { ON | OFF }   
  | NUMERIC_ROUNDABORT { ON | OFF }   
  | QUOTED_IDENTIFIER { ON | OFF }   
  | RECURSIVE_TRIGGERS { ON | OFF }   
}  
  
<termination>  ::=   
{  
    ROLLBACK AFTER integer [ SECONDS ]   
  | ROLLBACK IMMEDIATE   
  | NO_WAIT  
}  

<temporal_history_retention>  ::=  TEMPORAL_HISTORY_RETENTION { ON | OFF }
```  
  
 有关这些设置选项的完整说明，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md) 和 [ALTER DATABASE 兼容级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
## <a name="arguments"></a>参数  

*database_name*  

要修改的数据库的名称。  
  
CURRENT  

指定应更改当前使用的数据库。  
  
MODIFY NAME *=***new_database_name  

使用指定的名称 new_database_name 重命名数据库。 以下示例将 `db1` 数据库的名称更改为 `db2`：   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

MODIFY (EDITION = ['basic' | 'standard' | 'premium' |'GeneralPurpose' | 'BusinessCritical'])    

更改数据库的服务层。 已删除对“premiumrs”的支持。 如有问题，请使用此电子邮件别名：premium-rs@microsoft.com。

以下示例将版本更改为 `premium`：
  
```  
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

**常规用途服务层**

|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_4|GP_Gen4_8|GP_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|最大数据大小 (GB)|1024|1024|1536|3072|4096|

**业务关键型服务层**

|性能级别|BC_Gen4_1|BC_Gen4_2|BC_Gen4_4|BC_Gen4_8|BC_Gen4_16|
|:--- | --: |--: |--: |--: |--: |
|最大数据大小 (GB)|1024|1024|1536|2048|2048|

如果使用 vCore 模型时未设置 `MAXSIZE` 值，则默认为 32 GB。 有关基于 vCore 的模型的资源限制的其他详细信息，请参阅[基于 vCore 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)。
  
以下规则适用于 MAXSIZE 和 EDITION 参数：  
  
- 如果指定了 EDITION 但未指定 MAXSIZE，则使用版本的默认值。 例如，如果 EDITION 设置为 Standard 并且未指定 MAXSIZE，则 MAXSIZE 将自动设置为 500 MB。  
  
- 如果 MAXSIZE 和 EDITION 均未指定，则 EDITION 设置为 Standard (S0)，MAXSIZE 设置为 250 GB。  

MODIFY (SERVICE_OBJECTIVE = \<service-objective>)  

指定性能级别。 以下示例将高级数据库的服务目标更改为 `P6`：
 
```sql  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  

指定性能级别。 服务目标的可用值包括：`S0`、`S1`、`S2`、`S3`、`S4`、`S6`、`S7`、`S9`、`S12`、`P1`、`P2`、`P4`、`P6`、`P11`、`P15`、`GP_GEN4_1`、`GP_GEN4_2`、`GP_GEN4_4`、`GP_GEN4_8`、`GP_GEN4_16`、`BC_GEN4_1`、`BC_GEN4_2`、`BC_GEN4_4`、`BC_GEN4_8`、`BC_GEN4_16`。 

有关服务目标说明以及大小、版本和服务目标组合的详细信息，请参阅 [Azure SQL 数据库服务层和性能级别](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)、[基于 DTU 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)和[基于 vCore 的资源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits)。 删除了对 PRS 服务目标的支持。 如有问题，请使用此电子邮件别名：premium-rs@microsoft.com。 
  
MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>)  

若要向弹性池中添加现有数据库，请将数据库的 SERVICE_OBJECTIVE 设置为 ELASTIC_POOL，并提供弹性池的名称。 还可以使用此选项将数据库更改为相同服务器中的不同弹性池。 有关详细信息，请参阅[弹性池有助于管理和缩放多个 Azure SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)。 若要从弹性池中删除数据库，请使用 ALTER DATABASE 将 SERVICE_OBJECTIVE 设置为单个数据库性能级别。  

ADD SECONDARY ON SERVER \<partner_server_name>  

在伙伴服务器上创建具有相同名称的异地复制辅助数据库（使本地数据库进入异地复制主数据库），并开始将数据从主数据库异步复制到新的辅助数据库。 如果辅助数据库上已存在同名的数据库，则命令会失败。 命令会对承载的本地数据库会成为主数据库的服务器上的 master 数据库执行。  
  
WITH ALLOW_CONNECTIONS { ALL | NO }  

未指定 ALLOW_CONNECTIONS 时，它在默认情况下会设置为 ALL。 如果它设置为 ALL，则是允许拥有适当权限的所有登录名进行连接的只读数据库。  
  
WITH SERVICE_OBJECTIVE {  `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16` }  

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
  
在下列情况下，也会刷新过程缓存：  
  
- 数据库的 AUTO_CLOSE 数据库选项设置为 ON。 在没有用户连接引用或使用该数据库时，后台任务将尝试关闭并自动关闭数据库。  
  
- 针对具有默认选项的数据库运行多个查询。 然后，删除数据库。  
  
- 您已成功重新生成数据库的事务日志。  
  
- 还原数据库备份。  
  
- 分离数据库。  
  
## <a name="viewing-database-information"></a>查看数据库信息  

可以使用目录视图、系统函数和系统存储过程返回有关数据库、文件和文件组的信息。  
  
## <a name="permissions"></a>权限  

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
  
[CREATE DATABASE - Azure SQL 数据库](../../t-sql/statements/create-database-azure-sql-database.md)   
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
  
  
