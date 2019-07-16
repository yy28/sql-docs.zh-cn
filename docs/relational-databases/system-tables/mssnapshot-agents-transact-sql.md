---
title: MSsnapshot_agents (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshot_agents
- MSsnapshot_agents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_agents system table
ms.assetid: aeae0a2e-4c21-4c45-be65-1e426fa52bdd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2d57700abecccf3dae55289b49d4fd6c1af3e537
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079958"
---
# <a name="mssnapshotagents-transact-sql"></a>MSsnapshot_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshot_agents**表包含一行，为每个快照代理与本地分发服务器相关联。 此表存储在分发数据库中。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|快照代理的 ID。|  
|**name**|**nvarchar(100)**|快照代理的名称。|  
|**publisher_id**|**smallint**|发布服务器的 ID。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**publication**|**sysname**|发布的名称。|  
|**publication_type**|**int**|发布类型：<br /><br /> **0** = 事务。<br /><br /> **1** = 快照。<br /><br /> **2** = 合并。|  
|**local_job**|**bit**|指示在本地分发服务器上是否有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。|  
|**job_id**|**binary(16)**|作业标识号。|  
|**profile_id**|**int**|中的配置 ID [MSagent_profiles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)表。|  
|**dynamic_filter_login**|**sysname**|该值用于计算[SUSER_SNAME &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/suser-sname-transact-sql.md)中定义分区的参数化筛选器函数。 此列用于分区快照。|  
|**dynamic_filter_hostname**|**sysname**|该值用于计算[HOST_NAME &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/host-name-transact-sql.md)中定义分区的参数化筛选器函数。 此列用于分区快照。|  
|**publisher_security_mode**|**smallint**|连接到发布服务器上，可以是以下值之一时，代理所使用的安全模式：<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证。|  
|**publisher_login**|**sysname**|连接发布服务器时所使用的登录名。|  
|**publisher_password**|**nvarchar(524)**|连接发布服务器时所使用的密码的加密值。|  
|**job_step_uid**|**uniqueidentifier**|启动代理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤的唯一 ID。|  
|**job_login**|**sysname**||  
|**job_password**|**nvarchar(524)**||  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
