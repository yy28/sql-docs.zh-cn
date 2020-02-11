---
title: sp_changedynamicsnapshot_job （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 4db6a29d92fe093e9704f88fcc528c9fa687ccff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68768950"
---
# <a name="sp_changedynamicsnapshot_job-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  修改为带有参数化行筛选器的发布的订阅生成快照的代理作业。 此存储过程在发布服务器上对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'`发布的名称。 *发布*为**sysname**，无默认值。  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`要更改的快照作业的名称。 *dynamic_snapshot_jobname*的值为**sysname**，默认值为 N '% '。 如果指定*dynamic_snapshot_jobid* ，则必须使用*dynamic_snapshot_jobname*的默认值。  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`要更改的快照作业的 ID。 *dynamic_snapshot_jobid*为**uniqueidentifier**，默认值为 NULL。 如果指定*dynamic_snapshot_jobname*，则必须使用*dynamic_snapshot_jobid*的默认值。  
  
`[ @frequency_type = ] frequency_type`计划代理的频率。 *frequency_type*为**int**，可以是下列值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|一次性|  
|**2**|按需|  
|**4**|每天一次|  
|**8**|每周|  
|**16**|每月|  
|**32**|与“每月”选项相关|  
|**64**|自动启动|  
|**128**|重复执行|  
|NULL（默认值）||  
  
`[ @frequency_interval = ] frequency_interval`代理运行的天数。 *frequency_interval*为**int**，可以是下列值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**3**|星期二|  
|**4**|星期三|  
|**5**|星期四|  
|**6**|星期五|  
|**7**|星期六|  
|**8**|日期|  
|**900**|工作日|  
|**万**|周末|  
|NULL（默认值）||  
  
`[ @frequency_subday = ] frequency_subday`在定义的时间段内重新计划的频率。 *frequency_subday*为**int**，可以是下列值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|秒|  
|**4**|分钟|  
|**8**|Hour|  
|NULL（默认值）||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*的间隔。 *frequency_subday_interval*的值为**int**，默认值为 NULL。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`合并代理运行的日期。 如果*frequency_type*设置为**32** （每月相对），则使用此参数。 *frequency_relative_interval*为**int**，可以是下列值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|第一个|  
|**2**|秒|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|最后一个|  
|NULL（默认值）||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*使用的重复因子。 *frequency_recurrence_factor*的值为**int**，默认值为 NULL。  
  
`[ @active_start_date = ] active_start_date`第一次计划合并代理的日期，格式为 YYYYMMDD。 *active_start_date*的值为**int**，默认值为 NULL。  
  
`[ @active_end_date = ] active_end_date`停止计划合并代理的日期，格式为 YYYYMMDD。 *active_end_date*的值为**int**，默认值为 NULL。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`第一次计划合并代理的时间，格式为 HHMMSS。 *active_start_time_of_day*的值为**int**，默认值为 NULL。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`停止计划合并代理的时间，格式为 HHMMSS。 *active_end_time_of_day*的值为**int**，默认值为 NULL。  
  
`[ @job_login = ] 'job_login'`为使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]参数化行筛选器的订阅生成快照时，运行快照代理所用的 Windows 帐户。 *job_login*为**nvarchar （257）**，默认值为 NULL。  
  
`[ @job_password = ] 'job_password'`使用参数化行筛选器为订阅生成快照时，运行快照代理的 Windows 帐户的密码。 *job_password*为**nvarchar （257）**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changedynamicsnapshot_job**用于具有参数化行筛选器的发布的合并复制。  
  
 更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_changedynamicsnapshot_job**。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
  
