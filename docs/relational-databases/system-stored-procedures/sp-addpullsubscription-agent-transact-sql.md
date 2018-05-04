---
title: sp_addpullsubscription_agent (TRANSACT-SQL) |Microsoft 文档
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
- sp_addpullsubscription_agent
- sp_addpullsubscription_agent_TSQL
helpviewer_keywords:
- sp_addpullsubscription_agent
ms.assetid: b9c2eaed-6d2d-4b78-ae9b-73633133180b
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1c2d31df834b2809612604d1392f860b222da73c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spaddpullsubscriptionagent-transact-sql"></a>sp_addpullsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
 
  向事务发布添加用于同步请求订阅的新计划的代理作业。 此存储过程在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addpullsubscription_agent [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]          , [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor = ] 'distributor' ]  
    [ , [ @distribution_db = ] 'distribution_db' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]  
    [ , [ @distributor_login = ] 'distributor_login' ]  
    [ , [ @distributor_password = ] 'distributor_password' ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
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
    [ , [ @distribution_jobid = ] distribution_jobid OUTPUT ]  
    [ , [ @encrypted_distributor_password = ] encrypted_distributor_password ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port = ] ftp_port ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]  
    [ , [ @working_directory = ] 'working_directory' ]  
    [ , [ @use_ftp = ] 'use_ftp' ]  
    [ , [ @publication_type = ] publication_type ]  
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @offloadagent = ] 'remote_agent_activation' ]  
    [ , [ @offloadserver = ] 'remote_agent_server_name']  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher=**] **'***publisher***'**  
 发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [  **@publisher_db=**] *** * * publisher_db'*  
 发布服务器数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。 *publisher_db*忽略的 Oracle 发布服务器。  
  
 [ **@publication=**] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@subscriber=**] *****订阅服务器*****  
 订阅服务器的名称。 *订阅服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。  
  
 [  **@subscriber_db=**] *****subscriber_db*****  
 是订阅数据库的名称。 *subscriber_db*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。  
  
 [  **@subscriber_security_mode=**] *subscriber_security_mode*  
 同步时连接到订阅服务器所使用的安全模式。 *subscriber_security_mode*是**int、**默认值为 NULL。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 **1**指定 Windows 身份验证。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 分发代理始终使用 Windows 身份验证连接到本地订阅服务器。 如果非 NULL 值或**1**指定对于此参数，将返回一条警告消息。  
  
 [  **@subscriber_login =**] *****subscriber_login*****  
 是同步时，连接到订阅服务器时要使用的订阅服务器登录。*subscriber_login*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 如果为此参数指定一个值，则返回一条警告消息，但忽略的值。  
  
 [  **@subscriber_password=**] *****subscriber_password*****  
 订阅服务器密码。 *subscriber_password*是必需的如果*subscriber_security_mode*设置为**0**。 *subscriber_password*是**sysname**，默认值为 NULL。 如果使用订阅服务器密码，将自动对密码进行加密。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 如果为此参数指定一个值，则返回一条警告消息，但忽略的值。  
  
 [  **@distributor=**] *****分发服务器*****  
 是分发服务器的名称。 *分发服务器*是**sysname**，默认值为指定的值*发布服务器*。  
  
 [  **@distribution_db=**] *****distribution_db*****  
 是分发数据库的名称。 *distribution_db*是**sysname**，默认值为 NULL。  
  
 [  **@distributor_security_mode=**] *distributor_security_mode*  
 是要同步时，连接到分发服务器时使用的安全模式。 *distributor_security_mode*是**int**，默认值为**1**。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 **1**指定 Windows 身份验证。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login=**] *****distributor_login*****  
 同步时连接到分发服务器所使用的分发服务器登录名。 *distributor_login*是必需的如果*distributor_security_mode*设置为**0**。 *distributor_login*是**sysname**，默认值为 NULL。  
  
 [  **@distributor_password =**] *****distributor_password*****  
 分发服务器密码。 *distributor_password*是必需的如果*distributor_security_mode*设置为**0**。 *distributor_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  不要使用空密码。 请使用强密码。 如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
 [  **@optional_command_line=**] *****optional_command_line*****  
 提供给分发代理的可选命令提示符。 例如， **-DefinitionFile** C:\Distdef.txt 或 **-CommitBatchSize** 10。 *optional_command_line*是**nvarchar （4000)**，默认值为空字符串。  
  
 [  **@frequency_type=**] *frequency_type*  
 安排分发代理计划的频率。 *frequency_type*是**int**，和可以是以下值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**2** （默认值）|按需|  
|**4**|每天|  
|**8**|每周|  
|**16**|每月|  
|**32**|与“每月”选项相关|  
|**64**|自动启动|  
|**128**|重复执行|  
  
> [!NOTE]  
>  指定的值**64**导致分发代理以连续模式运行。 这对应于设置 **-连续**代理程序的参数。 有关详细信息，请参阅 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
 [  **@frequency_interval=**] *frequency_interval*  
 是要应用于通过设置的频率的值*frequency_type*。 *frequency_interval*是**int**，默认值为 1。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 分发代理的日期。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，和可以是以下值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**1** （默认值）|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 是由重复因素*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为**1**。  
  
 [  **@frequency_subday=**] *frequency_subday*  
 在指定期内重新安排计划的频率。 *frequency_subday*是**int**，和可以是以下值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**1** （默认值）|一次|  
