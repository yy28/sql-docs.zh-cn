---
title: 管理数据收集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
- data collector [SQL Server], Transact-SQL
- data collector [SQL Server], SQL Server Management Studio
ms.assetid: bc137daa-9f37-4c01-9766-8b7350c75af8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 543f972f5c5805bb1508b6a256f7a7ed3a2aaa3b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52768289"
---
# <a name="manage-data-collection"></a>管理数据收集
  可使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程和功能来管理数据收集的各个方面，例如启用或禁用数据收集、更改收集组配置或查看管理数据仓库中的数据。  
  
## <a name="manage-data-collection-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 管理数据收集  
 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的对象资源管理器可以执行以下与数据收集器相关的任务：  
  
-   [配置管理数据仓库 (SQL Server Management Studio)](configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
-   [配置数据收集器的属性](configure-properties-of-a-data-collector.md)  
  
-   [启用或禁用数据收集](data-collection.md)  
  
-   [启动或停止收集组](start-or-stop-a-collection-set.md)  
  
-   [使用 SQL Server Profiler 创建 SQL 跟踪收集组 (SQL Server Management Studio)](use-sql-server-profiler-to-create-a-sql-trace-collection-set.md)  
  
-   [查看收集组日志 (SQL Server Management Studio)](view-collection-set-logs-sql-server-management-studio.md)  
  
-   [查看或更改收集组计划 (SQL Server Management Studio)](view-or-change-collection-set-schedules-sql-server-management-studio.md)  
  
-   [查看收集组报表 (SQL Server Management Studio)](view-a-collection-set-report-sql-server-management-studio.md)  
  
## <a name="manage-data-collection-by-using-transact-sql"></a>使用 Transact-SQL 管理数据收集  
 数据收集器提供了一系列内容丰富的存储过程，这些过程可用于执行任何与数据收集器相关的任务。 例如，可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]执行以下任务：  
  
-   [配置数据收集参数 (Transact-SQL)](configure-data-collection-parameters-transact-sql.md)  
  
-   [启用或禁用数据收集](data-collection.md)  
  
-   [启动或停止收集组](start-or-stop-a-collection-set.md)  
  
-   [创建使用一般 T-SQL 查询收集器类型的自定义收集组 (Transact-SQL)](create-custom-collection-set-generic-t-sql-query-collector-type.md)  
  
-   [将收集项添加到收集组中 (Transact-SQL)](add-a-collection-item-to-a-collection-set-transact-sql.md)  
  
 另外，它还包括一些函数和视图，这些函数和视图可用来获取 msdb 数据库和管理数据仓库数据库的配置数据、执行日志数据和存储在管理数据仓库中的数据。  
  
 您可使用提供的存储过程、函数和视图来创建自己的端到端数据收集方案。  
  
> [!IMPORTANT]  
>  与常规存储过程不同的是，数据收集器存储过程使用严格类型化的参数，不支持自动的数据类型转换。 如果这些参数不是使用正确的输入参数数据类型（正如参数说明中指定的一样）调用的，则存储过程会返回错误。  
  
 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来创建和执行提供的代码示例。 有关详细信息，请参阅 [对象资源管理器](../../ssms/object/object-explorer.md)。 或者，您可在任何编辑器中创建查询并将其保存为文件扩展名为 .sql 的文本文件。 您可以从 Windows 命令提示符处使用 `sqlcmd` 实用程序执行查询。 有关详细信息，请参阅 [使用 sqlcmd 实用工具](../scripting/sqlcmd-use-the-utility.md)。  
  
### <a name="stored-procedures-and-views"></a>存储过程和视图  
 **使用数据收集器**  
  
 下表介绍了使用数据收集器时可以使用的存储过程。  
  
|过程名称|Description|  
|--------------------|-----------------|  
|[sp_syscollector_enable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql)|启用数据收集器。|  
|[sp_syscollector_disable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql)|禁用数据收集器。|  
  
 **使用收集组**  
  
 下表介绍了使用收集组时可以使用的存储过程。  
  
