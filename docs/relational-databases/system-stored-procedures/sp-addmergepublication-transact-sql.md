---
title: "sp_addmergepublication (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_addmergepublication
- sp_addmergepublication_TSQL
helpviewer_keywords: sp_addmergepublication
ms.assetid: 28a629a1-7374-4614-9b04-279d290a942a
caps.latest.revision: "72"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3f61d6ab3c2154020be3eb1ecf4407f57541918
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
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
 [  **@publication =** ] *发布*  
 是要创建的合并发布的名称。 *发布*是**sysname**，没有默认值，且必须与不是关键字所有。 发布的名称在数据库内必须唯一。  
  
 [  **@description =** ] *说明*  
 是发布说明。 *说明*是**nvarchar （255)**，默认值为 NULL。  
  
 [  **@retention =** ]*保留*  
 是的保持期，保持期单位，用于保存有关更改给定*发布*。 *保留*是**int**，默认值为 14 单位。 保持期单位由定义*retention_period_unit*。 如果在保持期内没有同步该订阅，并在分发服务器上使用清除操作删除了该订阅本应接收到的挂起更改，则该订阅将过期，必须重新初始化。 所允许的最大保持期为当前日期到 9999 年 12 月 31 日之间的天数。  
  
> [!NOTE]  
>  合并发布的保持期具有一个 24 小时宽限期，以适应订阅服务器在不同时区。 例如，如果将保持期设置为 1 天，则实际的保持期为 48 小时。  
  
 [  **@sync_mode =** ] *sync_mode*  
 是订阅服务器对发布进行初始同步时采用的模式。 *sync_mode*是**nvarchar(10)**，和可以是以下值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**本机**（默认值）|生成所有表的本机模式大容量复制程序输出。|  
