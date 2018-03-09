---
title: "sys.sp_cdc_enable_table (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_enable_table_TSQL
- sp_cdc_enable_table_TSQL
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
ms.assetid: 26150c09-2dca-46ad-bb01-3cb3165bcc5d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 43e2866c70c60e8b7c7b7f1eaffabebf53a98ebe
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sysspcdcenabletable-transact-sql"></a>sys.sp_cdc_enable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为当前数据库中指定的源表启用变更数据捕获。 对表启用变更数据捕获时，应用于此表的每个数据操纵语言 (DML) 操作的记录都将写入事务日志中。 变更数据捕获进程将从日志中检索此信息，并将其写入可通过使用一组函数访问的更改表中。  
  
 并非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供变更数据捕获功能。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_enable_table   
  [ @source_schema = ] 'source_schema',   
  [ @source_name = ] 'source_name' ,  [,[ @capture_instance = ] 'capture_instance' ]  
  [,[ @supports_net_changes = ] supports_net_changes ]  
  , [ @role_name = ] 'role_name'  
  [,[ @index_name = ] 'index_name' ]  
  [,[ @captured_column_list = ] 'captured_column_list' ]  
  [,[ @filegroup_name = ] 'filegroup_name' ]  
  [,[ @allow_partition_switch = ] 'allow_partition_switch' ]  
  [;]  
