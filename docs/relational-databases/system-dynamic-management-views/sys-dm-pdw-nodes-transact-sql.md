---
title: sys.dm_pdw_nodes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6b2a17f1fd57b70dbee056e66a76c0416b0a25c1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533575"
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (Transact SQL)
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
  
  
