---
title: sp_addsubscription (Transact SQL) |Microsoft 文档
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addsubscription
- sp_addsubscription_TSQL
helpviewer_keywords:
- sp_addsubscription
ms.assetid: 61ddf287-1fa0-4c1a-8657-ced50cebf0e0
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 42e9a7a49aab996a26ed0514854e7f2c1db9ce0b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spaddsubscription-transact-sql"></a>sp_addsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将订阅添加到发布并设置订阅服务器的状态。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addsubscription [ @publication = ] 'publication'  
    [ , [ @article = ] 'article']  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
        [ , [ @sync_type = ] 'sync_type' ]  
    [ , [ @status = ] 'status'  
        [ , [ @subscription_type = ] 'subscription_type' ]  
    [ , [ @update_mode = ] 'update_mode' ]  
    [ , [ @loopback_detection = ] 'loopback_detection' ]  
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
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
    [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @backupdevicetype = ] 'backupdevicetype' ]  
    [ , [ @backupdevicename = ] 'backupdevicename' ]  
    [ , [ @mediapassword = ] 'mediapassword' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @fileidhint = ] fileidhint ]  
    [ , [ @unload = ] unload ]  
    [ , [ @subscriptionlsn = ] subscriptionlsn ]  
    [ , [ @subscriptionstreams = ] subscriptionstreams ]  
    [ , [ @subscriber_type = ] subscriber_type ]  
    [ , [ @memory_optimized = ] memory_optimized ]  
