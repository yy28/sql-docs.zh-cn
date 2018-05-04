---
title: sp_addmergesubscription (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
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
- sp_addmergesubscription_TSQL
- sp_addmergesubscription
helpviewer_keywords:
- sp_addmergesubscription
ms.assetid: a191d817-0132-49ff-93ca-76f13e609b38
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 56355da01ed689279680d595b6b0733b2fc26413
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spaddmergesubscription-transact-sql"></a>sp_addmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建推送合并订阅或请求合并订阅。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addmergesubscription [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @subscriber_type= ] 'subscriber_type' ]  
    [ , [ @subscription_priority= ] subscription_priority ]  
    [ , [ @sync_type= ] 'sync_type' ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @optional_command_line= ] 'optional_command_line' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @use_interactive_resolver= ] 'use_interactive_resolver' ]  
    [ , [ @merge_job_name= ] 'merge_job_name' ]  
    [ , [ @hostname = ] 'hostname'  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。 该发布必须已存在。  
  
 [  **@subscriber =**] *****订阅服务器*****  
 订阅服务器的名称。 *订阅服务器*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_db=**] *****subscriber_db*****  
 是订阅数据库的名称。 *subscriber_db*是**sysname**，默认值为 NULL。  
  
 [  **@subscription_type=**] *****subscription_type*****  
 是一种订阅。 *subscription_type*是**nvarchar(15)**，默认值为推送。 如果**推送**，推送订阅已添加并合并代理在分发服务器时添加。 如果**请求**，而无需添加合并代理在分发服务器上添加请求订阅。  
  
> [!NOTE]  
>  匿名订阅无需使用此存储过程。  
  
 [  **@subscriber_type=**] *****subscriber_type*****  
 订阅服务器的类型。 *subscriber_type*是**nvarchar(15)**，和可以是以下值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**本地**（默认值）|订阅服务器仅对发布服务器是已知的。|  
|**全局**|订阅服务器对所有服务器都是已知的。|  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本中，本地订阅称为客户端订阅，全局订阅称为服务器订阅  
  
 [  **@subscription_priority=**] *subscription_priority*  
 指示订阅的优先级的数字。 *subscription_priority*是**实际**，默认值为 NULL。 对于本地订阅和匿名订阅，优先级为 0.0。 对于全局订阅，优先级必须小于 100.0。  
  
 [  **@sync_type=**] *****sync_type*****  
 订阅同步类型。 *sync_type*是**nvarchar(15)**，默认值为**自动**。 可以是**自动**或**无**。 如果**自动**，架构和已发布表的初始数据传输到订阅服务器第一次。 如果**无**，假定您在订阅服务器已拥有的架构和初始数据已发布表。 始终会传输系统表和数据。  
  
> [!NOTE]  
>  我们建议对不指定值**无**。  
  
 [  **@frequency_type=**] *frequency_type*  
 指示合并代理将在何时运行的值。 *frequency_type*是**int**，和可以是以下值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**4**|每天|  
|**8**|每周|  
|**10**|每月|  
|**20**|每月，相对于频率间隔|  
|**40**|当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理启动时|  
|NULL（默认值）||  
  
 [  **@frequency_interval=**] *frequency_interval*  
 合并代理在星期几运行。 *frequency_interval*是**int**，和可以是以下值之一。  
  
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
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 每月计划的合并频率间隔。 *frequency_relative_interval*是**int**，并且可以为这些值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
|NULL（默认值）||  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 是由重复因素*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 NULL。  
  
 [  **@frequency_subday=**] *frequency_subday*  
 是的单位*frequency_subday_interval*。 *frequency_subday*是**int**，和可以是以下值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4**|Minute|  
|**8**|Hour|  
|NULL（默认值）||  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 是的频率*frequency_subday*每次合并之间发生。 *frequency_subday_interval*是**int**，默认值为 NULL。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 第一次安排合并代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为 NULL。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 停止安排合并代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 NULL。  
  
 [  **@active_start_date=**] *active_start_date*  
 第一次安排合并代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 NULL。  
  
 [  **@active_end_date=**] *active_end_date*  
 停止安排合并代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 NULL。  
  
 [  **@optional_command_line=**] *****optional_command_line*****  
 要执行的可选命令提示符。 *optional_command_line*是**nvarchar （4000)**，默认值为 NULL。 此参数用于添加捕获输出并将输出保存到文件的命令，或者用于指定配置文件或属性。  
  
 [  **@description=**] *****说明*****  
 是此合并订阅的简要说明。 *说明*是**nvarchar （255)**，默认值为 NULL。 此值显示在复制监视器**友好名称**列，可用于对监视发布的订阅进行排序。  
  
 [  **@enabled_for_syncmgr=**] *****enabled_for_syncmgr*****  
 指定是否可以通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 同步管理器同步订阅。 *enabled_for_syncmgr*是**nvarchar(5)**，默认值为 FALSE。 如果**false**，订阅未注册使用同步管理器。 如果**true**，该订阅已注册使用同步管理器，可以同步而无需启动[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 [  **@offloadagent=** ] *remote_agent_activation*  
 指定可远程激活代理。 *remote_agent_activation*是**位**默认值为**0**。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它只是为了让脚本能够向后兼容。  
  
 [  **@offloadserver=** ] *****remote_agent_server_name*****  
 指定用于远程代理激活的服务器网络名称。 *remote_agent_server_name*是**sysname**，默认值为 NULL。  
  
 [  **@use_interactive_resolver=** ] *****use_interactive_resolver*****  
 允许交互式地解决所有允许交互式解决的项目的冲突。 *use_interactive_resolver*是**nvarchar(5)**，默认值为 FALSE。  
  
 [  **@merge_job_name=** ] *****merge_job_name*****  
 *@merge_job_name*参数已弃用，并且不能设置。 *merge_job_name*是**sysname**，默认值为 NULL。  
  
 [ **@hostname**=] *****主机名*****  
 重写返回的值[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)当在参数化筛选器的 WHERE 子句中使用此函数。 *主机名*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  出于性能方面的考虑，我们建议您不要将这些函数应用于参数化行筛选器子句（如 `LEFT([MyColumn]) = SUSER_SNAME()`）中的列名。 如果你使用[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)在筛选器子句和替代 HOST_NAME 值中，可能有必要将使用的数据类型转换[转换](../../t-sql/functions/cast-and-convert-transact-sql.md)。 有关此情况的最佳实践的详细信息，请参阅主题 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)中的“覆盖 HOST_NAME() 值”一节。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_addmergesubscription**合并复制中使用。  
  
 当**sp_addmergesubscription**的成员执行**sysadmin**固定服务器角色，以创建推送订阅，合并代理作业隐式创建和运行下[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务帐户。 我们建议你执行[sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)并指定不同的、 特定代理的 Windows 帐户的凭据**@job_login**和 **@job_password**. 有关详细信息，请参阅 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergesubscription-_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addmergesubscription**。  
  
## <a name="see-also"></a>另请参阅  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [交互式冲突解决方法](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_changemergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
