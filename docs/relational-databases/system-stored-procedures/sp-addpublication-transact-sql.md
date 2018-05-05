---
title: sp_addpublication (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
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
- sp_addpublication_TSQL
- sp_addpublication
helpviewer_keywords:
- sp_addpublication
ms.assetid: c7167ed1-2b7e-4824-b82b-65f4667c4407
caps.latest.revision: 69
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 59fcdcebd8c8397de2669491d4ea18cb38cfc853
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spaddpublication-transact-sql"></a>sp_addpublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建快照或事务发布。 在发布服务器的发布数据库上执行此存储的过程。  
  
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
 [ **@publication=**] **'***publication***'**  
 要创建的发布的名称。 *发布*是**sysname**，无默认值。 该名称在数据库中必须唯一。  
  
 [  **@taskid=**] *taskid*  
 为了向后兼容; 仅支持使用[sp_addpublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。  
  
 [  **@restricted=**] *****受限*****  
 为了向后兼容; 仅支持使用*default_access*。  
  
 [  **@sync_method=**] *' sync_method * * ***  
 同步模式。 *sync_method*是**nvarchar(13)**，和可以是以下值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**native**|生成所有表的本机模式大容量复制程序输出。 *对 Oracle 发布服务器不支持*。|  
|**character**|生成所有表的字符模式大容量复制程序输出。 *有关 Oracle 发布服务器，* **字符***仅对快照复制有效*。|  
|**并发**|生成所有表的本机模式大容量复制程序输出，但在快照过程中并不锁定表。 只有事务发布支持该值。 *对 Oracle 发布服务器不支持*。|  
|**concurrent_c**|生成所有表的字符模式大容量复制程序输出，但在快照过程中并不锁定表。 只有事务发布支持该值。|  
|**数据库快照**|从数据库快照生成所有表的本机模式大容量复制程序输出。 数据库快照不可用的每个版本[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。|  
|**数据库快照字符**|从数据库快照生成所有表的字符模式大容量复制程序输出。 数据库快照不可用的每个版本[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。|  
|NULL（默认值）|默认为**本机**为[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 有关非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器，默认为**字符**时的值*repl_freq*是**快照**并对其**concurrent_c**对于所有其他情况。|  
  
 [  **@repl_freq=**] *****repl_freq*****  
 是一种复制频率*repl_freq*是**nvarchar(10)**，和可以是以下值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**连续**（默认值）|发布服务器提供所有基于日志的事务的输出。 有关非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器，这种方式要求*sync_method*设置为**concurrent_c**。|  
|**快照**|发布服务器仅生成计划的同步事件。 有关非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器，这种方式要求*sync_method*设置为**字符**。|  
  
 [  **@description=**] *****说明*****  
 发布的可选说明。 *说明*是**nvarchar （255)**，默认值为 NULL。  
  
 [  **@status=**] *****状态*****  
 指定发布数据是否可用。 *状态*是**nvarchar （8)**，和可以是以下值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**活动**|发布数据可立即用于订阅服务器。|  
|**非活动**（默认值）|首次创建发布时，发布数据不能由订阅服务器使用（订阅服务器可以订阅，但这些订阅不被处理）。|  
  
 *对 Oracle 发布服务器不支持*。  
  
 [  **@independent_agent=**] *****independent_agent*****  
 指定是否有用于该发布的独立分发代理。 *independent_agent*是**nvarchar(5)**，默认值为 FALSE。 如果**true**，为此发布的独立分发代理。 如果**false**，发布使用共享的分发代理，并每个发布服务器订阅服务器数据库/数据库对具有共享代理。  
  
 [  **@immediate_sync=**] *****immediate_synchronization*****  
 指定每次运行快照代理时是否为发布创建同步文件。 *immediate_synchronization*是**nvarchar(5)**，默认值为 FALSE。 如果**true**，创建或重新创建运行快照代理每次同步文件。 如果快照代理在订阅创建前完成，则订阅服务器可以立即获得同步文件。 新订阅将获取最近一次执行快照代理所生成的最新同步文件。 *independent_agent*必须**true**为*immediate_synchronization*要**true**。 如果**false**，仅当有新订阅时，才会创建同步文件。 必须调用[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)为每个订阅时以增量方式将新项目添加到现有发布。 订阅后订阅服务器无法接收同步文件，直到启动并完成快照代理为止。  
  
 [  **@enabled_for_internet=**] *****enabled_for_internet*****  
 指定是否为 Internet 启用此发布，并确定是否可以使用文件传输协议 (FTP) 将快照文件传输到订阅服务器。 *enabled_for_internet*是**nvarchar(5)**，默认值为 FALSE。 如果**true**，为发布同步文件将放置到 C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp 目录。 用户必须创建 Ftp 目录。  
  
 [  **@allow_push=**] *****allow_push*****  
 指定是否可为给定发布创建推入订阅。 *allow_push*是**nvarchar(5)**，这样默认值为 TRUE，对该发布的推送订阅。  
  
 [  **@allow_pull=**] *****allow_pull*****  
 指定是否可为给定发布创建拉出订阅。 *allow_pull*是**nvarchar(5)**，默认值为 FALSE。 如果**false**，对该发布不允许请求订阅。  
  
 [  **@allow_anonymous=**] *****allow_anonymous*****  
 指定是否可为给定发布创建匿名订阅。 *allow_anonymous*是**nvarchar(5)**，默认值为 FALSE。 如果**true**， *immediate_synchronization*还必须设置为**true**。 如果**false**，对该发布不允许匿名订阅。  
  
 [  **@allow_sync_tran=**] *****allow_sync_tran*****  
 指定是否允许对发布使用立即更新订阅。 *allow_sync_tran*是**nvarchar(5)**，默认值为 FALSE。 **true**是*Oracle 发布服务器不支持*。  
  
 [  **@autogen_sync_procs=**] *****autogen_sync_procs*****  
 指定是否在发布服务器中为更新订阅生成同步存储过程。 *autogen_sync_procs*是**nvarchar(5)**，和可以是以下值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**true**|在启用更新订阅时自动设置。|  
|**false**|在未启动更新订阅或没有为 Oracle 发布服务器启动更新订阅时自动设置。|  
|NULL（默认值）|默认为**true**启用更新订阅，到**false**更新订阅未启用。|  
  
> [!NOTE]  
>  用户提供的值*autogen_sync_procs*将根据为指定的值中被重写*allow_queued_tran*和*allow_sync_tran*。  
  
 [  **@retention=**]*保留*  
 订阅活动的保持期（小时）。 *保留*是**int**，默认值为 336 个小时。 如果订阅在保持期内不活动，则过期后将其删除。 该值可以大于发布服务器使用的分发数据库的最大保持期。 如果**0**，对发布的已知的订阅将永不过期，并且通过过期订阅清除代理。  
  
 [  **@allow_queued_tran=** ] *****allow_queued_updating*****  
 在订阅服务器中启用或禁用更改的队列，直到可在发布服务器上应用这些更改为止。 *allow_queued_updating*是**nvarchar(5)** 默认值为 FALSE。 如果**false**，订阅服务器上的更改不会排队。 **true**是*Oracle 发布服务器不支持*。  
  
 [  **@snapshot_in_defaultfolder=** ] *****snapshot_in_default_folder*****  
 指定是否将快照文件存储在默认文件夹中。 *snapshot_in_default_folder*是**nvarchar(5)** 默认值为 TRUE。 如果**true**，可以在默认文件夹中找到快照文件。 如果**false**，快照文件存储在指定的备用位置*alternate_snapshot_folder*。 备用位置可以在另一台服务器、一个网络驱动器或可移动介质（如光盘或可移动磁盘）上。 也可以将快照文件保存到 FTP 站点以供订阅服务器以后检索。 请注意此参数可以是 true，在仍有一个位置**@alt_snapshot_folder**参数。 该组合指定将快照文件同时存储在默认位置和备用位置。  
  
 [  **@alt_snapshot_folder=** ] *****alternate_snapshot_folder*****  
 指定快照的备用文件夹的位置。 *alternate_snapshot_folder*是**nvarchar （255)** 默认值为 NULL。  
  
 [  **@pre_snapshot_script=** ] *****pre_snapshot_script*****  
 指定指向的指针 **.sql**文件位置。 *pre_snapshot_script*是**nvarchar （255)，**默认值为 NULL。 分发代理将运行之前运行的任何复制的对象脚本时应用在订阅服务器上快照的快照前脚本。 该脚本在分发代理连接到订阅数据库时使用的安全上下文中执行。  
  
 [  **@post_snapshot_script=** ] *****post_snapshot_script*****  
 指定指向的指针 **.sql**文件位置。 *post_snapshot_script*是**nvarchar （255)**，默认值为 NULL。 分发代理将在初始同步过程中已应用所有其他复制的对象脚本和数据之后才运行快照后脚本。 该脚本在分发代理连接到订阅数据库时使用的安全上下文中执行。  
  
 [  **@compress_snapshot=** ] *****compress_snapshot*****  
 指定写入到快照**@alt_snapshot_folder**位置是压缩成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 *compress_snapshot*是**nvarchar(5)**，默认值为 FALSE。 **false**指定，将不会压缩快照;**true**指定将压缩的快照。 不能压缩大于 2 GB 的快照文件。 压缩快照文件在分发代理运行的位置解压缩；请求订阅通常与压缩快照一起使用，以便在订阅服务器上解压缩文件。 不能压缩默认文件夹中的快照。  
  
 [  **@ftp_address =** ] *****ftp_address*****  
 分发服务器的 FTP 服务网络地址。 *ftp_address*是**sysname**，默认值为 NULL。 指定供订阅服务器的分发代理或合并代理拾取的发布快照文件的位置。 由于此属性存储为每个发布中，每个发布都可以具有不同*ftp_address*。 该发布必须支持使用 FTP 来传播快照。  
  
 [  **@ftp_port=** ] *ftp_port*  
 分发服务器 FTP 服务的端口号。 *ftp_port*是**int**，默认值为 21。 指定分发代理或合并代理的订阅服务器以拾取发布快照文件的位置。 由于此属性存储为每个发布中，每个发布都有其自己*ftp_port*。  
  
 [  **@ftp_subdirectory =** ] *****ftp_subdirectory*****  
 指定供订阅服务器的分发代理或合并代理拾取的快照文件的位置（如果发布支持使用 FTP 传播快照）。 *ftp_subdirectory*是**nvarchar （255)**，默认值为 NULL。 由于此属性存储为每个发布中，每个发布都有其自己*ftp_subdirctory*或者选择子目录，并用 NULL 值。  
  
 [  **@ftp_login =** ] *****ftp_login*****  
 用于连接到 FTP 服务用户名。 *ftp_login*是**sysname**，默认值为 ANONYMOUS。  
  
 [  **@ftp_password =** ] *****ftp_password*****  
 用于连接到 FTP 服务的用户密码。 *ftp_password*是**sysname**，默认值为 NULL。  
  
 [  **@allow_dts =** ] *****allow_dts*****  
 指定发布允许数据转换。 创建订阅时可以指定 DTS 包。 *allow_transformable_subscriptions*是**nvarchar(5)** 默认值为 FALSE，它不允许 DTS 转换。 当*allow_dts*为 true， *sync_method*必须设置为**字符**或**concurrent_c**。  
  
 **true**是*Oracle 发布服务器不支持*。  
  
 [  **@allow_subscription_copy =** ] *****allow_subscription_copy*****  
 启用或禁用对订阅此发布的订阅数据库的复制功能。 *allow_subscription_copy*是**nvarchar(5)**，默认值为 FALSE。  
  
 [  **@conflict_policy =** ] *****conflict_policy*****  
 指定使用排队更新订阅服务器选项时遵循的冲突解决策略。 *conflict_policy*是**nvarchar(100)** 默认值为 NULL，并且可以为以下值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**pub wins**|发布服务器在冲突中入选。|  
