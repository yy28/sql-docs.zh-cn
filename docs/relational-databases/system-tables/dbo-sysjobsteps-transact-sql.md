---
title: dbo.sysjobsteps (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysjobsteps
- dbo.sysjobsteps_TSQL
- sysjobsteps
- sysjobsteps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobsteps system table
ms.assetid: 978b8205-535b-461c-91f3-af9b08eca467
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5fff8cb852214733a96d1641cd767d578420cb9a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259387"
---
# <a name="dbosysjobsteps-transact-sql"></a>dbo.sysjobsteps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理要执行的作业中的各个步骤的信息。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|作业 ID。|  
|**step_id**|**int**|作业中步骤的 ID。|  
|**step_name**|**sysname**|作业步骤的名称。|  
|**subsystem**|**nvarchar(40)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理用于执行作业步骤的子系统的名称。|  
|**command**|**nvarchar(max)**|要执行的命令**子系统**。|  
|**flag**|**int**|保留。|  
|**additional_parameters**|**ntext**|保留。|  
|**cmdexec_success_code**|**int**|返回的错误级值**CmdExec**子系统步骤，以指明成功。|  
|**on_success_action**|**tinyint**|成功执行了某个步骤时将要执行的操作。|  
|**on_success_step_id**|**int**|成功执行了某个步骤时将要执行的下一个步骤的 ID。|  
|**on_fail_action**|**tinyint**|未成功执行某个步骤时将要执行的操作。|  
|**on_fail_step_id**|**int**|未成功执行某个步骤时将要执行的下一个步骤的 ID。|  
|服务器|**sysname**|保留。|  
|**database_name**|**sysname**|在其中的数据库名称**命令**如果执行**子系统**是 TSQL。|  
|**database_user_name**|**sysname**|执行该步骤时使用的帐户所属的数据库用户的名称。|  
|**retry_attempts**|**int**|步骤失败时的重试次数。|  
|**retry_interval**|**int**|每次重试间的等待时间。|  
|**os_run_priority**|**int**|保留。|  
|**output_file_name**|**nvarchar(200)**|在其中步骤的输出文件的名称保存时**子系统**是 TSQL、 PowerShell 或 **CmdExec * * *。*|  
|**last_run_outcome**|**int**|前一次执行作业步骤的结果。<br /><br /> **0** = 失败<br /><br /> **1** = 成功<br /><br /> **2** = 重试<br /><br /> **3** = 取消<br /><br /> **5** = 未知|  
|**last_run_duration**|**int**|该步骤上次运行时的持续时间 (hhmmss)。|  
|**last_run_retries**|**int**|上一次执行作业步骤时的重试次数。|  
|**last_run_date**|**int**|上次开始执行该步骤的日期 (yyyymmdd)。|  
|**last_run_time**|**int**|上次开始执行该步骤的时间 (hhmmss)。|  
|**proxy_id**|**int**|作业步骤的代理。|  
|**step_uid**|**uniqueidentifier**|作业步骤的标识符。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 代理表&#40;Transact SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
