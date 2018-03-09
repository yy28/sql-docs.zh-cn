---
title: "MSsubscription_agents (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
applies_to:
- SQL Server
f1_keywords:
- MSsubscription_agents
- MSsubscription_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_agents system table
ms.assetid: 86ad5891-0bef-4963-9381-7d5b45245a0c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 11ad8bb029c1a083a4490cfe62e2bacf54b37d01
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssubscriptionagents-transact-sql"></a>MSsubscription_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_agents**表由分发代理和触发器的可更新的订阅来跟踪订阅属性。 此表存储在订阅数据库中。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|行的 ID。|  
|**发布服务器**|**sysname**|发布服务器的名称。|  
|**publisher_db**|**sysname**|发布数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**subscription_type**|**int**|订阅类型：<br /><br /> 0 = 推送。<br /><br /> 1 = 请求<br /><br /> 2 = 匿名请求。|  
|**queue_id**|**sysname**|ID[!INCLUDE[msCoName](../../includes/msconame-md.md)]消息发布服务器上的队列。 *queue_id*设置为**SQL**的基于 SQL 的排队更新。|  
|**update_mode**|**tinyint**|更新的类型：<br /><br /> **0** = 只读的。<br /><br /> **1** = 立即更新。<br /><br /> **2** = 使用消息队列的已排队更新。<br /><br /> **3** = 即时使用排队更新作为故障转移使用消息队列来更新。<br /><br /> **4** = 使用 SQL Server 队列的已排队更新。<br /><br /> **5** = 具有排队的更新故障转移功能，使用 SQL Server 队列立即更新。|  
|**failover_mode**|**bit**|如果选择了更新的故障转移类型，则此参数值为选择的故障转移类型：<br /><br /> **0** = 即时更新正在使用。 不启用故障转移。<br /><br /> **1** = 已排队更新正在使用。 已启用故障转移。 中指定为故障转移正在使用的队列*update_mode*值。|  
|**spid**|**int**|当前正在运行或刚运行过的分发代理使用的连接的系统进程 ID。|  
|**login_time**|**datetime**|当前正在运行或刚运行过的分发代理连接的日期和时间。|  
|**allow_subscription_copy**|**bit**|指定是否允许使用复制订阅数据库的功能。|  
|**attach_state**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**attach_version**|**binary （16)**|代表附加订阅版本的唯一标识符。|  
|**last_sync_status**|**int**|当前正在运行或刚运行过的分发代理的最后运行状态。 状态可以为：<br /><br /> **1** = 启动。<br /><br /> **2** = 成功。<br /><br /> **3** = 正在进行。<br /><br /> **4** = 空闲。<br /><br /> **5** = 重试。<br /><br /> **6** = 失败。|  
|**last_sync_summary**|**sysname**|当前正在运行或刚运行过的分发代理的上一条消息。 状态可以为：<br /><br /> **启动。**<br /><br /> **已成功。**<br /><br /> **正在进行。**<br /><br /> **空闲。**<br /><br /> **重试。**<br /><br /> **失败。**|  
|**last_sync_time**|**datetime**|日期和时间*last_sync_summary*和*last_sync_status*列已更新。 作为 SqlServer 代理服务作业运行的请求分发代理或匿名分发代理不更新这些列。 在这种情况下，会将历史记录信息记录到作业历史表中。|  
|**queue_server**|**sysname**|仅限内部使用。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 &#40;Transact SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)  
  
  
