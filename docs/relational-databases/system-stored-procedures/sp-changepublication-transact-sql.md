---
title: sp_changepublication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication
- sp_changepublication_TSQL
helpviewer_keywords:
- sp_changepublication
ms.assetid: c36e5865-25d5-42b7-b045-dc5036225081
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c715b7af71fc98df34036daf9311f1ed32b1c772
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689725"
---
# <a name="spchangepublication-transact-sql"></a>sp_changepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改发布的属性。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_changepublication [ [ @publication = ] 'publication' ]  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication =** ] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，默认值为 NULL。  
  
 [  **@property =** ] **'***属性*****  
 要更改的发布属性。 *属性*是**nvarchar(255)**。  
  
 [  **@value =** ] **'***值*****  
 新属性值。 *值*是**nvarchar(255)**，默认值为 NULL。  
  
 下表说明了可以更改的发布属性以及对这些属性值的限制。  
  
|“属性”|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|可以为给定发布创建匿名订阅并*immediate_sync*也必须**true**。 对于对等发布，无法更改此属性。|  
||**false**|不能为给定发布创建匿名订阅。 对于对等发布，无法更改此属性。|  
|**allow_initialize_from_backup**|**true**|订阅服务器可以从备份而非初始快照中初始化对此发布的订阅。 此属性不能更改为非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布。|  
||**false**|订阅服务器必须使用初始快照。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**allow_partition_switch**|**true**|可以对已发布的数据库执行 ALTER TABLE…SWITCH 语句。 有关详细信息，请参阅[复制已分区表和索引](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。|  
||**false**|不能对已发布的数据库执行 ALTER TABLE…SWITCH 语句。|  
|**allow_pull**|**true**|给定的发布允许请求订阅。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
||**false**|给定的发布不允许进行请求订阅。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**allow_push**|**true**|给定的发布允许推送订阅。|  
||**false**|给定的发布不允许进行推送订阅。|  
|**allow_subscription_copy**|**true**|启用复制订阅该发布的数据库的功能。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
||**false**|禁用复制订阅该发布的数据库的功能。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**alt_snapshot_folder**||快照的备用文件夹的位置。|  
|**centralized_conflicts**|**true**|在发布服务器上存储冲突记录。 只有在没有任何活动订阅的情况下才能更改此属性。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
||**false**|冲突记录同时存储在导致冲突的发布服务器和订阅服务器上。 只有在没有任何活动订阅的情况下才能更改此属性。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**compress_snapshot**|**true**|备用快照文件夹中的快照压缩为 .cab 文件格式。 不能压缩默认快照文件夹中的快照。|  
||**false**|不压缩快照，这是复制的默认行为。|  
|**conflict_policy**|**pub wins**|更新订阅服务器的冲突解决策略，此时发布服务器入选冲突。 只有在没有活动订阅时才能更改该属性。 Oracle 发布服务器不支持。|  
||**sub reinit**|要更新订阅服务器，如果出现冲突，则必须重新初始化订阅。 只有在没有活动订阅时才能更改该属性。 Oracle 发布服务器不支持。|  
||**sub wins**|更新订阅服务器的冲突解决策略，此时订阅服务器入选冲突。 只有在没有活动订阅时才能更改该属性。 Oracle 发布服务器不支持。|  
|**conflict_retention**||**int** ，指定冲突保持期，以天为单位。 默认保持期为 14 天。 **0**表示需要清除没有冲突。 Oracle 发布服务器不支持。|  
|**description**||用于说明发布的可选项。|  
|**enabled_for_het_sub**|**true**|启用发布以支持非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。 **enabled_for_het_sub**存在对发布的订阅时不能更改。 您可能需要执行[复制存储过程 (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)遵守以下要求，然后设置**enabled_for_het_sub**为 true:<br /> - **allow_queued_tran**必须是**false**。<br /> - **allow_sync_tran**必须是**false**。<br /> 更改**enabled_for_het_sub**到**true**可能会更改现有发布设置。 有关详细信息，请参阅 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
||**false**|发布不支持非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**enabled_for_internet**|**true**|为 Internet 启用发布，此时可以使用文件传输协议 (FTP) 向订阅服务器传输快照文件。 发布的同步文件将放入以下目录中：C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\ftp。 *ftp_address*不能为 NULL。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
||**false**|不为 Internet 启用发布。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**enabled_for_p2p**|**true**|发布支持对等复制。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。<br /> 若要设置**enabled_for_p2p**到**true**，以下限制适用：<br /> - **allow_anonymous**必须是**false**<br /> - **allow_dts**必须是**false**。<br /> - **allow_initialize_from_backup**必须是 **，则返回 true**<br /> - **allow_queued_tran**必须是**false**。<br /> - **allow_sync_tran**必须是**false**。<br /> - **enabled_for_het_sub**必须是**false**。<br /> - **independent_agent**必须是**true**。<br /> - **repl_freq**必须是**连续**。<br /> - **replicate_ddl**必须是**1**。|  
||**false**|发布不支持对等复制。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**ftp_address**||发布快照文件的可访问 FTP 地址。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**ftp_login**||用于连接到 FTP 服务的用户名，允许使用值 ANONYMOUS。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**ftp_password**||用于连接到 FTP 服务的用户名的密码。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**ftp_port**||分发服务器的 FTP 服务端口号。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**ftp_subdirectory**||指定创建快照文件的位置如果发布支持使用 FTP 传播快照。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
|**immediate_sync**|**true**|每次运行快照代理时创建或重新创建发布的同步文件。 如果订阅前已完成一次快照代理，则订阅服务器可以在订阅后立即收到同步文件。 新订阅将获取最近一次执行快照代理所生成的最新同步文件。 *independent_agent*也必须**true**。 请参阅下面的其他信息的备注，了解**immediate_sync**。|  
||**false**|仅当有新订阅时，才创建同步文件。 快照代理已启动并完成之前，订阅服务器无法订阅之后接收的同步文件。|  
|**independent_agent**|**true**|发布具有专用的分发代理。|  
||**false**|发布使用共享分发代理，每一对发布/订阅数据库共享一个代理。|  
|**p2p_continue_onconflict**|**true**|检测到冲突时，分发代理继续处理更改。<br /> **注意：** 我们建议你使用的默认值`FALSE`。 如果此选项设置为`TRUE`，分发代理尝试应用来自具有最高的原始发件人 ID 的节点的冲突行收敛拓扑中的数据 此方法不保证将会收敛。 您应确保检测到冲突之后拓扑保持一致。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)中的“处理冲突”。|  
||**false**|检测到冲突时，分发代理将停止处理更改。|  
|**post_snapshot_script**||指定在初始同步过程中应用了其他所有复制对象脚本和数据后，分发代理所运行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件的位置。|  
|**pre_snapshot_script**||指定在初始同步过程中应用其他所有复制对象脚本和数据之前，分发代理所运行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件的位置。|  
|**publish_to_ActiveDirectory**|**true**|已不推荐使用该参数，支持该参数只是为了让脚本能够向后兼容。 不能再向 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中添加发布信息。|  
||**false**|将发布信息从 Active Directory 上删除。|  
|**queue_type**|**sql**|使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储事务。 只有在没有活动订阅时才能更改该属性。<br /><br /> 请注意： 支持使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]消息队列已停止使用。 指定的值**msmq**有关*值*会导致出现错误。|  
|**repl_freq**|**连续**|发布所有基于日志的事务的输出。|  
||**快照**|仅发布计划的同步事件。|  
|**replicate_ddl**|**1**|复制在发布服务器上执行的数据定义语言 (DDL) 语句。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。|  
||**0**|不复制 DDL 语句。 对于非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布，无法更改此属性。 使用对等复制时，无法禁用架构更改复制功能。|  
|**replicate_partition_switch**|**true**|应将对已发布的数据库执行的 ALTER TABLE…SWITCH 语句复制到订阅服务器。 此选项才有效才*allow_partition_switch*设置为 TRUE。 有关详细信息，请参阅[复制已分区表和索引](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。|  
||**false**|不应将 ALTER TABLE…SWITCH 语句复制到订阅服务器。|  
|**保留期**||**int**表示的保持期，以小时为单位，订阅活动。 如果订阅在保持期内不活动，则将其删除。|  
|**snapshot_in_defaultfolder**|**true**|在默认快照文件夹中存储快照文件。 如果*alt_snapshot_folder*还指定，则快照文件存储在默认和备用位置。|  
||**false**|快照文件存储在指定的备用位置*alt_snapshot_folder*。|  
|**status**|**活动**|发布创建后，发布数据立即可用于订阅服务器。 Oracle 发布服务器不支持。|  
||**非活动状态**|发布创建后，发布数据不可用于订阅服务器。 Oracle 发布服务器不支持。|  
|**sync_method**|**native**|同步订阅时，使用所有表的本机模式大容量复制输出。|  
||**character**|同步订阅时，使用所有表的字符模式大容量复制输出。|  
||**并发**|在快照生成期间生成所有表的本机模式大容量复制程序输出，但不锁定表。 对快照复制无效。|  
||**concurrent_c**|在快照生成期间生成所有表的字符模式大容量复制程序输出，但不锁定表。 对快照复制无效。|  
|**任务 id**||不推荐使用该属性，也不再支持该属性。|  
|**allow_drop**|**true**|使`DROP TABLE`DLL 的支持文章都是事务复制的一部分。 支持的最低版本： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2 或更高版本和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]Service Pack 1 或更高版本。 其他参考： [KB 3170123](https://support.microsoft.com/en-us/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)|
||**false**|禁用`DROP TABLE`属于事务复制的项目的支持 DLL。 这是**默认**此属性的值。|
|**NULL** （默认值）||返回支持的值的列表*属性*。|  
  
[  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 确认此存储过程所执行的操作是否会使现有快照失效。 *force_invalidate_snapshot*是**位**，默认值为**0**。  
  - **0**指定对项目的更改不会导致快照无效。 如果该存储过程检测到更改确实需要新的快照，则会发生错误，并且不进行任何更改。  
  - **1**指定对项目的更改可能导致快照无效。 如果有现有订阅需要新快照，该值授予将现有快照标记为过时快照的权限，并生成新快照。   
有关在更改时需要生成新快照的属性，请参阅“备注”部分。  
  
[ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 确认此存储过程所执行的操作可能需要重新初始化现有订阅。 *force_reinit_subscription*是**位**默认值为**0**。  
  - **0**指定对项目的更改不会导致重新初始化订阅。 如果该存储过程检测到更改将需要重新初始化现有订阅，则会发生错误，并且不进行任何更改。  
  - **1**指定对项目的更改会导致现有订阅重新初始化，并授予重新初始化订阅发生的权限。  
  
[ **@publisher** = ] **'***publisher***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
  > [!NOTE]  
  >  *发布服务器*在更改项目属性时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changepublication**快照复制和事务复制中使用。  
  
 更改后的任何以下属性，必须生成新快照，并且必须指定的值**1**有关*force_invalidate_snapshot*参数。  
-   **alt_snapshot_folder**  
-   **compress_snapshot**  
-   **enabled_for_het_sub**  
-   **ftp_address**  
-   **ftp_login**  
-   **ftp_password**  
-   **ftp_port**  
-   **ftp_subdirectory**  
-   **post_snapshot_script**  
-   **pre_snapshot_script**  
-   **snapshot_in_defaultfolder**  
-   **sync_mode**  
  
列出在 Active Directory 中使用的发布对象**publish_to_active_directory**参数，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必须已在 Active Directory 中创建对象。  
  
## <a name="impact-of-immediate-sync"></a>立即同步的影响  
 启用后立即同步，即使没有任何订阅生成初始快照后立即跟踪日志中的所有更改。 客户使用的备份以添加新的对等节点时，将使用日志记录的更改。 还原备份后，对等方是与创建备份后发生的任何其他更改同步。 由于在分发数据库中跟踪命令，因此同步逻辑可以查找最后一个备份 LSN，并使用此作为起点，了解该命令最大保持期内执行备份时才可用。 (默认值最小保持期为 0 小时，最大保持期为 24 小时。)  
  
 关闭立即同步时，至少保持最小保持期和已复制的所有事务立即清除更改。 如果已关闭立即同步并为其配置了默认保持期，很可能会清理在进行备份后所需要的更改，并且不会正确初始化新的对等节点。 剩下的唯一选项是使拓扑静止。 将立即同步设置为打开可提供更大的灵活性，并且是用于 P2P 复制的推荐设置。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_changepublication](../../relational-databases/replication/codesnippet/tsql/sp-changepublication-tra_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_changepublication**。  
  
## <a name="see-also"></a>请参阅  
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [更改发布和项目属性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_droppublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
