---
title: sys. query_store_runtime_stats_interval （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_RUNTIME_STATS_INTERVAL
- SYS.QUERY_STORE_RUNTIME_STATS_INTERVAL
- QUERY_STORE_RUNTIME_STATS_INTERVAL_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS_INTERVAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_store_runtime_stats_interval catalog view
- query_store_runtime_stats_interval catalog view
ms.assetid: 2be83785-0569-41a3-88c8-59bfa0932e6e
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f4c652ee6f0634816a4bc5313c968ee2e59197b5
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834108"
---
# <a name="sysquery_store_runtime_stats_interval-transact-sql"></a>sys. query_store_runtime_stats_interval （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含有关查询的运行时执行统计信息收集到的每个间隔的开始和结束时间的信息。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**runtime_stats_interval_id**|**bigint**|主密钥。|
|**start_time**|**datetimeoffset**|间隔的开始时间。|
|**end_time**|**datetimeoffset**|间隔的结束时间。|
|**comment**|**nvarchar(32)**|始终为 NULL。|
  
## <a name="permissions"></a>权限  
 需要**VIEW DATABASE STATE**权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys. database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys. query_context_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys. query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys. query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys. query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys. query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [相关视图、函数和过程](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询存储存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
