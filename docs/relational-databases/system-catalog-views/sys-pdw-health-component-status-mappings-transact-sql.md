---
title: sys.pdw_health_component_status_mappings (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4b2d572b79c15c369e33190c183c249de3b8fb0c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="syspdwhealthcomponentstatusmappings-transact-sql"></a>sys.pdw_health_component_status_mappings (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  定义之间的映射[!INCLUDE[ssDW](../../includes/ssdw-md.md)]组件状态和制造商定义的组件名称。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|属性的唯一标识符。<br /><br /> property_id、 component_id 和 physical_name 窗体的密钥，此视图。|NOT NULL|  
|component_id|**int**|组件的 ID。 请参阅[sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> property_id、 component_id 和 physical_name 窗体的密钥，此视图。|NOT NULL|  
|physical_name|**nvarchar(32)**|由制造商定义的属性名称。<br /><br /> property_id、 component_id 和 physical_name 窗体的密钥，此视图。|NOT NULL|  
|logical_name|**nvarchar(255)**|属性名称由定义[!INCLUDE[ssDW](../../includes/ssdw-md.md)]。|NOT NULL<br /><br /> 0-设备实例都是唯一的。<br /><br /> 1-设备实例不是唯一的。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