|**2**|第二个|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 是的间隔*frequency_subday*。 *frequency_subday_interval*是**int**，默认值为**1**。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 第一次安排分发代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为**0**。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 停止安排分发代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为**0**。  
  
 [  **@active_start_date=**] *active_start_date*  
 第一次安排分发代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为**0**。  
  
 [  **@active_end_date=**] *active_end_date*  
 停止安排分发代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为**0**。  
  
 [  **@distribution_jobid =**] *distribution_jobid * * * 输出**  
 此作业的分发代理 ID。 *distribution_jobid*是**binary （16)**，默认值为 NULL，并且它是一个输出参数。  
  
 [  **@encrypted_distributor_password=**] *encrypted_distributor_password*  
 设置*encrypted_distributor_password*不再受支持。 尝试设置这**位**参数**1**将导致错误。  
  
 [  **@enabled_for_syncmgr=**] *****enabled_for_syncmgr*****  
 是是否通过同步订阅[!INCLUDE[msCoName](../../includes/msconame-md.md)]同步管理器。 *enabled_for_syncmgr*是**nvarchar(5)**，默认值为 FALSE。 如果**false**，订阅未注册使用同步管理器。 如果**true**，该订阅已注册使用同步管理器，可以同步而无需启动[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 [  **@ftp_address=**] *****ftp_address*****  
 仅为保持向后兼容。  
  
 [  **@ftp_port=**] *ftp_port*  
 仅为保持向后兼容。  
  
 [  **@ftp_login=**] *****ftp_login*****  
 仅为保持向后兼容。  
  
 [  **@ftp_password=**] *****ftp_password*****  
 仅为保持向后兼容。  
  
 [  **@alt_snapshot_folder=** ] *** * * alternate_snapshot_folder*  
 指定快照的备用文件夹的位置。 *alternate_snapshot_folder*是**nvarchar （255)**，默认值为 NULL。  
  
 [ **@working_directory**=] *****working_director*****  
 用于存储发布的数据和架构文件的工作目录的名称。 *working_directory*是**nvarchar （255)**，默认值为 NULL。 名称应按 UNC 格式指定。  
  
 [ **@use_ftp**=] *****use_ftp*****  
 指定使用 FTP 而非常规协议检索快照。 *use_ftp*是**nvarchar(5)**，默认值为 FALSE。  
  
 [ **@publication_type**=] *publication_type*  
 指定发布的复制类型。 *publication_type*是**tinyint**默认值为**0**。 如果**0**，发布是一种事务类型。 如果**1**，发布是快照类型。 如果**2**，发布是合并类型。  
  
 [ **@dts_package_name**=] *****dts_package_name*****  
 指定 DTS 包的名称。 *dts_package_name*是**sysname**默认值为 NULL。 例如，若要将包名称指定为 `DTSPub_Package`，则该参数应为 `@dts_package_name = N'DTSPub_Package'`。  
  
 [ **@dts_package_password**=] *****dts_package_password*****  
 指定用于包的密码（如果有）。 *dts_package_password*是**sysname**以及默认值为 NULL，这意味着密码不是包。  
  
> [!NOTE]  
>  如果满足以下条件，则必须指定密码*dts_package_name*指定。  
  
 [ **@dts_package_location**=] *****dts_package_location*****  
 指定包位置。 *dts_package_location*是**nvarchar(12)**，默认值为**订阅服务器**。 包的位置可以是**分发服务器**或**订阅服务器**。  
  
 [ **@reserved**=] *****保留*****  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@offloadagent**=] '*remote_agent_activation*  
 > [!NOTE]  
>  已不推荐使用远程代理激活，也不再支持该功能。 支持此参数只是为了让脚本能够向后兼容。 设置*remote_agent_activation*到以外的其他值**false**将生成错误。  
  
 [ **@offloadserver**=] '*remote_agent_server_name*  
 > [!NOTE]  
>  已不推荐使用远程代理激活，也不再支持该功能。 支持此参数只是为了让脚本能够向后兼容。 设置*remote_agent_server_name*为任何非 NULL 值，则将生成错误。  
  
 [ **@job_name**=] '*job_name*  
 现有代理作业的名称。 *job_name*是**sysname**，默认值为 NULL。 只有在使用现有作业而不是新创建的作业（此为默认设置）来同步订阅时，才需要指定此参数。 如果你不属于**sysadmin**固定服务器角色，你必须指定*job_login*和*job_password*时指定*job_name*.  
  
 [ **@job_login**=] *****job_login*****  
 用于运行代理的 Windows 帐户的登录名。 *job_login*是**nvarchar(257)**，无默认值。 代理始终可以使用此 Windows 帐户连接到订阅服务器。  
  
 [ **@job_password**=] *****job_password*****  
 用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，无默认值。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_addpullsubscription_agent**快照复制和事务复制中使用。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-a_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addpullsubscription_agent**。  
  
## <a name="see-also"></a>另请参阅  
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
