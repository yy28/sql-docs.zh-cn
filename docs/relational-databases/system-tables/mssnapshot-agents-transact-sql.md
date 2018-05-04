---
title: MSsnapshot_agents (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- MSsnapshot_agents
- MSsnapshot_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_agents system table
ms.assetid: aeae0a2e-4c21-4c45-be65-1e426fa52bdd
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8dfe60e5ae1ad3443fde1b7655941b70f53663cd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mssnapshotagents-transact-sql"></a>MSsnapshot_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshot_agents**表包含一个行，每个快照代理程序与本地分发服务器关联。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|快照代理的 ID。|  
|**名称**|**nvarchar(100)**|快照代理的名称。|  
|**publisher_id**|**int**|发布服务器的 ID。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**publication_type**|**int**|发布类型：<br /><br /> **0** = 事务。<br /><br /> **1** = 快照。<br /><br /> **2** = 合并。|  
|**local_job**|**bit**|指示在本地分发服务器上是否有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。|  
|**job_id**|**binary(16)**|作业标识号。|  
|**profile_id**|**int**|中的配置 ID [MSagent_profiles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)表。|  
|**dynamic_filter_login**|**sysname**|用于评估的值[SUSER_SNAME &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/suser-sname-transact-sql.md)中定义分区的参数化筛选器函数。 此列用于分区快照。|  
|**dynamic_filter_hostname**|**sysname**|用于评估的值[HOST_NAME &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/host-name-transact-sql.md)中定义分区的参数化筛选器函数。 此列用于分区快照。|  
|**publisher_security_mode**|**int**|连接到发布服务器，可以是以下之一时使用代理的安全模式：<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证。|  
|**publisher_login**|**sysname**|连接发布服务器时所使用的登录名。|  
|**publisher_password**|**nvarchar(524)**|连接发布服务器时所使用的密码的加密值。|  
|**job_step_uid**|**uniqueidentifier**|启动代理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤的唯一 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
