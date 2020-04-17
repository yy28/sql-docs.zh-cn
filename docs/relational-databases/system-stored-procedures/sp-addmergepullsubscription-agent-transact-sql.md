---
title: sp_addmergepullsubscription_agent（转算 SQL） |微软文档
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
ms.openlocfilehash: 07cc514d615c86a90dcf37fbd4748c3ab1776f06
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528971"
---
# <a name="sp_addmergepullsubscription_agent-transact-sql"></a>sp_addmergepullsubscription_agent (Transact-SQL)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  向合并发布添加一个用于计划请求订阅同步的新代理作业。 此存储过程在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @name = ] 'name'`是代理的名称。 *名称*是**sysname，** 默认值为 NULL。  
  
`[ @publisher = ] 'publisher'`是发布服务器的名称。 *发布者*是**sysname，** 没有默认值。  
  
`[ @publisher_db = ] 'publisher_db'`是发布者数据库的名称。 *publisher_db*是**系统名称**，没有默认值。  
  
`[ @publication = ] 'publication'`是发布的名称。 *发布*是**sysname，** 没有默认值。  
  
`[ @publisher_security_mode = ] publisher_security_mode`是同步时连接到发布服务器时使用的安全模式。 *publisher_security_mode*为**int，** 默认值为 1。 如果**为**0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则指定身份验证。 如果**为 1**，则指定 Windows 身份验证。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`是同步时连接到发布服务器时使用的登录名。 *publisher_login*是**系统名称**，默认值为 NULL。  
  
`[ @publisher_password = ] 'publisher_password'`是连接到发布服务器时使用的密码。 *publisher_password*是**系统名称**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
`[ @publisher_encrypted_password = ]publisher_encrypted_password`不再支持设置*publisher_encrypted_password。* 尝试将此**位**参数设置为**1**将导致错误。  
  
`[ @subscriber = ] 'subscriber'`是订阅者的名称。 *订户*是**sysname，** 默认值为 NULL。  
  
`[ @subscriber_db = ] 'subscriber_db'`是订阅数据库的名称。 *subscriber_db*是**系统名称**，默认值为 NULL。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`是同步时连接到订阅服务器时使用的安全模式。 *subscriber_security_mode* **为 int，** 默认值为 1。 如果**为**0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则指定身份验证。 如果**为 1**，则指定 Windows 身份验证。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 合并代理始终使用 Windows 身份验证连接到本地订阅服务器。 如果为此参数指定了值，将返回警告消息，但将忽略该值。  
  
`[ @subscriber_login = ] 'subscriber_login'`在同步时连接到订阅服务器时使用的订阅服务器登录名是。 如果subscriber_security_mode设置为**0，** 则需要*subscriber_login。* *subscriber_security_mode* *subscriber_login*是**系统名称**，默认值为 NULL。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 如果为此参数指定了值，将返回警告消息，但将忽略该值。  
  
`[ @subscriber_password = ] 'subscriber_password'`是身份验证的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅者密码。 如果subscriber_security_mode设置为**0，** 则需要*subscriber_password。* *subscriber_security_mode* *subscriber_password*是**sysname，** 默认值为 NULL。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 如果为此参数指定了值，将返回警告消息，但将忽略该值。  
  
`[ @distributor = ] 'distributor'`是分发服务器的名称。 *分发服务器*是**sysname，** 默认为*发布者*;也就是说，发布者也是分发服务器。  
  
