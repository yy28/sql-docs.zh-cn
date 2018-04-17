---
title: sp_addpublication_snapshot (Transact SQL) |Microsoft 文档
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
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a04d94d0a650eb0349e599814fc2f1f614d4732
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spaddpublicationsnapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为指定的发布创建快照代理。 在发布服务器的发布数据库上执行此存储的过程。  
  
> [!IMPORTANT]  
>  使用远程分发服务器配置发布服务器时，为所有参数提供的值（包括 *job_login* 和 *job_password*）都会以纯文本方式发送到该分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
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
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@frequency_type=**] *frequency_type*  
 执行快照代理的频率。 *frequency_type*是**int**，和可以是以下值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|一次。|  
|**4** （默认值）|每天。|  
|**8**|每周。|  
|**16**|每月。|  
|**32**|每月，相对于频率间隔。|  
|**64**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理启动时。|  
|**128**|计算机空闲时运行|  
  
 [  **@frequency_interval=**] *frequency_interval*  
 是要应用于通过设置的频率的值*frequency_type*。 *frequency_interval*是**int**，和可以是以下值之一。  
  
|frequency_type 的值|对 frequency_interval 的影响|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval*未使用。|  
|**4** （默认值）|每个*frequency_interval*天，默认值为每日。|  
|**8**|*frequency_interval*是一个或多个以下 (结合[ &#124; (按位 OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)逻辑运算符):<br /><br /> **1** = 星期日&#124;<br /><br /> **2** = 星期一&#124;<br /><br /> **4** = 星期二&#124;<br /><br /> **8** = 星期三&#124;<br /><br /> **16** = 星期四&#124;<br /><br /> **32** = 星期五&#124;<br /><br /> **64** = 星期六|  
|**16**|上*frequency_interval*天的月份。|  
|**32**|*frequency_interval*是以下之一：<br /><br /> **1** = 星期日&#124;<br /><br /> **2** = 星期一&#124;<br /><br /> **3** = 星期二&#124;<br /><br /> **4** = 星期三&#124;<br /><br /> **5** = 星期四&#124;<br /><br /> **6** = 星期五&#124;<br /><br /> **7** = 星期六&#124;<br /><br /> **8** = 某一天&#124;<br /><br /> **9** = 工作日&#124;<br /><br /> **10** = 休息日|  
|**64**|*frequency_interval*未使用。|  
|**128**|*frequency_interval*未使用。|  
  
 [  **@frequency_subday=**] *frequency_subday*  
 是的单位*freq_subday_interval*。 *frequency_subday*是**int**，并且可以为这些值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4** （默认值）|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 是的间隔*frequency_subday*。 *frequency_subday_interval*是**int**，默认值为 5，这意味着每 5 分钟。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 快照代理运行的日期。 *frequency_relative_interval*是**int**，默认值为 1。  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 是由重复因素*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 0。  
  
 [  **@active_start_date=**] *active_start_date*  
 第一次安排快照代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 0。  
  
 [  **@active_end_date=**] *active_end_date*  
 停止安排快照代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 99991231，这意味着年 12 月 31 日到 9999。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 第一次安排快照代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为 0。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 停止安排快照代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 235959，这意味着 11:59:59 PM 根据在 24 小时制测量值。  
  
 [  **@snapshot_job_name =** ] *****snapshot_agent_name*****  
 使用现有作业时现有快照代理作业的名称。 *snapshot_agent_name*是**nvarchar(100)**默认值为 NULL。 此参数只限内部使用，创建新发布时不应指定它。 如果*snapshot_agent_name*未指定，则*job_login*和*job_password*必须为 NULL。  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 连接到发布服务器时代理所使用的安全模式。 *publisher_security_mode*是**smallint**，默认值为 1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，和**1**指定 Windows 身份验证。 值为**0**必须为指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [ **@publisher_login**=] *****publisher_login*****  
 连接到发布服务器时所使用的登录名。 *publisher_login*是**sysname**，默认值为 NULL。 *publisher_login*时，必须指定*publisher_security_mode*是**0**。 如果*publisher_login*为 NULL 和*publisher_security_mode*是**1**，然后中指定的 Windows 帐户*job_login*将使用当连接到发布服务器。  
  
 [ **@publisher_password**=] *****publisher_password*****  
 连接到发布服务器时所使用的密码。 *publisher_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为了提高安全性，建议您在运行时提供登录名和密码。  
  
 [ **@job_login**=] *****job_login*****  
 用于运行代理的 Windows 帐户的登录名。 *job_login*是**nvarchar(257)**，默认值为 NULL。 此 Windows 帐户总是用于与分发服务器建立代理连接。 创建新的快照代理作业时，必须提供此参数。  
  
> [!NOTE]  
>  有关非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器，这必须是相同的登录名中指定[sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)。  
  
 [ **@job_password**=] *****job_password*****  
 用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，无默认值。 创建新的快照代理作业时，必须提供此参数。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为了提高安全性，建议您在运行时提供登录名和密码。  
  
 [ **@publisher**=] *****发布服务器*****  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*创建在快照代理时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_addpublication_snapshot**快照复制、 事务复制和合并复制中使用。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addpublication_snapshot**。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [创建并应用快照](../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [sp_addpublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_startpublication_snapshot &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
