---
title: dbo.sysjobactivity (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysjobactivity_TSQL
- dbo.sysjobactivity
- sysjobactivity
- sysjobactivity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobactivity system table
ms.assetid: fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a1d9e79856ac767d231993165b0c6d565d791464
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="dbosysjobactivity-transact-sql"></a>dbo.sysjobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  记录当前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业活动和状态。  此表存储在**msdb**数据库。
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|存储在会话 ID **syssessions**表中**msdb**数据库。|  
|**job_id**|**uniqueidentifier**|作业 ID。|  
|**run_requested_date**|**datetime**|请求运行作业的日期和时间。|  
|**run_requested_source**|**sysname(nvarchar(128))**|请求运行作业的请求者。<br /><br /> **1** = SOURCE_SCHEDULER<br /><br /> **2** = SOURCE_ALERTER<br /><br /> **3** = SOURCE_BOOT<br /><br /> **4** = SOURCE_USER<br /><br /> **6** = SOURCE_ON_IDLE_SCHEDULE|  
|**queued_date**|**datetime**|该作业排队的日期和时间。 如果直接运行该作业，则此列为 NULL。|  
|**start_execution_date**|**datetime**|计划运行作业的日期和时间。|  
|**last_executed_step_id**|**int**|上一个运行的作业步骤的 ID。|  
|**last_executed_step_**<br /><br /> **date**|**datetime**|上一个作业步骤开始运行的日期和时间。|  
|**stop_execution_date**|**datetime**|作业完成运行的日期和时间。|  
|**job_history_id**|**int**|用于标识中的行**sysjobhistory**表。|  
|**next_scheduled_run_date**|**datetime**|下一步的日期和作业计划运行的时间。|  

## <a name="example"></a>示例
此示例将返回所有 SQL Server 代理作业的运行时状态。  在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中执行以下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
```sql
SELECT sj.Name, 
    CASE
        WHEN sja.start_execution_date IS NULL THEN 'Not running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NULL THEN 'Running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NOT NULL THEN 'Not running'
    END AS 'RunStatus'
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobactivity sja
ON sj.job_id = sja.job_id
WHERE session_id = (
    SELECT MAX(session_id) FROM msdb.dbo.sysjobactivity); 
```
  
## <a name="see-also"></a>另请参阅  
 [dbo.sysjobhistory &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
  
