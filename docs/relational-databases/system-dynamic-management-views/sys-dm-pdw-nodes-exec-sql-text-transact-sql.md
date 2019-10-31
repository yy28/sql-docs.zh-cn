---
title: sys.databases _pdw_nodes_exec_sql_text （Transact-sql） |Microsoft Docs
description: 动态管理视图，它返回由指定的 sql_handle 标识的 SQL 批处理的文本。
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
ms.openlocfilehash: fd886217b2fb2caf0fe3f32e88b7bf0215ece1a9
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73145672"
---
# <a name="syspdw_nodes_dm_exec_sql_text-transact-sql"></a>sys.databases _nodes_dm_exec_sql_text （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

返回由指定的*sql_handle*标识的 SQL 批处理的文本。 此表值函数将替换系统函数**fn_get_sql**。  
   
## <a name="table-returned"></a>返回的表  
|列名|“名称”|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**smallint**|与节点关联的唯一数字 ID。|
|**dbid**|**int**|数据库的 ID。<br /><br /> 对于计划外和预定义 SQL 语句，是编译语句的数据库的 ID。|  
|**objectid**|**smallint**|对象的 ID。<br /><br /> 对于临时和预定义 SQL 语句为 NULL。|  
|**number**|**int**|对于带编号的存储过程，此列返回存储过程的编号。 有关详细信息，请参阅[numbered_procedures &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)。<br /><br /> 对于临时和预定义 SQL 语句为 NULL。|  
|**过**|**bit**|1： SQL 文本已加密。<br /><br /> 0：不加密 SQL 文本。|  
|**text**|**nvarchar(max)**|SQL 查询的文本。<br /><br /> 对于已加密对象为 NULL。|  

## <a name="remarks"></a>注释  
[_Exec_sql_text](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql?view=sql-server-ver15)中的相同备注适用。  
  
## <a name="permissions"></a>Permissions  
 要求具有服务器上的**sysadmin**服务器角色或 `VIEW SERVER STATE` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  

  ## <a name="next-steps"></a>后续步骤
 有关更多开发技巧，请参阅[SQL 数据仓库开发概述](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)。