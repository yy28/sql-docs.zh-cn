---
title: sys. pdw_health_component_status_mappings （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ec631e9008cc37a7b4f91ed3f530e5388bdf9c0d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127502"
---
# <a name="syspdw_health_component_status_mappings-transact-sql"></a>sys. pdw_health_component_status_mappings （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  定义[!INCLUDE[ssDW](../../includes/ssdw-md.md)]组件状态与制造商定义的组件名称之间的映射。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|属性的唯一标识符。<br /><br /> property_id、component_id 和 physical_name 构成此视图的键。|NOT NULL|  
|component_id|**int**|组件的 ID。 请参阅[sys.databases &#40;transact-sql&#41;pdw_health_components ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> property_id、component_id 和 physical_name 构成此视图的键。|NOT NULL|  
|physical_name|**nvarchar （32）**|制造商定义的属性名称。<br /><br /> property_id、component_id 和 physical_name 构成此视图的键。|NOT NULL|  
|logical_name|**nvarchar(255)**|由定义的[!INCLUDE[ssDW](../../includes/ssdw-md.md)]属性名称。|NOT NULL<br /><br /> 0-设备实例是唯一的。<br /><br /> 1-设备实例不唯一。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
