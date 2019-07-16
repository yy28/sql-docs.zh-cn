---
title: sp_addpublication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
author: stevestein
ms.author: sstein
ms.openlocfilehash: f676acf9b3ee91bb5a1fb46cae2f7c693dc66983
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061821"
---
# <a name="spaddpublication-transact-sql"></a>sp_addpublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建快照或事务发布。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addpublication [ @publication = ] 'publication'  
    [ , [ @taskid = ] tasked ]  
    [ , [ @restricted = ] 'restricted' ]  
    [ , [ @sync_method = ] 'sync_method' ]  
    [ , [ @repl_freq = ] 'repl_freq' ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @status = ] 'status' ]  
    [ , [ @independent_agent = ] 'independent_agent' ]  
    [ , [ @immediate_sync = ] 'immediate_sync' ]  
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]  
    [ , [ @allow_push = ] 'allow_push'  
    [ , [ @allow_pull = ] 'allow_pull' ]  
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]  
    [ , [ @allow_sync_tran = ] 'allow_sync_tran' ]  
    [ , [ @autogen_sync_procs = ] 'autogen_sync_procs' ]  
    [ , [ @retention = ] retention ]  
    [ , [ @allow_queued_tran= ] 'allow_queued_updating' ]  
    [ , [ @snapshot_in_defaultfolder= ] 'snapshot_in_default_folder' ]  
    [ , [ @alt_snapshot_folder= ] 'alternate_snapshot_folder' ]  
    [ , [ @pre_snapshot_script= ] 'pre_snapshot_script' ]  
    [ , [ @post_snapshot_script= ] 'post_snapshot_script' ]  
    [ , [ @compress_snapshot= ] 'compress_snapshot' ]  
    [ , [ @ftp_address = ] 'ftp_address' ]  
    [ , [ @ftp_port= ] ftp_port ]  
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]  
    [ , [ @ftp_login = ] 'ftp_login' ]  
    [ , [ @ftp_password = ] 'ftp_password' ]  
    [ , [ @allow_dts = ] 'allow_dts' ]  
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]  
    [ , [ @conflict_policy = ] 'conflict_policy' ]  
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @conflict_retention = ] conflict_retention ]  
    [ , [ @queue_type = ] 'queue_type' ]  
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]  
    [ , [ @logreader_job_name = ] 'logreader_agent_name' ]  
    [ , [ @qreader_job_name = ] 'queue_reader_agent_name' ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @allow_initialize_from_backup = ] 'allow_initialize_from_backup' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @enabled_for_p2p = ] 'enabled_for_p2p' ]  
    [ , [ @publish_local_changes_only = ] 'publish_local_changes_only' ]  
    [ , [ @enabled_for_het_sub = ] 'enabled_for_het_sub' ]  
    [ , [ @p2p_conflictdetection = ] 'p2p_conflictdetection' ]  
    [ , [ @p2p_originator_id = ] p2p_originator_id  
    [ , [ @p2p_continue_onconflict = ] 'p2p_continue_onconflict'  
    [ , [ @allow_partition_switch = ] 'allow_partition_switch'  
    [ , [ @replicate_partition_switch = ]'replicate_partition_switch'  
```  
  
## <a name="arguments"></a>参数  
`[ \@publication = ] 'publication'` 是要创建的名称。 *发布*是**sysname**，无默认值。 该名称在数据库中必须唯一。  
  
`[ \@taskid = ] taskid` 向后兼容; 仅支持使用[sp_addpublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。  
  
`[ \@restricted = ] 'restricted'` 向后兼容; 仅支持使用*default_access*。  
  
`[ \@sync_method = ] _'sync_method'` 是同步模式。 *sync_method*是**nvarchar(13)** ，可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**native**|生成所有表的本机模式大容量复制程序输出。 *对 Oracle 发布服务器不支持*。|  
|**character**|生成所有表的字符模式大容量复制程序输出。 _为 Oracle 发布服务器中，_ **字符**_仅对快照复制有效_。|  
|**并发**|生成所有表的本机模式大容量复制程序输出，但在快照过程中并不锁定表。 只有事务发布支持该值。 *对 Oracle 发布服务器不支持*。|  
|**concurrent_c**|生成所有表的字符模式大容量复制程序输出，但在快照过程中并不锁定表。 只有事务发布支持该值。|  
|**数据库快照**|从数据库快照生成所有表的本机模式大容量复制程序输出。 数据库快照的每个版本中不可[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。|  
|**数据库快照字符**|从数据库快照生成所有表的字符模式大容量复制程序输出。 数据库快照的每个版本中不可[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。|  
|NULL（默认值）|默认情况下**本机**有关[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 对于非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器，默认值为**字符**时的值*repl_freq*是**快照**并对其**concurrent_c**对于所有其他情况。|  
  
`[ \@repl_freq = ] 'repl_freq'` 是一种复制频率*repl_freq*是**nvarchar(10)** ，可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**连续**（默认值）|发布服务器提供所有基于日志的事务的输出。 对于非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器，这就要求*sync_method*设置为**concurrent_c**。|  
|**快照**|发布服务器仅生成计划的同步事件。 对于非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器，这就要求*sync_method*设置为**字符**。|  
  
`[ \@description = ] 'description'` 是发布的可选描述。 *描述*是**nvarchar(255)** ，默认值为 NULL。  
  
`[ \@status = ] 'status'` 指定发布数据是否可用。 *状态*是**nvarchar(8)** ，可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**active**|发布数据可立即用于订阅服务器。|  
|**非活动**（默认值）|首次创建发布时，发布数据不能由订阅服务器使用（订阅服务器可以订阅，但这些订阅不被处理）。|  
  
 *对 Oracle 发布服务器不支持*。  
  
`[ \@independent_agent = ] 'independent_agent'` 指定是否有用于此发布的独立分发代理。 *independent_agent*是**nvarchar(5)** ，默认值为 FALSE。 如果 **，则返回 true**，没有用于此发布的独立分发代理。 如果**false**，发布使用共享的分发代理，并且每个发布服务器数据库/订阅服务器数据库对具有单一的共享代理。  
  
`[ \@immediate_sync = ] 'immediate_synchronization'` 指定是否每次快照代理运行的时创建发布的同步文件。 *immediate_synchronization*是**nvarchar(5)** ，默认值为 FALSE。 如果 **，则返回 true**，创建或重新创建每次快照代理运行的时的同步文件。 如果快照代理在订阅创建前完成，则订阅服务器可以立即获得同步文件。 新订阅将获取最近一次执行快照代理所生成的最新同步文件。 *independent_agent*必须是**true**有关*immediate_synchronization*要**true**。 如果**false**，仅当有新订阅，才创建同步文件。 必须调用[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)为每个订阅时以增量方式将新项目添加到现有发布。 订阅后订阅服务器无法接收同步文件，直到启动并完成快照代理为止。  
  
`[ \@enabled_for_internet = ] 'enabled_for_internet'` 指定是否为 Internet 启用发布，并确定是否可以使用文件传输协议 (FTP) 将快照文件传输到订阅服务器。 *enabled_for_internet*是**nvarchar(5)** ，默认值为 FALSE。 如果 **，则返回 true**，发布的同步文件将放入 C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp 目录。 用户必须创建 Ftp 目录。  
  
`[ \@allow_push = ] 'allow_push'` 指定是否可以为给定发布创建推送订阅。 *allow_push*是**nvarchar(5)** ，其默认值为 TRUE，表示允许推送订阅发布。  
  
`[ \@allow_pull = ] 'allow_pull'` 指定是否可以为给定发布创建请求订阅。 *allow_pull*是**nvarchar(5)** ，默认值为 FALSE。 如果**false**，对该发布不允许请求订阅。  
  
`[ \@allow_anonymous = ] 'allow_anonymous'` 指定是否可以为给定发布创建匿名订阅。 *allow_anonymous*是**nvarchar(5)** ，默认值为 FALSE。 如果 **，则返回 true**， *immediate_synchronization*还必须设置为**true**。 如果**false**，对该发布不允许匿名订阅。  
  
`[ \@allow_sync_tran = ] 'allow_sync_tran'` 指定是否对该发布允许立即更新订阅。 *allow_sync_tran*是**nvarchar(5)** ，默认值为 FALSE。 **true**是*Oracle 发布服务器不支持*。  
  
`[ \@autogen_sync_procs = ] 'autogen_sync_procs'` 指定是否在发布服务器上生成同步可更新订阅的存储的过程。 *autogen_sync_procs*是**nvarchar(5)** ，可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**true**|在启用更新订阅时自动设置。|  
|**false**|在未启动更新订阅或没有为 Oracle 发布服务器启动更新订阅时自动设置。|  
|NULL（默认值）|默认情况下 **，则返回 true**何时启用更新订阅以及向**false**更新订阅未启用时。|  
  
> [!NOTE]  
>  用户提供的值*autogen_sync_procs*将根据为指定的值重写*allow_queued_tran*并*allow_sync_tran*。  
  
`[ \@retention = ] retention` 是以小时为单位订阅活动的保持期。 *保留期*是**int**，默认值为 336 小时。 如果订阅在保持期内不活动，则过期后将其删除。 该值可以大于发布服务器使用的分发数据库的最大保持期。 如果**0**，对发布的已知订阅将永不过期，并通过过期订阅清除代理删除。  
  
`[ \@allow_queued_tran = ] 'allow_queued_updating'` 启用或禁用的订阅服务器上的更改进行排队，直到它们可以应用于发布。 *allow_queued_updating*是**nvarchar(5)** 默认值为 FALSE。 如果**false**，则不在订阅服务器上的更改进行排队。 **true**是*Oracle 发布服务器不支持*。  
  
`[ \@snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'` 指定快照文件是否存储在默认文件夹中。 *snapshot_in_default_folder*是**nvarchar(5)** 默认值为 TRUE。 如果 **，则返回 true**，可以在默认文件夹中找到快照文件。 如果**false**，快照文件存储在由指定的备用位置*alternate_snapshot_folder*。 备用位置可以在另一台服务器、一个网络驱动器或可移动介质（如光盘或可移动磁盘）上。 也可以将快照文件保存到 FTP 站点以供订阅服务器以后检索。 请注意，此参数可以为 true，仍有一个位置 **\@alt_snapshot_folder**参数。 该组合指定将快照文件同时存储在默认位置和备用位置。  
  
`[ \@alt_snapshot_folder = ] 'alternate_snapshot_folder'` 指定备用快照文件夹的位置。 *alternate_snapshot_folder*是**nvarchar(255)** 默认值为 NULL。  
  
`[ \@pre_snapshot_script = ] 'pre_snapshot_script'` 指定一个指向 **.sql**文件位置。 *pre_snapshot_script*是**nvarchar(255)，** 默认值为 NULL。 分发代理将在运行任何复制的对象时在订阅服务器上应用快照之前运行快照前脚本。 该脚本在分发代理连接到订阅数据库时使用的安全上下文中执行。  
  
`[ \@post_snapshot_script = ] 'post_snapshot_script'` 指定一个指向 **.sql**文件位置。 *post_snapshot_script*是**nvarchar(255)** ，默认值为 NULL。 分发代理将在初始同步过程中已应用所有其他复制的对象脚本和数据之后才运行快照后脚本。 该脚本在分发代理连接到订阅数据库时使用的安全上下文中执行。  
  
`[ \@compress_snapshot = ] 'compress_snapshot'` 指定写入到的快照 **\@alt_snapshot_folder**位置是将压缩成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 *compress_snapshot*是**nvarchar(5)** ，默认值为 FALSE。 **false**指定，将不压缩快照; **，则返回 true**指定将压缩的快照。 不能压缩大于 2 GB 的快照文件。 压缩快照文件在分发代理运行的位置解压缩；请求订阅通常与压缩快照一起使用，以便在订阅服务器上解压缩文件。 不能压缩默认文件夹中的快照。  
  
`[ \@ftp_address = ] 'ftp_address'` 是分发服务器的 FTP 服务的网络地址。 *ftp_address*是**sysname**，默认值为 NULL。 指定供订阅服务器的分发代理或合并代理拾取的发布快照文件的位置。 由于为每个发布都存储此属性，因此每个发布可以具有不同*ftp_address*。 该发布必须支持使用 FTP 来传播快照。  
  
`[ \@ftp_port = ] ftp_port` 是分发服务器的 FTP 服务的端口号。 *ftp_port*是**int**，默认值为 21。 指定供分发代理或合并代理拾取的订阅服务器的发布快照文件的位置。 由于此属性存储每个发布，每个发布可以具有其自己*ftp_port*。  
  
`[ \@ftp_subdirectory = ] 'ftp_subdirectory'` 指定快照文件将在其中可用的分发代理或合并代理要选取如果发布支持使用 FTP 传播快照的订阅服务器。 *ftp_subdirectory*是**nvarchar(255)** ，默认值为 NULL。 由于此属性存储每个发布，每个发布可以具有其自己*ftp_subdirctory*或选择允许使用 NULL 值指示没有子目录。  
  
`[ \@ftp_login = ] 'ftp_login'` 用于连接到 FTP 服务用户名。 *ftp_login*是**sysname**，默认值为 ANONYMOUS。  
  
`[ \@ftp_password = ] 'ftp_password'` 用于连接到 FTP 服务的用户密码。 *ftp_password*是**sysname**，默认值为 NULL。  
  
`[ \@allow_dts = ] 'allow_dts'` 指定该发布允许数据转换。 创建订阅时可以指定 DTS 包。 *allow_transformable_subscriptions*是**nvarchar(5)** ，默认值为 FALSE，它不允许 DTS 转换。 当*allow_dts*为 true， *sync_method*必须设置为**字符**或者**concurrent_c**。  
  
 **true**是*Oracle 发布服务器不支持*。  
  
`[ \@allow_subscription_copy = ] 'allow_subscription_copy'` 启用或禁用复制订阅此发布的订阅数据库的能力。 *allow_subscription_copy*是**nvarchar(5)** ，默认值为 FALSE。  
  
`[ \@conflict_policy = ] 'conflict_policy'` 指定使用排队更新订阅服务器选项时后, 接冲突解决策略。 *conflict_policy*是**nvarchar(100)** 默认值为 NULL，可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**pub wins**|发布服务器在冲突中入选。|  
|**sub reinit**|重新初始化订阅。|  
|**sub wins**|订阅服务器在冲突中入选。|  
|NULL（默认值）|如果为 NULL，且该发布是快照发布，默认策略将变成**sub reinit**。 如果为 NULL 且该发布不是快照发布，默认值将成为**pub wins**。|  
  
 *对 Oracle 发布服务器不支持*。  
  
`[ \@centralized_conflicts = ] 'centralized_conflicts'` 指定是否在发布服务器上存储冲突记录。 *centralized_conflicts*是**nvarchar(5)** ，默认值为 TRUE。 如果 **，则返回 true**，发布服务器上存储冲突记录。 如果**false**，这两个发布服务器上和在导致冲突的订阅服务器上存储冲突记录。 *对 Oracle 发布服务器不支持*。  
  
`[ \@conflict_retention = ] conflict_retention` 指定冲突保持期，以天为单位。 这是为对等事务复制和排队更新订阅保存冲突元数据的一段时间。 *conflict_retention*是**int**，默认值为 14。 *对 Oracle 发布服务器不支持*。  
  
`[ \@queue_type = ] 'queue_type'` 指定使用哪种类型的队列。 *queue_type*是**nvarchar(10)** ，默认值为 NULL，并且可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**sql**|使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储事务。|  
|NULL（默认值）|默认情况下**sql**，该值指定使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]来存储事务。|  
  
> [!NOTE]  
>  不再支持使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 消息队列。 指定的值**msmq**会导致一条警告，并且复制自动将值设置为**sql**。  
  
 *对 Oracle 发布服务器不支持*。  
  
`[ \@add_to_active_directory = ] 'add\to_active_directory'` 此参数已弃用，仅支持向后兼容性的脚本。 不能再向 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中添加发布信息。  
  
`[ \@logreader_job_name = ] 'logreader_agent_name'` 是现有的代理作业的名称。 *logreader_agent_name*是**sysname**，默认值为 NULL。 仅当日志读取器代理将使用现有作业而不是新建作业时，才指定该参数。  
  
`[ \@qreader_job_name = ] 'queue_reader_agent_name'` 是现有的代理作业的名称。 *queue_reader_agent_name*是**sysname**，默认值为 NULL。 仅当队列读取器代理将使用现有作业而不是新建作业时，才指定该参数。  
  
`[ \@publisher = ] 'publisher'` 指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*添加到发布时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
`[ \@allow_initialize_from_backup = ] 'allow_initialize_from_backup'` 指示是否订阅服务器可以从备份而不是初始快照对此发布中初始化的订阅。 *allow_initialize_from_backup*是**nvarchar(5)** ，可以是下列值之一：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**true**|启用从备份进行的初始化。|  
|**false**|禁用从备份进行的初始化。|  
|NULL（默认值）|默认情况下 **，则返回 true**对等复制拓扑中的发布和**false**对于所有其他发布。|  
  
 有关详细信息，请参阅 [初始化事务订阅（不使用快照）](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手动初始化订阅。  
  
> [!WARNING]  
>  为了避免丢失订阅服务器数据，在将 **sp_addpublication** 与 `@allow_initialize_from_backup = N'true'`一起使用时，始终使用 `@immediate_sync = N'true'`。  
  
`[ \@replicate_ddl = ] replicate_ddl` 指示发布是否支持架构复制。 *replicate_ddl*是**int**，默认值为**1**有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器和**0**为非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 **1**指示复制在发布服务器上执行数据定义语言 (DDL) 语句是的并**0**指示不复制 DDL 语句。 *Oracle 发布服务器不支持架构复制。* 有关详细信息，请参阅[对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
 *\@Replicate_ddl* DDL 语句添加列时，会遵循参数。 *\@Replicate_ddl* DDL 语句更改或删除列，出于以下原因时，将忽略参数。  
  
-   删除列后，必须更新 sysarticlecolumns 以防止新的 DML 语句包括已删除的列，这会导致分发代理失败。 *\@Replicate_ddl*参数被忽略，因为复制功能必须始终复制架构更改。  
  
-   更改列时，源数据类型或为 Null 性可能已更改，这导致 DML 语句包含可能与订阅服务器上的表不兼容的值。 这种 DML 语句可能导致分发代理失败。 *\@Replicate_ddl*参数被忽略，因为复制功能必须始终复制架构更改。  
  
-   DDL 语句添加新列时, sysarticlecolumns 不包括新列。 DML 语句将不尝试复制新列的数据。 采用该参数，因为复制或不复制 DDL 均可接受。  
  
`[ \@enabled_for_p2p = ] 'enabled_for_p2p'` 启用发布以在对等复制拓扑中使用。 *enabled_for_p2p*是**nvarchar(5)** ，默认值为 FALSE。 **true**指示发布支持对等复制。 设置时*enabled_for_p2p*到**true**，以下限制适用：  
  
-   *allow_anonymous*必须是**false**。  
  
-   *allow_dts*必须是**false**。  
  
-   *allow_initialize_from_backup*必须是**true**。  
  
-   *allow_queued_tran*必须是**false**。  
  
-   *allow_sync_tran*必须是**false**。  
  
-   *conflict_policy*必须是**false**。  
  
-   *independent_agent*必须是**true**。  
  
-   *repl_freq*必须是**连续**。  
  
-   *replicate_ddl*必须是**1**。  
  
 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
`[ \@publish_local_changes_only = ] 'publish_local_changes_only'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ \@enabled_for_het_sub = ] 'enabled_for_het_sub'` 启用发布以支持非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。 *enabled_for_het_sub*是**nvarchar(5)** ，默认值为 FALSE。 值为 **，则返回 true**意味着该发布支持非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。 当*enabled_for_het_sub*是**true**，以下限制适用：  
  
-   *allow_initialize_from_backup*必须是**false**。  
  
-   *allow_push*必须是**true**。  
  
-   *allow_queued_tran*必须是**false**。  
  
-   *allow_subscription_copy*必须是**false**。  
  
-   *allow_sync_tran*必须是**false**。  
  
-   *autogen_sync_procs*必须是**false**。  
  
-   *conflict_policy*必须为 NULL。  
  
-   *enabled_for_internet*必须是**false**。  
  
-   *enabled_for_p2p*必须是**false**。  
  
-   *ftp_address*必须为 NULL。  
  
-   *ftp_subdirectory*必须为 NULL。  
  
-   *ftp_password*必须为 NULL。  
  
-   *pre_snapshot_script*必须为 NULL。  
  
-   *post_snapshot_script*必须为 NULL。  
  
-   *replicate_ddl*必须为 0。  
  
-   *qreader_job_name*必须为 NULL。  
  
-   *queue_type*必须为 NULL。  
  
-   *sync_method*不能**本机**或**并发**。  
  
 有关详细信息，请参阅 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
`[ \@p2p_conflictdetection = ] 'p2p_conflictdetection'` 启用的分发代理以检测冲突，如果为对等复制启用发布。 *p2p_conflictdetection*是**nvarchar(5)** ，默认值为 TRUE。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。  
  
`[ \@p2p_originator_id = ] p2p_originator_id` 指定对等拓扑中节点的 ID。 *p2p_originator_id*是**int**，默认值为 NULL。 此 ID 用于进行冲突检测，如果*p2p_conflictdetection*设置为 TRUE。 指定一个从未在拓扑中用过的正的非零 ID。 已使用的 Id 的列表，执行[sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md)。  
  
`[ \@p2p_continue_onconflict = ] 'p2p_continue_onconflict'` 确定是否继续处理更改，检测到冲突后分发代理。 *p2p_continue_onconflict*是**nvarchar(5)** ，默认值为 FALSE。  
  
> [!CAUTION]  
>  建议您使用默认值 FALSE。 如果此选项设置为 TRUE，则分发代理会尝试应用来自具有最高发起方 ID 的节点的冲突行来收敛拓扑中的数据。 此方法不保证将会收敛。 您应确保检测到冲突之后拓扑保持一致。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)中的“处理冲突”。  
  
  
`[ \@allow_partition_switch = ] 'allow_partition_switch'` 指定是否更改表...可以对已发布数据库执行 SWITCH 语句。 *allow_partition_switch*是**nvarchar(5)** ，默认值为 FALSE。 有关详细信息，请参阅[复制已分区表和索引](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。  
  
`[ \@replicate_partition_switch = ] 'replicate_partition_switch'` 指定是否更改表...对已发布数据库执行的 SWITCH 语句应复制到订阅服务器。 *replicate_partition_switch*是**nvarchar(5)** ，默认值为 FALSE。 此选项才有效才*allow_partition_switch*设置为 TRUE。  

## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addpublication**快照复制和事务复制中使用。  
  
 如果存在多个发布的发布相同的数据库对象，只能具有发布*replicate_ddl*的值**1**将复制 ALTER TABLE、 ALTER VIEW、 ALTER PROCEDURE、 ALTER FUNCTION 和ALTER TRIGGER DDL 语句。 但是，发布已删除列的所有发布都将复制 ALTER TABLE DROP COLUMN DDL 语句。  
  
 启用 DDL 复制 (*replicate_ddl* = **1**) 对于发布，若要进行非复制 DDL 更改为该发布， [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)必须首先执行设置*replicate_ddl*到**0**。 在发出非复制 DDL 语句后， [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)可以再次运行以再次打开 DDL 复制。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addpublication**。 Windows 身份验证登录名必须在数据库中具有代表其 Windows 用户帐户的用户帐户。 代表 Windows 组的用户帐户是不足够的。  
  
## <a name="see-also"></a>请参阅  
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_addpublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_replicationdboption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
