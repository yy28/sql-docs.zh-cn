---
title: sp_help_jobactivity (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_jobactivity_TSQL
- sp_help_jobactivity
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobactivity
ms.assetid: d344864f-b4d3-46b1-8933-b81dec71f511
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 648fb94f5a14365356a293f6fb0652336ca0625b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpjobactivity-transact-sql"></a>sp_help_jobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的运行时状态的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_jobactivity { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @session_id = ] session_id ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@job_id =**] *job_id*  
 作业标识号。 *job_id*是**uniqueidentifier**，默认值为 NULL。  
  
 [ **@job_name =**] **'***job_name***'**  
 作业的名称。 *job_name*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必须指定，但不能同时指定。  
  
 [ **@session_id** = ] *session_id*  
 报告其信息的会话的 ID。 *session_id*是**int**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 返回以下结果集：  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|代理会话标识号。|  
|**job_id**|**uniqueidentifier**|作业标识符。|  
|**job_name**|**sysname**|作业的名称。|  
|**run_requested_date**|**datetime**|请求运行作业的时间。|  
|**run_requested_source**|**sysname**|请求运行作业的请求源。 可为下列值之一：<br /><br /> **1** = 按计划运行<br /><br /> **2** = 运行以响应警报<br /><br /> **3** = 在启动时运行<br /><br /> **4** = 由用户运行<br /><br /> **6** = CPU 空闲计划上的运行|  
|**queued_date**|**datetime**|将请求加入队列的时间。 如果直接运行作业，则该值为 NULL。|  
|**start_execution_date**|**datetime**|将作业分配给可运行线程的时间。|  
|**last_executed_step_id**|**int**|最近运行的作业步骤的 ID。|  
|**last_exectued_step_date**|**datetime**|最近运行的作业步骤开始运行的时间。|  
|**stop_execution_date**|**datetime**|作业停止运行的时间。|  
|**next_scheduled_run_date**|**datetime**|计划下一次作业运行的时间。|  
|**job_history_id**|**int**|作业历史记录表中作业历史记录的标识符。|  
|message|**nvarchar(1024)**|上次运行作业期间产生的消息。|  
|**run_status**|**int**|作业上次运行时返回的状态：<br /><br /> **0** = 失败错误<br /><br /> **1** = 成功<br /><br /> **3** = 取消<br /><br /> **5** = 状态未知|  
|**operator_id_emailed**|**int**|作业完成时通过电子邮件通知的操作员的 ID 号。|  
|**operator_id_netsent**|**int**|通过通知的操作员的 ID 号**网络发送**在作业完成。|  
|**operator_id_paged**|**int**|作业完成时通过寻呼通知的操作员的 ID 号。|  
  
## <a name="remarks"></a>注释  
 此过程可提供作业的当前状态快照。 返回的结果表示处理请求时的有关信息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在每次启动代理服务时都会创建一个会话 ID。 表中存储的会话 id **msdb.dbo.syssessions**。  
  
 如果没有*session_id*提供，将列出有关最新的会话的信息。  
  
 如果没有*job_name*或*job_id*提供，将列出所有作业的信息。  
  
## <a name="permissions"></a>权限  
 默认情况下，成员的**sysadmin**固定的服务器角色可以运行此存储的过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 只有的成员**sysadmin**可以查看其他用户拥有的作业的活动。  
  
## <a name="examples"></a>示例  
 以下示例列出了当前用户有权查看的全部作业的活动。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobactivity ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 代理存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
