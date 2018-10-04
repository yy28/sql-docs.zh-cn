---
title: dbo.cdc_jobs (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 321e6b1809f6dc8f30710c98665316c50a6ab50a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47719747"
---
# <a name="dbocdcjobs-transact-sql"></a>dbo.cdc_jobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  存储用于捕获和清除作业的变更数据捕获配置参数。 此表存储中**msdb**。  
  
 
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|特定数据库的 ID，作业在此数据库中运行。|  
|**job_type**|**nvarchar(20)**|作业的类型，为“capture”或“cleanup”。|  
|**job_id**|**uniqueidentifier**|与作业关联的唯一 ID。|  
|**maxtrans**|**int**|在每个扫描循环中要处理的最大事务数。<br /><br /> **maxtrans**仅对捕获作业有效。|  
|**maxscans**|**int**|最大扫描循环要执行，以从日志提取所有行数。<br /><br /> **maxscans**仅对捕获作业有效。|  
|**连续**|**bit**|指示捕获作业是连续运行 (1) 还是以一次性模式运行 (0) 的标志。 有关详细信息，请参阅[sys.sp_cdc_add_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)。<br /><br /> **连续**仅对捕获作业有效。|  
|**pollinginterval**|**bigint**|日志扫描循环之间间隔的秒数。<br /><br /> **pollinginterval**仅对捕获作业有效。|  
|**保留期**|**bigint**|更改行要在更改表中保留的分钟数。<br /><br /> **保留期**仅对清除作业有效。|  
|**threshold**|**bigint**|清除时可以使用一条语句删除的删除条目的最大数量。|  
  
## <a name="see-also"></a>请参阅  
 [sys.sp_cdc_add_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)   
 [sys.sp_cdc_change_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)   
 [sys.sp_cdc_help_jobs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)   
 [sys.sp_cdc_drop_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-drop-job-transact-sql.md)  
  
  