```  
  
## <a name="arguments"></a>参数  
 [ @publication=] '*发布*  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ @article=] '*文章*  
 发布所订阅的项目。 *文章*是**sysname**，默认值为所有。 如果为 all，则订阅将添加到该发布的所有项目中。 Oracle 发布服务器只支持 all 或 NULL 值。  
  
 [ @subscriber=] '*订阅服务器*  
 订阅服务器的名称。 *订阅服务器*是**sysname**，默认值为 NULL。  
  
 [ @destination_db=] '*destination_db*'  
 用于放置复制数据的目标数据库的名称。 *destination_db*是**sysname**，默认值为 NULL。 当为 NULL 时， *destination_db*设置为发布数据库的名称。 对于 Oracle 发布者， *destination_db*必须指定。 对于非 SQL Server 订阅服务器，请为指定值的 （默认目标） *destination_db*。  
  
 [ @sync_type=] '*sync_type*'  
 订阅同步类型。 *sync_type*是**nvarchar （255)**，和可以是以下值之一：  
  
|“值”|Description|  
|-----------|-----------------|  
|none|订阅服务器已包含发布表的架构和初始数据。<br /><br /> 注意： 此选项已弃用。 请改用仅支持复制。|  
|automatic（默认值）|已发布表的架构和初始数据将首先传输到订阅服务器。|  
|replication support only|如果需要，在项目的订阅服务器上自动生成支持更新订阅的自定义存储过程和触发器。 假定订阅服务器已拥有已发布表的架构和初始数据。 在配置对等事务复制拓扑时，确保该拓扑中所有节点上的数据都相同。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。<br /><br /> *不支持非 SQL Server 发布的订阅。*|  
|initialize with backup|从发布数据库的备份获取已发布表的架构和初始数据。 假定订阅服务器对发布数据库的备份具有访问权。 备份的备份和媒体类型的位置由*backupdevicename*和*backupdevicetype*。 在使用此选项时，无需在配置期间停止对等事务复制拓扑。<br /><br /> *不支持非 SQL Server 发布的订阅。*|  
|initialize from lsn|在向对等事务复制拓扑添加节点时使用。 和 @subscriptionlsn 一起使用，以确保将所有相关事务都复制到新节点。 假定订阅服务器已拥有已发布表的架构和初始数据。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。|  
  
> [!NOTE]  
>  始终会传输系统表和数据。  
  
 [ @status=] '*状态*  
 订阅状态。 *状态*是**sysname**，默认值为 NULL。 当此参数未显式设置时，复制会自动将其设置为下列值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|active|订阅已初始化并可接受更改。 当设置此选项的值*sync_type*为 none，与备份或复制仅支持 32 位的初始化。|  
|subscribed|订阅需要进行初始化。 当设置此选项的值*sync_type*是自动的。|  
  
 [ @subscription_type=] '*subscription_type*'  
 是一种订阅。 *subscription_type*是**nvarchar(4)**，默认值为推送。 可以为 push 或 pull。 推送订阅的分发代理程序驻留在分发服务器，而请求订阅的分发代理程序驻留在订阅服务器上。 *subscription_type*可以请求创建对发布服务器已知的命名的请求订阅。 有关详细信息，请参阅[订阅发布](../../relational-databases/replication/subscribe-to-publications.md)。  
  
> [!NOTE]  
>  匿名订阅无需使用此存储过程。  
  
 [ @update_mode=] '*update_mode*'  
 是更新的类型。*update_mode*是**nvarchar (30)**，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|read only（默认值）|该订阅是只读的。 在订阅服务器上所做的更改不会发送到发布服务器。|  
|sync tran|支持立即更新订阅。 Oracle 发布服务器不支持。|  
|queued tran|支持订阅进行排队更新。 可以在订阅服务器上进行数据修改，将其存储在队列中，然后传播到发布服务器。 Oracle 发布服务器不支持。|  
|failover|将排队更新作为故障转移的情况下启用用于即时更新的订阅。 可以在订阅服务器上进行数据修改并立即传播到发布服务器。 如果发布服务器与订阅服务器未连接在一起，则可以更改更新模式以便将在订阅服务器上所做的数据修改存储在队列中，直到订阅服务器与发布服务器重新连接在一起。 Oracle 发布服务器不支持。|  
|queued failover|支持将订阅作为排队更新订阅，并允许更改为立即更新模式。 在订阅服务器和发布服务器之间建立连接之前，可以在订阅服务器上修改数据，并将数据修改存储在队列中。 建立起持续连接后，即可将更新模式更改为立即更新。 Oracle 发布服务器不支持。|  
  
 请注意在被订阅该发布允许 DTS 是否不允许的值同步事务和排队的 tran。  
  
 [ @loopback_detection=] '*loopback_detection*  
 指定分发代理是否将从订阅服务器发起的事务发送回该订阅服务器。 *loopback_detection*是**nvarchar(5)**，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|true|分发代理不将从订阅服务器上发起的事务发送回该订阅服务器。 与双向事务复制一起使用。 有关详细信息，请参阅[双向事务复制](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md)。|  
|false|分发代理将在订阅服务器上发起的事务发送回订阅服务器。|  
|NULL（默认值）|对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器，自动设置为 true，对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器，则设置为 false。|  
  
 [ @frequency_type=] *frequency_type*  
 安排分发任务所使用的频率。 *frequency_type* int，并且可以是下列值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|1|一次|  
|2|按需|  
|4|每天|  
|8|每周|  
|16|每月|  
|32|与“每月”选项相关|  
|64 （默认值）|自动启动|  
|128|重复执行|  
  
 [ @frequency_interval=] *frequency_interval*  
 是要应用于通过设置的频率的值*frequency_type*。 *frequency_interval*是**int**，默认值为 NULL。  
  
 [ @frequency_relative_interval=] *frequency_relative_interval*  
 分发代理的日期。 使用此参数时*frequency_type*设置为 32 （每月相对）。 *frequency_relative_interval*是**int**，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|1|第一个|  
|2|第二个|  
|4|第三个|  
|8|第四个|  
|16|上一次|  
|NULL（默认值）||  
  
 [ @frequency_recurrence_factor=] *frequency_recurrence_factor*  
 是由重复因素*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 NULL。  
  
 [ @frequency_subday=] *frequency_subday*  
 在定义周期内重新调度的频率（分钟）。 *frequency_subday*是**int**，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|1|一次|  
|2|第二个|  
|4|Minute|  
|8|Hour|  
|NULL||  
  
 [ @frequency_subday_interval=] *frequency_subday_interval*  
 是的间隔*frequency_subday*。 *frequency_subday_interval*是**int**，默认值为 NULL。  
  
 [ @active_start_time_of_day=] *active_start_time_of_day*  
 第一次安排分发代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为 NULL。  
  
 [ @active_end_time_of_day=] *active_end_time_of_day*  
 停止安排分发代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 NULL。  
  
 [ @active_start_date=] *active_start_date*  
 第一次安排分发代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 NULL。  
  
 [ @active_end_date=] *active_end_date*  
 停止安排分发代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 NULL。  
  
 [ @optional_command_line=] '*optional_command_line*'  
 要执行的可选命令提示符。 *optional_command_line*是**nvarchar （4000)**，默认值为 NULL。  
  
 [ @reserved=] '*保留*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @enabled_for_syncmgr=] '*enabled_for_syncmgr*'  
 是是否通过同步订阅[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 同步管理器。 *enabled_for_syncmgr*是**nvarchar(5)**，默认值为 FALSE。 如果为 false，则表示订阅没有在 Windows 同步管理器中注册。 如果为 true，则表示订阅已向 Windows 同步管理器注册，因而可以在不启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的情况下同步。 Oracle 发布服务器不支持。  
  
 [ @offloadagent= ] '*remote_agent_activation*'  
 指定可远程激活代理。 *remote_agent_activation*是**位**默认值为 0。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它只是为了让脚本能够向后兼容。  
  
 [ @offloadserver= ] '*remote_agent_server_name*'  
 指定用于远程激活的服务器的网络名称。 *remote_agent_server_name*是**sysname**，默认值为 NULL。  
  
 [ @dts_package_name= ] '*dts_package_name*'  
 指定 Data Transformation Services (DTS) 包的名称。 *dts_package_name*是**sysname**默认值为 NULL。 例如，若要指定 DTSPub_Package 包，则该参数将为 `@dts_package_name = N'DTSPub_Package'`。 该参数可用于推送订阅。 若要将 DTS 包信息添加到请求订阅，请使用 sp_addpullsubscription_agent。  
  
 [ @dts_package_password= ] '*dts_package_password*'  
 指定用于包的密码（如果有）。 *dts_package_password*是**sysname**默认值为 NULL。  
  
> [!NOTE]  
>  如果满足以下条件，则必须指定密码*dts_package_name*指定。  
  
 [ @dts_package_location= ] '*dts_package_location*'  
 指定包位置。 *dts_package_location*是**nvarchar(12)**，默认值为分发服务器。 包的位置可以是 distributor 或 subscriber。  
  
 [ @distribution_job_name= ] '*distribution_job_name*'  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ @publisher= ] '*publisher*'  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*不应为指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
 [ @backupdevicetype= ] '*backupdevicetype*'  
 指定从备份初始化订阅服务器时使用的备份设备的类型。 *backupdevicetype*是**nvarchar(20)**，并且可以为这些值之一：  
  
|“值”|Description|  
|-----------|-----------------|  
|logical（默认值）|备份设备是逻辑设备。|  
|disk|备份设备是磁盘驱动器。|  
|tape|备份设备是磁带机。|  
  
 *backupdevicetype*仅当使用*sync_method*设置为 initialize_with_backup。  
  
 [ @backupdevicename= ] '*backupdevicename*'  
 指定从备份初始化订阅服务器时使用的设备的名称。 *backupdevicename*是**nvarchar(1000)**，默认值为 NULL。  
  
 [ @mediapassword= ] '*mediapassword*'  
 指定介质集的密码（如果在格式化介质时设置了密码）。 *mediapassword*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 [ @password= ] '*password*'  
 指定备份的密码（如果在创建备份时设置了密码）。 *密码*是**sysname**，默认值为 NULL。  
  
 [ @fileidhint= ] *fileidhint*  
 标识要还原的备份集的序号值。 *fileidhint*是**int**，默认值为 NULL。  
  
 [ @unload=]*卸载*  
 指定在从备份进行的初始化完成后是否应取出磁带备份设备。 *卸载*是**位**，默认值为 1。 1 表示指定应卸载磁带。 *卸载*仅当使用*backupdevicetype*是磁带。  
  
 [ @subscriptionlsn= ] *subscriptionlsn*  
 指定订阅应从其开始将更改传递给对等事务复制拓扑中的节点的日志序列号 (LSN)。 与使用@sync_type从 lsn，若要确保所有的相关事务将复制到新节点的初始化值。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 [ @subscriptionstreams= ] *subscriptionstreams*  
 每个分发代理允许的连接数，用于将成批更改并行应用于订阅服务器，同时保留在使用单线程时具有的多种事务特征。 *subscriptionstreams*是**tinyint**，默认值为 NULL。 支持使用 1 到 64 之间的值。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器、Oracle 发布服务器和对等订阅均不支持此参数。 每当使用订阅流时，都会在 msreplication_subscriptions 表中添加附加行（每个流一行），且 agent_id 设置为 NULL。  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)]订阅流不适用于配置为传递  的项目。 若要使用订阅流，请改将项目配置为传递存储过程调用。  
  
 [ @subscriber_type=] *subscriber_type*  
 订阅服务器的类型。 *subscriber_type*是**tinyint**，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|0（默认值）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器|  
|1|ODBC 数据源服务器|  
|2|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet 数据库|  
|3|OLE DB 访问接口|  
  
 [ @memory_optimized=] *memory_optimized*  
 指示订阅支持内存优化表。 *memory_optimized*是**位**、 1 等于 true （的订阅支持内存优化表）。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 sp_addsubscription 用于快照复制和事务复制。  
  
 当 sysadmin 固定服务器角色的成员执行 sp_addsubscription 以创建推送订阅时，将隐式创建分发代理作业并将在 SQL Server 代理服务帐户下运行该作业。 我们建议你执行[sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)并指定不同的、 特定代理的 Windows 帐户的凭据@job_login和@job_password。 有关详细信息，请参阅 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
 sp_addsubscription 禁止 ODBC 和 OLE DB 订阅服务器访问下列发布：  
  
-   使用本机创建*sync_method*对的调用中[sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。  
  
-   包含已添加到与发布的文章[sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)存储过程具有*pre_creation_cmd*参数值为 3 （截断）。  
  
-   尝试设置*update_mode*同步 tran。  
  
-   含有被配置为使用参数化语句的项目的发布。  
  
 此外，如果发布具有*allow_queued_tran*选项设置为 true （可启用队列的订阅服务器上的更改，直到它们可以应用于发布服务器），时间戳列的项目中编写脚本为**时间戳**，和对该列的更改发送到订阅服务器。 订阅服务器将生成并更新时间戳列值。 对于 ODBC 或 OLE DB 订阅服务器，sp_addsubscription 失败如果尝试对已发布订阅*allow_queued_tran*设置为 true，与它的时间戳列的文章。  
  
 如果订阅不使用 DTS 包，它无法订阅发布设置为*allow_transformable_subscriptions*。 如果来自发布的表需要同时复制到 DTS 订阅和非 DTS 订阅，则必须创建两种单独的发布：每种发布分别针对一种订阅类型。  
  
 选择 **sync_type** 选项 *replication support only*、 *initialize with backup*或 *initialize from lsn*时，日志读取器代理必须在执行 **sp_addsubscription**后运行，以便将设置脚本写入分发数据库。 日志读取器代理必须在作为 **sysadmin** 固定服务器角色成员的帐户下运行。 将 **sync_type** 选项设置为 *Automatic*时，不需要执行任何特殊日志读取器代理操作。  
  
## <a name="permissions"></a>权限  
 只有 sysadmin 固定服务器角色成员或 db_owner 固定数据库角色成员才能执行 sp_addsubscription。 对于请求订阅，在发布访问列表中有登录权的用户可以执行 sp_addsubscription。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addsubscription-trans_1.sql)]  
  
## <a name="see-also"></a>另请参阅  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [为非 SQL Server 订阅服务器创建订阅](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpushsubscription_agent &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_changesubstatus &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
