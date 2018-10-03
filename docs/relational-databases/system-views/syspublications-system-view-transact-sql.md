---
title: syspublications （系统视图） (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspublications view
ms.assetid: e5f57c32-efc0-4455-a74f-684dc2ae51f8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf2c03c08d6653756fa9a65cc0dbe5be8ec2e173
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780487"
---
# <a name="syspublications-system-view-transact-sql"></a>syspublications（系统视图）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Syspublications**视图显示发布信息。 此视图存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**description**|**nvarchar(255)**|发布的说明项。|  
|**名称**|**sysname**|与发布关联的唯一名称。|  
|**pubid**|**int**|为发布提供唯一 ID 的标识列。|  
|**repl_freq**|**tinyint**|复制频率：<br /><br /> **0** = 基于事务 （事务）。<br /><br /> **1** = 计划表刷新 （快照）。|  
|**status**|**tinyint**|发布的状态：<br /><br /> **0** = 非活动状态。<br /><br /> **1** = 活动。|  
|**sync_method**|**tinyint**|同步方法包括：<br /><br /> **0** = 本机大容量复制程序实用工具 (BCP)。<br /><br /> **1** = 字符 BCP。<br /><br /> **3** = 并发，表示使用本机 BCP 但不是在快照期间锁定表。<br /><br /> **4** = Concurrent_c，表示使用的字符 BCP 但表未锁定在快照期间。|  
|**snapshot_jobid**|**binary(16)**|标识计划生成初始快照的代理作业。|  
|**independent_agent**|**bit**|指定是否存在用于此发布的独立分发代理。<br /><br /> **0** = 发布使用共享的分发代理，并且每个发布服务器数据库/订阅服务器数据库对具有单一的共享代理。<br /><br /> **1** = 没有用于此发布的独立分发代理。|  
|**immediate_sync**|**bit**|指示同步文件是创建还是重新创建每次运行快照代理，其中**1**意味着每次运行代理时创建它们。|  
|**enabled_for_internet**|**bit**|指示是否通过文件传输协议 (FTP) 和其他服务，向 Internet 公开发布的同步文件位置**1**意味着可以从 Internet 访问它们。|  
|**allow_push**|**bit**|指示是否对该发布允许推送订阅其中**1**允许它们的方式。|  
|**allow_pull**|**bit**|指示是否对该发布允许请求订阅其中**1**允许它们的方式。|  
|**allow_anonymous**|**bit**|指示是否对该发布允许匿名订阅其中**1**允许它们的方式。|  
|**immediate_sync_ready**|**bit**|指示快照代理是否已生成快照且该快照是否准备好用于新的订阅。 仅对于立即更新发布才有意义。 **1**指示快照已准备好。|  
|**allow_sync_tran**|**bit**|指定是否对该发布允许立即更新订阅。 **1**意味着允许立即更新订阅。|  
|**autogen_sync_procs**|**bit**|指定是否在发布服务器中为立即更新订阅生成同步存储过程。 **1**表示生成在发布服务器。|  
|**保留期**|**int**|对发布的更改在分发数据库中保留的时间（小时）。|  
|**allow_queued_tran**|**bit**|指定是否启用在订阅服务器上对更改进行排队，直到更改可以在发布服务器上应用为止。 如果**1**，则订阅服务器上的更改进行排队。|  
|**snapshot_in_defaultfolder**|**bit**|指定是否在默认文件夹中存储快照文件。 如果**0**，快照文件存储在由指定的备用位置*alternate_snapshot_folder*。 如果为 1，则可以在默认文件夹中找到快照文件。|  
|**alt_snapshot_folder**|**nvarchar(510)**|指定快照的备用文件夹的位置。|  
|**pre_snapshot_script**|**nvarchar(510)**|指定一个指向 **.sql**文件位置。 在订阅服务器上应用快照时，分发代理将在运行任何复制的对象脚本之前运行快照前脚本。|  
|**post_snapshot_script**|**nvarchar(510)**|指定一个指向 **.sql**文件位置。 在初始同步过程中，分发代理将在应用所有其他复制的对象脚本和数据之后运行快照后脚本。|  
|**compress_snapshot**|**bit**|指定写入到的快照*alt_snapshot_folder*位置是将压缩成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 **1**意味着将压缩的快照。|  
|**ftp_address**|**sysname**|分发服务器的 FTP 服务的网络地址。 指定发布快照文件所在的位置以供分发代理拾取。|  
|**ftp_port**|**int**|分发服务器的 FTP 服务的端口号。 指定供分发代理拾取的发布快照文件所在的位置。|  
|**ftp_subdirectory**|**nvarchar(510)**|指定如果发布支持使用 FTP 传播快照，分发代理应从何处拾取快照文件。|  
|**ftp_login**|**nvarchar(256)**|用于连接到 FTP 服务的用户名。|  
|**ftp_password**|**nvarchar(1048)**|用于连接到 FTP 服务的用户密码。|  
|**allow_dts**|**bit**|指定发布是否允许 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Data Transformation Services (DTS) 转换。 **1**指定允许 DTS 转换。|  
|**allow_subscription_copy**|**bit**|指定是否已启用复制订阅该发布的订阅数据库的功能。 **1**意味着允许复制。|  
|**centralized_conflicts**|**bit**|指定冲突记录是否存储在发布服务器上：<br /><br /> **0** = 均存储的冲突记录的发布服务器和订阅服务器导致冲突。<br /><br /> **1** = 的冲突记录存储在发布服务器。|  
|**conflict_retention**|**int**|指定冲突记录的保持期（天）。|  
|**conflict_policy**|**int**|指定使用排队更新订阅服务器选项时遵循的冲突解决策略。 可以是下列值之一：<br /><br /> **1** = 发布服务器入选冲突。<br /><br /> **2** = 订阅服务器入选冲突。<br /><br /> **3** = 重新初始化订阅。|  
|**queue_type**|**int**|指定所使用的队列类型。 可以是下列值之一：<br /><br /> **1** =.msmq，使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]消息队列来存储事务。<br /><br /> **2** =.sql，它使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]来存储事务。<br /><br /> 注意： 使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]消息队列已被弃用，不再受支持。|  
|**ad_guidname**|**sysname**|指定是否在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中发布该发布。 有效的全局唯一标识符 (GUID) 指定在 Active Directory 中发布该发布，并且 GUID 是相应的 Active Directory 发布对象 objectGUID。 如果为 NULL，则将不在 Active Directory 中发布该发布。<br /><br /> 注意： 不再支持发布到 Active Directory。|  
|**backward_comp_level**|**int**|数据库兼容性级别，可以是下列值之一：<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|**allow_initialize_from_backup**|**bit**|指示订阅服务器是否可以从备份而不是初始快照对此发布初始化的订阅。 **1**意味着可以从备份初始化订阅并**0**表示不能。 有关详细信息，请参阅 [初始化事务订阅（不使用快照）](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手动初始化订阅。|  
|**min_autonosync_lsn**|**binary(1)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|指示发布是否支持架构复制。<br /><br /> **1** = DDL 复制在发布服务器执行语句。<br /><br /> **0** = 指示不复制 DDL 语句。 有关详细信息，请参阅[对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。|  
|**options**|**int**|指定其他发布选项的位图，其中的位选项值如下所示：<br /><br /> **0x1** -对等复制启用。<br /><br /> **0x2** -仅发布本地更改为对等复制。<br /><br /> **0x4** -对启用非-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。<br /><br /> **0x8** -启用对等冲突检测。|  
|**originator_id**|**smallint**|为进行冲突检测标识对等复制拓扑中的每个节点。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addpublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
