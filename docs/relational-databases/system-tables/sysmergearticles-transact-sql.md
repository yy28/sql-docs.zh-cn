---
title: sysmergearticles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sysmergearticles
- sysmergearticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergearticles system table
ms.assetid: e9b1648e-4660-4688-9f56-18b2baf7228c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 660b42ef3864e5c61d51edfc33c073b804237f45
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47712565"
---
# <a name="sysmergearticles-transact-sql"></a>sysmergearticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本地数据库中定义的每个合并项目都在表中占一行。 该表存储在发布数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|项目的名称。|  
|**类型**|**tinyint**|指示项目类型，可以为下列类型之一：<br /><br /> **10** = 表。<br /><br /> **32** = 存储过程 （仅限架构）。<br /><br /> **64** = 视图或索引视图 （仅限架构）。<br /><br /> **128** = 用户定义函数 （仅限架构）。<br /><br /> **160** = 同义词 （仅限架构）。|  
|**objid**|**int**|对象标识符。|  
|**sync_objid**|**int**|表示同步数据集的视图的对象 ID。|  
|**view_type**|**tinyint**|视图类型：<br /><br /> **0** = 不是视图; 使用所有基对象。<br /><br /> **1** = 永久视图。<br /><br /> **2** = 临时视图。|  
|**artid**|**uniqueidentifier**|给定项目的唯一标识号。|  
|**description**|**nvarchar(255)**|项目的简要说明。|  
|**pre_creation_command**|**tinyint**|在订阅数据库中创建项目时将执行的默认操作：<br /><br /> **0 =** 无-如果表已存在于订阅服务器中，不执行任何操作。<br /><br /> **1** = 删除-删除该表，然后重新创建它。<br /><br /> **2** = 删除-发出基于子集筛选器中的 WHERE 子句的 delete 命令。<br /><br /> **3** = 截断-与相同**2**，但会删除页而非行。 不过，不要使用 WHERE 子句。|  
|**pubid**|**uniqueidentifier**|当前项目所属发布的 ID。|  
|**昵称**|**int**|项目标识的别名映射。|  
|**column_tracking**|**int**|指示是否对项目执行列跟踪。|  
|**status**|**tinyint**|指示项目的状态，可以为下列状态之一：<br /><br /> **1** = Unsynced-用于发布表的初始处理脚本将在下一步次运行快照代理运行。<br /><br /> **2** = 活动-用于发布表的初始处理脚本已运行。<br /><br /> **5** = new_inactive-内容待定要添加。<br /><br /> **6** = new_active-内容待定要添加。|  
|**conflict_table**|**sysname**|包含当前项目冲突记录的本地表的名称。 该表仅用于提供信息，其内容可以由自定义冲突解决例程修改或删除，或直接由系统管理员修改或删除。|  
|**creation_script**|**nvarchar(255)**|此项目的创建脚本。|  
|**conflict_script**|**nvarchar(255)**|此项目的冲突脚本。|  
|**article_resolver**|**nvarchar(255)**|此项目的自定义行级冲突解决程序。|  
|**ins_conflict_proc**|**sysname**|用来写入到的冲突**conflict_table**。|  
|**insert_proc**|**sysname**|由默认冲突解决程序用来在同步过程中插入行的过程。|  
|**update_proc**|**sysname**|由默认冲突解决程序用来在同步过程中更新行的过程。|  
|**select_proc**|**sysname**|自动生成的存储过程的名称，合并代理使用该存储过程来完成锁定并查找项目的行和列。|  
|**metadata_select_proc**|**sysname**|自动生成用于访问合并复制系统表中的元数据的存储过程的名称。|  
|**delete_proc**|**sysname**|由默认冲突解决程序用来在同步过程中删除行的过程。|  
|**schema_option**|**binary(8)**|有关支持的值*schema_option*，请参阅[sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。|  
|**destination_object**|**sysname**|在订阅服务器上创建的表的名称。|  
|**destination_owner**|**sysname**|目标对象的所有者的名称。|  
|**resolver_clsid**|**nvarchar(50)**|自定义冲突解决程序的 ID。|  
|**subset_filterclause**|**nvarchar(1000)**|此项目的筛选子句。|  
|**missing_col_count**|**int**|缺少的列数。|  
|**missing_cols**|**varbinary(128)**|缺少的列的位图。|  
|**excluded_cols**|**varbinary(128)**|当项目发送到订阅服务器时，从项目中排除的列的位图。|  
|**excluded_col_count**|**int**|排除的列数。|  
|**columns**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary(128)**|已从源表中删除的列的位图。|  
|**resolver_info**|**nvarchar(255)**|存储自定义冲突解决程序所需的其他信息。|  
|**view_sel_proc**|**nvarchar(290)**|存储过程的名称，合并代理使用此存储过程初始填充动态筛选发布中的项目，并且枚举在任何筛选发布中的更改的行。|  
|**gen_cur**|**int**|对项目基表所做的本地更改的生成数。|  
|**vertical_partition**|**int**|指定是否对表项目启用列筛选。 **0**指示没有垂直筛选并且发布所有列。|  
|**identity_support**|**int**|指定是否启用自动标识范围处理。 **1**表示启用标识范围处理，并**0**表示没有标识范围支持。|  
|**before_image_objid**|**int**|跟踪表对象 ID。 通过创建发布时，跟踪表将包含某些键列值*@keep_partition_changes*  =  **true**。|  
|**before_view_objid**|**int**|视图表的对象 ID。 视图所在的表用于在删除或更新行之前跟踪行是否属于特定的订阅服务器。 应用仅发布创建与*@keep_partition_changes*  =  **，则返回 true。**|  
|**verify_resolver_signature**|**int**|指定在合并复制中使用冲突解决程序之前是否验证数字签名：<br /><br /> **0** = 不验证签名。<br /><br /> **1** = 验证签名，以确定它是否来自可信来源。|  
|**allow_interactive_resolver**|**bit**|指定是否对项目启用交互式冲突解决程序。 **1**指定对项目使用交互式冲突解决程序。|  
|**fast_multicol_updateproc**|**bit**|指定是否已启用合并代理来使用一条 UPDATE 语句在同一行的多个列中应用更改。<br /><br /> **0** = 为每个列的独立更新已更改的问题。<br /><br /> **1** = 发出 UPDATE 语句，这会导致要到在一个语句中的多个列进行更新。|  
|**check_permissions**|**int**|当合并代理将更改应用于发布服务器时要验证的表级权限的位图。 *check_permissions*可以具有下列值之一：<br /><br /> **0x00 =** 不检查权限。<br /><br /> **0x10 =** 检查发布服务器上的权限，才能上载订阅服务器上的插入。<br /><br /> **0x20 =** 检查发布服务器上的权限，才能上载订阅服务器上所做的更新。<br /><br /> **0x40 =** 可以上载订阅服务器上的 delete 操作之前检查发布服务器上的权限。|  
|**maxversion_at_cleanup**|**int**|清除了元数据的最高版本。|  
|**processing_order**|**int**|指示合并发布; 中的项目的处理顺序其中的值**0**指示项目未排序，并从最低到最高值的顺序处理项目。 如果两个项目具有相同值，将对其进行并发处理。 有关详细信息，请参阅[指定合并项目的处理顺序](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)。|  
|**upload_options**|**tinyint**|定义对具有客户端订阅的订阅服务器上所进行更新的限制，可以为下列值之一：<br /><br /> **0** = 上具有客户端订阅的订阅服务器所做的更新没有限制; 所有更改都上载到发布服务器。<br /><br /> **1** = 允许使用客户端订阅，订阅服务器上进行更改，但不是将其上载到发布服务器。<br /><br /> **2** = 不允许在具有客户端订阅的订阅服务器的更改。<br /><br /> 有关详细信息，请参阅[使用仅下载项目优化合并复制性能](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。|  
|**published_in_tran_pub**|**bit**|指示合并发布中的项目也将在事务发布中发布。<br /><br /> **0** = 项目不在事务项目中发布。<br /><br /> **1** = 事务项目中也发布了一文。|  
|**轻型**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|内容待定。|  
|**delete_tracking**|**bit**|指示是否复制删除内容。<br /><br /> **0** = 不复制删除<br /><br /> **1** = 复制删除，这是合并复制的默认行为。<br /><br /> 时的值*delete_tracking*是**0**、 必须在发布服务器，手动删除在订阅服务器中删除的行和删除发布服务器上的行必须手动删除在订阅服务器。<br /><br /> 注意： 的值**0**导致非收敛性。|  
|**compensate_for_errors**|**bit**|指示在同步过程中遇到错误时是否执行补救措施。<br /><br /> **0** = 补救操作已被禁用。<br /><br /> **1** = 无法应用于订阅服务器或发布服务器通常会导致采取补救措施来撤消这些更改，这是合并复制的默认行为的更改。<br /><br /> 注意： 的值**0**导致非收敛性。|  
|**pub_range**|**bigint**|发布服务器标识范围大小。|  
|**范围**|**bigint**|将分配到调整中订阅服务器的连续标识值的大小。|  
|**threshold**|**int**|标识范围阈值百分比。|  
|**stream_blob_columns**|**bit**|指定在复制二进制大型对象列时是否使用数据流优化。 **1**意味着尝试进行优化。|  
|**preserve_rowguidcol**|**bit**|指示复制是否使用现有 rowguid 列。 值为**1**表示使用现有 ROWGUIDCOL 列。 **0**意味着复制添加了 ROWGUIDCOL 列。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)  
  
  
