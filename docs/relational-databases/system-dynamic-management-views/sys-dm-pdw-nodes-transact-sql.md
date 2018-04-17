---
title: sys.dm_pdw_nodes (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 267eac5c7f4aa7d73827f377002f4383374d853f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关中的节点的所有信息[!INCLUDE[ssAPS](../../includes/ssaps-md.md)]。 它列出每个设备中的节点的一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|与节点关联的唯一数字 id。<br /><br /> 此视图的键。|唯一的设备，无论何种类型。|  
|type|**nvarchar(32)**|节点的类型。|计算、 控制，管理|  
|name|**nvarchar(32)**|节点的逻辑名称。|相应的长度的任何字符串。|  
|address|**nvarchar(32)**|此节点的 IP 地址。|在 [0-255] 的格式。[0-255]。[0-255]。[0-255]。|  
|is_passive|**int**|指示运行节点的虚拟机分配的服务器上运行还是已故障转移到备用服务器。|0 – 节点 VM 在原始服务器上运行。<br /><br /> 1 – 节点 VM 备用服务器上运行。|  
|区域 (region)|**nvarchar(32)**|节点正在其中运行的区域。|PDW，HDINSIGHT|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
