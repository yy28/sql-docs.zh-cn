---
title: sys.query_context_settings (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS
- QUERY_CONTEXT_SETTINGS
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_context_settings catalog view
ms.assetid: 3c1887df-6bd8-491e-82fc-d25ad9589faf
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c7ab77981c329c334b22d6fd9735188882b385c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013538"
---
# <a name="sysquerycontextsettings-transact-sql"></a>sys.query_context_settings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含有关影响上下文设置与查询关联的语义信息。 有大量的上下文设置中提供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]影响查询语义 （定义查询的正确的结果）。 相同的查询文本不同设置下编译可能会产生不同的结果 （具体取决于基础数据）。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|主键。 此值中显示计划 XML 公开的查询。|  
|**set_options**|**varbinary(8)**|专用于反映将多个 SET 选项的状态的位掩码。 有关详细信息，请参阅[sys.dm_exec_plan_attributes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)。|  
|**language_id**|**smallint**|语言的 id。 有关详细信息，请参阅[sys.syslanguages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)。|  
|**date_format**|**smallint**|日期格式。 有关详细信息，请参阅 [SET DATEFORMAT (Transact-SQL)](../../t-sql/statements/set-dateformat-transact-sql.md).|  
|**date_first**|**tinyint**|日期第一个值。 有关详细信息，请参阅 [SET DATEFIRST (Transact-SQL)](../../t-sql/statements/set-datefirst-transact-sql.md).|  
|**status**|**varbinary(2)**|位屏蔽字段以指示查询或执行查询时的上下文的类型。 <br />列的值可以是 （以十六进制格式表示） 的多个标志的组合：<br /><br /> 0x0-常规查询 （没有特定的标志）<br /><br /> 0x1-已通过游标 Api 存储过程之一执行查询<br /><br /> 0x2-通知查询<br /><br /> 0x4-内部查询<br /><br /> 0x8-没有通用的参数化自动参数化查询<br /><br /> 0x10-游标提取刷新查询<br /><br /> 0x20-查询能耗在游标更新请求<br /><br /> 0x40-初始结果集返回时打开的游标 （游标自动提取）<br /><br /> 0x80-加密的查询<br /><br /> 0x100-在行级别安全性谓词的上下文中的查询|  
|**required_cursor_options**|**int**|用户指定的游标选项，例如游标类型。|  
|**acceptable_cursor_options**|**int**|为了支持语句的执行，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以隐式转换采用的游标选项。|  
|**merge_action_type**|**smallint**|触发器执行计划用作的结果的类型**合并**语句。<br /><br /> 0 表示非触发器计划，不会执行的结果作为触发器计划**合并**语句或作为的结果执行的触发器计划**合并**语句，以便仅指定**删除**操作。<br /><br /> 1 指示**插入**的结果作为运行的触发器计划**合并**语句。<br /><br /> 2 表示**更新**的结果作为运行的触发器计划**合并**语句。<br /><br /> 3 表示**删除**的结果作为运行的触发器计划**合并**包含相应语句**插入**或者**更新**操作。<br /><br /> <br /><br /> 对于由级联操作运行的嵌套触发器，此值，此操作**合并**导致级联的语句。|  
|**default_schema_id**|**int**|默认架构，用来解析不是完全限定的名称的 ID。|  
|**is_replication_specific**|**bit**|用于复制。|  
|**is_contained**|**varbinary(1)**|1 表示包含的数据库。|  
  
## <a name="permissions"></a>权限  
 需要**VIEW DATABASE STATE**权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询存储存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL)](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
