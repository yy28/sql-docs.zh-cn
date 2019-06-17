---
title: sys.dm_pdw_component_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7b3c6cb1c61c15cb81a5c9452b874263cf62bc02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690501"
---
# <a name="sysdmpdwcomponenthealthalerts-transact-sql"></a>sys.dm_pdw_component_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  存储以前颁发的有关设备组件的通知。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|唯一标识符[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]节点。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 构成此视图的键。|NOT NULL|  
|component_id|**int**|组件的 ID。 请参阅[sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 构成此视图的键。|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 构成此视图的键。|NOT NULL|  
|alert_id|**int**|警报类型的 ID。 请参阅[sys.pdw_health_alerts &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 构成此视图的键。|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|标识给定警报的实例。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 构成此视图的键。|NOT NULL|  
|previous_value|**nvarchar(255)**|当警报类型 StatusChange 时使用。 这是以前的组件状态。 值为 NULL 的类型的阈值的警报。 请参阅[sys.pdw_health_alerts &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)有关的警报类型的列表。|NULL|  
|current_value|**nvarchar(255)**|当警报类型 StatusChange 时使用。 这是当前的组件状态。 值为 NULL 的类型的阈值的警报。 请参阅[sys.pdw_health_alerts &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)有关的警报类型的列表。|NULL|  
|create_time|**datetime**|生成警报的日期和时间。|NOT NULL|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
