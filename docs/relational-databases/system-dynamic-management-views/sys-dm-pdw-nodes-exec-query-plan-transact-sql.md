---
title: sys.databases _pdw_nodes_exec_query_plan （Transact-sql） |Microsoft Docs
description: 动态管理视图，以 XML 格式返回计划句柄指定的批处理的显示计划。 计划句柄指定的计划可以处于缓存或正在执行状态。
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 96b499ea5bc38d2a4cf9c380116108009ea46086
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145632"
---
# <a name="syspdw_nodes_dm_exec_query_plan-transact-sql"></a>sys.databases _nodes_dm_exec_query_plan （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

以 XML 格式返回计划句柄指定的批查询的显示计划。 计划句柄指定的计划可以处于缓存或正在执行状态。  

## <a name="table-returned"></a>返回的表  
  
|列名|“名称”|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**smallint**|与节点关联的唯一数字 ID。| 
|**dbid**|**int**|在编译对应于此计划的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句时有效的上下文数据库的 ID。 对于计划外和预定义 SQL 语句，是编译语句的数据库的 ID。<br /><br /> 此列可为空值。|  
|**objectid**|**smallint**|此查询计划的对象（如存储过程或用户定义函数）的 ID。 对于即席和已准备批处理，此列为**null**。<br /><br /> 此列可为空值。|  
|**number**|**int**|为存储过程编号的整数。 对于即席和已准备批处理，此列为**null**。<br /><br /> 此列可为空值。| 
|**过**|**bit**|指示对应的存储过程是否已加密。<br /><br /> 0 = 未加密<br /><br /> 1 = 已加密<br /><br /> 此列不可为空值。|  
|**query_plan**|**xml**|包含用*plan_handle*指定的查询执行计划的编译时显示计划表示形式。 显示计划的格式为 XML。 为包含即席 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句、存储过程调用以及用户定义函数调用等内容的每个批查询生成一个计划。<br /><br /> 此列可为空值。|  
  
## <a name="remarks"></a>注释  
[_Exec_query_plan](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql?view=sql-server-ver15)中的相同备注适用。  
  
## <a name="permissions"></a>Permissions  
 要求具有服务器上的**sysadmin**服务器角色或 `VIEW SERVER STATE` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

 ## <a name="next-steps"></a>后续步骤
 有关更多开发技巧，请参阅[SQL 数据仓库开发概述](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)。