|**sub 重新初始化**|重新初始化订阅。|  
|**sub wins**|订阅服务器在冲突中入选。|  
|NULL（默认值）|如果 NULL，并且发布是快照发布，默认策略将成为**sub 重新初始化**。 如果 NULL 和发布不是快照发布，默认值将成为**pub wins**。|  
  
 *对 Oracle 发布服务器不支持*。  
  
 [  **@centralized_conflicts =** ] *****centralized_conflicts*****  
 指定是否在发布服务器上存储冲突记录。 *centralized_conflicts*是**nvarchar(5)**，默认值为 TRUE。 如果**true**，发布服务器上存储冲突记录。 如果**false**，同时在发布服务器和订阅服务器引起冲突存储冲突记录。 *对 Oracle 发布服务器不支持*。  
  
 [  **@conflict_retention =** ] *conflict_retention*  
 指定冲突保持期（天）。 这是为对等事务复制和排队更新订阅保存冲突元数据的一段时间。 *conflict_retention*是**int**，默认值为 14。 *对 Oracle 发布服务器不支持*。  
  
 [  **@queue_type =** ] *****queue_type*****  
 指定所使用的队列类型。 *queue_type*是**nvarchar(10)**，默认值为 NULL，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**sql**|使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储事务。|  
|NULL（默认值）|默认为**sql**，该选项指定使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要存储的事务。|  
  
