---
title: sp_adddynamicsnapshot_job (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_adddynamicsnapshot_job
- sp_adddynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_adddynamicsnapshot_job
ms.assetid: ef50ccf6-e360-4e4b-91b9-6706b8fabefa
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5592667914cc3109058b81366288dba3d27234da
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032208"
---
# <a name="spadddynamicsnapshotjob-transact-sql"></a>sp_adddynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建一个代理作业，该代理作业可为具有参数化行筛选器的发布生成筛选数据快照。 在发布服务器上对发布数据库执行此存储的过程。 管理员使用此存储过程可手动为订阅服务器创建筛选数据快照作业。  
  
> [!NOTE]  
>  为了创建筛选数据快照作业，必须存在该发布的标准快照作业。  
  
 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_adddynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]   
    [ , [ @host_name = ] 'host_name' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' OUTPUT ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' OUTPUT ]   
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 为其添加筛选数据快照作业的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@suser_sname**=] **'***suser_sname*****  
 使用创建订阅筛选的数据快照的值进行筛选时的值[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)订阅服务器上的函数。 *suser_sname*是**sysname**，无默认值。 *suser_sname*应为 NULL，如果不使用此函数的发布进行动态筛选。  
  
 [ **@host_name**=] **'***host_name*****  
 使用创建订阅筛选的数据快照的值进行筛选时的值[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)订阅服务器上的函数。 *host_name*是**sysname**，无默认值。 *host_name*应为 NULL，如果不使用此函数的发布进行动态筛选。  
  
 [ **@dynamic_snapshot_jobname**=] **'***dynamic_snapshot_jobname*****  
 创建的筛选数据快照作业的名称。 *dynamic_snapshot_jobname*是**sysname**，默认值为 NULL，并且是可选的 OUTPUT 参数。 如果指定， *dynamic_snapshot_jobname*必须解析为分发服务器上唯一作业。 如果不指定，则将自动生成并在结果集中返回一个作业名，该名称的创建方式如下：  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  生成动态快照作业的名称时，您可以截断标准快照作业的名称。  
  
 [ **@dynamic_snapshot_jobid**=] **'***dynamic_snapshot_jobid*****  
 创建的筛选数据快照作业的标识符。 *dynamic_snapshot_jobid*是**uniqueidentifier**，默认值为 NULL，并且是可选的 OUTPUT 参数。  
  
 [  **@frequency_type=**] *frequency_type*  
 安排筛选数据快照作业所用的频率。 *frequency_type*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|按需|  
|**4** （默认值）|每天|  
|**8**|每周|  
|**16**|每月|  
|**32**|与“每月”选项相关|  
|**64**|自动启动|  
|**128**|重复执行|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 执行筛选数据快照作业的时间段（以天计）。 *frequency_interval*是**int**，默认值为 1，并取决于值*frequency_type*。  
  
|值*frequency_type*|在影响*frequency_interval*|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval*是未使用。|  
|**4** （默认值）|每个*frequency_interval*天，默认值为每日。|  
|**8**|*frequency_interval*是一个或多个以下 (结合[ &#124; &#40;位或&#41; &#40;-&#41; ](../../t-sql/language-elements/bitwise-or-transact-sql.md)逻辑运算符):<br /><br /> **1** = 星期日&#124; **2** = 星期一&#124; **4** = 星期二&#124; **8** = 星期三&#124; **16** =星期四&#124; **32** = 星期五&#124; **64** = 星期六|  
|**16**|上*frequency_interval*天的月份。|  
|**32**|*frequency_interval*是以下之一：<br /><br /> **1** = 星期日&#124; **2** = 星期一&#124; **3** = 星期二&#124; **4** = 星期三&#124; **5** =星期四&#124; **6** = 星期五&#124; **7** = 星期六&#124; **8** = 天&#124; **9** = 工作日&#124; **10** = 休息日|  
|**64**|*frequency_interval*是未使用。|  
|**128**|*frequency_interval*是未使用。|  
  
 [  **@frequency_subday=**] *frequency_subday*  
 指定的单位*frequency_subday_interval*。 *frequency_subday*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4** （默认值）|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 是的数字*frequency_subday*作业每次执行之间的段。 *frequency_subday_interval*是**int**，默认值为 5。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 每月中筛选数据快照作业的发生情况。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1** （默认值）|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 使用的重复因子*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 0。  
  
 [  **@active_start_date=**] *active_start_date*  
 第一次安排筛选数据快照作业的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 NULL。  
  
 [  **@active_end_date=**] *active_end_date*  
 停止安排筛选数据快照作业的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 NULL。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 第一次安排筛选数据快照作业的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为 NULL。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 停止安排筛选数据快照作业的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 NULL。  
  
## <a name="result-set"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|标识中的已筛选的数据快照作业[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)系统表。|  
|**dynamic_snapshot_jobname**|**sysname**|已筛选数据快照作业的名称。|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|唯一标识[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]分发服务器上的代理作业。|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_adddynamicsnapshot_job**用于使用参数化筛选器的发布用于合并复制。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_adddynamicsnapshot_job**。  
  
## <a name="see-also"></a>请参阅  
 [为带有参数化筛选器的合并发布创建快照](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [sp_dropdynamicsnapshot_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [sp_helpdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
