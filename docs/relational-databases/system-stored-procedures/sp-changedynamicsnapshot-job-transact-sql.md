---
title: sp_changedynamicsnapshot_job (Transact SQL) |Microsoft 文档
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
- sp_changedynamicsnapshot_job
- sp_changedynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_changedynamicsnapshot_job
ms.assetid: ea0dacd2-a5fd-42f4-88dd-7d289b0ae017
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 160831b54f96bb06652287934da87142c855a348
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spchangedynamicsnapshotjob-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改为带有参数化行筛选器的发布的订阅生成快照的代理作业。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changedynamicsnapshot_job [ @publication = ] 'publication'  
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@publication =** ] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 要更改的快照作业的名称。 *dynamic_snapshot_jobname*是**sysname**，默认值为 N %。 如果*dynamic_snapshot_jobid*指定，则必须使用的默认值为*dynamic_snapshot_jobname*。  
  
 [ **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 要更改的快照作业的 ID。 *dynamic_snapshot_jobid*是**uniqueidentifier**，默认值为 NULL。 如果*dynamic_snapshot_jobname*指定，则必须使用的默认值为*dynamic_snapshot_jobid*。  
  
 [  **@frequency_type =** ] *frequency_type*  
 安排代理的频率。 *frequency_type*是**int**，和可以是以下值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|按需|  
|**4**|每天|  
|**8**|每周|  
|**16**|每月|  
|**32**|与“每月”选项相关|  
|**64**|自动启动|  
|**128**|重复执行|  
|NULL（默认值）||  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 代理运行的天数。 *frequency_interval*是**int**，和可以是以下值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**3**|星期二|  
|**4**|星期三|  
|**5**|星期四|  
|**6**|星期五|  
|**7**|星期六|  
|**8**|Day|  
|**9**|工作日|  
|**10**|周末|  
|NULL（默认值）||  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 在指定期内重新安排计划的频率。 *frequency_subday*是**int**，和可以是以下值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4**|Minute|  
|**8**|Hour|  
|NULL（默认值）||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 是的间隔*frequency_subday*。 *frequency_subday_interval*是**int**，默认值为 NULL。  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 合并代理运行的日期。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，和可以是以下值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
|NULL（默认值）||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 是由重复因素*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 NULL。  
  
 [ **@active_start_date =** ] *active_start_date*  
 第一次安排合并代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 NULL。  
  
 [ **@active_end_date =** ] *active_end_date*  
 停止安排合并代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 NULL。  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 第一次安排合并代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为 NULL。  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 停止安排合并代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 NULL。  
  
 [  **@job_login=** ] *****job_login*****  
 为使用参数化行筛选器的订阅生成快照时，运行快照代理所用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户。 *job_login*是**nvarchar(257)**，默认值为 NULL。  
  
 [  **@job_password=** ] *****job_password*****  
 为使用参数化行筛选器的订阅生成快照时，运行快照代理所用的 Windows 帐户的密码。 *job_password*是**nvarchar(257)**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_changedynamicsnapshot_job**用于合并复制中发布带有参数化的行筛选器。  
  
 更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_changedynamicsnapshot_job**。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