|**字符**|生成所有表的字符模式大容量复制程序输出。 需要该项以支持[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssEW](../../includes/ssew-md.md)]和非-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。|  
  
 [  **@allow_push =** ] *allow_push*  
 指定是否可为给定发布创建推入订阅。 *allow_push*是**nvarchar(5)**，这样默认值为 TRUE，对该发布的推送订阅。  
  
 [  **@allow_pull =** ] *allow_pull*  
 指定是否可为给定发布创建拉出订阅。 *allow_pull*是**nvarchar(5)**，默认值为 TRUE，这样，请求订阅的发布上。 必须指定 true 支持[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器。  
  
 [  **@allow_anonymous =** ] *allow_anonymous*  
 指定是否可为给定发布创建匿名订阅。 *allow_anonymous*是**nvarchar(5)**，对该发布默认值为 TRUE，允许匿名订阅。 若要支持[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器，你必须指定**true**。  
  
 [  **@enabled_for_internet =** ] *enabled_for_internet*  
 指定是否为 Internet 启用此发布，并确定是否可以使用文件传输协议 (FTP) 将快照文件传输到订阅服务器。 *enabled_for_internet*是**nvarchar(5)**，默认值为 FALSE。 如果**true**，为发布同步文件将放置到 C:\Program Files\Microsoft SQL Server\MSSQL\MSSQL.x\Repldata\Ftp 目录。 用户必须创建 Ftp 目录。 如果**false**，发布无法进行 Internet 访问权限。  
  
 [  **@centralized_conflicts =**] *centralized_conflicts*  
 已不推荐使用该参数，支持该参数只是为了让脚本能够向后兼容。 使用*conflict_logging*指定存储冲突记录的位置的位置。  
  
 [  **@dynamic_filters =**] *dynamic_filters*  
 允许合并发布使用参数化行筛选器。 *dynamic_filters*是**nvarchar(5)**，默认值为 FALSE。  
  
> [!NOTE]  
>  如果正在使用参数化行筛选器，请勿指定此参数，而应由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自行确定。 如果指定的值**true**为*dynamic_filters*，必须定义为项目参数化的行筛选器。 有关详细信息，请参阅 [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
 [  **@snapshot_in_defaultfolder =** ] *snapshot_in_default_folder*  
 指定快照文件是否存储在默认文件夹中。 *snapshot_in_default_folder*是**nvarchar(5)**，默认值为 TRUE。 如果**true**，可以在默认文件夹中找到快照文件。 如果**false**，快照文件将存储在指定的备用位置*alternate_snapshot_folder*。 备用位置可以是另一台服务器、 网络驱动器，或可移动媒体 （如 CD-ROM 或可移动磁盘）。 也可以将快照文件保存到文件传输协议 (FTP) 站点以供订阅方以后检索。 请注意此参数可以是 true，仍具有由指定的位置*alt_snapshot_folder*。 该组合指定将快照文件同时存储在默认位置和备用位置。  
  
 [  **@alt_snapshot_folder =** ] *alternate_snapshot_folder*  
 指定快照的备用文件夹的位置。 *alternate_snapshot_folder*是**nvarchar （255)**，默认值为 NULL。  
  
 [  **@pre_snapshot_script =** ] *pre_snapshot_script*  
 指定指向的指针**.sql**文件位置。 *pre_snapshot_script*是**nvarchar （255)**，默认值为 NULL。 在订阅服务器上应用快照时，合并代理将在运行任何复制的对象脚本之前运行快照前脚本。 该脚本将在合并代理连接到订阅数据库时使用的安全上下文中执行。 快照前脚本不运行[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器。  
  
 [  **@post_snapshot_script =** ] *post_snapshot_script*  
 指定指向的指针**.sql**文件位置。 *post_snapshot_script*是**nvarchar （255)**，默认值为 NULL。 当所有其他复制的对象脚本和数据均已在初始同步过程中应用之后，合并代理将运行快照后脚本。 该脚本将在合并代理连接到订阅数据库时使用的安全上下文中执行。 快照后脚本不运行[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器。  
  
 [  **@compress_snapshot =** ] *compress_snapshot*  
 指定的写入到的快照 **@alt_snapshot_folder** 位置是压缩成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 *compress_snapshot*是**nvarchar(5)**，默认值为 FALSE。 **false**指定，将不会压缩快照;**true**指定要压缩快照。 无法压缩大于 2GB 的快照文件。 压缩的快照文件被解压缩到合并代理所在的位置；一般对压缩的快照使用请求订阅，以便在订阅服务器上解压缩文件。 不能压缩默认文件夹中的快照。 若要支持[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器，你必须指定**false**。  
  
 [  **@ftp_address =** ] *ftp_address*  
 分发服务器的 FTP 服务网络地址。 *ftp_address*是**sysname**，默认值为 NULL。 指定订阅服务器来选取的合并代理发布快照文件的位置。 由于此属性存储为每个发布中，每个发布都可以具有不同*ftp_address*。 该发布必须支持使用 FTP 来传播快照。  
  
 [  **@ftp_port=** ] *ftp_port*  
 分发服务器 FTP 服务的端口号。 *ftp_port*是**int**，默认值为 21。 指定发布快照文件所在的位置以供订阅服务器的合并代理挑选。 由于此属性存储为每个发布中，每个发布都有其自己*ftp_port*。  
  
 [  **@ftp_subdirectory =** ] *ftp_subdirectory*  
 指定在发布支持使用 FTP 传播快照时，快照文件将位于何处以供订阅服务器的合并代理挑选。 *ftp_subdirectory*是**nvarchar （255)**，默认值为 NULL。 由于此属性存储为每个发布中，每个发布都有其自己*ftp_subdirctory*或者选择子目录，并用 NULL 值。  
  
 在使用参数化筛选器为发布预先生成快照时，需要将每个订阅服务器分区的数据快照置于自己的文件夹中。 使用 FTP 的预先生成快照的目录结构必须为以下结构：  
  
 *alternate_snapshot_folder*\ftp\\*publisher_publicationDB_publication*\\*partitionID*。  
  
> [!NOTE]  
>  上面以斜体显示的值取决于发布和订阅服务器分区的具体情况。  
  
 [  **@ftp_login =** ] *ftp_login*  
 用于连接到 FTP 服务用户名。 *ftp_login*是**sysname**，默认值为 'anonymous'。  
  
 [  **@ftp_password =** ] *ftp_password*  
 用于连接到 FTP 服务的用户密码。 *ftp_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  不要使用空密码。 请使用强密码。  
  
 [  **@conflict_retention =** ] *conflict_retention*  
 指定保留冲突的保持期（天）。 *conflict_retention*是**int**，默认值为 14 天之前冲突行清除从冲突表。  
  
 [  **@keep_partition_changes =** ] *keep_partition_changes*  
 指定在无法使用预计算分区时是否启用分区更改优化。 *keep_partition_changes*是**nvarchar(5)**，默认值为 TRUE。 **false**意味着对更改进行分区都不优化，并且分区中的数据更改时，当不使用预计算的分区，将验证发送到所有订阅服务器的分区。 **true**对更改进行分区的方式进行了优化，和订阅服务器，具有已更改的分区中的行受到影响。 当使用预计算的分区，设置*use_partition_groups*到**true**并设置*keep_partition_changes*到**false**。 有关详细信息，请参阅[使用预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
> [!NOTE]  
>  如果指定的值**true**为*keep_partition_changes*，将值指定为**1**为快照代理参数**-MaxNetworkOptimization**. 有关此参数的详细信息，请参阅[复制快照代理](../../relational-databases/replication/agents/replication-snapshot-agent.md)。 有关如何指定代理参数的信息，请参阅[复制代理管理](../../relational-databases/replication/agents/replication-agent-administration.md)。  
  
 与[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器， *keep_partition_changes*必须设置为 true，以确保将正确地传播删除。 设置为 false 时，订阅服务器可能有比预期更多的行。  
  
 [  **@allow_subscription_copy=** ] *allow_subscription_copy*  
 启用或禁用对订阅此发布的订阅数据库的复制功能。 *allow_subscription_copy*是**nvarchar(5)**，默认值为 FALSE。 要复制的订阅数据库的大小必须小于 2 GB。  
  
 [  **@allow_synctoalternate =** ] *allow_synctoalternate*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@validate_subscriber_info =** ] *validate_subscriber_info*  
 列出在使用参数化行筛选器时用于定义已发布数据的订阅服务器分区的函数。 *validate_subscriber_info*是**nvarchar(500)**，默认值为 NULL。 合并代理利用该信息来验证订阅服务器分区。 例如，如果[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)使用在参数化的行筛选器，该参数应`@validate_subscriber_info=N'SUSER_SNAME()'`。  
  
> [!NOTE]  
>  该参数不应由用户指定，而应由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来自动确定筛选准则。  
  
 [  **@add_to_active_directory =** ] *add_to_active_directory*  
 已不推荐使用该参数，支持该参数只是为了让脚本能够向后兼容。 不能再向 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中添加发布信息。  
  
 [  **@max_concurrent_merge =** ] *maximum_concurrent_merge*  
 并发合并进程的最大数目。 *maximum_concurrent_merge*是**int**默认值为 0。 值为**0**为此属性是对并发合并进程在任何给定时间运行的数量没有限制。 该属性对可以同时在合并发布上运行的并发合并进程数设置限制。 如果同时调度的合并进程数大于所允许的数目，则将多出的作业放置在队列中等待，直到当前正在运行的合并进程结束。  
  
 [  **@max_concurrent_dynamic_snapshots =**] *max_concurrent_dynamic_snapshots*  
 为生成订阅服务器分区的筛选数据快照而可以并发运行的最大快照代理会话数目。 *maximum_concurrent_dynamic_snapshots*是**int**默认值为 0。 如果**0**，编号快照会话没有限制。 如果同时调度的快照进程数比允许运行的数多，则多出的作业将放置在队列中等待，直到当前正在运行的快照进程完成。  
  
 [  **@use_partition_groups =** ] *use_partition_groups*  
 指定应使用预计算分区来优化同步进程。 *use_partition_groups*是**nvarchar(5)**，并且可以为这些值之一：  
  
|值|Description|  
|-----------|-----------------|  
|**true**|发布使用预计算分区。|  
|**false**|发布不使用预计算分区。|  
|NULL（默认值）|由系统确定分区策略。|  
  
 默认情况下，使用预计算分区。 若要避免使用预计算的分区， *use_partition_groups*必须设置为**false**。 如果设置为 NULL，则系统会确定预计算分区是否可用。 如果预计算分区不能使用，则此值将有效地成为**false**而不生成任何错误。 在这种情况下， *keep_partition_changes*可以将设置为**true**提供某些优化。 有关详细信息，请参阅[参数化行筛选器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)和[与预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 [  **@publication_compatibility_level =** ] *backward_comp_level*  
 指示发布的向后兼容性。 *backward_comp_level*是**nvarchar(6)**，并且可以为这些值之一：  
  
|值|版本|  
|-----------|-------------|  
|**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
  
 [  **@replicate_ddl =** ] *replicate_ddl*  
 指示是否架构复制支持发布。 *replicate_ddl*是**int**，默认值为 1。 **1**指明可将复制发布服务器上执行数据定义语言 (DDL) 语句，和**0**指示 DDL 语句不会复制。 有关详细信息，请参阅[对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
 *@replicate_ddl* 当 DDL 语句将添加一个列时，接受参数。 *@replicate_ddl*  DDL 语句更改或删除下列原因造成的列时，将忽略参数。  
  
-   当除去的列时，则必须更新 sysarticlecolumns 以防止新的 DML 语句，从包括已删除的列，从而导致分发代理失败。 *@replicate_ddl* 参数将被忽略，因为复制必须始终复制架构更改。  
  
-   更改列时，源数据类型或为 Null 性可能已更改，这导致 DML 语句包含可能与订阅服务器上的表不兼容的值。 这种 DML 语句可能导致分发代理失败。 *@replicate_ddl* 参数将被忽略，因为复制必须始终复制架构更改。  
  
-   当 DDL 语句将添加一个新列时，sysarticlecolumns 不包括新的列。 DML 语句将不尝试复制新列的数据。 采用该参数，因为复制或不复制 DDL 均可接受。  
  
 [  **@allow_subscriber_initiated_snapshot =** ] *allow_subscriber_initiated_snapshot*  
 指示此发布的订阅服务器是否可以启动快照进程来为它们的数据分区生成筛选快照。 *allow_subscriber_initiated_snapshot*是**nvarchar(5)**，默认值为 FALSE。 **true**指示订阅服务器可以启动快照进程。  
  
 [  **@allow_web_synchronization =** ] *allow_web_synchronization*  
 指定是否为 Web 同步启用此发布。 *allow_web_synchronization*是**nvarchar(5)**，默认值为 FALSE。 **true**指定对此发布的订阅可以通过 HTTPS 进行同步。 有关详细信息，请参阅 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)。 若要支持[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器，你必须指定**true**。  
  
 [  **@web_synchronization_url=** ] *web_synchronization_url*  
 指定用于 Web 同步的 Internet URL 的默认值。 *web_synchronization_url 我*s **nvarchar(500)**，默认值为 NULL。 如果一个未显式设置时定义了默认的 Internet URL [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)执行。  
  
 [  **@allow_partition_realignment =** ] *allow_partition_realignment*  
 确定在发布服务器上对行所做的修改导致该行更改其分区时是否要将删除内容发送到订阅服务器。 *allow_partition_realignment*是**nvarchar(5)**，默认值为 TRUE。 **true**将删除发送到订阅服务器以通过删除不再属于订阅服务器的分区的数据中反映分区更改的结果。 **false**在订阅服务器，其中对此发布服务器上的数据所做的更改不会复制到此订阅服务器，但订阅服务器上所做的更改将复制到发布服务器上从旧的分区中保留的数据。 设置*allow_partition_realignment*到**false**用于时需要可作为历史记录数据保留旧的分区从订阅中的数据。  
  
> [!NOTE]  
>  在设置由于订阅服务器上的剩余数据*allow_partition_realignment*到**false**应被视为就像它是只读的; 但是，这不由实施复制系统。  
  
 [  **@retention_period_unit =** ] *retention_period_unit*  
 指定的单位在保留期设*保留*。 *retention_period_unit*是**nvarchar(10)**，和可以是以下值之一。  
  
|值|版本|  
|-----------|-------------|  
|**天**（默认值）|按天指定保持期。|  
|**周**|按周指定保持期。|  
|**月**|按月指定保持期。|  
|**年**|按年指定保持期。|  
  
 [  **@generation_leveling_threshold=** ] *generation_leveling_threshold*  
 指定在生成中包含的更改数。 代次是传递到发布服务器或订阅服务器的更改的集合。 *generation_leveling_threshold*是**int**，默认值为 1000年。  
  
 [  **@automatic_reinitialization_policy =** ] *automatic_reinitialization_policy*  
 指定是否从之前所需的更改发布，其中的值自动重新初始化订阅服务器上载更改**1**为指定 **@force_reinit_subscription** 。 *automatic_reinitialization_policy*位，默认值为 0。 **1**表示自动重新初始化之前，将更改上载从订阅服务器。  
  
> [!IMPORTANT]  
>  如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
 [  **@conflict_logging =** ] *conflict_logging*  
 指定存储冲突记录的位置。 *conflict_logging*是**nvarchar(15)**，和可以是以下值之一：  
  
|值|Description|  
|-----------|-----------------|  
|**发布服务器**|在发布服务器上存储冲突记录。|  
|**订阅服务器**|在导致冲突的订阅服务器上存储冲突记录。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 订阅服务器不支持此值。|  
|**两者**|在发布服务器和订阅服务器上都存储冲突记录。|  
|NULL（默认值）|复制会自动设置*conflict_logging*到**同时**时值*backward_comp_level*是**90RTM**和**发布服务器**在所有其他情况下。|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 **sp_addmergepublication**合并复制中使用。  
  
 与列表发布对象和 Active Directory 使用 **@add_to_active_directory** 参数，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必须已在 Active Directory 中创建对象。  
  
 如果存在多个发布，发布同一个数据库对象，仅发布*replicate_ddl*值**1**将复制 ALTER TABLE、 ALTER VIEW、 ALTER PROCEDURE、 ALTER FUNCTION 和ALTER TRIGGER DDL 语句。 但是，发布已删除列的所有发布都将复制 ALTER TABLE DROP COLUMN DDL 语句。  
  
 有关[!INCLUDE[ssEW](../../includes/ssew-md.md)]订阅服务器的值*alternate_snapshot_folder*仅时使用的值*snapshot_in_default_folder*是**false**。  
  
 已启用 DDL 复制的 (*replicate_ddl***= 1**) 对于发布，以便非复制 DDL 更改为发布， [sp_changemergepublication &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)必须首先执行设置*replicate_ddl*到**0**。 已颁发的非复制 DDL 语句后， **sp_changemergepublication**可以再次运行，以启用 DDL 复制。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddMergePub](../../relational-databases/replication/codesnippet/tsql/sp-addmergepublication-t_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addmergepublication**。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
