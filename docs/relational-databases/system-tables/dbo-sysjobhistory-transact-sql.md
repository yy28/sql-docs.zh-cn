---
title: dbo.sysjobhistory (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/24/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobhistory_TSQL
- dbo.sysjobhistory
- sysjobhistory
- sysjobhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobhistory system table
ms.assetid: 1b1fcdbb-2af2-45e6-bf3f-e8279432ce13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 809e8c80ec1734c24f6930b4042b5e1a84356597
ms.sourcegitcommit: 65ceea905030582f8d89e75e97758abf3b1f0bd6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2019
ms.locfileid: "67400106"
---
# <a name="dbosysjobhistory-transact-sql"></a>dbo.sysjobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

包含有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理执行预定作业的信息。
  
> [!NOTE]
> 在大多数情况下，仅作业步骤完成，并且表通常包含有关当前正在进行的作业步骤的任何记录之后，但在某些情况下，基本过程更新的数据*执行*提供有关中的信息正在进行的作业步骤。

此表存储中**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|行的唯一标识符。|  
|**job_id**|**uniqueidentifier**|作业 ID。|  
|**step_id**|**int**|作业中步骤的 ID。|  
|**step_name**|**sysname**|步骤的名称。|  
|**sql_message_id**|**int**|作业失败时返回的任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息的 ID。|  
|**sql_severity**|**int**|任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的严重级别。|  
|message |**nvarchar(4000)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的文本（如果有）。|  
|**run_status**|**int**|作业的执行状态：<br /><br /> **0** = 失败<br /><br /> **1** = 成功<br /><br /> **2** = 重试<br /><br /> **3** = 已取消<br /><br />**4** = 正在进行|  
|**run_date**|**int**|日期作业或步骤开始的执行。 对于正在进行中的历史记录，这是写入历史记录的日期/时间。|  
|**run_time**|**int**|作业或步骤开始的时间。|  
|**run_duration**|**int**|中的作业或步骤中的执行的运行时间**HHMMSS**格式。|  
|**operator_id_emailed**|**int**|作业完成时通知的操作员的 ID。|  
|**operator_id_netsent**|**int**|作业完成时用消息通知的操作员的 ID。|  
|**operator_id_paged**|**int**|作业完成时用寻呼通知的操作员的 ID。|  
|**retries_attempted**|**int**|尝试执行作业或步骤的重试次数。|  
|服务器 |**sysname**|执行作业时所在服务器的名称。|  
  
  ## <a name="example"></a>示例
 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]查询会将转换**run_time**并**运行时间**为更多的用户友好格式的列。  执行中的脚本[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
 
 ```sql
 SET NOCOUNT ON;
 
 SELECT sj.name,
        sh.run_date,
        sh.step_name,
        STUFF(STUFF(RIGHT(REPLICATE('0', 6) +  CAST(sh.run_time as varchar(6)), 6), 3, 0, ':'), 6, 0, ':') 'run_time',
        STUFF(STUFF(STUFF(RIGHT(REPLICATE('0', 8) + CAST(sh.run_duration as varchar(8)), 8), 3, 0, ':'), 6, 0, ':'), 9, 0, ':') 'run_duration (DD:HH:MM:SS)  '
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobhistory sh
ON sj.job_id = sh.job_id
```
