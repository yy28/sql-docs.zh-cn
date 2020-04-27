---
title: sys. dm_pdw_component_health_status （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 68cc3f7a-693c-4d5d-a76b-455352af8d7f
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 51e364650f8b8f8dae386126bdc820f9c72e571c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899513"
---
# <a name="sysdm_pdw_component_health_status-transact-sql"></a>sys. dm_pdw_component_health_status （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存有关设备组件的当前运行状况的信息。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**||不为 NULL|  
|component_id|int|组件的 ID。 请参阅[sys.databases &#40;transact-sql&#41;pdw_health_components ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> pdw_node_id、component_id、property_id 和 component_instance_id 构成此视图的键。|不为 NULL|  
|property_id|**int**|属性的 ID。 请参阅[sys.databases &#40;transact-sql&#41;pdw_health_component_properties ](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)。|NOT NULL|  
|component_instance_id|**nvarchar(255)**|标识组件的实例。 例如，可以 component_instance_id = "CPU1" 标识 CPU 的实例。<br /><br /> pdw_node_id、component_id、property_id 和 component_instance_id 构成此视图的键。|NOT NULL|  
|property_value|**nvarchar(255)**|当前属性值。|Null|  
|update_time|**datetime**|上次更新指标的时间。|NOT NULL|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
