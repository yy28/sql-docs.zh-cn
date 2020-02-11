---
title: sys. dm_pdw_nodes （Transact-sql） |Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 61593522e09ed86ec10f08a6ad8ff7a941a2e10e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899347"
---
# <a name="sysdm_pdw_nodes-transact-sql"></a>sys. dm_pdw_nodes （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关中[!INCLUDE[ssAPS](../../includes/ssaps-md.md)]所有节点的信息。 它为设备中的每个节点列出一行。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|与节点关联的唯一数字 id。<br /><br /> 此视图的键。|在设备中唯一，而不考虑类型。|  
|type|**nvarchar （32）**|节点的类型。|"计算"、"控制" 和 "管理"|  
|name|**nvarchar （32）**|节点的逻辑名称。|任何适当长度的字符串。|  
|地址|**nvarchar （32）**|此节点的 IP 地址。|格式为 [0-255]。[0-255]。[0-255]。[0-255]。|  
|is_passive|**int**|指示运行该节点的虚拟机是在分配的服务器上运行还是已故障转移到备用服务器。|0-节点 VM 正在原始服务器上运行。<br /><br /> 1-节点 VM 正在备用服务器上运行。|  
|region|**nvarchar （32）**|节点正在其中运行的区域。|"PDW"、"HDINSIGHT"|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
