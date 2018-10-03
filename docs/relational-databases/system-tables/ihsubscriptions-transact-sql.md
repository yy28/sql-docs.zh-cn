---
title: IHsubscriptions (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- IHsubscriptions_TSQL
- IHsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- IHsubscriptions system table
ms.assetid: 9ec21119-35f1-4e39-abaa-b2c790c485b1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8f3b3727c7a332fb96cafaa7376d3a5ca67fff66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47688425"
---
# <a name="ihsubscriptions-transact-sql"></a>IHsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHsubscriptions**系统表中占一行为每个订阅的发布从非 SQL Server 发布服务器使用当前分发服务器。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|唯一地标识已发布的项目。|  
|**srvid**|**smallint**|订阅服务器的服务器 ID。|  
|**dest_db**|**sysname**|目标数据库的名称|  
|**login_name**|**sysname**|添加订阅时所使用的登录名。|  
|**distribution_jobid**|**binary(16)**|分发代理的作业 ID|  
|**timestamp**|**timestamp**|创建订阅的日期和时间。|  
|**queued_reinit**|**bit**|指定是否将项目标记为初始化或重新初始化。 值为**1**指定订阅的项目标记为初始化或重新初始化。|  
|**status**|**tinyint**|订阅的状态：<br /><br /> **0** = 非活动状态。<br /><br /> **1** = 订阅。<br /><br /> **2** = 活动。|  
|**sync_type**|**tinyint**|初始同步的类型：<br /><br /> **1** = automatic。<br /><br /> **2** = none。|  
|**subscription_type**|**int**|订阅的类型：<br /><br /> **0** = 推送-分发代理在订阅服务器上运行。<br /><br /> **1** = 请求-分发代理在分发服务器上运行。|  
|**update_mode**|**tinyint**|更新模式：<br /><br /> **0** = 只读的。<br /><br /> **1** = 立即更新。|  
|**loopback_detection**|**bit**|适用于作为双向事务复制拓扑的一部分的订阅。 环回检测将确定分发代理是否将在订阅服务器上发起的事务发送回订阅服务器：<br /><br /> **0** = 发送回。<br /><br /> **1** = 不发回。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
