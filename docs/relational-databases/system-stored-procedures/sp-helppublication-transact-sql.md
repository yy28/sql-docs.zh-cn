---
title: sp_helppublication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_TSQL
- sp_helppublication
helpviewer_keywords:
- sp_helppublication
ms.assetid: e801c3f0-dcbd-4b4a-b254-949a05f63518
author: stevestein
ms.author: sstein
ms.openlocfilehash: 693e9f580c2b51c2ff8a6fd82973d06c2a80d287
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771134"
---
# <a name="sp_helppublication-transact-sql"></a>sp_helppublication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  返回有关发布的信息。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 对于发布,此存储过程在发布服务器上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对发布数据库执行。 对于 Oracle 发布，此存储过程在分发服务器上对任何数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'`要查看的发布的名称。 *发布*为 sysname, 默认值 **%** 为, 它返回有关所有发布的信息。  
  
`[ @found = ] 'found' OUTPUT`指示返回行的标志。 *找到* **int**和 OUTPUT 参数, 默认值为**23456**。 **1**指示已找到发布。 **0**表示找不到发布。  
  
`[ @publisher = ] 'publisher'`指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*的 sysname, 默认值为 NULL。  
  
> [!NOTE]  
>  当请求发布[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务器中的发布信息时, 不应指定*发布服务器*。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|pubid|**int**|发布的 ID。|  
|name|**sysname**|发布的名称。|  
|restricted|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**tinyint**|发布的当前状态。<br /><br /> **0** = 非活动。<br /><br /> **1** = 活动。|  
|任务 (task)||用于保持向后兼容性。|  
|replication frequency|**tinyint**|复制频率的类型：<br /><br /> **0** = 事务<br /><br /> **1** = 快照|  
|synchronization method|**tinyint**|同步模式：<br /><br /> **0** = 本机大容量复制程序 (**bcp**实用工具)<br /><br /> **1** = 字符大容量复制<br /><br /> **3** = 并发, 表示使用本机大容量复制 (**bcp**实用工具), 但在快照期间不锁定表<br /><br /> **4** = Concurrent_c, 这意味着将使用字符大容量复制, 但在快照过程中不锁定表|  
|description|**nvarchar(255)**|发布的可选说明。|  
|immediate_sync|**bit**|表示是否在每次快照代理运行时创建或重新创建同步文件。|  
|enabled_for_internet|**bit**|表示是否通过文件传输协议 (FTP) 和其他服务将发布的同步文件在 Internet 上公开。|  
|allow_push|**bit**|表示是否允许对发布使用推送订阅。|  
|allow_pull|**bit**|表示是否允许对发布使用请求订阅。|  
|allow_anonymous|**bit**|表示是否允许对发布使用匿名订阅。|  
|independent_agent|**bit**|表示是否有用于该发布的独立分发代理。|  
|immediate_sync_ready|**bit**|表示快照代理是否生成了准备由新订阅使用的快照。 只有当发布被设置为始终有可用于新订阅或重新初始化订阅的快照，才定义此参数。|  
|allow_sync_tran|**bit**|表示是否允许对发布使用立即更新订阅。|  
|autogen_sync_procs|**bit**|表示是否自动生成存储过程以支持立即更新订阅。|  
|snapshot_jobid|**binary(16)**|已计划任务 ID。|  
|retention|**int**|为给定的发布保存的更改量（小时）。|  
|has subscription|**bit**|表示发布是否具有活动订阅。 **1**表示发布具有活动订阅, **0**表示发布没有订阅。|  
|allow_queued_tran|**bit**|指定是否已启用在订阅服务器上禁用更改排队直到这些更改可以应用到发布服务器。 如果为**0**, 则不会对订阅服务器上的更改进行排队。|  
|snapshot_in_defaultfolder|**bit**|指定是否在默认文件夹中存储快照文件。 如果为**0**, 则将快照文件存储在*alternate_snapshot_folder*指定的备用位置中。 如果为**1**, 则可以在默认文件夹中找到快照文件。|  
|alt_snapshot_folder|**nvarchar(255)**|指定快照的备用文件夹的位置。|  
|pre_snapshot_script|**nvarchar(255)**|指定指向 **.sql**文件位置的指针。 在订阅服务器上应用快照时, 分发代理将在运行任何复制的对象脚本之前运行快照前脚本。|  
|post_snapshot_script|**nvarchar(255)**|指定指向 **.sql**文件位置的指针。 分发代理将在初始同步过程中已应用所有其他复制的对象脚本和数据之后才运行快照后脚本。|  
|compress_snapshot|**bit**|指定将写入*alt_snapshot_folder*位置的快照压缩[!INCLUDE[msCoName](../../includes/msconame-md.md)]为 CAB 格式。 **0**指定不压缩快照。|  
|ftp_address|**sysname**|分发服务器的 FTP 服务的网络地址。 指定供订阅服务器的分发代理或合并代理拾取的发布快照文件的位置。|  
|ftp_port|**int**|分发服务器的 FTP 服务的端口号。|  
|ftp_subdirectory|**nvarchar(255)**|指定供订阅服务器的分发代理或合并代理拾取的快照文件的位置（如果发布支持使用 FTP 传播快照）。|  
|ftp_login|**sysname**|用于连接到 FTP 服务的用户名。|  
|allow_dts|**bit**|指定发布允许数据转换。 **0**指定不允许 DTS 转换。|  
|allow_subscription_copy|**bit**|指定是否已启用复制订阅该发布的订阅数据库的功能。 **0**表示不允许复制。|  
|centralized_conflicts|**bit**|指定冲突记录是否存储在发布服务器上：<br /><br /> **0** = 在导致冲突的发布服务器和订阅服务器上存储冲突记录。<br /><br /> **1** = 冲突记录存储在发布服务器上。|  
|conflict_retention|**int**|指定冲突保持期（天）。|  
|conflict_policy|**int**|指定使用排队更新订阅服务器选项时遵循的冲突解决策略。 可以是以下值之一:<br /><br /> **1** = 发布服务器入选冲突。<br /><br /> **2** = 订阅服务器入选冲突。<br /><br /> **3** = 重新初始化订阅。|  
|queue_type||指定所使用的队列类型。 可以是以下值之一:<br /><br /> **msmq** = 使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]消息队列存储事务。<br /><br /> **sql** = 用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存储事务。<br /><br /> 注意:已停止支持消息队列。|  
|backward_comp_level||数据库兼容级别，可以为下列值之一：<br /><br /> **90** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**bit**|指定是否在[!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中发布发布???。 如果值为**1** , 则表示它已发布, 值为**0**时表示未发布该值。|  
|allow_initialize_from_backup|**bit**|指示订阅服务器是否能够从备份而不是从初始快照来初始化对此发布的订阅。 **1**表示可以从备份中初始化订阅, **0**表示不能。 有关详细信息, 请参阅在没有快照的情况下[初始化事务订阅 (不使用快照](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md))。|  
|replicate_ddl|**int**|指示发布是否支持架构复制。 **1**指示复制在发布服务器上执行的数据定义语言 (DDL) 语句, **0**指示不复制 DDL 语句。 有关详细信息，请参阅[对发布数据库进行架构更改](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。|  
|enabled_for_p2p|**int**|表示发布是否可用于对等复制拓扑。 **1**指示发布支持对等复制。 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。|  
|publish_local_changes_only|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**int**|指定发布是否支持非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。 如果值为**1** , 则表示支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]非订阅服务器。 值**0**表示仅[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持订阅服务器。 有关详细信息，请参阅 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。|  
|enabled_for_p2p_conflictdetection|**int**|指定分发代理是否为针对对等复制启用的发布检测冲突。 如果值为**1** , 则表示检测到冲突。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
|originator_id|**int**|指定对等拓扑中某个节点的 ID。 如果**enabled_for_p2p_conflictdetection**设置为**1**, 则此 ID 用于冲突检测。 有关已经使用过的 ID 的列表，请查询 [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 系统表。|  
|p2p_continue_onconflict|**int**|指定检测到冲突时分发代理是否继续处理更改。 如果值为**1** , 则表示代理将继续处理更改。<br /><br /> 请注意, 我们建议使用默认值**0**。 **\* \* \* \*** 如果将此选项设置为**1**, 则分发代理尝试通过应用具有最高发起方 ID 的节点的冲突行来聚合拓扑中的数据。 此方法不保证将会收敛。 您应确保检测到冲突之后拓扑保持一致。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)中的“处理冲突”。|  
|allow_partition_switch|**int**|指定是否更改表 ...SWITCH 语句可针对已发布的数据库执行。 有关详细信息，请参阅[复制已分区表和索引](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。|  
|replicate_partition_switch|**int**|指定是否更改表 ...应将对已发布数据库执行的 SWITCH 语句复制到订阅服务器。 仅当*allow_partition_switch*设置为**1**时, 此选项才有效。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或**1** (失败)  
  
## <a name="remarks"></a>备注  
 sp_helppublication 用于快照复制和事务复制。  
  
 sp_helppublication 将返回执行此过程的用户所拥有的所有发布的信息。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有发布服务器上的 sysadmin 固定服务器角色成员或发布数据库上的 db_owner 固定数据库角色成员，或者发布访问列表 (PAL) 中的用户才能执行 sp_helppublication。  
  
 对于非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器, 只有分发服务器上 sysadmin 固定服务器角色的成员或分发数据库上的 db_owner 固定数据库角色的成员, 或者 PAL 中的用户可以执行 sp_helppublication。  
  
## <a name="see-also"></a>请参阅  
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
