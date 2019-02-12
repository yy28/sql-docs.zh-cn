---
title: sys.dm_pdw_component_health_active_alerts (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e396b20d2466c65a3ee91cbbb2770c6278c1b322
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56016098"
---
# <a name="sysdmpdwcomponenthealthactivealerts-transact-sql"></a>sys.dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  在存储活动警报[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]组件。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|唯一标识符[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]节点。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 构成此视图的键。|NOT NULL|  
|component_id|**int**|组件的 ID。 请参阅[sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 构成此视图的键。|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 构成此视图的键。|NOT NULL|  
|alert_id|**int**|警报类型的 ID。 请参阅[sys.pdw_health_alerts &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 构成此视图的键。|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|标识给定警报的实例。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 构成此视图的键。|NOT NULL|  
|current_value|**nvarchar(255)**|当警报类型 StatusChange 时使用。 这是当前的组件状态。 值为 NULL 的类型的阈值的警报。 请参阅[sys.pdw_health_alerts &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)有关的警报类型的列表。|NULL|  
|previous_value|**nvarchar(255)**|当警报类型 StatusChange 时使用。 这是以前的组件状态。 值为 NULL 的类型的阈值的警报。 请参阅[sys.pdw_health_alerts &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)有关的警报类型的列表。|NULL|  
|create_time|**datetime**|生成警报的日期和时间。|NOT NULL|  
  
 此视图按保留的最大行有关的信息，请参阅"最小值和最大值"中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