`[ @distributor_security_mode = ] distributor_security_mode`是同步时连接到分发服务器时使用的安全模式。 *distributor_security_mode* **为 int，** 默认值为 0。 **0** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定身份验证。 **1**指定 Windows 身份验证。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`在同步时连接到分发服务器时使用的分发服务器登录名是。 如果*distributor_security_mode*设置为**0，** 则需要*distributor_login。* *distributor_login*是**系统名称**，默认值为 NULL。  
  
`[ @distributor_password = ] 'distributor_password'`是分发服务器密码。 如果*distributor_security_mode*设置为**0，** 则需要*distributor_password。* *distributor_password*是**系统名称**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
`[ @encrypted_password = ] encrypted_password`不再支持设置*encrypted_password。* 尝试将此**位**参数设置为**1**将导致错误。  
  
`[ @frequency_type = ] frequency_type`是计划合并代理的频率。 *frequency_type*是**int，** 可以是以下值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|一次性|  
|**2**|按需|  
|**4**|每日|  
|**8**|每周|  
|**16**|每月|  
|**32**|与“每月”选项相关|  
|**64**|自动启动|  
|**128**|重复执行|  
|NULL（默认值）||  
  
> [!NOTE]  
>  指定值**64**会导致合并代理在连续模式下运行。 这对应于为代理设置 **-连续**参数。 有关详细信息，请参阅 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
`[ @frequency_interval = ] frequency_interval`合并代理运行的天数。 *frequency_interval*是**int，** 可以是这些值之一。  
  
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
|**9**|工作日|  
|**10**|周末|  
|NULL（默认值）||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`是合并代理的日期。 当*frequency_type*设置为**32（** 每月相对）时，使用此参数。 *frequency_relative_interval*是**int，** 可以是这些值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|第一个|  
|**2**|秒|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|最后一个|  
|NULL（默认值）||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`是*frequency_type*使用的复发系数。 *frequency_recurrence_factor*为**int，** 默认值为 NULL。  
  
`[ @frequency_subday = ] frequency_subday`是在定义的时间段内重新计划的频率。 *frequency_subday* **是 int，** 可以是这些值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|秒|  
|**4**|Minute|  
|**8**|Hour|  
|NULL（默认值）||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`是*frequency_subday*的间隔。 *frequency_subday_interval* **为 int，** 默认值为 NULL。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`是首次计划合并代理（格式化为 HHMMSS）的一天中的时间。 *active_start_time_of_day* **为 int，** 默认值为 NULL。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`是合并代理停止计划的时间，格式化为 HHMMSS。 *active_end_time_of_day* **为 int，** 默认值为 NULL。  
  
`[ @active_start_date = ] active_start_date`是首次计划合并代理的日期，格式化为 YYYYMMD。 *active_start_date* **为 int，** 默认值为 NULL。  
  
`[ @active_end_date = ] active_end_date`是合并代理停止计划的日期，格式化为 YYYYMMDD。 *active_end_date* **为 int，** 默认值为 NULL。  
  
`[ @optional_command_line = ] 'optional_command_line'`是提供给合并代理的可选命令提示符。 *optional_command_line*是**nvarchar（255），** 默认值为''。 可用于向合并代理提供其他参数，例如在以下示例中，将默认的查询超时值增加到 `600` 秒：  
  
```  
@optional_command_line = N'-QueryTimeOut 600'  
```  
  
`[ @merge_jobid = ] merge_jobid`是作业 ID 的输出参数。 *merge_jobid*是**二进制 （16），** 默认值为 NULL。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`指定是否可以通过 Windows 同步管理器同步订阅。 *enabled_for_syncmgr*是**nvarchar（5），** 默认值为FALSE。 如果**为 false，** 则订阅不会注册到同步管理器。 如果**为 true，** 则订阅在同步管理器中注册，无需启动[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]即可同步。  
  
`[ @ftp_address = ] 'ftp_address'`仅适用于向后兼容性。  
  
`[ @ftp_port = ] ftp_port`仅适用于向后兼容性。  
  
`[ @ftp_login = ] 'ftp_login'`仅适用于向后兼容性。  
  
`[ @ftp_password = ] 'ftp_password'`仅适用于向后兼容性。  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'`指定从中拾取快照文件的位置。 *alternate_snapshot_folder*是**nvarchar （255），** 默认值为 NULL。 如果为 NULL，则从发布服务器指定的默认位置拾取快照文件。  
  
`[ @working_directory = ] 'working_directory'`是用于在 FTP 传输快照文件时临时存储发布数据和架构文件的工作目录的名称。 *working_directory*是**nvarchar （255），** 默认值为 NULL。  
  
`[ @use_ftp = ] 'use_ftp'`指定使用 FTP 而不是典型的协议来检索快照。 *use_ftp*是**nvarchar（5），** 默认值为FALSE。  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver' ]`使用交互式解析器解决所有允许交互式解析的文章的冲突。 *use_interactive_resolver*是**nvarchar（5），** 默认值为FALSE。  
  
`[ @offloadagent = ] 'remote_agent_activation'`
 > [!NOTE]  
