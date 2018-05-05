---
title: sysmergepublications (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergepublications
- sysmergepublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepublications system table
ms.assetid: 7f82c6c3-22d1-47c0-a92b-4d64b98cc455
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 40763216075a551c244e72b0516e7ff2383ff913
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysmergepublications-transact-sql"></a>sysmergepublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  数据库中定义的每个合并发布在表中各占一行。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|默认服务器的名称。|  
|**publisher_db**|**sysname**|默认发布服务器数据库的名称。|  
|**名称**|**sysname**|发布的名称。|  
|**说明**|**nvarchar(255)**|对发布的简短说明。|  
|**保持期**|**int**|整个发布集，单元将由的值的保持期**retention_period_unit**列。|  
|**publication_type**|**tinyint**|指示发布是否经过筛选：<br /><br /> **0** = 未筛选。<br /><br /> **1** = 筛选。|  
|**pubid**|**uniqueidentifier**|此发布的唯一标识号。 它是在添加发布时生成的。|  
|**designmasterid**|**uniqueidentifier**|保留供将来使用。|  
|**parentid**|**uniqueidentifier**|指示据以创建当前对等发布或子集发布的父发布（用于层次结构发布拓朴）。|  
|**sync_mode**|**tinyint**|此发布的同步模式：<br /><br /> **0** = native。<br /><br /> **1** = 字符。|  
|**allow_push**|**int**|指示发布是否允许推送订阅。<br /><br /> **0** = 推送订阅不允许。<br /><br /> **1** = 的推送订阅允许。|  
|**allow_pull**|**int**|指示发布是否允许请求订阅。<br /><br /> **0** = 不允许的请求订阅。<br /><br /> **1** = 订阅允许的请求。|  
|**allow_anonymous**|**int**|指示发布是否允许匿名订阅。<br /><br /> **0** = 不允许匿名订阅。<br /><br /> **1** = 匿名订阅允许。|  
|**centralized_conflicts**|**int**|指示是否在发布服务器上存储冲突记录：<br /><br /> **0** = 记录不会存储在发布服务器上的冲突。<br /><br /> **1** = 记录存储在发布服务器上的冲突。|  
|**status**|**tinyint**|保留供将来使用。|  
|**snapshot_ready**|**tinyint**|指示发布的快照的状态：<br /><br /> **0** = 快照未准备好进行使用。<br /><br /> **1** = 快照是可供使用。<br /><br /> **2** = 新的快照，必须创建此发布。|  
|**enabled_for_internet**|**bit**|指示是否通过 FTP 和其他服务将用于发布的同步文件在 Internet 上公开。<br /><br /> **0** = 文件可以从 Internet 访问的同步。<br /><br /> **1** = 文件不能从 Internet 访问的同步。|  
|**dynamic_filters**|**bit**|指示是否使用参数化行筛选器筛选了发布。<br /><br /> **0** = 发布不行筛选。<br /><br /> **1** = 发布筛选行。|  
|**snapshot_in_defaultfolder**|**bit**|指定快照文件是否存储在默认文件夹中：<br /><br /> **0** = 文件的默认文件夹中的快照。<br /><br /> **1** = 的快照文件存储在指定的位置**alt_snapshot_folder**。|  
|**alt_snapshot_folder**|**nvarchar(255)**|快照的备用文件夹位置。|  
|**pre_snapshot_script**|**nvarchar(255)**|到指针。**sql**合并代理运行之前复制对象的任何文件的脚本时在订阅服务器上应用快照。|  
|**post_snapshot_script**|**nvarchar(255)**|指向的指针。**sql**文件运行合并代理在所有其他复制对象脚本，并且已在初始同步期间应用数据。|  
|**compress_snapshot**|**bit**|指定是否写入到快照**alt_snapshot_folder**位置将被压缩到[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 **0**指定文件不会压缩。|  
|**ftp_address**|**sysname**|分发服务器的文件传输协议 (FTP) 服务的网络地址。 如果启用了 FTP，则指定合并代理要拾取的发布快照文件所在的位置。|  
|**ftp_port**|**int**|分发服务器的 FTP 服务的端口号。|  
|**ftp_subdirectory**|**nvarchar(255)**|合并代理可拾取的快照文件所在的子目录。|  
|**ftp_login**|**sysname**|用于连接到 FTP 服务的用户名称。|  
|**ftp_password**|**nvarchar(524)**|用于连接到 FTP 服务的用户密码。|  
|**conflict_retention**|**int**|指定保留冲突的保持期（天）。 保持期过后，将从冲突表中清除冲突行。|  
|**keep_before_values**|**int**|指定是否对此发布的同步进行优化：<br /><br /> **0** = 不优化同步，并且在分区中的数据更改时，将验证发送到所有订阅服务器的分区。<br /><br /> **1** = 优化同步时，和订阅服务器，具有已更改的分区中的行受到影响。|  
|**allow_subscription_copy**|**bit**|指定是否启用了复制订阅数据库的功能。 **0**意味着不允许进行复制。|  
|**allow_synctoalternate**|**bit**|指定是否允许备用同步伙伴与该发布服务器同步。 **0**意味着，不允许同步伙伴。|  
|**validate_subscriber_info**|**nvarchar(500)**|列出用于检索订阅服务器信息和验证订阅服务器上的参数化行筛选条件的函数。|  
|**ad_guidname**|**sysname**|指定是否在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中发布该发布。 一个有效的 GUID 指定 Active Directory 中发布的发布和 GUID 是相应的 Active Directory 发布对象**objectGUID**。 如果为 NULL，则将不在 Active Directory 中发布该发布。|  
|**backward_comp_level**|**int**|数据库兼容级别。 可以是以下值之一：<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|**max_concurrent_merge**|**int**|允许的最大并发合并进程数。 值为**0**为此属性是对并发合并进程在任何给定时间运行的数量没有限制。 此属性设置对可以对合并发布一次运行的并发合并进程数限制。 如果同时调度的快照进程数比允许运行的进程数多，则多出的作业将放置在队列中等待，直到当前正在运行的合并进程完成。|  
|**max_concurrent_dynamic_snapshots**|**int**|允许针对合并发布运行的最大并发筛选数据快照会话数。 如果**0**，可以在任何给定时间发布针对同时运行的并发的已筛选的数据快照会话的最大次数没有限制。 此属性对可以同时对合并发布运行的最大并发快照进程数设置限制。 如果同时调度的快照进程数比允许运行的进程数多，则多出的作业将放置在队列中等待，直到当前正在运行的合并进程完成。|  
|**use_partition_groups**|**int**|指定发布是否使用预计算分区。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|一组分号分隔的函数，用于发布的参数化行筛选器。|  
|**partition_id_eval_proc**|**sysname**|指定由订阅服务器的合并代理运行的过程名称，以便确定为其分配的分区 ID。|  
|**publication_number**|**int**|指定标识列提供的 2 字节映射到**pubid**。 **pubid**是一个发布的全局唯一标识符，而发布号是只能在指定数据库中唯一。|  
|**replicate_ddl**|**int**|指示发布是否支持架构复制。<br /><br /> **0** = DDL 语句不会复制。<br /><br /> **1** = DDL 复制发布服务器上执行的语句。<br /><br /> 有关详细信息，请参阅[对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。|  
|**allow_subscriber_initiated_snapshot**|**bit**|指示订阅服务器是否可以启动使用参数化筛选器为发布生成快照的进程。 **1**指示订阅服务器可以启动快照进程。|  
|**dynamic_snapshot_queue_timeout**|**int**|指定使用参数化筛选器时，订阅服务器必须在队列中等待快照生成进程开始的分钟数。|  
|**dynamic_snapshot_ready_timeout**|**int**|指定使用参数化筛选器时，订阅服务器在队列中等待快照生成进程完成的分钟数。|  
|**分发服务器**|**sysname**|发布的分发服务器的名称。|  
|**snapshot_jobid**|**binary(16)**|订阅服务器可以启动快照生成进程时，标识生成快照的代理作业。|  
|**allow_web_synchronization**|**bit**|指定是否为 Web 同步启用发布其中**1**意味着，为该发布启用 Web 同步。|  
|**web_synchronization_url**|**nvarchar(500)**|指定用于 Web 同步的 Internet URL 的默认值。|  
|**allow_partition_realignment**|**bit**|指示对发布服务器上的行所做的修改导致了更改其分区时，是否向订阅服务器发送删除指令。<br /><br /> **0** = 从旧的数据分区将会留在订阅服务器，其中对此发布服务器上的数据所做的更改不会复制到此订阅服务器，但订阅服务器上所做的更改将复制到发布服务器上。<br /><br /> **1** = 到订阅服务器以反映分区更改的结果，通过删除不是更长的订阅服务器的分区的一部分的数据的删除。<br /><br /> 有关详细信息，请参阅[sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。<br /><br /> 注意： 如果此值为保留在订阅服务器上的数据**0**应被视为就像它是只读的; 但是，这不会严格强制进行复制系统。|  
|**retention_period_unit**|**tinyint**|定义定义时使用的单位*保留*，它可以是下列值之一：<br /><br /> **0** = 某一天。<br /><br /> **1** = 周。<br /><br /> **2** = 月。<br /><br /> **3** = 年。|  
|**decentralized_conflicts**|**int**|指示是否在导致冲突的订阅服务器上存储冲突记录：<br /><br /> **0** = 记录不会存储在订阅服务器上的冲突。<br /><br /> **1** = 记录存储在订阅服务器上的冲突。|  
|**generation_leveling_threshold**|**int**|指定生成中包含的更改次数。 代次是传递到发布服务器或订阅服务器的更改的集合。|  
|**automatic_reinitialization_policy**|**bit**|指示是否在进行自动重新初始化之前从订阅服务器上载更改。<br /><br /> **1** = 更改从订阅服务器自动重新初始化之前上载。<br /><br /> **0** = 更改不会自动重新初始化之前上载。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)  
  
  
