---
title: "sys.dm_pdw_component_health_active_alerts (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: faf1def3ee0fe5c13a61eaf3101e40999200015f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwcomponenthealthactivealerts-transact-sql"></a>sys.dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  存储上的活动警报[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]组件。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|唯一标识符[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]节点。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 窗体的密钥，此视图。|NOT NULL|  
|component_id|**int**|组件的 ID。 请参阅[sys.pdw_health_components &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 窗体的密钥，此视图。|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 窗体的密钥，此视图。|NOT NULL|  
|alert_id|**int**|警报类型的 ID。 请参阅[sys.pdw_health_alerts &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 窗体的密钥，此视图。|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|标识给定警报实例。<br /><br /> pdw_node_id、 component_id、 component_instance_id、 alert_id 和 alert_instance_id 窗体的密钥，此视图。|NOT NULL|  
|current_value|**nvarchar(255)**|类型 StatusChange 的警报时使用。 这是当前的组件状态。 对于警报类型阈值的情况下，该值为 NULL。 请参阅[sys.pdw_health_alerts &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)有关的警报类型的列表。|NULL|  
|previous_value|**nvarchar(255)**|类型 StatusChange 的警报时使用。 这是以前的组件状态。 对于警报类型阈值的情况下，该值为 NULL。 请参阅[sys.pdw_health_alerts &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)有关的警报类型的列表。|NULL|  
|create_time|**datetime**|生成警报的日期和时间。|NOT NULL|  
  
 有关通过此视图保留最大行数的信息，请参阅"最小值和最大值"中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
