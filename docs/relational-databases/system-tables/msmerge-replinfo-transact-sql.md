---
title: MSmerge_replinfo (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 045f9ab13b701b8dbd5e0895531932c21767853f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909062"
---
# <a name="msmergereplinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_replinfo**表包含每个订阅占一行。 此表可追踪有关订阅的信息。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|副本的唯一 ID。|  
|**use_interactive_resolver**|**bit**|指定调解期间是否使用交互式冲突解决程序。<br /><br /> **0** = 使用交互式冲突解决程序。<br /><br /> **1** = 使用交互式冲突解决程序。|  
|**validation_level**|**int**|对订阅执行的验证类型。 指定的验证级别可以是以下值之一：<br /><br /> **0** = 不验证。<br /><br /> **1** = 仅限行计数验证。<br /><br /> **2** = 验证行计数和校验和。<br /><br /> **3** = 行计数和二进制校验和验证。|  
|**resync_gen**|**bigint**|用于重新同步订阅的生成数。 值为**为-1**指示订阅未标记为重新同步。|  
|**login_name**|**sysname**|创建订阅的用户名。|  
|**主机名**|**sysname**|为订阅生成分区时由参数化行筛选器使用的值。|  
|**merge_jobid**|**binary(16)**|此订阅的合并作业 ID。|  
|**sync_info**|**int**|仅供内部使用。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
