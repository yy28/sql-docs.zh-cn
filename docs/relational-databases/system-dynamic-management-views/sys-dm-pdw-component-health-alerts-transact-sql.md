---
title: "sys.dm_pdw_component_health_alerts (Transact SQL) |Microsoft 文档"
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
ms.assetid: 88f05392-1e97-4693-ba60-a4910af3c000
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2f8a0a4af0fafa03492217a72626c17e394c3afc
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwcomponenthealthalerts-transact-sql"></a>sys.dm_pdw_component_health_alerts (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  存储之前颁发装置的组件的警报。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|唯一标识符[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]节点。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 窗体的密钥，此视图。|NOT NULL|  
|component_id|**int**|组件的 ID。 请参阅[sys.pdw_health_components &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 窗体的密钥，此视图。|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 窗体的密钥，此视图。|NOT NULL|  
|alert_id|**int**|警报类型的 ID。 请参阅[sys.pdw_health_alerts &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 窗体的密钥，此视图。|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|标识给定警报实例。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 窗体的密钥，此视图。|NOT NULL|  
|previous_value|**nvarchar(255)**|类型 StatusChange 的警报时使用。 这是以前的组件状态。 对于警报类型阈值的情况下，该值为 NULL。 请参阅[sys.pdw_health_alerts &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)有关的警报类型的列表。|NULL|  
|current_value|**nvarchar(255)**|类型 StatusChange 的警报时使用。 这是当前的组件状态。 对于警报类型阈值的情况下，该值为 NULL。 请参阅[sys.pdw_health_alerts &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)有关的警报类型的列表。|NULL|  
|create_time|**datetime**|生成警报的日期和时间。|NOT NULL|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