> [!NOTE]  
>  不再支持使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 消息队列。 指定的值**msmq**将导致了警告，并复制将自动将值设置为**sql**。  
  
 *对 Oracle 发布服务器不支持*。  
  
 [  **@add_to_active_directory =** ] *** * * 添加**_**to_active_directory * * ***  
 已不推荐使用该参数，支持该参数只是为了让脚本能够向后兼容。 不能再向 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中添加发布信息。  
  
 [  **@logreader_job_name =** ] *****logreader_agent_name*****  
 现有代理作业的名称。 *logreader_agent_name*是**sysname**，默认值为 NULL。 仅当日志读取器代理将使用现有作业而不是新建作业时，才指定该参数。  
  
 [  **@qreader_job_name =** ] *****queue_reader_agent_name*****  
 现有代理作业的名称。 *queue_reader_agent_name*是**sysname**，默认值为 NULL。 仅当队列读取器代理将使用现有作业而不是新建作业时，才指定该参数。  
  
 [  **@publisher =** ] *****发布服务器*****  
 指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*添加至发布时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
 [  **@allow_initialize_from_backup =** ] *****allow_initialize_from_backup*****  
 指示订阅服务器是否能够从备份而不是从初始快照来初始化对此发布的订阅。 *allow_initialize_from_backup*是**nvarchar(5)**，并且可以为这些值之一：  
  
