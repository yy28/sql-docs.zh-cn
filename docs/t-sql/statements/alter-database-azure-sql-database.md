---
title: "ALTER DATABASE （Azure SQL 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 02/13/2018
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6fc5fd95-2045-4f20-a914-3598091bc7cc
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 80aa017e3876a7a41077f770d5328e4c6c49b5be
ms.sourcegitcommit: aebbfe029badadfd18c46d5cd6456ea861a4e86d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="alter-database-azure-sql-database"></a>ALTER DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  修改[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 更改的一个数据库、 联接弹性池，以及设置数据库选项的数据库、 版本和服务目标的名称。  
  
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
    | EDITION = { 'basic' | 'standard' | 'premium' }   
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
                 | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15' }

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
  
<delayed_durability_option> ::=    DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }  
  
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
  
 有关这些 set 选项的完整说明，请参阅[ALTER DATABASE SET 选项 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)和[ALTER DATABASE 兼容级别 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="arguments"></a>参数  
 *database_name*  
 要修改的数据库的名称。  
  
 CURRENT  
 指定应更改当前使用的数据库。  
  
 MODIFY NAME **=***new_database_name*  
 重命名数据库名称指定为*new_database_name*。 下面的示例更改数据库的名称`db1`到`db2`:   

```  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

 修改 (版本 **=**  [基本 |标准 |高级]）    
 更改数据库的服务层。 删除了对 premiumrs 支持。 如有问题，使用此电子邮件别名： premium-rs@microsoft.com。

下面的示例更改版本到`premium`:
  
```  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

如果数据库的 MAXSIZE 属性设置为的值超出了该版本支持的有效范围，版本进行的更改将失败。  

 MODIFY (MAXSIZE **=** [100 MB | 500 MB | 1 | 1024…4096] GB)  
 指定数据库的最大大小。 该最大大小必须符合针对数据库的 EDITION 属性的有效值集。 更改数据库的最大大小可能导致更改数据库 EDITION。 下表列出 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务层支持的 MAXSIZE 值和默认值 (D)。  
  
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
|从 1024 GB 达 4096 GB 的增量的 256 GB *|N/A|N/A|N/A|N/A|√|√|  
  
 \* P11 和 P15 允许 MAXSIZE 达 4 TB 1024 gb 正在默认大小。  P11 和 P15 可以使用 4 TB 的包含存储，并且不额外收费。 在高级层中，最大大小大于 1 TB 是当前在以下区域中提供： 美国 East2、 美国西部、 US Gov Virginia、 西欧、 德国中央、 南部亚洲东部、 日本东部、 澳大利亚东部、 加拿大中央和加拿大东部。 当前限制，请参阅[单一数据库](https://docs.microsoft.com/azure/sql-database-single-database-resources)。  

  
 以下规则适用于 MAXSIZE 和 EDITION 参数：  
  
-   MAXSIZE 值，如果指定，必须是有效的值与上表中所示。  
  
-   如果指定了 EDITION 但未指定 MAXSIZE，使用版本的默认值。 例如，如果 EDITION 设置为 Standard 并且未指定 MAXSIZE，则 MAXSIZE 将自动设置为 500 MB。  
  
-   如果 MAXSIZE 和 EDITION 均未指定，则版本设置为标准 (S0)，并最大大小设置为 250 GB。  
 

 MODIFY (SERVICE_OBJECTIVE = \<service-objective>)  
 指定性能级别。 下面的示例更改服务的高级数据库到目标`P6`:
 
```  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  
 服务目标的可用值有： `S0`， `S1`， `S2`， `S3`， `S4`， `S6`， `S7`， `S9`， `S12`， `P1`， `P2`，`P4`， `P6`， `P11`，或`P15`。 服务目标说明和有关大小、 版本，以及服务目标组合的详细信息，请参阅[Azure SQL 数据库服务层和性能级别](http://msdn.microsoft.com/library/azure/dn741336.aspx)。 如果版本不支持指定的 SERVICE_OBJECTIVE，你将收到错误。 若要将 SERVICE_OBJECTIVE 值从一层更改为另一层（例如从 S1 更改为 P1），还必须更改 EDITION 值。 删除了的 PR 服务目标的支持。 如有问题，使用此电子邮件别名： premium-rs@microsoft.com。 
  
 MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>)  
 若要将现有数据库添加到弹性池，设置数据库的 SERVICE_OBJECTIVE 为 ELASTIC_POOL 并提供弹性池的名称。 你可以使用此选项以将数据库更改到同一服务器内的不同弹性池。 有关详细信息，请参阅[创建和管理 SQL 数据库弹性池](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)。 若要从弹性池删除数据库，请使用 ALTER DATABASE 设置 SERVICE_OBJECTIVE 到单个数据库的性能级别。  

 添加辅助 ON SERVER \<partner_server_name >  
 具有相同名称在伙伴服务器上，使主，到异地复制的本地数据库创建异地复制辅助数据库并开始以异步方式将数据从主复制到新的辅助数据库。 如果辅助副本上已存在具有相同名称的数据库，该命令将失败。 在托管本地数据库成为主服务器上的主数据库上执行该命令。  
  
 与 ALLOW_CONNECTIONS {所有 |**否**}  
 如果未指定 ALLOW_CONNECTIONS，则将它设置为否默认情况下。 如果它将所有设置，则允许有连接的适当权限的所有登录名的只读数据库。  
  
 与 SERVICE_OBJECTIVE {S0 |S1 |S2 |S3"|S4 |S6 |S7 |S9 |S12 |P1 |P2 |P4 |P6 |P11 |P15}  
 如果未指定 SERVICE_OBJECTIVE，在与主数据库相同的服务级别创建辅助数据库。 当指定 SERVICE_OBJECTIVE 时，在指定的级别创建辅助数据库。 此选项支持使用成本较低的服务级别创建异地复制的辅助数据库。 指定 SERVICE_OBJECTIVE 必须位于与源相同的版本。 例如，如果版本是高级无法指定 S0。  
  
 ELASTIC_POOL (name = \<elastic_pool_name)  
 如果未指定 ELASTIC_POOL，在弹性池中不创建辅助数据库。 当指定 ELASTIC_POOL 时，在指定的池中创建辅助数据库。  
  
> [!IMPORTANT]  
>  执行添加辅助数据库的命令的用户必须是主服务器上的 DBManager，拥有在本地数据库和 DBManager 辅助服务器上的 db_owner 成员身份。  
  
 删除辅助 ON SERVER \<partner_server_name >  
 删除指定的服务器上的指定的异地复制辅助数据库。 承载主数据库的服务器上的主数据库上执行该命令。  
  
> [!IMPORTANT]  
>  执行删除辅助命令的用户必须是主服务器上的 DBManager。  
  
 FAILOVER  
 提升辅助数据库在其执行该命令是为主，将降级当前主副本成为新的辅助数据库的异地复制合作关系中。 作为此过程的一部分，异地复制模式已暂时从异步模式切换到同步模式。 在故障转移过程中：  
  
1.  主停止采用新事务。  
  
2.  所有未完成事务刷新到辅助数据库。  
  
3.  辅助数据库将成为主并开始使用旧的主数据库异步异地复制 / 新的辅助数据库。  
  
 此顺序可确保不会丢失任何数据。 切换角色时，在此期间，这两个数据库都不可用则周期是时间大约为 0-25 秒。 应执行总操作不超过大约一分钟。 如果发出此命令时，主数据库不可用，则命令将失败错误消息，指出，主数据库不可用。 如果故障转移过程未完成，并且显示停滞，你可以使用强制故障转移命令和接受数据丢失的如果你需要恢复丢失的数据，然后，调用 devops (CSS) 以恢复丢失的数据。  
  
> [!IMPORTANT]  
>  执行故障转移命令的用户必须是主服务器和辅助服务器上的 DBManager。  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 提升辅助数据库在其执行该命令是为主，将降级当前主副本成为新的辅助数据库的异地复制合作关系中。 仅当当前主副本不再可用时，请使用此命令。 它专为仅，灾难恢复时还原可用性十分重要，也丢失某些数据是可接受。  
  
 在强制故障转移：  
  
1.  指定的辅助数据库将立即成为主数据库，并开始接受新事务。  
  
2.  当与新的主情况下，原始主副本可以重新连接时，创建增量备份是在原始主，并且原始主副本将成为新的辅助数据库。  
  
3.  若要从旧的主计算机上此增量备份中恢复数据，用户将参与 devops/CSS。  
  
4.  如果有其他辅助副本，自动重新配置它们成为新的主副本的辅助副本。 此过程是异步的此过程完成之前可能会出现延迟。 直到完成重新配置后，辅助副本仍是旧的主数据库的辅助副本。  
  
> [!IMPORTANT]  
>  执行 FORCE_FAILOVER_ALLOW_DATA_LOSS 命令的用户必须是主服务器和辅助服务器上的 DBManager。  
  
## <a name="remarks"></a>注释  
 若要删除数据库，使用[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)。  
  
 若要减小数据库大小，使用[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
 ALTER DATABASE 语句必须在自动提交模式（默认事务管理模式）下运行，且不允许用于显式或隐式事务中。  
  
 清除计划缓存将导致对所有后续执行计划进行重新编译，并可能导致查询性能暂时性地突然降低。 对于计划高速缓存中每个已清除的缓存存储区，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志包含以下信息性消息：“由于某些数据库维护或重新配置操作，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 经历了 '%s' 缓存存储区(计划高速缓存的一部分)的 %d 次刷新”。 每隔五分钟，只要缓存在这段时间间隔内得到刷新，此消息就记录一次。  
  
 在下列情况下，也会刷新过程缓存：  
  
-   数据库的 AUTO_CLOSE 数据库选项设置为 ON。 在没有用户连接引用或使用该数据库时，后台任务将尝试关闭并自动关闭数据库。  
  
-   针对具有默认选项的数据库运行多个查询。 然后，删除数据库。  
  
-   您已成功重新生成数据库的事务日志。  
  
-   还原数据库备份。  
  
-   分离数据库。  
  
## <a name="viewing-database-information"></a>查看数据库信息  
 可以使用目录视图、系统函数和系统存储过程返回有关数据库、文件和文件组的信息。  
  
## <a name="permissions"></a>权限  
 只有服务器级主体登录名（由设置过程创建）或 `dbmanager` 数据库角色的成员可以更改数据库。  
  
> [!IMPORTANT]  
>  数据库的所有者不能更改数据库，除非他们是 `dbmanager` 角色的成员。  
  
## <a name="examples"></a>示例  
  
### <a name="a-check-the-edition-options-and-change-them"></a>A. 检查版本选项并将其更改：

```
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>B. 将数据库移到不同的弹性池  
 将现有数据库移到名为 pool1 池：  
  
```  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>C. 添加异地复制辅助  
 在服务器上创建非可读辅助数据库 db1`secondaryserver`的本地服务器上 db1。  
  
```  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = NO )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>D. 删除异地复制辅助数据库  
 删除服务器上的辅助数据库 db1 `secondaryserver`。  
  
```  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>E. 故障转移到异地复制辅助数据库  
 将升级服务器上的辅助数据库 db1`secondaryserver`成为新的主数据库服务器上执行时`secondaryserver`。  
  
```  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建数据库 &#40;Azure SQL Database &#41;](../../t-sql/statements/create-database-azure-sql-database.md)   
 [DATABASEPROPERTYEX (Transact-SQL)](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE (Transact SQL)](../../t-sql/statements/drop-database-transact-sql.md)   
 [将事务隔离级别设置 &#40;Transact SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.data_spaces &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [系统数据库](../../relational-databases/databases/system-databases.md)  
  
  
