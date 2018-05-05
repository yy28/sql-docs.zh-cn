---
title: syssubscriptions (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions system table
ms.assetid: 106c1707-e0e0-49b4-ba50-25380c40fab2
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 620cc0de62221ad784c4e38dbf51aba39eea5047
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="syssubscriptions-transact-sql"></a>syssubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  数据库中的每个订阅均包含一行。 该表存储在发布数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|项目的唯一 ID|  
|**srvid**|**int**|订阅服务器的服务器 ID。|  
|**dest_db**|**sysname**|目标数据库的名称。|  
|**status**|**tinyint**|订阅的状态：<br /><br /> **0** = 处于非活动状态。<br /><br /> **1** = 订阅。<br /><br /> **2** = 活动。|  
|**sync_type**|**tinyint**|初始同步的类型：<br /><br /> **1** = automatic。<br /><br /> **2** = none|  
|**login_name**|**sysname**|添加订阅时所使用的登录名。|  
|**subscription_type**|**int**|订阅的类型：<br /><br /> 0 = 推送 - 分发代理在分发服务器上运行。<br /><br /> 1 = 请求 - 分发代理在订阅服务器上运行。|  
|**distribution_jobid**|**binary(16)**|分发代理作业 ID。|  
|**timestamp**|**timestamp**|时间戳。|  
|**update_mode**|**tinyint**|更新模式：<br /><br /> **0** = 只是读取。<br /><br /> **1** = 立即更新。|  
|**loopback_detection**|**bit**|适用于作为双向事务复制拓扑的一部分的订阅。 环回检测将确定分发代理是否将在订阅服务器上发起的事务发送回订阅服务器：<br /><br /> **0**回 = 发送。<br /><br /> **1** = 不发回。|  
|**queued_reinit**|**bit**|指定是否将项目标记为初始化或重新初始化。 值为**1**指定订阅的项目被标记为初始化或重新初始化。|  
|**nosync_type**|**tinyint**|订阅初始化的类型：<br /><br /> **0** = automatic (snapshot)<br /><br /> **1** = 复制仅支持 32 位<br /><br /> **2** = 使用备份初始化<br /><br /> **3** = 从日志序列号 (LSN) 的初始化<br /><br /> 有关详细信息，请参阅**@sync_type**参数[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。|  
|**srvname**|**sysname**|订阅服务器的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
