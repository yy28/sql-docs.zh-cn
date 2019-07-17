---
title: sp_addmergepublication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepublication
- sp_addmergepublication_TSQL
helpviewer_keywords:
- sp_addmergepublication
ms.assetid: 28a629a1-7374-4614-9b04-279d290a942a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c6571ce334c1534dd6fe869f37f007da793469d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118052"
---
# <a name="spaddmergepublication-transact-sql"></a>sp_addmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建新合并发布。 此存储过程针对发布服务器上要发布的数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addmergepublication [ @publication = ] 'publication'   
    [ , [ @description = ] 'description'   
    [ , [ @retention = ] retention ]   
    [ , [ @sync_mode = ] 'sync_mode' ]   
    [ , [ @allow_push = ] 'allow_push' ]   
    [ , [ @allow_pull = ] 'allow_pull' ]   
    [ , [ @allow_anonymous = ] 'allow_anonymous' ]   
    [ , [ @enabled_for_internet = ] 'enabled_for_internet' ]   
    [ , [ @centralized_conflicts = ] 'centralized_conflicts' ]   
    [ , [ @dynamic_filters = ] 'dynamic_filters' ]   
    [ , [ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder' ]   
    [ , [ @alt_snapshot_folder = ] 'alternate_snapshot_folder' ]   
    [ , [ @pre_snapshot_script = ] 'pre_snapshot_script' ]   
    [ , [ @post_snapshot_script = ] 'post_snapshot_script' ]   
    [ , [ @compress_snapshot = ] 'compress_snapshot' ]   
    [ , [ @ftp_address = ] 'ftp_address' ]   
    [ , [ @ftp_port = ] ftp_port ]   
    [ , [ @ftp_subdirectory = ] 'ftp_subdirectory' ]   
    [ , [ @ftp_login = ] 'ftp_login' ]   
    [ , [ @ftp_password = ] 'ftp_password' ]   
    [ , [ @conflict_retention = ] conflict_retention ]   
    [ , [ @keep_partition_changes = ] 'keep_partition_changes' ]   
    [ , [ @allow_subscription_copy = ] 'allow_subscription_copy' ]   
    [ , [ @allow_synctoalternate = ] 'allow_synctoalternate' ]   
    [ , [ @validate_subscriber_info = ] 'validate_subscriber_info' ]   
    [ , [ @add_to_active_directory = ] 'add_to_active_directory' ]   
    [ , [ @max_concurrent_merge = ] maximum_concurrent_merge ]   
    [ , [ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots ]  
    [ , [ @use_partition_groups = ] 'use_partition_groups' ]  
    [ , [ @publication_compatibility_level = ] 'backward_comp_level' ]  
    [ , [ @replicate_ddl = ] replicate_ddl ]  
    [ , [ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot' ]   
    [ , [ @allow_web_synchronization = ] 'allow_web_synchronization' ]   
    [ , [ @web_synchronization_url = ] 'web_synchronization_url' ]  
    [ , [ @allow_partition_realignment = ] 'allow_partition_realignment' ]  
    [ , [ @retention_period_unit = ] 'retention_period_unit' ]  
    [ , [ @generation_leveling_threshold = ] generation_leveling_threshold ]  
    [ , [ @automatic_reinitialization_policy = ] automatic_reinitialization_policy ]  
    [ , [ @conflict_logging = ] 'conflict_logging' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是要创建的合并发布的名称。 *发布*是**sysname**，无默认值，并且不能为关键字所有。 发布的名称在数据库内必须唯一。  
  
`[ @description = ] 'description'` 是发布说明。 *描述*是**nvarchar(255)** ，默认值为 NULL。  
  
`[ @retention = ] retention` 是的保持期，以保留期的单位，要保存更改的给定*发布*。 *保留期*是**int**，默认值为 14 个单位。 由定义保持期单位*retention_period_unit*。 如果在保持期内没有同步该订阅，并在分发服务器上使用清除操作删除了该订阅本应接收到的挂起更改，则该订阅将过期，必须重新初始化。 所允许的最大保持期为当前日期到 9999 年 12 月 31 日之间的天数。  
  
> [!NOTE]  
>  对于合并发布的保持期具有 24 小时的宽限期，以适应不同的时区中的订阅服务器。 例如，如果将保持期设置为 1 天，则实际的保持期为 48 小时。  
  
`[ @sync_mode = ] 'sync_mode'` 是发布的订阅服务器的初始同步模式。 *sync_mode*是**nvarchar(10)** ，可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**本机**（默认值）|生成所有表的本机模式大容量复制程序输出。|  
|**character**|生成所有表的字符模式大容量复制程序输出。 支持所需[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssEW](../../includes/ssew-md.md)]和非-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。|  
  
`[ @allow_push = ] 'allow_push'` 指定是否可以为给定发布创建推送订阅。 *allow_push*是**nvarchar(5)** ，其默认值为 TRUE，表示允许推送订阅发布。  
  
`[ @allow_pull = ] 'allow_pull'` 指定是否可以为给定发布创建请求订阅。 *allow_pull*是**nvarchar(5)** ，其默认值为 TRUE，表示允许为请求订阅此发布。 必须指定为 true，则支持[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器。  
  
`[ @allow_anonymous = ] 'allow_anonymous'` 指定是否可以为给定发布创建匿名订阅。 *allow_anonymous*是**nvarchar(5)** ，其默认值为 TRUE，表示允许匿名订阅发布。 若要支持[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器，必须指定**true**。  
  
`[ @enabled_for_internet = ] 'enabled_for_internet'` 指定是否为 Internet 启用发布，并确定是否可以使用文件传输协议 (FTP) 将快照文件传输到订阅服务器。 *enabled_for_internet*是**nvarchar(5)** ，默认值为 FALSE。 如果 **，则返回 true**，发布的同步文件将放入 C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp 目录。 用户必须创建 Ftp 目录。 如果**false**，该发布无法进行 Internet 访问权限。  
  
`[ @centralized_conflicts = ] 'centralized_conflicts'` 此参数已弃用，仅支持向后兼容性的脚本。 使用*conflict_logging*指定存储冲突记录的位置的位置。  
  
`[ @dynamic_filters = ] 'dynamic_filters'` 允许合并发布使用参数化的行筛选器。 *dynamic_filters*是**nvarchar(5)** ，默认值为 FALSE。  
  
> [!NOTE]  
>  如果正在使用参数化行筛选器，请勿指定此参数，而应由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自行确定。 如果指定的值 **，则返回 true**有关*dynamic_filters*，必须定义项目的参数化的行筛选器。 有关详细信息，请参阅 [定义和修改合并项目的参数化行筛选器](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
`[ @snapshot_in_defaultfolder = ] 'snapshot_in_default_folder'` 指定快照文件是否存储在默认文件夹中。 *snapshot_in_default_folder*是**nvarchar(5)** ，默认值为 TRUE。 如果 **，则返回 true**，可以在默认文件夹中找到快照文件。 如果**false**，快照文件将存储在指定的备用位置*alternate_snapshot_folder*。 备用位置可以是另一台服务器、 网络驱动器或可移动媒体 （如 CD-ROM 或可移动磁盘）。 也可以将快照文件保存到文件传输协议 (FTP) 站点以供订阅方以后检索。 请注意，此参数可以为 true，仍然可以通过指定的位置*alt_snapshot_folder*。 该组合指定将快照文件同时存储在默认位置和备用位置。  
  
`[ @alt_snapshot_folder = ] 'alternate_snapshot_folder'` 指定备用快照文件夹的位置。 *alternate_snapshot_folder*是**nvarchar(255)** ，默认值为 NULL。  
  
`[ @pre_snapshot_script = ] 'pre_snapshot_script'` 指定一个指向 **.sql**文件位置。 *pre_snapshot_script*是**nvarchar(255)** ，默认值为 NULL。 在订阅服务器上应用快照时，合并代理将在运行任何复制的对象脚本之前运行快照前脚本。 该脚本将在合并代理连接到订阅数据库时使用的安全上下文中执行。 快照前脚本不会运行[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器。  
  
`[ @post_snapshot_script = ] 'post_snapshot_script'` 指定一个指向 **.sql**文件位置。 *post_snapshot_script*是**nvarchar(255)** ，默认值为 NULL。 当所有其他复制的对象脚本和数据均已在初始同步过程中应用之后，合并代理将运行快照后脚本。 该脚本将在合并代理连接到订阅数据库时使用的安全上下文中执行。 快照后脚本不会运行[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器。  
  
`[ @compress_snapshot = ] 'compress_snapshot'` 指定的写入到的快照 **@alt_snapshot_folder** 位置是将压缩成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 *compress_snapshot*是**nvarchar(5)** ，默认值为 FALSE。 **false**指定，将不压缩快照; **，则返回 true**指定快照将进行压缩。 无法压缩大于 2GB 的快照文件。 压缩的快照文件被解压缩到合并代理所在的位置；一般对压缩的快照使用请求订阅，以便在订阅服务器上解压缩文件。 不能压缩默认文件夹中的快照。 若要支持[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器，必须指定**false**。  
  
`[ @ftp_address = ] 'ftp_address'` 是分发服务器的 FTP 服务的网络地址。 *ftp_address*是**sysname**，默认值为 NULL。 指定供合并代理拾取的订阅服务器的发布快照文件的位置。 由于为每个发布都存储此属性，因此每个发布可以具有不同*ftp_address*。 该发布必须支持使用 FTP 来传播快照。  
  
`[ @ftp_port = ] ftp_port` 是分发服务器的 FTP 服务的端口号。 *ftp_port*是**int**，默认值为 21。 指定发布快照文件所在的位置以供订阅服务器的合并代理挑选。 由于此属性存储每个发布，每个发布可以具有其自己*ftp_port*。  
  
`[ @ftp_subdirectory = ] 'ftp_subdirectory'` 指定快照文件将可用于选取如果发布支持使用 FTP 传播快照的订阅服务器的合并代理。 *ftp_subdirectory*是**nvarchar(255)** ，默认值为 NULL。 由于此属性存储每个发布，每个发布可以具有其自己*ftp_subdirctory*或选择允许使用 NULL 值指示没有子目录。  
  
 在使用参数化筛选器为发布预先生成快照时，需要将每个订阅服务器分区的数据快照置于自己的文件夹中。 使用 FTP 的预先生成快照的目录结构必须为以下结构：  
  
 *alternate_snapshot_folder*\ftp\\*publisher_publicationDB_publication*\\*partitionID*。  
  
> [!NOTE]  
>  上面以斜体显示的值取决于发布和订阅服务器分区的具体情况。  
  
`[ @ftp_login = ] 'ftp_login'` 用于连接到 FTP 服务用户名。 *ftp_login*是**sysname**，默认值为 'anonymous'。  
  
`[ @ftp_password = ] 'ftp_password'` 用于连接到 FTP 服务的用户密码。 *ftp_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  不要使用空密码。 请使用强密码。  
  
`[ @conflict_retention = ] conflict_retention` 指定的保持期，以天为单位，为其保留冲突。 *conflict_retention*是**int**，行从冲突表清除默认值为 14 天前此冲突。  
  
`[ @keep_partition_changes = ] 'keep_partition_changes'` 指定是否启用分区更改优化时不能使用预计算的分区。 *keep_partition_changes*是**nvarchar(5)** ，默认值为 TRUE。 **false**对更改进行分区的方式不进行优化，并且发送到所有订阅服务器分区时不使用预计算的分区，将一个分区中的数据更改时验证。 **true**对更改进行分区的方式进行优化，并且订阅者，已更改的分区内具有行受影响。 如果使用预计算的分区，设置*use_partition_groups*到**true**并设置*keep_partition_changes*到**false**。 有关详细信息，请参阅[使用预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
> [!NOTE]  
>  如果指定的值 **，则返回 true**有关*keep_partition_changes*，将值指定为**1**快照代理参数 **-MaxNetworkOptimization**. 有关此参数的详细信息，请参阅[复制快照代理](../../relational-databases/replication/agents/replication-snapshot-agent.md)。 有关如何指定代理参数的信息，请参阅[复制代理管理](../../relational-databases/replication/agents/replication-agent-administration.md)。  
  
 与[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器， *keep_partition_changes*必须设置为 true 以确保正确传播删除操作。 设置为 false 时，订阅服务器可能有比预期更多的行。  
  
`[ @allow_subscription_copy = ] 'allow_subscription_copy'` 启用或禁用复制订阅此发布的订阅数据库的能力。 *allow_subscription_copy*是**nvarchar(5)** ，默认值为 FALSE。 要复制的订阅数据库的大小必须小于 2 GB。  
  
`[ @allow_synctoalternate = ] 'allow_synctoalternate'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @validate_subscriber_info = ] 'validate_subscriber_info'` 列出了用于定义订阅服务器分区的已发布数据时使用参数化的行筛选器的函数。 *validate_subscriber_info*是**nvarchar(500)** ，默认值为 NULL。 合并代理利用该信息来验证订阅服务器分区。 例如，如果[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)使用参数化的行筛选器中的参数应`@validate_subscriber_info=N'SUSER_SNAME()'`。  
  
> [!NOTE]  
>  该参数不应由用户指定，而应由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来自动确定筛选准则。  
  
`[ @add_to_active_directory = ] 'add_to_active_directory'` 此参数已弃用，仅支持向后兼容性的脚本。 不能再向 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中添加发布信息。  
  
`[ @max_concurrent_merge = ] maximum_concurrent_merge` 最大并发合并进程数。 *maximum_concurrent_merge*是**int**默认值为 0。 值为**0**此属性则表示没有在任何给定时间运行的并发合并进程数没有限制。 该属性对可以同时在合并发布上运行的并发合并进程数设置限制。 如果同时调度的合并进程数大于所允许的数目，则将多出的作业放置在队列中等待，直到当前正在运行的合并进程结束。  
  
`[ @max_concurrent_dynamic_snapshots = ] max_concurrent_dynamic_snapshots` 可以同时运行，以便生成订阅服务器分区的筛选的数据快照的快照代理会话的最大数目。 *maximum_concurrent_dynamic_snapshots*是**int**默认值为 0。 如果**0**，对快照会话数目没有限制。 如果同时调度的快照进程数比允许运行的数多，则多出的作业将放置在队列中等待，直到当前正在运行的快照进程完成。  
  
`[ @use_partition_groups = ] 'use_partition_groups'` 指定的预计算应使用分区来优化同步过程。 *use_partition_groups*是**nvarchar(5)** ，可以是下列值之一：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**true**|发布使用预计算分区。|  
|**false**|发布不使用预计算分区。|  
|NULL（默认值）|由系统确定分区策略。|  
  
 默认情况下，使用预计算分区。 若要避免使用预计算的分区*use_partition_groups*必须设置为**false**。 如果设置为 NULL，则系统会确定预计算分区是否可用。 如果预计算分区不能使用，则此值将有效地成为**false**而不会生成任何错误。 在这种情况下， *keep_partition_changes*可设置为**true**提供一些优化。 有关详细信息，请参阅[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)并[使用预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
`[ @publication_compatibility_level = ] backward_comp_level` 指示发布的向后兼容性。 *backward_comp_level*是**nvarchar(6)** ，可以是下列值之一：  
  
|ReplTest1|Version|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
`[ @replicate_ddl = ] replicate_ddl` 指示发布是否支持架构复制。 *replicate_ddl*是**int**，默认值为 1。 **1**指示复制在发布服务器上执行数据定义语言 (DDL) 语句是的并**0**指示不复制 DDL 语句。 有关详细信息，请参阅[对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
 *@replicate_ddl* DDL 语句添加列时，会遵循参数。 *@replicate_ddl* DDL 语句更改或删除列，出于以下原因时，将忽略参数。  
  
-   删除列后，必须更新 sysarticlecolumns 以防止新的 DML 语句包括已删除的列，这会导致分发代理失败。 *@replicate_ddl* 参数被忽略，因为复制功能必须始终复制架构更改。  
  
-   更改列时，源数据类型或为 Null 性可能已更改，这导致 DML 语句包含可能与订阅服务器上的表不兼容的值。 这种 DML 语句可能导致分发代理失败。 *@replicate_ddl* 参数被忽略，因为复制功能必须始终复制架构更改。  
  
-   DDL 语句添加新列时, sysarticlecolumns 不包括新列。 DML 语句将不尝试复制新列的数据。 采用该参数，因为复制或不复制 DDL 均可接受。  
  
`[ @allow_subscriber_initiated_snapshot = ] 'allow_subscriber_initiated_snapshot'` 指示此发布的订阅服务器可以启动快照进程来生成其数据分区的筛选的快照。 *allow_subscriber_initiated_snapshot*是**nvarchar(5)** ，默认值为 FALSE。 **true**指示订阅服务器可以启动快照进程。  
  
`[ @allow_web_synchronization = ] 'allow_web_synchronization'` 指定是否为 Web 同步启用发布。 *allow_web_synchronization*是**nvarchar(5)** ，默认值为 FALSE。 **true**指定对此发布的订阅可以通过 HTTPS 进行同步。 有关详细信息，请参阅 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)。 若要支持[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器，必须指定**true**。  
  
`[ @web_synchronization_url = ] 'web_synchronization_url'` 指定用于 Web 同步的 Internet URL 的默认值。 *web_synchronization_url 我*s **nvarchar(500)** ，默认值为 NULL。 如果未显式设置时定义默认的 Internet URL [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)执行。  
  
`[ @allow_partition_realignment = ] 'allow_partition_realignment'` 确定在发布服务器上的行的修改后，即可更改其分区时是否将删除发送到订阅服务器。 *allow_partition_realignment*是**nvarchar(5)** ，默认值为 TRUE。 **true**将删除发送到订阅服务器以通过删除不再属于订阅服务器的分区的数据来反映分区更改的结果。 **false**旧分区中的数据留在订阅服务器，其中对此发布服务器上的数据所做的更改不会复制到此订阅服务器，但在订阅服务器上所做的更改将复制到发布服务器上。 设置*allow_partition_realignment*到**false**用于保留旧分区中的订阅中的数据时的数据必须可用于历史查询。  
  
> [!NOTE]  
>  在由于设置订阅服务器上保留的数据*allow_partition_realignment*到**false**应视为如同它是只读的; 但是，不强制这一点由复制系统。  
  
`[ @retention_period_unit = ] 'retention_period_unit'` 指定的设置的保持期单位*保留*。 *retention_period_unit*是**nvarchar(10)** ，可以是下列值之一。  
  
|ReplTest1|Version|  
|-----------|-------------|  
|**一天**（默认值）|按天指定保持期。|  
|**week**|按周指定保持期。|  
|month |按月指定保持期。|  
|year |按年指定保持期。|  
  
`[ @generation_leveling_threshold = ] generation_leveling_threshold` 指定生成中包含的更改数。 生成是指传递到发布服务器或订阅服务器的更改的集合。 *generation_leveling_threshold*是**int**，其默认值为 1000年。  
  
`[ @automatic_reinitialization_policy = ] automatic_reinitialization_policy` 指定是否从订阅服务器上的值，对发布更改所要求的自动重新初始化之前上载更改**1**为指定 **@force_reinit_subscription** 。 *automatic_reinitialization_policy*为 bit，默认值为 0。 **1**意味着自动重新初始化之前从订阅服务器上载更改。  
  
> [!IMPORTANT]  
>  如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
`[ @conflict_logging = ] 'conflict_logging'` 指定存储冲突记录的位置。 *conflict_logging*是**nvarchar(15)** ，可以是下列值之一：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**publisher**|在发布服务器上存储冲突记录。|  
|**订阅服务器**|在导致冲突的订阅服务器上存储冲突记录。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 订阅服务器不支持此值。|  
|**两者**|在发布服务器和订阅服务器上都存储冲突记录。|  
|NULL（默认值）|复制会自动设置*conflict_logging*到**两者**时值*backward_comp_level*是**90RTM**和到**发布服务器**在所有其他情况下。|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_addmergepublication**合并复制中使用。  
  
 列出发布到 Active Directory 使用的对象 **@add_to_active_directory** 参数，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必须已在 Active Directory 中创建对象。  
  
 如果存在多个发布的发布相同的数据库对象，只能具有发布*replicate_ddl*的值**1**将复制 ALTER TABLE、 ALTER VIEW、 ALTER PROCEDURE、 ALTER FUNCTION 和ALTER TRIGGER DDL 语句。 但是，发布已删除列的所有发布都将复制 ALTER TABLE DROP COLUMN DDL 语句。  
  
 有关[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器的值*alternate_snapshot_folder*时，才使用的值*snapshot_in_default_folder*是**false**。  
  
 启用 DDL 复制 (_replicate_ddl_ **= 1**) 对于发布，为了进行非复制 DDL 更改对该发布[sp_changemergepublication &#40;Transact SQL&#41; ](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)必须首先执行设置*replicate_ddl*到**0**。 在发出非复制 DDL 语句后， **sp_changemergepublication**可以再次运行以再次打开 DDL 复制。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addmergepublication**。  
  
## <a name="see-also"></a>请参阅  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
