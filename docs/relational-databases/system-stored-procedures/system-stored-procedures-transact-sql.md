---
title: 系统存储过程 (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 02/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql13.TSQLSysNoExpandPortal.f1
- sql13.TSQLSysNoExpandPortal.f1_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server]
- APIs [SQL Server]
- stored procedures [SQL Server], categories
- system stored procedures [SQL Server], categories
- system stored procedures [SQL Server]
ms.assetid: a5c4d5b8-5a24-4a2d-99b4-d003b546ee3a
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3d44d8031daaac656cb99a7477991dc6c30ce864
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666506"
---
# <a name="system-stored-procedures-transact-sql"></a>系统存储过程 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，可以使用系统存储过程来执行许多管理和信息活动。 系统存储过程可划分为下表所示的类别。  
  
## <a name="in-this-section"></a>本节内容  
  
|类别|Description|  
|--------------|-----------------|  
|[活动异地复制存储过程](https://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)|用于管理来管理 Azure SQL 数据库中的活动异地复制配置|  
|[目录存储的过程](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)|用于实现 ODBC 数据字典功能，并隔离 ODBC 应用程序以使其不受基础系统表更改的影响。|  
|[变更数据捕获存储的过程](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)|用于启用、禁用、或报告变更数据捕获对象。|  
|[游标存储过程](../../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)|用于实现游标变量功能。|  
|[数据收集器存储过程](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)|用于处理数据收集器和以下组件：收集组、收集项和收集类型。|  
|[数据库引擎存储过程](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)|用于 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的常规维护。|  
|[数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)|用于从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例内执行电子邮件操作。|  
|[数据库维护计划存储过程](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)|用于设置管理数据库性能所需的核心维护任务。|  
|[分布式的查询存储过程](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)|用于实现和管理分布式查询。|  
|[Filestream 和 FileTable 存储的过程&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/54beca08-c012-4ebd-aa68-d8a10d221b64)|用于配置和管理 FILESTREAM 和 FileTable 功能。|  
|[防火墙规则存储过程&#40;Azure SQL 数据库&#41;](../../relational-databases/system-stored-procedures/firewall-rules-stored-procedures-azure-sql-database.md)|用于配置 Azure SQL 数据库防火墙。|  
|[全文搜索存储过程](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)|用于实现和查询全文索引。|  
|[常规扩展存储的过程](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)|用于提供从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例到外部程序的接口，以便进行各种维护活动。|  
|[日志传送存储过程](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)|用于配置、修改和监视日志传送配置。|  
|[管理数据仓库存储的过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)|用于配置管理数据仓库。|  
|[OLE 自动化存储过程](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)|用于使标准自动化对象能够在标准 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中使用。|  
|[基于策略的管理存储过程](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)|用于基于策略的管理。|  
|[PolyBase 存储过程](https://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)|添加或从 PolyBase 横向扩展组中删除计算机。|  
|[查询存储存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)|用于优化性能。|  
|[复制存储过程](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|用于管理复制。|  
|[安全性存储过程](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)|用于管理安全性。|  
|[快照备份的存储的过程](https://msdn.microsoft.com/library/c278db87-5770-4037-a1e6-b9853a943339)|用于删除 FILE_SNAPSHOT 备份以及所有快照或删除单个备份文件快照。|  
|[空间索引存储过程](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)|用于分析和改善空间索引的索引性能。|  
|[SQL Server 代理存储过程](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)|由 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 用于监视性能和活动。|  
|[SQL Server Profiler 存储过程](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理用于管理计划的活动和事件驱动的活动。|  
|[Stretch Database 存储过程](../../relational-databases/system-stored-procedures/stretch-database-extended-stored-procedures-transact-sql.md)|用于管理延伸数据库。|  
|[临时表的存储的过程](https://msdn.microsoft.com/library/f28ca74e-7876-4592-b794-e78e3690fff6)|使用的临时表|  
|[XML 存储过程](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)|用于 XML 文本管理。|  
  
> [!NOTE]  
>  除非另外特别说明，否则所有的系统存储过程将返回一个 0 值以表示成功。 若要表示失败，则返回一个非零值。  
  
## <a name="api-system-stored-procedures"></a>API 系统存储过程  
 针对 ADO、OLE DB 以及 ODBC 应用程序运行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的用户可能会注意到这些使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 引用未涵盖的系统存储过程的应用程序。 通过使用这些存储的过程[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序用于实现数据库 API 的功能。 这些存储过程只不过是访问接口或驱动程序所使用的机制，用来传达用户对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的请求。 它们只供提供程序或驱动程序内部使用。 调用它们显式从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-不支持基于应用程序。  
  
 Sp_createorphan 和 sp_droporphans 存储过程用于 ODBC **ntext**，**文本**，并**图像**处理。  
  
 sp_reset_connection 存储过程由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用来支持事务中的远程存储过程调用。 从连接池中重用连接时，该存储过程还将导致激发 Audit Login 和 Audit Logout 事件。  
  
 下列表中的系统存储过程只在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中使用或通过客户端 API 使用，不适于一般客户使用。 随时可能对其进行更改，不保证兼容性。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书介绍了下列存储过程：  
  
|||  
|-|-|  
|sp_catalogs|sp_column_privileges|  
|sp_column_privileges_ex|sp_columns|  
|sp_columns_ex|sp_databases|  
|sp_cursor|sp_cursorclose|  
|sp_cursorexecute|sp_cursorfetch|  
|sp_cursoroption|sp_cursoropen|  
|sp_cursorprepare|sp_cursorprepexec|  
|sp_cursorunprepare|sp_execute|  
|sp_datatype_info|sp_fkeys|  
|sp_foreignkeys|sp_indexes|  
|sp_pkeys|sp_primarykeys|  
|sp_prepare|sp_prepexec|  
|sp_prepexecrpc|sp_unprepare|  
|sp_server_info|sp_special_columns|  
|sp_sproc_columns|sp_statistics|  
|sp_table_privileges|sp_table_privileges_ex|  
|sp_tables|sp_tables_ex|  
  
 未介绍下列存储过程：  
  
|||  
|-|-|  
|sp_assemblies_rowset|sp_assemblies_rowset_rmt|  
|sp_assemblies_rowset2|sp_assembly_dependencies_rowset|  
|sp_assembly_dependencies_rowset_rmt|sp_assembly_dependencies_rowset2|  
|sp_bcp_dbcmptlevel|sp_catalogs_rowset|  
|sp_catalogs_rowset;2|sp_catalogs_rowset;5|  
|sp_catalogs_rowset_rmt|sp_catalogs_rowset2|  
|sp_check_constbytable_rowset|sp_check_constbytable_rowset;2|  
|sp_check_constbytable_rowset2|sp_check_constraints_rowset|  
|sp_check_constraints_rowset;2|sp_check_constraints_rowset2|  
|sp_column_privileges_rowset|sp_column_privileges_rowset;2|  
|sp_column_privileges_rowset;5|sp_column_privileges_rowset_rmt|  
|sp_column_privileges_rowset2|sp_columns_90|  
|sp_columns_90_rowset|sp_columns_90_rowset_rmt|  
|sp_columns_90_rowset2|sp_columns_ex_90|  
|sp_columns_rowset|sp_columns_rowset;2|  
|sp_columns_rowset;5|sp_columns_rowset_rmt|  
|sp_columns_rowset2|sp_constr_col_usage_rowset|  
|sp_datatype_info_90|sp_ddopen;1|  
|sp_ddopen;10|sp_ddopen;11|  
|sp_ddopen;12|sp_ddopen;13|  
|sp_ddopen;2|sp_ddopen;3|  
|sp_ddopen;4|sp_ddopen;5|  
|sp_ddopen;6|sp_ddopen;7|  
|sp_ddopen;8|sp_ddopen;9|  
|sp_foreign_keys_rowset|sp_foreign_keys_rowset;2|  
|sp_foreign_keys_rowset;3|sp_foreign_keys_rowset;5|  
|sp_foreign_keys_rowset_rmt|sp_foreign_keys_rowset2|  
|sp_foreign_keys_rowset3|sp_indexes_90_rowset|  
|sp_indexes_90_rowset_rmt|sp_indexes_90_rowset2|  
|sp_indexes_rowset|sp_indexes_rowset;2|  
|sp_indexes_rowset;5|sp_indexes_rowset_rmt|  
|sp_indexes_rowset2|sp_linkedservers_rowset|  
|sp_linkedservers_rowset;2|sp_linkedservers_rowset2|  
|sp_oledb_database|sp_oledb_defdb|  
|sp_oledb_deflang|sp_oledb_language|  
|sp_oledb_ro_usrname|sp_primary_keys_rowset|  
|sp_primary_keys_rowset;2|sp_primary_keys_rowset;3|  
|sp_primary_keys_rowset;5|sp_primary_keys_rowset_rmt|  
|sp_primary_keys_rowset2|sp_procedure_params_90_rowset|  
|sp_procedure_params_90_rowset2|sp_procedure_params_rowset|  
|sp_procedure_params_rowset;2|sp_procedure_params_rowset2|  
|sp_procedures_rowset|sp_procedures_rowset;2|  
|sp_procedures_rowset2|sp_provider_types_90_rowset|  
|sp_provider_types_rowset|sp_schemata_rowset|  
|sp_schemata_rowset;3|sp_special_columns_90|  
|sp_sproc_columns_90|sp_statistics_rowset|  
|sp_statistics_rowset;2|sp_statistics_rowset2|  
|sp_stored_procedures|sp_table_constraints_rowset|  
|sp_table_constraints_rowset;2|sp_table_constraints_rowset2|  
|sp_table_privileges_rowset|sp_table_privileges_rowset;2|  
|sp_table_privileges_rowset;5|sp_table_privileges_rowset_rmt|  
|sp_table_privileges_rowset2|sp_table_statistics_rowset|  
|sp_table_statistics_rowset;2|sp_table_statistics2_rowset|  
|sp_tablecollations|sp_tablecollations_90|  
|sp_tables_info_90_rowset|sp_tables_info_90_rowset_64|  
|sp_tables_info_90_rowset2|sp_tables_info_90_rowset2_64|  
|sp_tables_info_rowset|sp_tables_info_rowset;2|  
|sp_tables_info_rowset_64|sp_tables_info_rowset_64;2|  
|sp_tables_info_rowset2|sp_tables_info_rowset2_64|  
|sp_tables_rowset;2|sp_tables_rowset;5|  
|sp_tables_rowset_rmt|sp_tables_rowset2|  
|sp_usertypes_rowset|sp_usertypes_rowset_rmt|  
|sp_usertypes_rowset2|sp_views_rowset|  
|sp_views_rowset2|sp_xml_schema_rowset|  
|sp_xml_schema_rowset2||  
  
## <a name="see-also"></a>请参阅  
 [CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [存储过程（数据库引擎）](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [运行存储的过程&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)   
 [运行存储的过程](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [运行存储过程](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
