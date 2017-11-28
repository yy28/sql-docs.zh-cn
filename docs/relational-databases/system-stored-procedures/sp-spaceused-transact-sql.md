---
title: "sp_spaceused (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_spaceused_TSQL
- sp_spaceused
dev_langs: TSQL
helpviewer_keywords: sp_spaceused
ms.assetid: c6253b48-29f5-4371-bfcd-3ef404060621
caps.latest.revision: "62"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2ed6f3bfcb2e034dd782ed477ebcd75e9a43a483
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spspaceused-transact-sql"></a>sp_spaceused (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  显示行数、保留的磁盘空间以及当前数据库中的表、索引视图或 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 队列所使用的磁盘空间，或显示由整个数据库保留和使用的磁盘空间。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_spaceused [[ @objname = ] 'objname' ]   
[, [ @updateusage = ] 'updateusage' ]  
[, [ @mode = ] 'mode' ]  
[, [ @oneresultset = ] oneresultset ]  
[, [ @include_total_xtp_storage = ] include_total_xtp_storage ]
```  
  
## <a name="arguments"></a>参数  

有关[!INCLUDE[sssdw-md](../../includes/sssdw-md.md)]，`sp_spacedused`必须指定命名的参数 (例如`sp_spacedused (@objname= N'Table1');`而不依赖于参数的序号位置。 

 [  **@objname=**] *objname* 
   
 请求其空间使用信息的表、索引视图或队列的限定或非限定名称。 仅当指定限定对象名称时，才需要使用引号。 如果提供完全限定对象名称（包括数据库名称），则数据库名称必须是当前数据库的名称。  
如果*objname*未指定，则为整个数据库返回结果。  
*objname*是**nvarchar(776)**，默认值为 NULL。  
> [!NOTE]  
> [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)]和[!INCLUDE[sspdw-md](../../includes/sspdw-md.md)]仅支持数据库和表对象。
  
 [  **@updateusage=**] *updateusage*  
 指示应运行 DBCC UPDATEUSAGE 以更新空间使用信息。 当*objname*是未指定，在整个数据库上运行该语句; 否则，运行该语句*objname*。 值可以是**true**或**false**。 *updateusage*是**varchar(5)**，默认值为**false**。  
  
 [  **@mode=**] *模式*  
 指示结果的范围。 为延伸的表或数据库，*模式*参数允许你包括或排除的对象的远程部分。 有关详细信息，请参阅 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)。  
  
 *模式*自变量可以具有下列值：  
  
|值|Description|  
|-----------|-----------------|  
|ALL|返回对象或数据库中包括的本地部分和远程部分的存储统计的信息。|  
|LOCAL_ONLY|返回仅对象或数据库的本地部分的存储统计信息。 如果对象或数据库不是已启用延伸的返回相同的统计信息与何时@mode= ALL。|  
|REMOTE_ONLY|返回仅对象或数据库的远程部分的存储统计信息。 当满足以下条件之一时，此选项将引发错误：<br /><br /> 未启用延伸的表。<br /><br /> 为表启用 Stretch，但您从未启用数据迁移。 在这种情况下，远程表还没有架构。<br /><br /> 用户已手动删除远程表。<br /><br /> 远程数据存档设置恢复状态为成功，但事实上失败了。|  
  
 *模式*是**varchar(11)**，默认值为**N'ALL'**。  
  
 [  **@oneresultset=**] *oneresultset*  
 指示是否返回单个结果集。 *Oneresultset*自变量可以具有下列值：  
  
|值|说明|  
|-----------|-----------------|  
|0|当 *@objname* 为 null 或为未指定，返回两个结果集。 两个结果集是默认行为。|  
|1|当 *@objname*  = null 或未指定，则返回单个结果集。|  
  
 *oneresultset*是**位**，默认值为**0**。  

[  **@include_total_xtp_storage** ] *include_total_xtp_storage*  
**适用于：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]， [!INCLUDE[sssds-md](../../includes/sssds-md.md)]。  
  
 当@oneresultset= 1，参数@include_total_xtp_storage确定单个结果集是否包含列，MEMORY_OPTIMIZED_DATA 存储。 默认值为 0，即，默认情况下 （如果省略此参数） XTP 列不包含在结果集中。  

## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 如果*objname*省略和的值*oneresultset*为 0，则返回以下结果集以提供当前数据库大小信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar （128)**|当前数据库的名称。|  
|**database_size**|**varchar(18)**|当前数据库的大小 (MB)。 **database_size**包括数据和日志文件。|  
|**未分配的空间**|**varchar(18)**|未保留供数据库对象使用的数据库空间。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**保留**|**varchar(18)**|由数据库中对象分配的空间总量。|  
|**数据**|**varchar(18)**|数据使用的空间总量。|  
|**index_size**|**varchar(18)**|索引使用的空间总量。|  
|**未使用**|**varchar(18)**|为数据库中的对象保留但尚未使用的空间总量。|  
  
 如果*objname*省略和的值*oneresultset*为 1，将返回以下的单个结果集以提供当前数据库大小信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar （128)**|当前数据库的名称。|  
|**database_size**|**varchar(18)**|当前数据库的大小 (MB)。 **database_size**包括数据和日志文件。|  
|**未分配的空间**|**varchar(18)**|未保留供数据库对象使用的数据库空间。|  
|**保留**|**varchar(18)**|由数据库中对象分配的空间总量。|  
|**数据**|**varchar(18)**|数据使用的空间总量。|  
|**index_size**|**varchar(18)**|索引使用的空间总量。|  
|**未使用**|**varchar(18)**|为数据库中的对象保留但尚未使用的空间总量。|  
  
 如果*objname*指定，则为指定的对象返回以下结果集。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**nvarchar （128)**|请求其空间使用信息的对象的名称。<br /><br /> 不返回对象的架构名称。 如果架构名称是必需的使用[sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)或[sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)动态管理视图来获取等效大小信息。|  
|**行**|**char(20)**|表中现有的行数。 如果指定的对象是 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 队列，该列将指示队列中的消息数。|  
|**保留**|**varchar(18)**|有关保留空间总量*objname*。|  
|**数据**|**varchar(18)**|使用中的数据的空间总量*objname*。|  
|**index_size**|**varchar(18)**|使用中的索引的空间总量*objname*。|  
|**未使用**|**varchar(18)**|为保留的空间总量*objname*但尚未使用。|  
 
这是默认模式中，当未指定参数。 下面的结果集返回详细列出磁盘上的数据库大小信息。 

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar （128)**|当前数据库的名称。|  
|**database_size**|**varchar(18)**|当前数据库的大小 (MB)。 **database_size**包括数据和日志文件。 如果数据库具有 MEMORY_OPTIMIZED_DATA 文件组，这将包括文件组中的所有检查点文件的总磁盘上大小。|  
|**未分配的空间**|**varchar(18)**|未保留供数据库对象使用的数据库空间。 如果数据库具有 MEMORY_OPTIMIZED_DATA 文件组，这会包括文件组中的 PRECREATED 状态的检查点文件的总磁盘上大小。|  

使用的数据库中的表空间: （此结果集不会反映内存优化表，因为没有任何每个表所施加的磁盘使用情况） 

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**保留**|**varchar(18)**|由数据库中对象分配的空间总量。|  
|**数据**|**varchar(18)**|数据使用的空间总量。|  
|**index_size**|**varchar(18)**|索引使用的空间总量。|  
|**未使用**|**varchar(18)**|为数据库中的对象保留但尚未使用的空间总量。|

将返回以下结果集**仅当**数据库具有 MEMORY_OPTIMIZED_DATA 文件组与至少一个容器： 

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**xtp_precreated**|**varchar(18)**|具有状态 PRECREATED，以 kb 为单位的检查点文件的总大小。 向作为一个整体的数据库的未分配空间的计数。 [例如，如果没有 600000 KB 的预先创建的检查点文件，此列将包含"600000 KB]|  
|**xtp_used**|**varchar(18)**|其中包含在构造、 活动分区和合并的目标，以 kb 为单位的状态的检查点文件的总大小。 这是主要使用内存优化表中数据的磁盘空间。|  
|**xtp_pending_truncation**|**varchar(18)**|具有状态 WAITING_FOR_LOG_TRUNCATION，以 kb 为单位的检查点文件的总大小。 这是等待清理，一旦进行日志截断的检查点文件使用的磁盘空间。|

如果*objname*是省略，oneresultset 的值为 1，和*include_total_xtp_storage*为 1，将返回以下的单个结果集以提供当前数据库大小信息。 如果`include_total_xtp_storage`为 0 （默认值），则将忽略最后三个列。 

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar （128)**|当前数据库的名称。|  
|**database_size**|**varchar(18)**|当前数据库的大小 (MB)。 **database_size**包括数据和日志文件。 如果数据库具有 MEMORY_OPTIMIZED_DATA 文件组，这将包括文件组中的所有检查点文件的总磁盘上大小。|
|**未分配的空间**|**varchar(18)**|未保留供数据库对象使用的数据库空间。 如果数据库具有 MEMORY_OPTIMIZED_DATA 文件组，这会包括文件组中的 PRECREATED 状态的检查点文件的总磁盘上大小。|  
|**保留**|**varchar(18)**|由数据库中对象分配的空间总量。|  
|**数据**|**varchar(18)**|数据使用的空间总量。|  
|**index_size**|**varchar(18)**|索引使用的空间总量。|  
|**未使用**|**varchar(18)**|为数据库中的对象保留但尚未使用的空间总量。|
|**xtp_precreated**|**varchar(18)**|具有状态 PRECREATED，以 kb 为单位的检查点文件的总大小。 这向数据库中未分配的空间计为一个整体。 如果数据库没有与至少一个容器 memory_optimized_data 文件组，则返回 NULL。 *此列才包含的如果@include_total_xtp_storage= 1*。| 
|**xtp_used**|**varchar(18)**|其中包含在构造、 活动分区和合并的目标，以 kb 为单位的状态的检查点文件的总大小。 这是主要使用内存优化表中数据的磁盘空间。 如果数据库没有与至少一个容器 memory_optimized_data 文件组，则返回 NULL。 *此列才包含的如果@include_total_xtp_storage= 1*。| 
|**xtp_pending_truncation**|**varchar(18)**|具有状态 WAITING_FOR_LOG_TRUNCATION，以 kb 为单位的检查点文件的总大小。 这是等待清理，一旦进行日志截断的检查点文件使用的磁盘空间。 如果数据库没有与至少一个容器 memory_optimized_data 文件组，则返回 NULL。 此列才包含的如果`@include_total_xtp_storage=1`。|

## <a name="remarks"></a>注释  
 **database_size**是始终大于的总和**保留** + **未分配的空间**因为它包含的日志文件的大小但**保留**和**unallocated_space**考虑仅将数据页。  
  
 使用的 XML 索引和全文索引的页都将纳入**index_size**对于这两个结果集。 当*objname* XML 索引和对象的全文索引的页还会在总计中统计的指定**保留**和**index_size**结果。  
  
 如果为数据库或具有空间索引，列的空间大小，如的对象计算空间使用情况**database_size**，**保留**，和**index_size**，包括空间索引的大小。  
  
 当*updateusage*指定，则[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]扫描数据页在数据库中，并使任何所需的更正**sys.allocation_units**和**sys.partitions**目录有关存储空间使用的每个表的视图。 在某些情况下（例如删除索引后、表的空间信息不是当前信息时），需要执行该操作。 *updateusage*可能需要一些时间才能在大型表或数据库上运行。 使用*updateusage*只有当你怀疑所返回的不正确的值和当过程不会产生不利影响其他用户或进程在数据库中。 如果首选该进程，则可以单独运行 DBCC UPDATEUSAGE。  
  
> [!NOTE]  
>  在删除或重新生成大型索引时，或者在删除或截断大型表时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将延迟实际页释放及其关联锁，直至事务提交完毕为止。 延迟的删除操作不会立即释放已分配的空间。 因此，返回的值**sp_spaceused**后立即删除或截断的大型对象可能无法反映可用的实际磁盘空间。  
  
## <a name="permissions"></a>Permissions  
 执行 **sp_spaceused** 的权限授予 **public** 角色。 只有 **db_owner** 固定数据库角色的成员可以指定 **@updateusage** 参数。  
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-disk-space-information-about-a-table"></a>A. 显示表的磁盘空间信息  
 以下示例报告 `Vendor` 表及其索引的磁盘空间信息。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
### <a name="b-displaying-updated-space-information-about-a-database"></a>B. 显示数据库的已更新空间信息  
 下例对当前数据库中使用的空间进行了汇总，并使用可选参数 `@updateusage` 确保返回当前值。  
  
```sql  
USE AdventureWorks008R2;  
GO  
EXEC sp_spaceused @updateusage = N'TRUE';  
GO  
```  
  
### <a name="c-displaying-space-usage-information-about-the-remote-table-associated-with-a-stretch-enabled-table"></a>C. 显示有关远程表的空间使用情况信息与已启用延伸的表  
 下面的示例概述了通过使用与已启用延伸的表关联的远程表占用的空间 **@mode** 自变量以指定在远程目标。 有关详细信息，请参阅 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)。  
  
```sql  
USE StretchedAdventureWorks2016  
GO  
EXEC sp_spaceused N'Purchasing.Vendor', @mode = 'REMOTE_ONLY'  
```  
  
### <a name="d-displaying-space-usage-information-for-a-database-in-a-single-result-set"></a>D. 在单个结果中显示数据库的空间使用情况信息设置  
 下面的示例概述了中单个结果集的当前数据库的空间使用情况。  
  
```sql  
USE AdventureWorks2016  
GO  
EXEC sp_spaceused @oneresultset = 1  
```  

### <a name="e-displaying-space-usage-information-for-a-database-with-at-least-one-memoryoptimized-file-group-in-a-single-result-set"></a>E. 在单个结果集中显示与至少一个 MEMORY_OPTIMIZED 文件组数据库的空间使用情况信息 
 下面的示例总结了在单个结果集的至少一个 MEMORY_OPTIMIZED 文件组的当前数据库的空间使用情况。
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused @updateusage = 'FALSE', @mode = 'ALL', @oneresultset = '1', @include_total_xtp_storage = '1';
GO
``` 

### <a name="f-displaying-space-usage-information-for-a-memoryoptimized-table-object-in-a-database"></a>F. 在数据库中为 MEMORY_OPTIMIZED 表对象的显示空间使用情况信息。
 下面的示例总结了在至少一个 MEMORY_OPTIMIZED 文件组的当前数据库中为 MEMORY_OPTIMIZED 表对象的空间使用情况。
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused
@objname = N'VehicleTemparatures',
@updateusage = 'FALSE',
@mode = 'ALL',
@oneresultset = '0',
@include_total_xtp_storage = '1';
GO
```  

## <a name="see-also"></a>另请参阅  
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC UPDATEUSAGE &#40;Transact SQL &#41;](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [sys.allocation_units &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.partitions &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
