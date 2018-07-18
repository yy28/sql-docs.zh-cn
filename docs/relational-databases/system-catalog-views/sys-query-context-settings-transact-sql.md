---
title: sys.query_context_settings (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/22/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 448727aa29d55e0cd41b0859f620ad393b738e09
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33182093"
---
# <a name="sysquerycontextsettings-transact-sql"></a>sys.query_context_settings (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含有关影响与查询关联的上下文设置的语义信息。 有可用的各种上下文设置中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]影响 （定义查询的正确的结果） 的查询语义。 在不同的设置下编译的相同查询文本可能会产生不同的结果 （具体取决于基础数据）。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|主键。 Showplan XML 中公开此值是查询。|  
|**set_options**|**varbinary(8)**|反映了多个状态的位掩码设置选项。 有关详细信息，请参阅[sys.dm_exec_plan_attributes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)。|  
|**language_id**|**int**|语言的 id。 有关详细信息，请参阅[sys.syslanguages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)。|  
|**date_format**|**int**|日期格式。 有关详细信息，请参阅 [SET DATEFORMAT (Transact-SQL)](../../t-sql/statements/set-dateformat-transact-sql.md).|  
|**date_first**|**tinyint**|日期第一个值。 有关详细信息，请参阅 [SET DATEFIRST (Transact-SQL)](../../t-sql/statements/set-datefirst-transact-sql.md).|  
|**status**|**varbinary(2)**|位掩码字段，它指示的查询或执行查询时的上下文的类型。 <br />列的值可以是 （以十六进制表示） 的多个标志的组合：<br /><br /> 0x0-常规查询 （没有特定的标志）<br /><br /> 0x1-已通过游标 Api 存储过程之一执行的查询<br /><br /> 0x2-查询通知<br /><br /> 0x4-内部查询<br /><br /> 0x8-没有通用参数化的自动参数化查询<br /><br /> 0x10 – 游标提取刷新查询<br /><br /> 0x20-游标更新请求中正在使用的查询<br /><br /> 0x40-初始返回的结果集时打开一个游标 （光标自动提取）<br /><br /> 0x80 – 加密查询<br /><br /> 0x100 – 在行级别安全性谓词的上下文中的查询|  
|**required_cursor_options**|**int**|用户指定的游标选项，例如游标类型。|  
|**acceptable_cursor_options**|**int**|为了支持语句的执行，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以隐式转换采用的游标选项。|  
|**merge_action_type**|**int**|触发器的执行计划用作的结果的类型**合并**语句。<br /><br /> 0 表示非触发器计划，不会执行的结果作为触发器计划**合并**语句或作为的结果执行的触发器计划**合并**语句，以便仅指定**删除**操作。<br /><br /> 1 表示**插入**触发器计划将运行的结果作为**合并**语句。<br /><br /> 2 表示**更新**触发器计划将运行的结果作为**合并**语句。<br /><br /> 3 表示**删除**触发器计划将运行的结果作为**合并**包含相应语句**插入**或**更新**操作。<br /><br /> <br /><br /> 对于运行由级联操作的嵌套触发器，该值是操作的**合并**语句导致 cascade。|  
|**default_schema_id**|**int**|默认架构，用于将不是完全限定的名称解析的 ID。|  
|**is_replication_specific**|**bit**|用于复制。|  
|**is_contained**|**varbinary(1)**|1 表示包含的数据库。|  
  
## <a name="permissions"></a>权限  
 需要**VIEW DATABASE STATE**权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys.database_query_store_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询存储存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt (Transact-SQL)](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