|“值”|Description|  
|-----------|-----------------|  
|**true**|启用从备份进行的初始化。|  
|**false**|禁用从备份进行的初始化。|  
|NULL（默认值）|默认为**true**为对等复制拓扑中发布和**false**对于所有其他发布。|  
  
 有关详细信息，请参阅 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手动初始化订阅。  
  
> [!WARNING]  
>  为了避免丢失订阅服务器数据，在将 **sp_addpublication** 与 `@allow_initialize_from_backup = N'true'`一起使用时，始终使用 `@immediate_sync = N'true'`。  
  
 [  **@replicate_ddl =** ] *replicate_ddl*  
 指示是否架构复制支持发布。 *replicate_ddl*是**int**，默认值为**1**为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器和**0**为非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 **1**指明可将复制发布服务器上执行数据定义语言 (DDL) 语句，和**0**指示 DDL 语句不会复制。 *Oracle 发布服务器不支持架构复制。* 有关详细信息，请参阅[对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
 *@replicate_ddl*当 DDL 语句将添加一个列时，接受参数。 *@replicate_ddl* DDL 语句更改或删除下列原因造成的列时，将忽略参数。  
  
-   当除去的列时，则必须更新 sysarticlecolumns 以防止新的 DML 语句，从包括已删除的列，从而导致分发代理失败。 *@replicate_ddl*参数将被忽略，因为复制必须始终复制架构更改。  
  
-   更改列时，源数据类型或为 Null 性可能已更改，这导致 DML 语句包含可能与订阅服务器上的表不兼容的值。 这种 DML 语句可能导致分发代理失败。 *@replicate_ddl*参数将被忽略，因为复制必须始终复制架构更改。  
  
-   当 DDL 语句将添加一个新列时，sysarticlecolumns 不包括新的列。 DML 语句将不尝试复制新列的数据。 采用该参数，因为复制或不复制 DDL 均可接受。  
  
 [  **@enabled_for_p2p =** ] *****enabled_for_p2p*****  
 允许将发布用于对等复制拓扑中。 *enabled_for_p2p*是**nvarchar(5)**，默认值为 FALSE。 **true**指示发布支持对等复制。 设置时*enabled_for_p2p*到**true**，以下限制适用：  
  
-   *allow_anonymous*必须**false**。  
  
-   *allow_dts*必须**false**。  
  
-   *allow_initialize_from_backup*必须**true**。  
  
-   *allow_queued_tran*必须**false**。  
  
-   *allow_sync_tran*必须**false**。  
  
-   *conflict_policy*必须**false**。  
  
-   *independent_agent*必须**true**。  
  
-   *repl_freq*必须**连续**。  
  
-   *replicate_ddl*必须**1**。  
  
 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 [  **@publish_local_changes_only =** ] *****publish_local_changes_only*****  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@enabled_for_het_sub=** ] *****enabled_for_het_sub*****  
 启用发布以支持非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。 *enabled_for_het_sub*是**nvarchar(5)** 默认值为 FALSE。 值为**true**意味着发布支持非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。 当*enabled_for_het_sub*是**true**，以下限制适用：  
  
