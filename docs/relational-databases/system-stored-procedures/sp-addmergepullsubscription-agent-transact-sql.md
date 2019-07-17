---
title: sp_addmergepullsubscription_agent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_agent
- sp_addmergepullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addmergepullsubscription_agent
ms.assetid: a2f4b086-078d-49b5-8971-8a1e3f6a6feb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8bfa9ff0683f67a1d38aeb17bccd0cfc1443d6d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117956"
---
# <a name="spaddmergepullsubscriptionagent-transact-sql"></a>sp_addmergepullsubscription_agent (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  向合并发布添加一个用于计划请求订阅同步的新代理作业。 此存储过程在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addmergepullsubscription_agent [ [ @name = ] 'name' ]   
        , [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication =] 'publication'   
    [ , [ @publisher_security_mod e= ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher_encrypted_password = ] publisher_encrypted_password ]   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password= ] 'subscriber_password' ]   
    [ , [ @distributor = ] 'distributor' ]   
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @encrypted_password = ] encrypted_password ]   
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
    [ , [ @optional_command_line = ] 'optional_command_line' ]   
    [ , [ @merge_jobid = ] merge_jobid ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]    
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @working_directory = ] 'working_directory' ]   
    [ , [ @use_ftp = ] 'use_ftp' ]   
    [ , [ @reserved = ] 'reserved' ]   
    [ , [ @use_interactive_resolver = ] 'use_interactive_resolver' ]   
    [ , [ @offloadagent = ] 'remote_agent_activation' ]   
    [ , [ @offloadserver = ] 'remote_agent_server_name']   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]  
    [ , [ @use_web_sync = ] use_web_sync ]  
        [ , [ @internet_url = ] 'internet_url' ]  
    [ , [ @internet_login = ] 'internet_login' ]  
        [ , [ @internet_password = ] 'internet_password' ]  
    [ , [ @internet_security_mode = ] internet_security_mode ]  
        [ , [ @internet_timeout = ] internet_timeout ]  
    [ , [ @hostname = ] 'hostname' ]  
        [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>参数  
`[ @name = ] 'name'` 为代理的名称。 *名称*是**sysname**，默认值为 NULL。  
  
`[ @publisher = ] 'publisher'` 是发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
`[ @publisher_db = ] 'publisher_db'` 是发布服务器数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
`[ @publication = ] 'publication'` 是发布的名称。 *发布*是**sysname**，无默认值。  
  
`[ @publisher_security_mode = ] publisher_security_mode` 是同步时连接到发布服务器时要使用的安全模式。 *publisher_security_mode*是**int**，默认值为 1。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 如果**1**，指定 Windows 身份验证。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` 是要进行同步时连接到发布服务器时使用的登录名。 *publisher_login*是**sysname**，默认值为 NULL。  
  
`[ @publisher_password = ] 'publisher_password'` 连接到发布服务器时使用的密码。 *publisher_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
`[ @publisher_encrypted_password = ]publisher_encrypted_password` 设置*publisher_encrypted_password*不再受支持。 尝试将此项设置**位**参数**1**将导致错误。  
  
`[ @subscriber = ] 'subscriber'` 是订阅服务器的名称。 *订阅服务器上*是**sysname**，默认值为 NULL。  
  
`[ @subscriber_db = ] 'subscriber_db'` 是订阅数据库的名称。 *subscriber_db*是**sysname**，默认值为 NULL。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode` 是同步时连接到订阅服务器时要使用的安全模式。 *subscriber_security_mode*是**int**，默认值为 1。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 如果**1**，指定 Windows 身份验证。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 合并代理始终使用 Windows 身份验证连接到本地订阅服务器。 如果为此参数指定了值，将返回警告消息，但将忽略该值。  
  
`[ @subscriber_login = ] 'subscriber_login'` 是使用同步时连接到订阅服务器的订阅服务器登录名。 *subscriber_login*如果，则需要*subscriber_security_mode*设置为**0**。 *subscriber_login*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 如果为此参数指定了值，将返回警告消息，但将忽略该值。  
  
`[ @subscriber_password = ] 'subscriber_password'` 为订阅服务器密码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 *subscriber_password*如果，则需要*subscriber_security_mode*设置为**0**。 *subscriber_password*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 如果为此参数指定了值，将返回警告消息，但将忽略该值。  
  
`[ @distributor = ] 'distributor'` 是分发服务器的名称。 *分发服务器*是**sysname**，默认值为*发布服务器*; 即，发布服务器也是分发服务器。  
  
`[ @distributor_security_mode = ] distributor_security_mode` 是同步时连接到分发服务器时要使用的安全模式。 *distributor_security_mode*是**int**，默认值为 0。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 **1**指定 Windows 身份验证。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'` 是使用同步时连接到分发服务器的分发服务器登录名。 *distributor_login*如果，则需要*distributor_security_mode*设置为**0**。 *distributor_login*是**sysname**，默认值为 NULL。  
  
`[ @distributor_password = ] 'distributor_password'` 是分发服务器密码。 *distributor_password*如果，则需要*distributor_security_mode*设置为**0**。 *distributor_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
`[ @encrypted_password = ] encrypted_password` 设置*encrypted_password*不再受支持。 尝试将此项设置**位**参数**1**将导致错误。  
  
`[ @frequency_type = ] frequency_type` 是用来安排合并代理的频率。 *frequency_type*是**int**，可以是下列值之一。  
  
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
  
`[ @frequency_interval = ] frequency_interval` 一天中的合并代理运行。 *frequency_interval*是**int**，可以是下列值之一。  
  
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
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 是合并代理的日期。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
|NULL（默认值）||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 使用的重复因子*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 NULL。  
  
`[ @frequency_subday = ] frequency_subday` 是如何通常定义的周期内重新计划。 *frequency_subday*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4**|Minute|  
|**8**|Hour|  
|NULL（默认值）||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 间隔。 *frequency_subday*。 *frequency_subday_interval*是**int**，默认值为 NULL。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 为合并代理时第一天的时间安排，格式为 HHMMSS。 *active_start_time_of_day* 是 **int**，默认值为 NULL。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 为合并代理停止的时间安排，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 NULL。  
  
`[ @active_start_date = ] active_start_date` 是第一个合并代理的日期安排，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 NULL。  
  
`[ @active_end_date = ] active_end_date` 为合并代理停止的日期安排，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 NULL。  
  
`[ @optional_command_line = ] 'optional_command_line'` 是提供给合并代理的可选命令提示符。 *optional_command_line*是**nvarchar(255)** ，默认值为。 可用于向合并代理提供其他参数，例如在以下示例中，将默认的查询超时值增加到 `600` 秒：  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
`[ @merge_jobid = ] merge_jobid` 输出参数为作业 id。 *merge_jobid*是**binary(16)** ，默认值为 NULL。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` 指定是否可以同步订阅通过 Windows 同步管理器。 *enabled_for_syncmgr* 是 **nvarchar(5)** ，默认值为 FALSE。 如果**false**，该订阅未注册使用同步管理器。 如果 **，则返回 true**，订阅已注册使用同步管理器，可以同步而无需启动[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
`[ @ftp_address = ] 'ftp_address'` 为了向后兼容。  
  
`[ @ftp_port = ] ftp_port` 为了向后兼容。  
  
`[ @ftp_login = ] 'ftp_login'` 为了向后兼容。  
  
`[ @ftp_password = ] 'ftp_password'` 为了向后兼容。  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'` 指定从中提取快照文件的位置。 *alternate_snapshot_folder*是**nvarchar(255)** ，默认值为 NULL。 如果为 NULL，则从发布服务器指定的默认位置拾取快照文件。  
  
`[ @working_directory = ] 'working_directory'` 是用于临时存储发布的数据和架构文件，使用 FTP 传输快照文件时的工作目录的名称。 *working_directory*是**nvarchar(255)** ，默认值为 NULL。  
  
`[ @use_ftp = ] 'use_ftp'` 指定使用 FTP 而不是典型的协议来检索快照。 *use_ftp*是**nvarchar(5)** ，默认值为 FALSE。  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver' ]` 使用交互式冲突解决程序解决所有允许交互式解决方法的项目的冲突。 *use_interactive_resolver* 是 **nvarchar(5)** ，默认值为 FALSE。  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  已不推荐使用远程代理激活，也不再支持该功能。 支持此参数只是为了让脚本能够向后兼容。 设置*remote_agent_activation*以外的值为**false**将生成错误。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  已不推荐使用远程代理激活，也不再支持该功能。 支持此参数只是为了让脚本能够向后兼容。 设置*remote_agent_server_name*为任何非 NULL 值将生成错误。  
  
`[ @job_name = ] 'job_name' ]` 是现有的代理作业的名称。 *job_name*是**sysname**，默认值为 NULL。 只有在使用现有作业而不是新创建的作业（此为默认设置）来同步订阅时，才需要指定此参数。 如果你不属于**sysadmin**固定服务器角色，则必须指定*job_login*并*job_password*时指定*job_name*.  
  
`[ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]` 要使用其中的快照文件将读取已筛选的数据快照文件夹的路径。 *dynamic_snapshot_location*是**nvarchar(260)** ，默认值为 NULL。 有关详细信息，请参阅 [参数化行筛选器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
`[ @use_web_sync = ] use_web_sync` 指示已启用 Web 同步。 *use_web_sync*是**位**，默认值为 0。 **1**指定，可以使用 HTTP 通过 internet 同步请求订阅。  
  
`[ @internet_url = ] 'internet_url'` 是的位置的复制侦听器 (REPLISAPI。DLL) 实现 Web 同步。 *执行*是**nvarchar(260)** ，默认值为 NULL。 *执行*是一个完全限定的 URL，格式`http://server.domain.com/directory/replisapi.dll`。 如果将服务器配置为侦听端口 80 以外的端口，则提供的端口号的格式也必须为 `http://server.domain.com:portnumber/directory/replisapi.dll`，其中的 `portnumber` 表示端口。  
  
`[ @internet_login = ] 'internet_login'` 合并代理连接到承载 Web 同步的 Web 服务器时使用的登录名使用 HTTP 基本身份验证。 *internet_login*是**sysname**，默认值为 NULL。  
  
`[ @internet_password = ] 'internet_password'` 合并代理连接到承载 Web 同步的 Web 服务器时使用的密码使用 HTTP 基本身份验证。 *internet_password*是**nvarchar(524)** ，默认值为 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
`[ @internet_security_mode = ] internet_security_mode` 在 Web 同步期间连接到 Web 服务器时，合并代理所使用的身份验证方法使用 HTTPS。 *internet_security_mode*是**int**可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|使用基本身份验证。|  
|**1** （默认值）|使用 Windows 集成身份验证。|  
  
> [!NOTE]  
>  建议您将基本身份验证与 Web 同步结合使用。 若要使用 Web 同步，必须与 Web 服务器进行 SSL 连接。 有关详细信息，请参阅 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。  
  
`[ @internet_timeout = ] internet_timeout` 是 (秒)，Web 同步请求过期之前的长度。 *internet_timeout*是**int**，默认值为**300**秒。  
  
`[ @hostname = ] 'hostname'` 参数化筛选器的 WHERE 子句中使用此函数时将覆盖 host_name （） 的值。 *主机名*是**sysname**，默认值为 NULL。  
  
`[ @job_login = ] 'job_login'` 是用于运行代理的 Windows 帐户的登录名。 *job_login*是**nvarchar(257)** ，无默认值。 使用 Windows 集成身份验证时，该 Windows 帐户始终用于到订阅服务器的代理连接及到分发服务器和发布服务器的连接。  
  
`[ @job_password = ] 'job_password'` 是用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，无默认值。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为保证安全性，应当在运行时再提供登录名和密码。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_addmergepullsubscription_agent**用于合并复制，并使用类似于的功能[sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。  
  
 有关如何执行时正确地指定安全设置的示例**sp_addmergepullsubscription_agent**，请参阅[创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addmergepullsubscription_agent**。  
  
## <a name="see-also"></a>请参阅  
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
