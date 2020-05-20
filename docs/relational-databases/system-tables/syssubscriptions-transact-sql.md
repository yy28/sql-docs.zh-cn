---
title: syssubscriptions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions system table
ms.assetid: 106c1707-e0e0-49b4-ba50-25380c40fab2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0a7fa169bef5d105889bf9035155fef97505f723
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82812075"
---
# <a name="syssubscriptions-transact-sql"></a>syssubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  数据库中的每个订阅均包含一行。 该表存储在发布数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|项目的唯一 ID|  
|**srvid**|**smallint**|订阅服务器的服务器 ID。|  
|**dest_db**|**sysname**|目标数据库的名称。|  
|**status**|**tinyint**|订阅的状态：<br /><br /> **0** = 非活动。<br /><br /> **1** = 已订阅。<br /><br /> **2** = 活动。|  
|**sync_type**|**tinyint**|初始同步的类型：<br /><br /> **1** = 自动。<br /><br /> **2** = 无|  
|**login_name**|**sysname**|添加订阅时所使用的登录名。|  
|**subscription_type**|**int**|订阅的类型：<br /><br /> 0 = 推送 - 分发代理在分发服务器上运行。<br /><br /> 1 = 请求 - 分发代理在订阅服务器上运行。|  
|**distribution_jobid**|**binary(16)**|分发代理的作业 ID。|  
|**timestamp**|**timestamp**|时间戳。|  
|**update_mode**|**tinyint**|更新模式：<br /><br /> **0** = 只读。<br /><br /> **1** = 立即更新。|  
|**loopback_detection**|**bit**|适用于作为双向事务复制拓扑的一部分的订阅。 环回检测将确定分发代理是否将在订阅服务器上发起的事务发送回订阅服务器：<br /><br /> **0** = 发送回。<br /><br /> **1** = 不发送回。|  
|**queued_reinit**|**bit**|指定是否将项目标记为初始化或重新初始化。 如果值为**1** ，则指定订阅的项目已标记为进行初始化或重新初始化。|  
|**nosync_type**|**tinyint**|订阅初始化的类型：<br /><br /> **0** = 自动（快照）<br /><br /> **1** = 仅复制支持<br /><br /> **2** = 用备份初始化<br /><br /> **3** = 从日志序列号（LSN）初始化<br /><br /> 有关详细信息，请参阅[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)的** \@ sync_type**参数。|  
|**srvname**|**sysname**|订阅服务器的名称。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
