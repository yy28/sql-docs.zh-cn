---
title: "sys.dm_pdw_component_health_status (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 68cc3f7a-693c-4d5d-a76b-455352af8d7f
caps.latest.revision: "6"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d87c8ef38185e3194da1d13f8a9732991023f0ab
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwcomponenthealthstatus-transact-sql"></a>sys.dm_pdw_component_health_status (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存有关的当前运行状况的设备组件的信息。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**||不为 NULL|  
|component_id|int|组件的 ID。 请参阅[sys.pdw_health_components &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id、 component_id、 property_id 和 component_instance_id 窗体的密钥，此视图。|不为 NULL|  
|property_id|**int**|属性的 ID。 请参阅[sys.pdw_health_component_properties &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md).|NOT NULL|  
|component_instance_id|**nvarchar(255)**|标识组件的实例。 例如，CPU 的实例可能由 component_instance_id = CPU1。<br /><br /> pdw_node_id、 component_id、 property_id 和 component_instance_id 窗体的密钥，此视图。|NOT NULL|  
|property_value|**nvarchar(255)**|当前的属性值。|NULL|  
|update_time|**datetime**|更新该度量值的最后时间。|NOT NULL|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
