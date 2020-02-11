---
title: MSlogreader_agents （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSlogreader_agents_TSQL
- MSlogreader_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSlogreader_agents system table
ms.assetid: 8baa3c5a-cb40-42d0-b966-00e6d55368e8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 802d2075a0146febc4521fb17b65f236533596bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907303"
---
# <a name="mslogreader_agents-transact-sql"></a>MSlogreader_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在本地分发服务器上运行的每个日志读取器代理在**MSlogreader_agents**表中各占一行。 此表存储在分发数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**识别**|**int**|日志读取器代理的 ID。|  
|**路径名**|**nvarchar （100）**|日志读取器代理的名称。|  
|**publisher_id**|**smallint**|发布服务器的 ID。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**local_job**|**bit**|指示在本地分发服务器上是否有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。|  
|**job_id**|**binary （16）**|作业标识号。|  
|**profile_id**|**int**|[MSagent_profiles](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)表中的配置 ID。|  
|**publisher_security_mode**|**smallint**|代理在连接到发布服务器时使用的安全模式，可以是以下项之一：<br /><br /> **** =  0[!INCLUDE[msCoName](../../includes/msconame-md.md)]身份[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]验证。<br /><br /> **** =  1[!INCLUDE[msCoName](../../includes/msconame-md.md)]个 Windows 身份验证。|  
|**publisher_login**|**sysname**|连接发布服务器时所使用的登录名。|  
|**publisher_password**|**nvarchar （524）**|连接发布服务器时所使用的密码的加密值。|  
|**job_step_uid**|**uniqueidentifier**|启动代理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤的唯一 ID。|  
|**job_login**|**sysname**||  
|**job_password**|**nvarchar （524）**||  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