|过程名称|Description|  
|--------------------|-----------------|  
|[sp_syscollector_run_collection_set (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql)|按需运行收集组。|  
|[sp_syscollector_start_collection_set (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql)|启动收集组。|  
|[sp_syscollector_stop_collection_set (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql)|停止收集组。|  
|[sp_syscollector_create_collection_set (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql)|创建收集组。|  
|[sp_syscollector_delete_collection_set (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql)|删除收集组。|  
|[sp_syscollector_update_collection_set (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql)|更改收集组的配置|  
|[sp_syscollector_upload_collection_set (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql)|将收集组数据上载到管理数据仓库。 实际上，这是一种按需进行的上载。|  
  
 **使用收集项**  
  
 下表介绍了使用收集项时可以使用的存储过程。  
  
|过程名称|Description|  
|--------------------|-----------------|  
|[sp_syscollector_create_collection_item (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql)|创建收集项。|  
|[sp_syscollector_delete_collection_item (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql)|删除收集项。|  
|[sp_syscollector_update_collection_item (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql)|更新收集项。|  
  
 **使用收集器类型**  
  
 下表介绍了使用收集器类型时可以使用的存储过程。  
  
|过程名称|Description|  
|--------------------|-----------------|  
|[sp_syscollector_create_collector_type (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql)|创建收集器类型。|  
|[sp_syscollector_update_collector_type (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql)|更新收集器类型。|  
|[sp_syscollector_delete_collector_type (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql)|删除收集器类型。|  
  
 **获取配置信息**  
  
 下表介绍了可用于获取配置信息和执行日志数据的视图。  
  
|视图名称|Description|  
|---------------|-----------------|  
|[syscollector_config_store (Transact-SQL)](/sql/relational-databases/system-catalog-views/syscollector-config-store-transact-sql)|获取数据收集器的配置。|  
|[syscollector_collection_items (Transact-SQL)](/sql/relational-databases/system-catalog-views/syscollector-collection-items-transact-sql)|获取收集项信息。|  
|[syscollector_collection_sets (Transact-SQL)](/sql/relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql)|获取收集组信息。|  
|[syscollector_collector_types (Transact-SQL)](/sql/relational-databases/system-catalog-views/syscollector-collector-types-transact-sql)|获取收集器类型信息。|  
|[syscollector_execution_log (Transact-SQL)](/sql/relational-databases/system-catalog-views/syscollector-execution-log-transact-sql)|获取有关收集组和包执行的信息。|  
|[syscollector_execution_stats (Transact-SQL)](/sql/relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql)|获取有关任务执行的信息。|  
|[syscollector_execution_log_full (Transact-SQL)](/sql/relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql)|当执行日志已满时获取信息。|  
  
 **配置访问管理数据仓库的权限**  
  
 下表介绍了可用于配置访问管理数据仓库的权限的存储过程。  
  
|过程名称|Description|  
|--------------------|-----------------|  
|[sp_syscollector_set_warehouse_database_name (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql)|指定在连接字符串中为管理数据仓库定义的数据库名称。|  
|[sp_syscollector_set_warehouse_instance_name (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql)|指定在连接字符串中为管理数据仓库定义的实例。|  
  
 **配置管理数据仓库**  
  
 下表介绍了使用管理数据仓库配置时可以使用的存储过程。  
  
|过程名称|Description|  
|--------------------|-----------------|  
|[core.sp_create_snapshot (Transact-SQL)](/sql/relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql)|在管理数据仓库中创建一个收集快照。|  
|[core.sp_update_data_source (Transact-SQL)](/sql/relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql)|为数据收集更新数据源。|  
|[core.sp_add_collector_type (Transact-SQL)](/sql/relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql)|将收集器类型添加到管理数据仓库。|  
|[core.sp_remove_collector_type (Transact-SQL)](/sql/relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql)|从管理数据仓库中删除收集器类型。|  
|[core.sp_purge_data (Transact-SQL)](/sql/relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql)|从管理数据仓库中删除数据。|  
  
 **使用上载包**  
  
 下表介绍了使用上载包时可以使用的存储过程。  
  
|过程名称|Description|  
|--------------------|-----------------|  
|[sp_syscollector_set_cache_window (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql)|配置数据上载重试的次数。|  
|[sp_syscollector_set_cache_directory (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql)|指定在两次上载重试之间数据的临时存储区。|  
  
 **使用数据收集执行日志**  
  
 下表介绍了使用数据收集执行日志时可以使用的存储过程。  
  
|过程名称|Description|  
|--------------------|-----------------|  
|[sp_syscollector_delete_execution_log_tree (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql)|从执行日志删除收集组条目。|  
  
### <a name="functions"></a>函数  
 下表介绍了可用于获取执行和跟踪信息的函数。  
  
|函数名称|Description|  
|-------------------|-----------------|  
|[fn_syscollector_get_execution_details (Transact-SQL)](/sql/relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql)|为特定包获取 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 执行日志数据。|  
|[fn_syscollector_get_execution_stats (Transact-SQL)](/sql/relational-databases/system-functions/fn-syscollector-get-execution-stats-transact-sql)|为收集组或包获取执行统计信息。 此信息包含所记录的错误。|  
|[snapshots.fn_trace_getdata (Transact-SQL)](/sql/relational-databases/system-functions/snapshots-fn-trace-getdata-transact-sql)|获取使用一般 SQL Trace 收集器类型收集数据时记录的事件。|  
  
## <a name="see-also"></a>请参阅  
 [执行存储过程](../stored-procedures/execute-a-stored-procedure.md)   
 [使用 SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)   
 [数据收集](data-collection.md)  
  
  
