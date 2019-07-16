---
title: syssubscriptions （系统视图） (TRANSACT-SQL) |Microsoft Docs
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
- syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3a50ce1b42c8963aac0bc152e08c6d39eec73eb2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094777"
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions（系统视图）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Syssubscriptions**视图显示订阅信息。 此视图存储在分发数据库中。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|订阅项目的唯一 ID。|  
|**srvid**|**smallint**|订阅服务器的服务器 ID。|  
|**dest_db**|**sysname**|订阅数据库的名称。|  
|**status**|**tinyint**|订阅的状态：<br /><br /> **0** = 非活动状态。<br /><br /> **1** = 订阅。<br /><br /> **2** = 活动。|  
|**sync_type**|**tinyint**|初始同步的类型：<br /><br /> **1** = automatic。<br /><br /> **2** = none。|  
|**login_name**|**sysname**|连接到发布服务器以添加订阅时使用的登录名。|  
|**subscription_type**|**int**|订阅的类型：<br /><br /> **0** = 推送-分发代理在分发服务器上运行。<br /><br /> **1** = 请求-分发代理在订阅服务器上运行。|  
|**distribution_jobid**|**binary(16)**|标识用于同步订阅的分发代理作业。|  
|**timestmap**|**timestamp**|创建订阅的日期和时间。|  
|**update_mode**|**tinyint**|更新模式：<br /><br /> **0** = 只读的。<br /><br /> **1** = 立即更新。|  
|**loopback_detection**|**bit**|适用于作为双向事务复制拓扑的一部分的订阅。 环回检测将确定分发代理是否将在订阅服务器上发起的事务发送回订阅服务器：<br /><br /> **0** = 发送回。<br /><br /> **1** = 不发回。|  
|**queued_reinit**|**bit**|指定是否将项目标记为初始化或重新初始化。 值为**1**指定订阅的项目标记为初始化或重新初始化。|  
|**nosync_type**|**tinyint**|订阅初始化的类型：<br /><br /> **0** = 自动 （快照）<br /><br /> **1** = 仅支持复制<br /><br /> **2** = 使用备份初始化<br /><br /> **3** = 从日志序列号 (LSN) 初始化<br /><br /> 有关详细信息，请参阅 **@sync_type** 参数[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。<br /><br /> **3** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|订阅服务器的名称。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [syssubscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
