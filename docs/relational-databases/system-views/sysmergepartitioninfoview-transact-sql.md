---
title: sysmergepartitioninfoview (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepartitioninfoview
- sysmergepartitioninfoview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfoview view
ms.assetid: 714e2935-1bc7-4901-aea2-64b1bbda03d6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 40b1ebc5319c13b5aa84a28e1a5c5546dd62bd03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094826"
---
# <a name="sysmergepartitioninfoview-transact-sql"></a>sysmergepartitioninfoview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysmergepartitioninfoview**视图公开表项目的分区信息。 此视图存储在发布服务器的发布数据库以及订阅服务器的订阅数据库中。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|项目的名称。|  
|**type**|**tinyint**|指示项目类型，可以为下列类型之一：<br /><br /> **0x0a** = 表。<br /><br /> **0x20** = 纯过程架构。<br /><br /> **0x40** = 仅视图架构或仅限索引的视图架构。<br /><br /> **0x80** = 仅函数架构。|  
|**objid**|**int**|已发布对象的标识符。|  
|**sync_objid**|**int**|表示同步数据集的视图的对象 ID。|  
|**view_type**|**tinyint**|视图类型：<br /><br /> **0** = 不是视图; 使用所有基对象。<br /><br /> **1** = 永久视图。<br /><br /> **2** = 临时视图。|  
|**artid**|**uniqueidentifier**|给定项目的唯一标识号。|  
|**description**|**nvarchar(255)**|项目的简要说明。|  
|**pre_creation_command**|**tinyint**|在订阅数据库中创建项目时将执行的默认操作：<br /><br /> **0** = 无-如果表已存在于订阅服务器上，执行任何操作。<br /><br /> **1** = 删除-删除该表，然后重新创建它。<br /><br /> **2** = 删除-删除基于子集筛选器中的 WHERE 子句的问题。<br /><br /> **3** = 截断-2，但是删除页而不是行相同。 不过，不要使用 WHERE 子句。|  
|**pubid**|**uniqueidentifier**|当前项目所属发布的 ID。|  
|**昵称**|**int**|项目标识的别名映射。|  
|**column_tracking**|**int**|指示是否为项目执行列跟踪。|  
|**status**|**tinyint**|指示项目的状态，可以为下列状态之一：<br /><br /> **1** = Unsynced-用于发布表的初始处理脚本将在下一步次运行快照代理运行。<br /><br /> **2** = 活动-用于发布表的初始处理脚本已运行。|  
|**conflict_table**|**sysname**|包含当前项目冲突记录的本地表的名称。 该表仅用于提供信息，其内容可以由自定义冲突解决例程修改或删除，或直接由系统管理员修改或删除。|  
|**creation_script**|**nvarchar(255)**|此项目的创建脚本。|  
|**conflict_script**|**nvarchar(255)**|此项目的冲突脚本。|  
|**article_resolver**|**nvarchar(255)**|该项目的冲突解决程序。|  
|**ins_conflict_proc**|**sysname**|用于向冲突表写入冲突信息的过程。|  
|**insert_proc**|**sysname**|用于在同步过程中插入行的过程。|  
|**update_proc**|**sysname**|用于在同步过程中更新行的过程。|  
|**select_proc**|**sysname**|自动生成的存储过程的名称，合并代理使用该存储过程完成锁定并查找项目的行和列。|  
|**metadata_select_proc**|**sysname**|自动生成的存储过程的名称，该存储过程用于访问合并复制系统表中的元数据。|  
|**delete_proc**|**sysname**|用于在同步过程中删除行的过程。|  
|**schema_option**|**binary(8)**|给定项目的架构生成选项位图。 有关支持上的信息*schema_option*值，请参阅[sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。|  
|**destination_object**|**sysname**|在订阅服务器上创建的表的名称。|  
|**destination_owner**|**sysname**|目标对象的所有者的名称。|  
|**resolver_clsid**|**nvarchar(50)**|自定义冲突解决程序的 ID。 对于业务逻辑处理程序，该值为 NULL。|  
|**subset_filterclause**|**nvarchar(1000)**|此项目的筛选子句。|  
|**missing_col_count**|**int**|项目中缺少的已发布列数。|  
|**missing_cols**|**varbinary(128)**|用于说明项目中的缺少列的位图。|  
|**excluded_cols**|**varbinary(128)**|已从项目中排除的列的位图。|  
|**excluded_col_count**|**int**|从项目中排除的列数。|  
|**columns**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary(128)**|用于说明从项目中删除的列的位图。|  
|**resolver_info**|**nvarchar(255)**|存储自定义冲突解决程序所需的其他信息。|  
|**view_sel_proc**|**nvarchar(290)**|存储过程的名称，合并代理使用该存储过程初始填充动态筛选发布中的项目，并枚举在任何筛选发布中的已更改行。|  
|**gen_cur**|**bigint**|生成项目基表的本地更改数。|  
|**vertical_partition**|**int**|指定是否对表项目启用列筛选。 **0**指示没有垂直筛选并且发布所有列。|  
|**identity_support**|**int**|指定是否启用自动标识范围处理。 **1**表示启用标识范围处理，并**0**表示没有标识范围支持。|  
|**before_image_objid**|**int**|跟踪表对象 ID。 当已对发布启用分区更改优化时，跟踪表将包含某些键列值。|  
|**before_view_objid**|**int**|视图表的对象 ID。 视图所在的表用于在删除或更新行之前跟踪行是否属于特定的订阅服务器。 仅当对发布启用了分区更改优化时才适用。|  
|**verify_resolver_signature**|**int**|指定在合并复制中使用冲突解决程序之前是否验证数字签名：<br /><br /> **0** = 不验证签名。<br /><br /> **1** = 验证签名，以确定它是否来自可信来源。|  
|**allow_interactive_resolver**|**bit**|指定是否对项目启用交互式冲突解决程序。 **1**意味着可以对项目使用交互式冲突解决程序。|  
|**fast_multicol_updateproc**|**bit**|指定是否已启用合并代理来使用一条 UPDATE 语句在同一行的多个列中应用更改。<br /><br /> **0** = 为每个列的独立更新已更改的问题。<br /><br /> **1** = 发出 UPDATE 语句，这会导致要到在一个语句中的多个列进行更新。|  
|**check_permissions**|**int**|当合并代理更改应用到发布服务器验证将为表级权限的位图。 *check_permissions*可以具有下列值之一：<br /><br /> **0x00** = 不检查权限。<br /><br /> **0x10** = 的检查发布服务器之前插入操作都在订阅服务器上的权限来上传。<br /><br /> **0x20** = 检查发布服务器上的权限，才能上载订阅服务器上所做的更新。<br /><br /> **0x40** = 可以上载订阅服务器上的 delete 操作之前检查发布服务器上的权限。|  
|**maxversion_at_cleanup**|**int**|合并代理下次运行时清除的最大生成。|  
|**processing_order**|**int**|指示合并发布; 中的项目的处理顺序其中的值**0**指示项目未排序，并且从最低到最高值的顺序处理项目。 如果两个项目具有相同值，将对其进行并发处理。 有关详细信息，请参阅[指定合并复制属性](../../relational-databases/replication/merge/specify-merge-replication-properties.md)。|  
|**upload_options**|**tinyint**|定义是否可以在订阅服务器上进行更改或从订阅服务器上载更改，可以为下列值之一：<br /><br /> **0** = 在订阅服务器上所做的更新没有限制; 所有更改都上载到发布服务器。<br /><br /> **1** = 允许在订阅服务器上，进行更改，但不是将其上载到发布服务器。<br /><br /> **2** = 不允许在订阅服务器上进行更改。|  
|**published_in_tran_pub**|**bit**|指示合并发布中的项目也将在事务发布中发布。<br /><br /> **0** = 项目不在事务项目中发布。<br /><br /> **1** = 事务项目中也发布了一文。|  
|**轻型**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|更新前表视图的 ID。|  
|**delete_tracking**|**bit**|指示是否复制删除。<br /><br /> **0** = 不复制删除。<br /><br /> **1** = 复制删除，这是合并复制的默认行为。<br /><br /> 时的值*delete_tracking*是**0**、 必须在发布服务器，手动删除在订阅服务器中删除的行和删除发布服务器上的行必须手动删除在订阅服务器。<br /><br /> 注意:值为**0**导致非收敛性。|  
|**compensate_for_errors**|**bit**|指示在同步期间遇到错误时是否采取补救措施。<br /><br /> **0** = 补救操作已被禁用。<br /><br /> **1** = 无法应用于订阅服务器或发布服务器通常会导致采取补救措施来撤消这些更改，这是合并复制的默认行为的更改。<br /><br /> 注意:值为**0**导致非收敛性。|  
|**pub_range**|**bigint**|发布服务器标识范围大小。|  
|**范围**|**bigint**|将分配到调整中订阅服务器的连续标识值的大小。|  
|**threshold**|**int**|标识范围阈值百分比。|  
|**stream_blob_columns**|**bit**|指示是否使用针对二进制大型对象列的流式优化。 **1**意味着尝试进行优化。|  
|**preserve_rowguidcol**|**bit**|指示复制是否使用现有 rowguid 列。 值为**1**表示使用现有 ROWGUIDCOL 列。 **0**意味着复制添加了 ROWGUIDCOL 列。|  
|**partition_view_id**|**int**|标识定义订阅服务器分区的视图。|  
|**repl_view_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**partition_deleted_view_rule**|**sysname**|在合并复制触发器内部使用的语句，用于根据其旧列值检索每个已删除或已更新行的分区 ID。|  
|**partition_inserted_view_rule**|**sysname**|在合并复制触发器内部使用的语句，用于根据其新列值检索每个已插入或已更新行的分区 ID。|  
|**membership_eval_proc_name**|**sysname**|中的行的当前分区 Id 的计算结果的过程的名称[MSmerge_contents &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)。|  
|**column_list**|**sysname**|在项目中发布的列的逗号分隔列表。|  
|**column_list_blob**|**sysname**|在项目中发布的列（包括二进制大型对象列）的逗号分隔列表。|  
|**expand_proc**|**sysname**|重新评估分区 Id 的所有子行的新插入的父行和已经历了分区更改或已被删除的父行的过程的名称。|  
|**logical_record_parent_nickname**|**int**|逻辑记录中指定项目的顶级父项目的别名。|  
|**logical_record_view**|**int**|一个视图，用于输出与各子项目 rowguid 相对应的顶级父项目 rowguid。|  
|**logical_record_deleted_view_rule**|**sysname**|类似于**logical_record_view**，只不过它显示在"删除"的表中的子行更新和删除触发器。|  
|**logical_record_level_conflict_detection**|**bit**|指示应在逻辑记录级还是行级或列级检测冲突。<br /><br /> **0** = 行或列级别使用冲突检测。<br /><br /> **1** = 使用逻辑记录级冲突检测，则在发布服务器上的行中的更改和更改的单独行的同一逻辑记录在订阅服务器会被视为冲突。<br /><br /> 当该值为 1 时，只能使用逻辑记录级别的冲突解决。|  
|**logical_record_level_conflict_resolution**|**bit**|指示是否应在逻辑记录级或在行级或列级解决冲突。<br /><br /> **0** = 行或列级别使用解决方法。<br /><br /> **1** = 以防的冲突时，来自入选方的整个逻辑记录覆盖落选方的整个逻辑记录。<br /><br /> 值 1 既可用于逻辑记录级别的检测，也可用于行或列级别的检测。|  
|**partition_options**|**tinyint**|定义项目数据的分区方式，当所有行只属于一个分区或只属于一个订阅时，这将可以实现性能优化。 *Partition_options*可以是下列值之一。<br /><br /> **0** = 对项目的筛选是静态的或者不会生成唯一的每个分区的数据子集，即"重叠"分区。<br /><br /> **1** = 分区重叠，并且在订阅服务器所做的 DML 更新无法更改行所属的分区。<br /><br /> **2** = 筛选的项目生成不重叠分区，但多个订阅服务器可以接收相同的分区。<br /><br /> **3** = 筛选项目生成对于每个订阅都唯一的非重叠分区。|  
|**name**|**sysname**|分区的名称。|  
  
## <a name="see-also"></a>请参阅  
 [参数化筛选器为合并发布管理分区](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_helpmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)  
  
  
