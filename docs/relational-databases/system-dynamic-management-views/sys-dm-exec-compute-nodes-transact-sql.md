---
description: sys.dm_exec_compute_nodes (Transact-SQL)
title: sys. dm_exec_compute_nodes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODES_TSQL
- DM_EXEC_COMPUTE_NODES
- SYS.DM_EXEC_COMPUTE_NODES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_nodes management view
- PolyBase, views
- PolyBase management views
- dm_exec_compute_nodes management view
ms.assetid: 0de4b7a4-401f-4e2d-9ab0-c54587e05154
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4e13b8a3a6514548b05b3663a4a785128e23c80d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454899"
---
# <a name="sysdm_exec_compute_nodes-transact-sql"></a>sys.dm_exec_compute_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保存有关用于 PolyBase 数据管理的节点的信息。 每个节点在表中各占一行。  
  
 使用此 DMV 查看向外扩展群集中所有节点的列表及其角色、名称和 IP 地址。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|**int**|与节点关联的唯一数字 id。 此视图的键。|在扩展群集中唯一，而不考虑类型。|  
|type|**nvarchar(32)**|节点的类型。|"COMPUTE"、"HEAD"|  
|name|**nvarchar(32)**|节点的逻辑名称。|任何适当长度的字符串。|  
|address|**nvarchar(32)**|此节点的 IP 地址。|IP 地址范围|  
  
## <a name="see-also"></a>另请参阅  
 [通过动态管理视图进行 PolyBase 故障排除](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
