---
title: sp_addmergepushsubscription_agent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
- sp_addmergepushsubscription_agent_TSQL
- sp_addmergepushsubscription_agent
helpviewer_keywords:
- sp_addmergepushsubscription_agent
ms.assetid: 808a1925-be46-4999-8d69-b3a83010ec81
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 60058b5f9779ee9fead3284641cce81ae3702dfb
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032817"
---
# <a name="spaddmergepushsubscriptionagent-transact-sql"></a>sp_addmergepushsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  添加新的代理作业，用于制定合并发布推送订阅的同步计划。 在发布服务器上对发布数据库执行此存储的过程。  
  
> [!IMPORTANT]  
>  使用远程分发服务器配置发布服务器时，为所有参数提供的值（包括 *job_login* 和 *job_password*）都会以纯文本方式发送到该分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addmergepushsubscription_agent [ @publication =] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password = ] 'subscriber_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@publication =** ] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@subscriber =** ] **'***订阅服务器*****  
 订阅服务器的名称。 *订阅服务器上*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_db =** ] **'***subscriber_db*****  
 是订阅数据库的名称。 *subscriber_db*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_security_mode =** ] *subscriber_security_mode*  
 同步时连接到订阅服务器所使用的安全模式。 *subscriber_security_mode*是**int**，默认值为 1。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 如果**1**，指定 Windows 身份验证。  
  
 [  **@subscriber_login =** ] **'***subscriber_login*****  
 同步时连接到订阅服务器所使用的订阅服务器登录。 *subscriber_login*如果，则需要*subscriber_security_mode*设置为**0**。 *subscriber_login*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_password =** ] **'***subscriber_password*****  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的订阅服务器密码。 *subscriber_password*如果，则需要*subscriber_security_mode*设置为**0**。 *subscriber_password*是**sysname**，默认值为 NULL。 如果使用订阅服务器密码，将自动对密码进行加密。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
 [  **@publisher_security_mode =** ] *publisher_security_mode*  
 同步时连接到发布服务器所使用的安全模式。 *publisher_security_mode*是**int**，默认值为 1。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 如果**1**，指定 Windows 身份验证。  
  
 [  **@publisher_login =** ] **'***publisher_login*****  
 同步时连接到发布服务器所使用的登录名。 *publisher_login*是**sysname**，默认值为 NULL。  
  
 [  **@publisher_password =** ] **'***publisher_password*****  
 连接到发布服务器时所使用的密码。 *publisher_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
 [  **@job_login =** ] **'***job_login*****  
 用于运行代理的 Windows 帐户的登录名。 *job_login*是**nvarchar(257)**，默认值为 NULL。 此 Windows 帐户始终用于到分发服务器的代理连接，以及在使用 Windows 集成身份验证时用于到订阅服务器和发布服务器的连接。  
  
 [  **@job_password =** ] **'***job_password*****  
 用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，无默认值。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
 [ **@job_name =** ] **'***job_name***'**  
 现有代理作业的名称。 *job_name*是**sysname**，默认值为 NULL。 仅当使用现有作业而不是（默认的）新创建的作业同步订阅时，才指定此参数。 如果你不属于**sysadmin**固定服务器角色，则必须指定*job_login*并*job_password*时指定*job_name*.  
  
 [  **@frequency_type =** ] *frequency_type*  
 安排合并代理的频率。 *frequency_type*是**int**，可以是下列值之一。  
  
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
  
> [!NOTE]  
>  指定的值**64**使合并代理在连续模式下运行。 这相当于设置 **-连续**代理参数。 有关详细信息，请参阅 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 在运行合并代理的天。 *frequency_interval*是**int**，可以是下列值之一。  
  
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
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 合并代理的日期。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
|NULL（默认值）||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 使用的重复因子*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 NULL。  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 在指定期内重新安排计划的频率。 *frequency_subday*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4**|Minute|  
|**8**|Hour|  
|NULL（默认值）||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 间隔。 *frequency_subday*。 *frequency_subday_interval*是**int**，默认值为 NULL。  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 第一次安排合并代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为 NULL。  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 停止安排合并代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 NULL。  
  
 [ **@active_start_date =** ] *active_start_date*  
 第一次安排合并代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 NULL。  
  
 [ **@active_end_date =** ] *active_end_date*  
 停止安排合并代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 NULL。  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr*****  
 指定是否可以通过 Windows 同步管理器同步订阅。 *enabled_for_syncmgr*是**nvarchar(5)**，默认值为 FALSE。 如果**false**，该订阅未注册使用同步管理器。 如果 **，则返回 true**，订阅已注册使用同步管理器，可以同步而无需启动[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_addmergepushsubscription_agent**用于合并复制，并使用类似于的功能[sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepushsubscript_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addmergepushsubscription_agent**。  
  
## <a name="see-also"></a>请参阅  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
