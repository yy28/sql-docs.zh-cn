---
title: sp_changedynamicsnapshot_job (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedynamicsnapshot_job
- sp_changedynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_changedynamicsnapshot_job
ms.assetid: ea0dacd2-a5fd-42f4-88dd-7d289b0ae017
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ab11ccb8853c00439583162f33e76d0e14622a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62994306"
---
# <a name="spchangedynamicsnapshotjob-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改为带有参数化行筛选器的发布的订阅生成快照的代理作业。 在发布服务器上对发布数据库执行此存储的过程。  
  
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
`[ @publication = ] 'publication'` 是发布的名称。 *发布*是**sysname**，无默认值。  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'` 正在更改的快照作业的名称。 *dynamic_snapshot_jobname*是**sysname**，默认值为 N '%'。 如果*dynamic_snapshot_jobid*指定，则必须使用的默认值为*dynamic_snapshot_jobname*。  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'` 正在更改的快照作业的 ID。 *dynamic_snapshot_jobid*是**uniqueidentifier**，默认值为 NULL。 如果*dynamic_snapshot_jobname*指定，则必须使用的默认值为*dynamic_snapshot_jobid*。  
  
`[ @frequency_type = ] frequency_type` 已安排代理的频率。 *frequency_type*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
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
  
`[ @frequency_interval = ] frequency_interval` 在运行代理的天。 *frequency_interval*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
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
  
`[ @frequency_subday = ] frequency_subday` 是如何通常定义的周期内重新计划。 *frequency_subday*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4**|Minute|  
|**8**|Hour|  
|NULL（默认值）||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 间隔。 *frequency_subday*。 *frequency_subday_interval*是**int**，默认值为 NULL。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 是运行合并代理的日期。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
|NULL（默认值）||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 使用的重复因子*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 NULL。  
  
`[ @active_start_date = ] active_start_date` 是第一个合并代理的日期安排，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 NULL。  
  
`[ @active_end_date = ] active_end_date` 为合并代理停止的日期安排，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 NULL。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 为合并代理时第一天的时间安排，格式为 HHMMSS。 *active_start_time_of_day* 是 **int**，默认值为 NULL。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 为合并代理停止的时间安排，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 NULL。  
  
`[ @job_login = ] 'job_login'` 是[!INCLUDE[msCoName](../../includes/msconame-md.md)]生成使用参数化的行筛选器订阅的快照时快照代理运行的 Windows 帐户。 *job_login*是**nvarchar(257)**，默认值为 NULL。  
  
`[ @job_password = ] 'job_password'` 使用参数化的行筛选器在其下运行快照代理生成订阅的快照时的 Windows 帐户的密码。 *job_password*是**nvarchar(257)**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changedynamicsnapshot_job**用于合并复制的发布使用参数化的行筛选器。  
  
 更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_changedynamicsnapshot_job**。  
  
## <a name="see-also"></a>请参阅  
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
  
