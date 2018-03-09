---
title: "MSreplication_subscriptions (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MSreplication_subscriptions
- MSreplication_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_subscriptions system table
ms.assetid: fd0c5843-4e9b-4448-8bfb-0a4067d1d8d1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3840528a0a566f250eae99c2764f64766c4e0891
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msreplicationsubscriptions-transact-sql"></a>MSreplication_subscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_subscriptions**表包含的每个分发代理维护本地订阅服务器数据库的复制信息的一行。 此表存储在订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**发布服务器**|**sysname**|发布服务器的名称。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**independent_agent**|**bit**|表明该发布是否有独立的分发代理。|  
|**subscription_type**|**int**|订阅的类型：<br /><br /> 0 = 推送。<br /><br /> 1 = 请求。<br /><br /> 2 = 匿名。|  
|**distribution_agent**|**sysname**|分发代理的名称。|  
|**Time**|**smalldatetime**|分发代理上次更新的时间。|  
|**说明**|**nvarchar(255)**|订阅的说明。|  
|**transaction_timestamp**|**varbinary(16)**|仅供内部使用。|  
|**update_mode**|**tinyint**|更新的类型。|  
|**agent_id**|**binary （16)**|代理的 ID。|  
|**subscription_guid**|**binary （16)**|发布上订阅版本的全局标识符。|  
|**subid**|**binary （16)**|匿名订阅的全局标识符。|  
|**immediate_sync**|**bit**|指示每次运行快照代理时是否创建或重新创建同步文件。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 &#40;Transact SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
