---
title: "sp_query_store_reset_exec_stats (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_query_store_reset_exec_stats_TSQL
- sys.sp_query_store_reset_exec_stats_TSQL
- sys.sp_query_store_reset_exec_stats
- sp_query_store_reset_exec_stats
dev_langs: TSQL
helpviewer_keywords:
- sp_query_store_reset_exec_stats
- sys.sp_query_store_reset_exec_stats
ms.assetid: 899df1ff-e871-44df-9361-f3b87ac3ea31
caps.latest.revision: "6"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 782f8c1869efcdd69dcf87afcc53fd300423a6f1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spquerystoreresetexecstats-transact-sql"></a>sp_query_store_reset_exec_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  清除查询存储区中的特定查询计划的运行时统计信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_query_store_reset_exec_stats [ @plan_id = ] plan_id [;]  
```  
  
## <a name="arguments"></a>参数  
 [  **@plan_id =** ] *plan_id*  
 是查询计划对要清除的 id。 *plan_id*是**bigint**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
  
## <a name="permissions"></a>Permissions  
 需要**执行**对数据库拥有权限和**删除**查询存储目录视图的权限。  
  
## <a name="examples"></a>示例  
 下面的示例返回查询存储中查询的相关信息。  
  
```  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
  
 确定你想要清除统计信息 plan_id 后，使用下面的示例删除的特定查询计划的执行统计信息。 此示例将删除计划编号 3 的执行统计信息。  
  
```  
EXEC sp_query_store_reset_exec_stats 3;  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_query_store_force_plan &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_query &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [sp_query_store_unforce_plan &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [sp_query_store_remove_plan &#40;这 SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_flush_db &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)   
 [查询存储目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [使用查询存储来监视性能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
