---
title: MSqreader_agents (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSqreader_agents_TSQL
- MSqreader_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_agents system table
ms.assetid: dfa1f45e-c531-4385-a097-0a9edd1d7eab
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 68bca208f7e199ad65ff93a70f4d6c4a3b97fd8b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818819"
---
# <a name="msqreaderagents-transact-sql"></a>MSqreader_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSqreader_agents**表为本地分发服务器上运行每个队列读取器代理包含一行。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|队列读取器代理的 ID。|  
|**名称**|**nvarchar(100)**|队列读取器代理的名称。|  
|**job_id**|**binary(16)**|中的唯一作业 ID 号**sysjobs**表。|  
|**profile_id**|**int**|从配置文件 ID **MSagent_profiles**表。|  
|**job_step_uid**|**uniqueidentifier**|启动代理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤的唯一 ID。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
