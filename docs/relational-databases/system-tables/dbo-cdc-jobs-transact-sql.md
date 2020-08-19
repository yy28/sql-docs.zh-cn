---
description: dbo.cdc_jobs (Transact-SQL)
title: cdc_jobs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc_jobs
- cdc_jobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.cdc_jobs
ms.assetid: 85e2d580-1c54-4b81-b7e6-2e12997199fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ccb4db642eb449dfad33e5b1cd1f92aad59ddc6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419171"
---
# <a name="dbocdc_jobs-transact-sql"></a>dbo.cdc_jobs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  存储用于捕获和清除作业的变更数据捕获配置参数。 此表存储在 **msdb**中。  
  
 
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|特定数据库的 ID，作业在此数据库中运行。|  
|**job_type**|**nvarchar (20) **|作业的类型，为“capture”或“cleanup”。|  
|**job_id**|**uniqueidentifier**|与作业关联的唯一 ID。|  
|**maxtrans**|**int**|在每个扫描循环中要处理的最大事务数。<br /><br /> **maxtrans** 仅对捕获作业有效。|  
|**maxscans**|**int**|为了从日志中提取所有行而要执行的扫描周期的最大数目。<br /><br /> **maxscans** 仅对捕获作业有效。|  
|**持续**|**bit**|指示捕获作业是连续运行 (1) 还是以一次性模式运行 (0) 的标志。 有关详细信息，请参阅 [sys.databases&#41;sp_cdc_add_job &#40;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)。<br /><br /> **连续** 仅对捕获作业有效。|  
|**pollinginterval**|**bigint**|日志扫描循环之间间隔的秒数。<br /><br /> **pollinginterval** 仅对捕获作业有效。|  
|**保留**|**bigint**|更改行要在更改表中保留的分钟数。<br /><br /> **保留** 仅对清除作业有效。|  
|**threshold**|**bigint**|清除时可以使用一条语句删除的删除条目的最大数量。|  
  
## <a name="see-also"></a>另请参阅  
 [sys. sp_cdc_add_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)   
 [sys. sp_cdc_change_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)   
 [sys. sp_cdc_help_jobs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)   
 [sys. sp_cdc_drop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-drop-job-transact-sql.md)  
  
  