```  
  
## <a name="arguments"></a>参数  
 [  **@source_schema =** ] *source_schema*  
 源表所属架构的名称。 *source_schema*是**sysname**，无默认值，并不能为 NULL。  
  
 [  **@source_name =** ] *source_name*  
 是对其启用变更数据捕获的源表的名称。 *source_name*是**sysname**，无默认值，并不能为 NULL。  
  
 *source_name*必须存在于当前数据库。 中的表**cdc**架构不能启用了变更数据捕获。  
  
 [  **@role_name =** ] *role_name*  
 用于访问变更数据的数据库角色的名称。 *role_name*是**sysname**并且必须指定。 如果显式设置为 NULL，则没有控制角色用于限制对更改数据的访问。  
  
 如果当前存在该角色，则使用它。 如果不存在该角色，则会尝试创建具有指定名称的数据库角色。 在尝试创建该角色之前，将删除角色名称字符串右侧的空格。 如果调用方无权在数据库中创建角色，则存储过程操作将失败。  
  
 [  **@capture_instance =** ] *capture_instance*  
 是用于命名特定于实例的变更数据捕获对象的捕获实例的名称。 *capture_instance*是**sysname**和不能为 NULL。  
  
 如果未指定，将名称派生自将从源架构名称加上源表名称格式*schemaname_sourcename*。 *capture_instance*不能超过 100 个字符并且在数据库中必须唯一。 指定还是派生， *capture_instance*修整字符串右侧的任意空白。  
  
 源表最多可以有两个捕获实例。 有关详细信息，请参阅[sys.sp_cdc_help_change_data_capture &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md).  
  
 [  **@supports_net_changes =** ] *supports_net_changes*  
 指示是否对此捕获实例启用净更改查询支持。 *supports_net_changes*是**位**默认值为 1，如果表具有主键或该表不包含已发现使用的唯一索引@index_name参数。 否则，该参数默认为 0。  
  
 如果为 0，则只生成查询所有更改的支持函数。  
  
 如果为 1，则还会生成查询净更改所需的函数。  
  
 如果*supports_net_changes*设置为 1， *index_name*必须指定或源表必须具有定义的主键。  
  
 [  **@index_name =** ] *index_name*  
 用于唯一标识源表中的行的唯一索引的名称。 *index_name*是**sysname**而且可以为 NULL。 如果指定， *index_name*必须在源表上的有效唯一索引。 如果*index_name*标识的索引列作为表的唯一行标识符将优先于任何定义的主键列的指定。  
  
 [  **@captured_column_list =** ] *captured_column_list*  
 标识将包括在更改表中的源表列。 *captured_column_list*是**nvarchar (max)**而且可以为 NULL。 如果为 NULL，则所有列都将包括在更改表中。  
  
 列名称必须是源表中的有效列。 在主键索引中, 定义的列或列中引用的索引定义*index_name*必须包含。  
  
 *captured_column_list*是以逗号分隔列表的列名称。 可以选择将列表中的单个列名称放在双引号 ("") 或方括号 ([]) 中。 如果列名称包含嵌入的逗号，则必须将该列名称引起来。  
  
 *captured_column_list*不能包含以下保留的列名称： **__ $start_lsn**， **__ $end_lsn**， **__ $seqval**， **__$operation**，和**__ $update_mask**。  
  
 [  **@filegroup_name =** ] *filegroup_name*  
 要用于为捕获实例创建的更改表的文件组。 *filegroup_name*是**sysname**而且可以为 NULL。 如果指定， *filegroup_name*必须为当前数据库中定义。 如果为 NULL，则使用默认文件组。  
  
 我们建议为变更数据捕获的更改表创建一个单独的文件组。  
  
 [  **@allow_partition_switch=** ] *allow_partition_switch*  
 指示是否可以对启用了变更数据捕获的表执行 ALTER TABLE 的 SWITCH PARTITION 命令。 *allow_partition_switch*是**位**，默认值为 1。  
  
 对于非分区表，此开关设置始终为 1，并忽略实际的设置。 如果对于非分区表将此开关显式设置为 0，则发出警告 22857 以指示已忽略此开关设置。 如果对于分区表将此开关显式设置为 0，则发出警告 22356 以指示将禁止源表上的分区切换操作。 最后，如果此开关设置显式设置为 1 或允许默认为 1 并且被启用的表已分区，则发出警告 22855 以指示不会阻塞分区切换。 如果发生任何分区切换，则变更数据捕获不会跟踪由此切换产生的更改。 这将导致使用更改数据时数据不一致。  
  
> [!IMPORTANT]  
>  SWITCH PARTITION 为元数据操作，但能导致数据更改。 与此操作相关联的数据更改不会在变更数据捕获的更改表中捕获。 请考虑一个有三个分区的表，并对此表进行更改。 捕获进程将跟踪用户对该表执行的插入、更新和删除操作。 但是，如果分区切出到另一个表（例如，为了执行大容量删除操作），作为此操作的一部分移动的行不会被捕获为更改表中的已删除行。 同样，如果将已预填充行的新分区添加到该表，这些行将不会反映在更改表中。 当更改被应用程序使用并应用于目标时，这可能会导致数据不一致。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 在可以对表启用变更数据捕获之前，必须先对数据库启用变更数据捕获。 若要确定数据库是否已启用了变更数据捕获，请查询**is_cdc_enabled**中的列[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目录视图。 若要启用数据库，使用[sys.sp_cdc_enable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)存储过程。  
  
 对表启用变更数据捕获时，将生成一个更改表以及一个或两个查询函数。 更改表充当捕获进程从事务日志中提取的源表更改的存储库。 查询函数则用于从更改表中提取数据。 这些函数的名称派生自*capture_instance*通过以下方式的参数：  
  
-   所有更改函数： **cdc.fn_cdc_get_all_changes_ < capture_instance >**  
  
-   净更改函数： **cdc.fn_cdc_get_net_changes_ < capture_instance >**  
  
 **sys.sp_cdc_enable_table**如果源表为数据库启用了变更数据捕获中的第一个表，并且没有事务发布存在数据库还会创建数据库的捕获和清除作业。 它将设置**is_tracked_by_cdc**中的列[sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)目录视图为 1。  
  
> [!NOTE]  
>  对表启用变更数据捕获时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理不必正在运行。 但是，只有当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理正在运行时，捕获进程才会处理事务日志并将条目写入更改表。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**db_owner**固定的数据库角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-enabling-change-data-capture-by-specifying-only-required-parameters"></a>A. 通过仅指定必需的参数来启用变更数据捕获  
 下面的示例对 `HumanResources.Employee` 表启用了变更数据捕获。 仅指定了必需的参数。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Employee'  
  , @role_name = N'cdc_Admin';  
GO  
```  
  
### <a name="b-enabling-change-data-capture-by-specifying-additional-optional-parameters"></a>B. 通过指定其他可选参数启用变更数据捕获  
 下面的示例对 `HumanResources.Department` 表启用了变更数据捕获。 指定了除 `@allow_partition_switch` 以外的所有参数。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Department'  
  , @role_name = N'cdc_admin'  
  , @capture_instance = N'HR_Department'   
  , @supports_net_changes = 1  
  , @index_name = N'AK_Department_Name'   
  , @captured_column_list = N'DepartmentID, Name, GroupName'   
  , @filegroup_name = N'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.sp_cdc_disable_table &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60; capture_instance &#62; &#40;Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60; capture_instance &#62;&#40;Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sys.sp_cdc_help_jobs &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)  
  
  
