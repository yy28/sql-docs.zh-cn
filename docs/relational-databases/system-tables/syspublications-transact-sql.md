---
title: syspublications (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
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
- syspublications
- syspublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspublications system table
ms.assetid: a86eb4f5-1f7b-493e-af55-3d15cf878228
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ec8c1f12755afa1a12e4e28c9f84c2f21963fc9f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33012724"
---
# <a name="syspublications-transact-sql"></a>syspublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  数据库内定义的每个发布在表中对应一行。 该表存储在发布数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**说明**|**nvarchar(255)**|发布的说明项。|  
|**名称**|**sysname**|与发布关联的唯一名称。|  
|**pubid**|**int**|为发布提供唯一 ID 的标识列。|  
|**repl_freq**|**tinyint**|复制频率：<br /><br /> **0** = 基于的事务。<br /><br /> **1** = 计划表刷新。|  
|**status**|**tinyint**|状态：<br /><br /> **0** = 处于非活动状态。<br /><br /> **1** = 活动。|  
|**sync_method**|**tinyint**|同步方法包括：<br /><br /> **0** = 纯模式大容量复制程序实用工具 (**BCP**)。<br /><br /> **1** = 字符模式 BCP。<br /><br /> **3** = 并发，这意味着使用纯模式 BCP，但在快照期间不锁定表。<br /><br /> **4** = Concurrent_c，这意味着，使用字符模式 BCP，但在快照期间不锁定表。|  
|**snapshot_jobid**|**binary(16)**|预定任务 ID。|  
|**independent_agent**|**bit**|指定是否为此发布一个独立的分发代理。<br /><br /> **0** = 发布使用共享的分发代理，并且每个发布服务器订阅服务器数据库/数据库对具有共享代理。<br /><br /> **1** = 此发布的独立分发代理。|  
|**immediate_sync**|**bit**|指示是否创建或重新创建快照代理运行时，每次同步文件其中**1**意味着每次代理运行时创建它们。|  
|**enabled_for_internet**|**bit**|指示是否通过文件传输协议 (FTP) 和其他服务，internet 公开发布的同步文件其中**1**意味着它们可以从 Internet 进行访问。|  
|**allow_push**|**bit**|指示是否对该发布允许推送订阅其中**1**意味着被允许。|  
|**allow_pull**|**bit**|指示是否请求订阅允许对该发布，其中**1**意味着被允许。|  
|**allow_anonymous**|**bit**|指示是否对该发布允许匿名订阅其中**1**意味着被允许。|  
|**immediate_sync_ready**|**bit**|指示快照代理是否已生成快照且该快照是否准备好用于新的订阅。 仅对于立即更新发布才有意义。 **1**指示快照已准备就绪。|  
|**allow_sync_tran**|**bit**|指定是否对该发布允许立即更新订阅。 **1**表示允许立即更新订阅。|  
|**autogen_sync_procs**|**bit**|指定是否在发布服务器中为立即更新订阅生成同步存储过程。 **1**意味着生成在发布服务器。|  
|**保持期**|**int**|为给定发布保存的更改数量（小时）。|  
|**allowed_queued_tran**|**bit**|指定是否启用在订阅服务器上对更改进行排队，直到更改可以在发布服务器上应用为止。 如果**1**，订阅服务器上的更改进行排队。|  
|**snapshot_in_defaultfolder**|**bit**|指定是否在默认文件夹中存储快照文件。<br /><br /> **0** = 快照文件已存储在指定的备用位置*alternate_snapshot_folder*。<br /><br /> **1** = 快照文件可以位于默认文件夹。|  
|**alt_snapshot_folder**|**nvarchar(255)**|指定快照的备用文件夹的位置。|  
|**pre_snapshot_script**|**nvarchar(255)**|指定指向的指针 **.sql**文件位置。 在订阅服务器上应用快照时，分发代理将在运行任何复制的对象脚本之前运行快照前脚本。|  
|**post_snapshot_script**|**nvarchar(255)**|指定指向的指针 **.sql**文件位置。 在初始同步过程中，分发代理将在应用所有其他复制的对象脚本和数据之后运行快照后脚本。|  
|**compress_snapshot**|**bit**|指定写入到快照*alt_snapshot_folder*位置是压缩成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。**1**意味着将压缩的快照。|  
|**ftp_address**|**sysname**|分发服务器的 FTP 服务的网络地址。 指定发布快照文件所在的位置以供分发代理拾取。|  
|**ftp_port**|**int**|分发服务器的 FTP 服务的端口号。 指定的发布快照文件所在的位置来选取的分发代理|  
|**ftp_subdirectory**|**nvarchar(255)**|指定当发布支持使用 FTP 传播快照时的快照文件的位置以供分发代理获取。|  
|**ftp_login**|**sysname**|用于连接到 FTP 服务的用户名。|  
|**ftp_password**|**nvarchar(524)**|用于连接到 FTP 服务的用户密码。|  
|**allow_dts**|**bit**|指定发布是否允许数据转换。 **1**指定允许的 DTS 转换。|  
|**allow_subscription_copy**|**bit**|指定是否已启用复制订阅该发布的订阅数据库的功能。 **1**意味着，允许复制。|  
|**centralized_conflicts**|**bit**|指定冲突记录是否存储在发布服务器上：<br /><br /> **0** = 记录存储同时在发布服务器和订阅服务器引起冲突的冲突。<br /><br /> **1** = 记录存储在发布服务器上的冲突。|  
|**conflict_retention**|**int**|指定冲突保持期（天）。|  
|**conflict_policy**|**int**|指定使用排队更新订阅服务器选项时遵循的冲突解决策略。 可以是下列值之一：<br /><br /> **1** = 冲突的发布服务器入选。<br /><br /> **2** = 订阅服务器入选冲突。<br /><br /> **3** = 重新初始化订阅。|  
|**queue_type**|**int**|指定所使用的队列类型。 可以是下列值之一：<br /><br /> **1** = msmq，它使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]消息队列来存储事务。<br /><br /> **2** = sql，使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要存储的事务。<br /><br /> 注意： 使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]消息队列已弃用，不再可用。|  
|**ad_guidname**|**sysname**|指定是否在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中发布该发布。 一个有效的全局唯一标识符 (GUID) 指定在 Active Directory 中发布发布和 GUID 是相应的 Active Directory 发布对象**objectGUID**。 如果为 NULL，则将不在 Active Directory 中发布该发布。|  
|**backward_comp_level**|**int**|数据库兼容性级别，可以是以下值之一：<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].<br /><br /> **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].|  
|**allow_initialize_from_backup**|**bit**|指示订阅服务器是否可以从备份，而不是初始快照对此发布初始化订阅。 **1**意味着可以从备份初始化订阅和**0**意味着，它们不能。 有关详细信息，请参阅 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手动初始化订阅。|  
|**min_autonosync_lsn**|**binary**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|指示发布是否支持架构复制。 **1**指明可将复制发布服务器上执行数据定义语言 (DDL) 语句，和**0**指示 DDL 语句不会复制。 有关详细信息，请参阅[对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。|  
|**options**|**int**|指定其他发布选项的位图，其中的位选项值如下所示：<br /><br /> **0x1** -已启用对等复制。<br /><br /> **0x2** -发布仅本地更改为对等复制。<br /><br /> **0x4** -已启用有关非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。<br /><br /> **0x8** -对等冲突检测已启用。|  
|**originator_id**|**int**|为进行冲突检测标识对等复制拓扑中的每个节点。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
