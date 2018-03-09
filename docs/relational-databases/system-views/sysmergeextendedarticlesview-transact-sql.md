---
title: "sysmergeextendedarticlesview (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergeextendedarticlesview
- sysmergeextendedarticlesview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeextendedarticlesview view
ms.assetid: bd5c8414-5292-41fd-80aa-b55a50ced7e2
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c517abaa4c5ffdc5e0d84ac6d4c6268ddd524ac9
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysmergeextendedarticlesview-transact-sql"></a>sysmergeextendedarticlesview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysmergeextendedarticlesview**公开文章信息的视图。 此视图存储在发布服务器的发布数据库以及订阅服务器的订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|项目的名称。|  
|**类型**|**tinyint**|指示项目类型，可以为下列类型之一：<br /><br /> **10** = 表。<br /><br /> **32** = 仅限 Proc 架构。<br /><br /> **64** = 仅限视图架构或仅限索引的视图架构。<br /><br /> **128** = 仅限函数架构。<br /><br /> **160** = 仅限同义词架构。|  
|**objid**|**int**|发布服务器对象的标识符。|  
|**sync_objid**|**int**|表示同步数据集的视图标识符。|  
|**view_type**|**tinyint**|视图类型：<br /><br /> **0** = 不是视图; 使用所有基对象。<br /><br /> **1** = 永久视图。<br /><br /> **2** = 临时视图。|  
|**artid**|**uniqueidentifier**|给定项目的唯一标识号。|  
|**说明**|**nvarchar(255)**|项目的简要说明。|  
|**pre_creation_command**|**tinyint**|在订阅数据库中创建项目时将执行的默认操作：<br /><br /> **0** = none-如果订阅服务器上已存在表，不执行任何操作。<br /><br /> **1** = drop-删除表，然后再重新创建它。<br /><br /> **2** = delete-删除基于子集筛选器中的 WHERE 子句的问题。<br /><br /> **3** = Truncate-2，但删除页，而不是行相同。 不过，不要使用 WHERE 子句。|  
|**pubid**|**uniqueidentifier**|当前项目所属发布的 ID。|  
|**nickname**|**int**|项目标识的别名映射。|  
|**column_tracking**|**int**|指示是否为项目实现列跟踪。|  
|**status**|**tinyint**|指示项目的状态，可以为下列状态之一：<br /><br /> **1** = Unsynced-用于发布的表的初始处理脚本将运行的下次运行快照代理。<br /><br /> **2** = 活动-用于发布的表的初始处理脚本已运行。<br /><br /> **5** = New_inactive-要添加。<br /><br /> **6** = New_active-要添加。|  
|**conflict_table**|**sysname**|包含当前项目冲突记录的本地表的名称。 该表仅用于提供信息，其内容可以由自定义冲突解决例程修改或删除，或直接由系统管理员修改或删除。|  
|**creation_script**|**nvarchar(255)**|此项目的创建脚本。|  
|**conflict_script**|**nvarchar(255)**|此项目的冲突脚本。|  
|**article_resolver**|**nvarchar(255)**|此项目的自定义行级冲突解决程序。|  
|**ins_conflict_proc**|**sysname**|用于写入到的冲突的过程**conflict_table**。|  
|**insert_proc**|**sysname**|由默认冲突解决程序用来在同步过程中插入行的过程。|  
|**update_proc**|**sysname**|由默认冲突解决程序用来在同步过程中更新行的过程。|  
|**select_proc**|**sysname**|自动生成的存储过程的名称，合并代理使用该存储过程来完成锁定并查找项目的行和列。|  
|**schema_option**|**binary(8)**|有关支持的值的*schema_option*，请参阅[sp_addmergearticle &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|在订阅服务器上创建的表的名称。|  
|**resolver_clsid**|**nvarchar(50)**|自定义冲突解决程序的 ID。|  
|**subset_filterclause**|**nvarchar(1000)**|此项目的筛选子句。|  
|**missing_col_count**|**int**|缺少的列数。|  
|**missing_cols**|**varbinary(128)**|缺少的列的位图。|  
|**columns**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resolver_info**|**nvarchar(255)**|所需的自定义冲突解决程序的其他信息的存储。|  
|**view_sel_proc**|**nvarchar(290)**|存储过程的名称，合并代理使用此存储过程初始填充动态筛选发布中的项目，并且枚举在任何筛选发布中的更改的行。|  
|**gen_cur**|**int**|对项目基表所做的本地更改的生成数。|  
|**excluded_cols**|**varbinary(128)**|当项目发送到订阅服务器时，从项目中排除的列的位图。|  
|**excluded_col_count**|**int**|排除的列数。|  
|**vertical_partition**|**int**|指定是否对表项目启用列筛选。 **0**指示没有垂直筛选并发布所有列。|  
|**identity_support**|**int**|指定是否启用自动标识范围处理。 **1**意味着处理标识范围是否启用了，和**0**意味着没有任何标识范围支持。|  
|**destination_owner**|**sysname**|目标对象的所有者的名称。|  
|**before_image_objid**|**int**|跟踪表对象 ID。 如果将发布配置为启用分区更改优化，则跟踪表将包含某些键列值。|  
|**before_view_objid**|**int**|视图表的对象 ID。 视图所在的表用于在删除或更新行之前跟踪行是否属于特定的订阅服务器。 将应用仅发布创建与 *@keep_partition_changes*   =  **true**。|  
|**verify_resolver_signature**|**int**|指定在合并复制中使用冲突解决程序之前是否验证数字签名：<br /><br /> **0** = 不验证签名。<br /><br /> **1** = 验证签名以确定它是否来自可靠来源。|  
|**allow_interactive_resolver**|**bit**|指定是否对项目启用交互式冲突解决程序。 **1**指定项目使用交互式冲突解决程序。|  
|**fast_multicol_updateproc**|**bit**|指定是否已启用合并代理来使用一条 UPDATE 语句在同一行的多个列中应用更改。<br /><br /> **0** = 每个列的独立更新更改的问题。<br /><br /> **1** = 颁发 on UPDATE 语句，这会导致更新发生在一个语句中的多个列。|  
|**check_permissions**|**int**|将表级权限的位图验证合并代理将更改应用到发布服务器的时。 *check_permissions*可以具有这些值之一：<br /><br /> **0x00** = 则不检查权限。<br /><br /> **0x10** = 检查发布服务器上的权限，可以上载订阅服务器上所做插入之前。<br /><br /> **0x20** = 检查发布服务器上的权限，可以上载订阅服务器上所做的更新之前。<br /><br /> **0x40** = 检查发布服务器上的权限，可以上载订阅服务器上的 delete 操作之前。|  
|**maxversion_at_cleanup**|**int**|清除了元数据的最高版本。|  
|**processing_order**|**int**|指示合并发布; 中的项目的处理顺序其中的一个值**0**指示，本文是无序，并从最低到最高值的顺序处理项目。 如果两个项目具有相同值，将对其进行并发处理。 有关详细信息，请参阅[指定合并项目的处理顺序](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)。|  
|**published_in_tran_pub**|**bit**|指示合并发布中的项目也将在事务发布中发布。<br /><br /> **0** = 事务文章中未发布项目。<br /><br /> **1** = 文章也发布事务文章中。|  
|**upload_options**|**tinyiny**|定义是否可以在订阅服务器上进行更改或从订阅服务器上载更改，可以为下列值之一：<br /><br /> **0** = 没有在订阅服务器上所做的更新限制; 所有的更改上载到发布服务器。<br /><br /> **1** = 更改允许在订阅服务器上，但不是会上载到发布服务器。<br /><br /> **2** = 订阅服务器上不允许更改。|  
|**lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**delete_proc**|**sysname**|由默认冲突解决程序用来在同步过程中删除行的过程。|  
|**before_upd_view_objid**|**int**|在更新之前表视图的 ID。|  
|**delete_tracking**|**bit**|指示是否复制删除。<br /><br /> **0** = 删除不会复制。<br /><br /> **1** = 删除复制，这是合并复制的默认行为。<br /><br /> 时的值*delete_tracking*是**0**、 必须在发布服务器，手动删除订阅服务器上删除的行和删除发布服务器上的行都必须在订阅服务器上手动删除。<br /><br /> 注意： 一个的值的**0**导致非收敛。|  
|**compensate_for_errors**|**bit**|指示在同步期间遇到错误时是否采取补救措施。<br /><br /> **0** = Compensating 操作已被禁用。<br /><br /> **1** = 不在订阅服务器或发布服务器始终前导能应用于补偿操作要撤消这些更改，这是合并复制的默认行为的更改。<br /><br /> 注意： 一个的值的**0**导致非收敛。|  
|**pub_range**|**bigint**|发布服务器标识范围大小。|  
|**range**|**bigint**|将分配到调整中订阅服务器的连续标识值的大小。|  
|**threshold**|**int**|标识范围阈值百分比。|  
|**metadata_select_proc**|**sysname**|自动生成用于访问在合并复制系统表中的元数据的存储过程的名称。|  
|**stream_blob_columns**|**bit**|指定当复制二进制大型对象列时是否使用数据流优化。 **1**意味着将尝试优化。|  
|**preserve_rowguidcol**|**bit**|指示复制是否使用现有 rowguid 列。 值为**1**表示将使用现有的 ROWGUIDCOL 列。 **0**意味着复制添加 ROWGUIDCOL 列。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 &#40;Transact SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [sysmergearticles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)  
  
  
