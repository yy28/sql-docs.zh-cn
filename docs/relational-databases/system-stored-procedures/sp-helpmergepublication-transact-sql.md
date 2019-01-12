---
title: sp_helpmergepublication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepublication
- sp_helpmergepublication_TSQL
helpviewer_keywords:
- sp_helpmergepublication
ms.assetid: dfe1e1e1-9a65-406a-aced-6385a078e135
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 580ac26d2478de1f42800d6f8d6704f26bc6fff4
ms.sourcegitcommit: 170c275ece5969ff0c8c413987c4f2062459db21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2019
ms.locfileid: "54226644"
---
# <a name="sphelpmergepublication-transact-sql"></a>sp_helpmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关合并发布的信息。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpmergepublication [ [ @publication = ] 'publication' ]  
    [ , [ @found = ] 'found' OUTPUT ]  
    [ , [ @publication_id = ] 'publication_id' OUTPUT ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>参数  
 [ @publication **=** ] **'**_发布_  
 发布的名称。 *发布*是**sysname**，默认值为**%**，它返回当前数据库中所有合并发布的相关信息。  
  
 [ @found **=** ] **'***找到***'** 输出  
 用于指示返回行的标志。 *找到*是**int**而且是 OUTPUT 参数，默认值为 NULL。 **1**指示已找到发布。 **0**指示找不到该发布。  
  
 [ @publication_id **=**] **'***publication_id***'** 输出  
 发布的标识号。 *publication_id*是**uniqueidentifier**而且是 OUTPUT 参数，默认值为 NULL。  
  
 [ @reserved **=**] **'***保留***’**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *保留*是**nvarchar(20)**，默认值为 NULL。  
  
 [ @publisher **=** ] **'***发布服务器***’**  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。  
  
 [@publisher_db **=** ] **'***publisher_db***’**  
 发布数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|发布在结果集列表中的连续顺序。|  
|NAME|**sysname**|发布的名称。|  
|description|**nvarchar(255)**|对发布的说明。|  
|status|**tinyint**|指示发布数据何时可用。|  
|retention|**int**|用于保存对发布中项目所做更改的元数据的时间量。 此时间段单位可以为天、星期、月或年。 有关单位的信息，请参阅 retention_period_unit 列。|  
|sync_mode|**tinyint**|该发布的同步模式：<br /><br /> **0** = 本机大容量复制程序 (**bcp**实用程序)<br /><br /> **1** = 字符大容量复制|  
|allow_push|**int**|确定是否可以为给定发布创建推送订阅。 **0**表示不允许推送订阅。|  
|allow_pull|**int**|确定是否可以为给定发布创建请求订阅。 **0**表示不允许请求订阅。|  
|allow_anonymous|**int**|确定是否可以为给定发布创建匿名订阅。 **0**表示不允许匿名订阅。|  
|centralized_conflicts|**int**|确定是否将冲突记录存储在给定发布服务器上：<br /><br /> **0** = 均存储的冲突记录的发布服务器和订阅服务器导致冲突。<br /><br /> **1** = 所有冲突记录存储在发布服务器。|  
|priority|**float(8)**|环回订阅的优先级。|  
|snapshot_ready|**tinyint**|指示该发布的快照是否可以使用：<br /><br /> **0** = 快照便可供使用。<br /><br /> **1** = 快照尚不可供使用。|  
|publication_type|**int**|发布的类型：<br /><br /> **0** = 快照。<br /><br /> **1** = 事务。<br /><br /> **2** = 合并。|  
|pubid|**uniqueidentifier**|该发布的唯一标识符。|  
|snapshot_jobid|**binary(16)**|快照代理的作业 ID。 若要获取的快照作业中的条目[sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)系统表中，您必须将转换到该十六进制值**uniqueidentifier**。|  
|enabled_for_internet|**int**|确定是否为 Internet 启用发布。 如果**1**，为发布的同步文件放入`C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\Ftp`目录。 用户必须创建文件传输协议 (FTP) 目录。 如果**0**，该发布无法进行 Internet 访问权限。|  
|dynamic_filter|**int**|指示是否使用参数化行筛选器。 **0**表示不使用参数化的行筛选器。|  
|has_subscription|**bit**|指示发布是否具有任何订阅。 **0**意味着当前不存在对此发布的订阅。|  
|snapshot_in_default_folder|**bit**|指定快照文件是否存储在默认文件夹中。<br /><br /> 如果**1**，可以在默认文件夹中找到快照文件。<br /><br /> 如果**0**，快照文件存储在指定的备用位置**alt_snapshot_folder**。 备用位置可以是另一台服务器、 网络驱动器或可移动媒体 （如 CD-ROM 或可移动磁盘）。 也可以将快照文件保存到 FTP 站点以供订阅方以后检索。<br /><br /> 注意：此参数可以是 true，仍有一个位置**alt_snapshot_folder**参数。 这个组合指定将快照文件存储在默认位置和替代位置。|  
|alt_snapshot_folder|**nvarchar(255)**|指定快照的备用文件夹的位置。|  
|pre_snapshot_script|**nvarchar(255)**|指定一个指向 **.sql**应用在订阅服务器上的快照时，合并代理运行之前复制的任何的对象文件的脚本。|  
|post_snapshot_script|**nvarchar(255)**|指定一个指向 **.sql**文件的合并代理所有运行的其他复制对象脚本和数据已应用在初始同步过程。|  
|compress_snapshot|**bit**|指定写入到的快照**alt_snapshot_folder**位置将被压缩到[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。|  
|ftp_address|**sysname**|分发服务器的 FTP 服务网络地址。 指定合并代理拾取的发布快照文件的位置。|  
|ftp_port|**int**|分发服务器 FTP 服务的端口号。 **ftp_port**的默认值为**21**。 指定供合并代理拾取的发布快照文件所在的位置。|  
|ftp_subdirectory|**nvarchar(255)**|指定当使用 FTP 传递快照时，快照文件供合并代理拾取的位置。|  
|ftp_login|**sysname**|用于连接到 FTP 服务用户名。|  
|conflict_retention|**int**|指定保留冲突的保持期（天）。 指定的天数过后，冲突行将从冲突表中清除掉。|  
|keep_partition_changes|**int**|指定是否对此发布的同步进行优化。 **keep_partition_changes**的默认值为**0**。 值为**0**意味着不优化同步，并且一个分区中的数据更改时验证发送到所有订阅服务器的分区。<br /><br /> **1**表示优化同步，订阅者，已更改的分区内具有行受影响。<br /><br /> 注意：默认情况下，合并发布使用预计算分区，与该选项相比，它提供更大程度的优化。 有关详细信息，请参阅[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)并[使用预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。|  
|allow_subscription_copy|**int**|指定是否已启用复制订阅该发布的订阅数据库的功能。 值为**0**表示不允许复制。|  
|allow_synctoalternate|**int**|指定是否允许备用同步伙伴与该发布服务器同步。 值为**0**意味着不允许使用同步伙伴。|  
|validate_subscriber_info|**nvarchar(500)**|列出用于检索订阅服务器信息和验证订阅服务器上的参数化行筛选条件的函数。 有助于验证信息分区是否与每个合并一致。|  
|backward_comp_level|**int**|数据库兼容级别，可以为下列值之一：<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_activedirectory|**bit**|指定是否将发布信息发布到 Active Directory。 值为**0**意味着发布信息不可用于从 Active Directory。<br /><br /> 已不推荐使用该参数，支持该参数只是为了让脚本能够向后兼容。 您不再能够向 Active Directory 中添加发布信息。|  
|max_concurrent_merge|**int**|并发合并进程数。 如果**0**，到在任何给定时间运行的并发合并进程数没有限制。|  
|max_concurrent_dynamic_snapshots|**int**|针对合并发布可以运行的最大并发已筛选数据快照会话数。 如果**0**，可以针对任何给定时间上的发布同时运行的并发筛选的数据快照会话的最大数目没有限制。|  
|use_partition_groups|**int**|确定是否使用预计算分区。 值为**1**使用预计算分区的方式。|  
|num_of_articles|**int**|发布中的项目个数。|  
|replicate_ddl|**int**|表示是否复制对已发布表的架构更改。 值为**1**意味着复制架构更改。|  
|publication_number|**smallint**|分配给该发布的编号。|  
|allow_subscriber_initiated_snapshot|**bit**|确定订阅服务器是否可以启动已筛选数据快照生成进程。 值为**1**意味着订阅服务器可以启动快照进程。|  
|allow_web_synchronization|**bit**|确定是否为 Web 同步启用发布。 值为**1**表示启用 Web 同步。|  
|web_synchronization_url|**nvarchar(500)**|用于 Web 同步的 Internet URL。|  
|allow_partition_realignment|**bit**|确定在发布服务器上的行修改导致该发布服务器更改其分区时是否将删除指令发送到订阅服务器。 值为**1**意味着删除将发送到订阅服务器上。  有关详细信息，请参阅[sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。|  
|retention_period_unit|**tinyint**|指定用于定义保持期的单位。 这可以是下列值之一：<br /><br /> **0** = 天<br /><br /> **1** = 周<br /><br /> **2** = 月<br /><br /> **3** = 年|  
|has_downloadonly_articles|**bit**|指示属于发布的所有项目是否为仅用于下载的项目。 值为**1**指示仅下载项目。|  
|decentralized_conflicts|**int**|指示是否在导致冲突的订阅服务器上存储冲突记录。 值为**0**指示不在订阅服务器上存储冲突记录。 值为 1 表示在订阅服务器上存储冲突记录。|  
|generation_leveling_threshold|**int**|指定生成中包含的更改数。 生成是指已传递给发布服务器或订阅服务器的更改集合|  
|automatic_reinitialization_policy|**bit**|指示是否在进行自动重新初始化之前从订阅服务器上载更改。 值为**1**指示自动重新初始化之前从订阅服务器上载更改。 值为 0 表示在自动重新初始化之前不上载更改。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 sp_helpmergepublication 用于合并复制。  
  
## <a name="permissions"></a>权限  
 发布的发布访问列表的成员可以针对该发布执行 sp_helpmergepublication。 发布数据库中的 db_owner 固定数据库角色成员可以针对所有发布的信息执行 sp_helpmergepublication。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_helpmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-helpmergepublication-_1.sql)]  
  
## <a name="see-also"></a>请参阅  
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