-   *allow_initialize_from_backup*必须**false**。  
  
-   *allow_push*必须**true**。  
  
-   *allow_queued_tran*必须**false**。  
  
-   *allow_subscription_copy*必须**false**。  
  
-   *allow_sync_tran*必须**false**。  
  
-   *autogen_sync_procs*必须**false**。  
  
-   *conflict_policy*必须为 NULL。  
  
-   *enabled_for_internet*必须**false**。  
  
-   *enabled_for_p2p*必须**false**。  
  
-   *ftp_address*必须为 NULL。  
  
-   *ftp_subdirectory*必须为 NULL。  
  
-   *ftp_password*必须为 NULL。  
  
-   *pre_snapshot_script*必须为 NULL。  
  
-   *post_snapshot_script*必须为 NULL。  
  
-   *replicate_ddl*必须为 0。  
  
-   *qreader_job_name*必须为 NULL。  
  
-   *queue_type*必须为 NULL。  
  
-   *sync_method*不能为**本机**或**并发**。  
  
 有关详细信息，请参阅 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
 [  **@p2p_conflictdetection=** ] *****p2p_conflictdetection*****  
 如果为对等复制启用发布，则启用分发代理以检测冲突。 *p2p_conflictdetection*是**nvarchar(5)** 默认值为 TRUE。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。  
  
 [  **@p2p_originator_id=** ] *p2p_originator_id*  
 指定对等拓扑中某个节点的 ID。 *p2p_originator_id*是**int**，默认值为 NULL。 此 ID 用于冲突检测，如果*p2p_conflictdetection*设置为 TRUE。 指定一个从未在拓扑中用过的正的非零 ID。 有关已使用的 Id 的列表，执行[sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md)。  
  
 [  **@p2p_continue_onconflict=** ] *****p2p_continue_onconflict*****  
 确定检测到冲突后分发代理是否继续处理更改。 *p2p_continue_onconflict*是**nvarchar(5)** 默认值为 FALSE。  
  
> [!CAUTION]  
>  建议您使用默认值 FALSE。 如果此选项设置为 TRUE，则分发代理会尝试应用来自具有最高发起方 ID 的节点的冲突行来收敛拓扑中的数据。 此方法不保证将会收敛。 您应确保检测到冲突之后拓扑保持一致。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)中的“处理冲突”。  
  
 [  **@allow_partition_switch=** ] *****allow_partition_switch*****  
 指定是否对已发布的数据库执行 ALTER TABLE…SWITCH 语句。 *allow_partition_switch*是**nvarchar(5)** 默认值为 FALSE。 有关详细信息，请参阅[复制已分区表和索引](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。  
  
 [  **@replicate_partition_switch=** ] *****replicate_partition_switch*****  
 指定是否应将对已发布的数据库执行的 ALTER TABLE…SWITCH 语句复制到订阅服务器。 *replicate_partition_switch*是**nvarchar(5)** 默认值为 FALSE。 此选项才有效才*allow_partition_switch*设置为 TRUE。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_addpublication**快照复制和事务复制中使用。  
  
 如果存在多个发布，发布同一个数据库对象，仅发布*replicate_ddl*值**1**将复制 ALTER TABLE、 ALTER VIEW、 ALTER PROCEDURE、 ALTER FUNCTION 和ALTER TRIGGER DDL 语句。 但是，发布已删除列的所有发布都将复制 ALTER TABLE DROP COLUMN DDL 语句。  
  
 已启用 DDL 复制的 (*replicate_ddl* = **1**) 对于发布，以便非复制 DDL 更改为发布， [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)必须首先执行设置*replicate_ddl*到**0**。 已颁发的非复制 DDL 语句后， [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)可以再次运行，以启用 DDL 复制。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-transa_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addpublication**。 Windows 身份验证登录名必须在数据库中具有代表其 Windows 用户帐户的用户帐户。 代表 Windows 组的用户帐户是不足够的。  
  
## <a name="see-also"></a>另请参阅  
 [sp_addlogreader_agent &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_addpublication_snapshot &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [sp_replicationdboption &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
