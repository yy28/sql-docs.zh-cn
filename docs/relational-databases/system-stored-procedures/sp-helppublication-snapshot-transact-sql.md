---
title: sp_helppublication_snapshot (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helppublication_snapshot
- sp_helppublication_snapshot_TSQL
helpviewer_keywords:
- sp_helppublication_snapshot
ms.assetid: 97b4a7ae-40a5-4328-88f1-ff5d105bbb34
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1598b35bf6fc7148c288d61fba959ac6360903d3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sphelppublicationsnapshot-transact-sql"></a>sp_helppublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回给定发布的快照代理的相关信息。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helppublication_snapshot [ @publication = ] 'publication'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication =** ] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@publisher =** ] *****发布服务器*****  
 指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*添加到项目时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|快照代理程序的 ID。|  
|**名称**|**nvarchar(100)**|快照代理的名称。|  
|**publisher_security_mode**|**int**|代理在连接发布服务器时所使用的安全模式，可以是下列模式之一：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证<br /><br /> **1** = Windows 身份验证。|  
|**publisher_login**|**sysname**|连接到发布服务器时使用的登录名。|  
|**publisher_password**|**nvarchar(524)**|出于安全原因，值为**\* \* \* \* \* \* \* \* \* \***始终返回。|  
|**job_id**|**uniqueidentifier**|代理作业的唯一 ID。|  
|**job_login**|**nvarchar(512)**|是以格式返回的 Windows 帐户运行快照代理*域*\\*用户名*。|  
|**job_password**|**sysname**|出于安全原因，值为**\* \* \* \* \* \* \* \* \* \***始终返回。|  
|**schedule_name**|**sysname**|用于该代理作业的计划的名称。|  
|**frequency_type**|**int**|代理计划运行的频率，可以为下列值之一：<br /><br /> **1** = 一次<br /><br /> **2** = 按需<br /><br /> **4** = 每日<br /><br /> **8** = 每周<br /><br /> **16** = 每月<br /><br /> **32** = 每月相对<br /><br /> **64** = 自动启动<br /><br /> **128** = 重复执行|  
|**frequency_interval**|**int**|代理运行的日期，可以为下列值之一：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **3** = 星期二<br /><br /> **4** = 星期三<br /><br /> **5** = 星期四<br /><br /> **6** = 星期五<br /><br /> **7** = 星期六<br /><br /> **8** = 某一天<br /><br /> **9** = 工作日<br /><br /> **10** = 周末|  
|**frequency_subday_type**|**int**|是定义代理运行时的频率的类型*frequency_type*是**4** （每日），并且可以为这些值之一。<br /><br /> **1** = 在指定的时间<br /><br /> **2** = 秒<br /><br /> **4** = 分钟<br /><br /> **8** = 小时数|  
|**frequency_subday_interval**|**int**|间隔数*frequency_subday_type*发生之间的代理的计划执行。|  
|**frequency_relative_interval**|**int**|是在给定月份中运行代理的周时*frequency_type*是**32** （每月相对），并且可以为这些值之一。<br /><br /> **1** = 第一次<br /><br /> **2** = 秒<br /><br /> **4** = 第三<br /><br /> **8** = 第四个<br /><br /> **16** = 最后一次|  
|**frequency_recurrence_factor**|**int**|在计划的代理执行之间间隔的周数或月数。|  
|**active_start_date**|**int**|计划第一次运行代理的日期，格式为 YYYYMMDD。|  
|**active_end_date**|**int**|计划最后一次运行代理的日期，格式为 YYYYMMDD。|  
|**active_start_time**|**int**|计划第一次运行代理的时间，格式为 HHMMSS。|  
|**active_end_time**|**int**|计划最后一次运行代理的时间，格式为 HHMMSS。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_help_publication_snapshot**在所有类型的复制中使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色在发布服务器或成员的**db_owner**发布数据库上的固定的数据库角色可以执行**sp_help_publication_snapshot**.  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication_snapshot &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)  
  
  