>  已不推荐使用远程代理激活，也不再支持该功能。 支持此参数只是为了让脚本能够向后兼容。 将*remote_agent_activation*设置为**false**以外的值将生成错误。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  已不推荐使用远程代理激活，也不再支持该功能。 支持此参数只是为了让脚本能够向后兼容。 将*remote_agent_server_name*设置为任何非 NULL 值都会生成错误。  
  
`[ @job_name = ] 'job_name' ]`是现有代理作业的名称。 *job_name*是**sysname，** 默认值为 NULL。 只有在使用现有作业而不是新创建的作业（此为默认设置）来同步订阅时，才需要指定此参数。 如果您不是**sysadmin**固定服务器角色的成员，则必须在指定*job_name*时指定*job_login*和*job_password。*  
  
`[ @dynamic_snapshot_location = ] 'dynamic_snapshot_location' ]`如果要使用筛选的数据快照，则从其中读取快照文件的文件夹的路径。 *dynamic_snapshot_location*是**nvarchar （260），** 默认值为 NULL。 有关详细信息，请参阅 [参数化行筛选器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
`[ @use_web_sync = ] use_web_sync`指示启用了 Web 同步。 *use_web_sync* **位，** 默认值为 0。 **1**指定拉取订阅可以使用 HTTP 在互联网上同步。  
  
`[ @internet_url = ] 'internet_url'`是复制侦听器的位置 （REPLISAPI）。用于 Web 同步的 DLL）。 *internet_url*是**nvarchar（260），** 默认值为NULL。 *internet_url*是一个完全合格的 URL，格式`http://server.domain.com/directory/replisapi.dll`为 。 如果将服务器配置为侦听端口 80 以外的端口，则提供的端口号的格式也必须为 `http://server.domain.com:portnumber/directory/replisapi.dll`，其中的 `portnumber` 表示端口。  
  
`[ @internet_login = ] 'internet_login'`是合并代理使用 HTTP 基本身份验证连接到承载 Web 同步的 Web 服务器时使用的登录名。 *internet_login*是**系统名称**，默认值为 NULL。  
  
`[ @internet_password = ] 'internet_password'`是合并代理使用 HTTP 基本身份验证连接到承载 Web 同步的 Web 服务器时使用的密码。 *internet_password*是**nvarchar （524），** 默认值为 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
`[ @internet_security_mode = ] internet_security_mode`是合并代理在使用 HTTPS 在 Web 同步期间连接到 Web 服务器时使用的身份验证方法。 *internet_security_mode*是**int，** 可以是这些值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**0**|使用基本身份验证。|  
|**1** （默认值）|使用 Windows 集成身份验证。|  
  
> [!NOTE]  
>  建议您将基本身份验证与 Web 同步结合使用。 要使用 Web 同步，必须与 Web 服务器建立 TLS 连接。 有关详细信息，请参阅 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。  
  
`[ @internet_timeout = ] internet_timeout`是 Web 同步请求过期之前的时间长度（以秒为单位）。 *internet_timeout***是 int，** 默认为**300**秒。  
  
`[ @hostname = ] 'hostname'`在参数化筛选器的 WHERE 子句中使用此功能时，将覆盖HOST_NAME（）的值。 *主机名*是**系统名称**，默认值为 NULL。  
  
`[ @job_login = ] 'job_login'`是代理运行的 Windows 帐户的登录名。 *job_login*是**nvarchar（257），** 没有默认值。 使用 Windows 集成身份验证时，该 Windows 帐户始终用于到订阅服务器的代理连接及到分发服务器和发布服务器的连接。  
  
`[ @job_password = ] 'job_password'`是代理运行的 Windows 帐户的密码。 *job_password*是**系统名称**，没有默认值。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为保证安全性，应当在运行时再提供登录名和密码。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_addmergepullsubscription_agent**用于合并复制，并使用类似于[sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)的功能。  
  
 有关如何在执行**sp_addmergepullsubscription_agent**时正确指定安全设置的示例，请参阅[创建拉取订阅](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_1_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色才能**执行sp_addmergepullsubscription_agent**。  
  
## <a name="see-also"></a>另请参阅  
 [创建拉取订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [订阅出版物](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription&#40;转算-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
