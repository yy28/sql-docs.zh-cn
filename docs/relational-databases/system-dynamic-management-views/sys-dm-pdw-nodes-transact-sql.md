---
title: sys.dm_pdw_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a5df628a6b37c8d89843506c5b7f4c5050157158
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027388"
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关中的节点的所有信息[!INCLUDE[ssAPS](../../includes/ssaps-md.md)]。 它列出了每个节点在装置中的一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|与节点关联的唯一数字 id。<br /><br /> 此视图的键。|整个设备，而不考虑类型是唯一的。|  
|type|**nvarchar(32)**|节点的类型。|计算、 控制，管理|  
|NAME|**nvarchar(32)**|节点的逻辑名称。|适当的长度的任何字符串。|  
|address|**nvarchar(32)**|此节点的 IP 地址。|在 [0-255] 的格式。[0-255]。[0-255]。[0-255]。|  
|is_passive|**int**|指示运行该节点的虚拟机分配的服务器上运行还是已故障转移至备用服务器。|0-节点 VM 原始服务器上运行。<br /><br /> 1-节点 VM 备用服务器上运行。|  
|区域 (region)|**nvarchar(32)**|节点运行的区域。|PDW，HDINSIGHT|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
