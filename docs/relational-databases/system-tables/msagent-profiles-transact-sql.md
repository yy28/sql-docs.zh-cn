---
title: MSagent_profiles (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 99ba1785ffebebf87556258dbcf0278bebbf237d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817139"
---
# <a name="msagentprofiles-transact-sql"></a>MSagent_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSagent_profiles**表包含每个定义的复制代理配置文件的一行。 此表存储中**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|配置文件 id。|  
|**profile_name**|**sysname**|代理类型的唯一配置文件名。|  
|**agent_type**|**int**|代理的类型：<br /><br /> **1** = 快照代理<br /><br /> **2** = 日志读取器代理<br /><br /> **3** = 分发代理<br /><br /> **4** = 合并代理<br /><br /> **9** = 队列读取器代理|  
|**类型**|**int**|配置文件的类型：<br /><br /> **0** = 系统**1** = 自定义|  
|**description**|**nvarchar(3000)**|配置文件的说明。|  
|**def_profile**|**bit**|指定该配置文件是否是该代理类型的默认值。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
