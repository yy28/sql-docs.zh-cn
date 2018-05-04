---
title: MSmerge_replinfo (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
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
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5e7aab7d91bafcb79b7db8367011b36bd893e35d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="msmergereplinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_replinfo**表包含每个订阅的一行。 此表可追踪有关订阅的信息。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|副本的唯一 ID。|  
|**use_interactive_resolver**|**bit**|指定调解期间是否使用交互式冲突解决程序。<br /><br /> **0** = 使用交互式冲突解决程序。<br /><br /> **1** = 使用交互式冲突解决程序。|  
|**validation_level**|**int**|对订阅执行的验证类型。 指定的验证级别可以是以下值之一：<br /><br /> **0**不 = 任何验证。<br /><br /> **1** = 仅限行计数验证。<br /><br /> **2** = 行计数和校验和验证。<br /><br /> **3** = 行计数和二进制校验和验证。|  
|**resync_gen**|**bigint**|用于重新同步订阅的生成数。 值为**为-1**指示订阅未标记为重新同步。|  
|**login_name**|**sysname**|创建订阅的用户名。|  
|**主机名**|**sysname**|为订阅生成分区时由参数化行筛选器使用的值。|  
|**merge_jobid**|**binary(16)**|此订阅的合并作业 ID。|  
|**sync_info**|**int**|仅供内部使用。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
