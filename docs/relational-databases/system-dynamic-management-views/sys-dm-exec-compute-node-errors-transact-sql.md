---
title: sys. dm_exec_compute_node_errors （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
- DM_EXEC_COMPUTE_NODE_ERRORS
- DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase
- PolyBase, views
- dm_exec_compute_node_errors
- sys.dm_exec_compute_node_errors management view
ms.assetid: 9a03c039-70e4-4974-95d8-d3fa45984ffb
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5de36530fcf50a403558cb97fa72ad6a2d126e32
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830679"
---
# <a name="sysdm_exec_compute_node_errors-transact-sql"></a>sys.dm_exec_compute_node_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  返回 PolyBase 计算节点上发生的错误。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|error_id|`nvarchar(36)`|与错误关联的唯一数字 id。|系统中所有查询错误的唯一性|  
|源|`nvarchar(255)`|源线程或进程说明||  
|类型|`nvarchar(255)`|错误类型。||  
|create_time|`datetime`|发生错误的时间||  
|compute_node_id|`int`|特定计算节点的标识符|请参阅 compute_node_id [dm_exec_compute_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|  
|rexecution_id|`nvarchar(36)`|PolyBase 查询的标识符（如果有）。||  
|spid|`int`|SQL Server 会话的标识符||  
|thread_id|`int`|发生错误的线程的数值标识符。||  
|详细信息|nvarchar(4000)|错误详细信息的完整说明。||
|compute_pool_id|`int`|池的唯一标识符。|

  
## <a name="see-also"></a>另请参阅  
 [通过动态管理视图进行 PolyBase 故障排除](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
